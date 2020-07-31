## SQL

SQL can also be used for bulk uploads. However, SQL should primarily be used in the following cases:

1. correcting systemic data errors involving large numbers of rows
2. assigning non-point geometries to sites [this might be possible in YABA, I don't know]
3. associating experiments with sites and treatments
4. associating sites with cultivars

### Metadata Entry Workflow for BETYdb

The following steps have been implemented in the BETYdb-YABA API and python client, but are described below for reference

Here we show SQL code used to add metadata required each season by the TERRA REF database, including experiments, sites, treatments, cultivars, and citations that is required prior to uploading the trait or yield data. Most PEcAn users _will not_ need to add experiments and cultivars, or associate these records with sites.

Also note that in the TERRA REF and other agronomic applications, each record in the 'sites' table will correspond to an experimental plot.

### Step 1: Add new experiments

```sql
insert into experiments (name, start_date, end_date, user_id) 
values ('MAC Season 6: Sorghum BAP', '2018-04-06', '2018-08-01', 'some text', 'some text', 6000000004);
```

### Step 2: Add new sites

To add sites (or many plots at a single site) using the BETYdb-YABA API, you must provide shapefile for a site to have an associated geometry. 

Otherwise, you can add sites with points or polygons to the database as follows.

```sql
insert into sites (city, state, country, sitename) 
values ('Maricopa', 'Arizona', 'USA', 'MAC Field Scanner Season 7 Range 9 Column 15');
```

You can add simple locations with a single point thus:

```sql
insert into sites (city, state, country, sitename, geometry) 
values ('Urbana', 'Illinois', 'United States', 'My garden plot', ST_SetSRID(ST_makePoint(88, 40, 222), 4326));
For the TERRA REF Project, plot definitions may be copied from previous season if same plots are used.

```sql
with season6 as (
  select city, state, replace(sitename, 'Season 4', 'Season 6') as sitename, greenhouse, geometry, time_zone from sites where sitename like '%Season 4%' 
)
insert into sites (city, state, sitename, greenhouse, geometry, time_zone) select * from season6;
```


### Step 3: Add new treatments

```sql
insert into treatments (name, definition, control) 
values ('MAC Season 6: Sorghum', 'some text', 't');
```

### Step 4: Add new cultivars

Each cultivar must be associated with a species. If there is no entry for the species in the species table, it must be added before adding the new cultivar.


```sql
insert into cultivars (name, specie_id) 
values ('RIL-CS27_(TX2910/(Macia/R07007)-CS44)-CSF1-PRF2-CS27', 2588);
```

### Step 5: Add new citations

```sql
insert into citations (author, year, title) 
values ('Newcomb, Maria', 2016, 'Maricopa Agricultural Center Field Activities');
```

### Step 6: Associate experiments with sites

As an example, this statement could be used to associate the experiment named "MAC Season 6: Sorghum BAP" with the site named "MAC Field Scanner Season 6 Range 1 Column 1 E".
```sql
insert into experiments_sites (experiment_id, site_id) values 
  ((select id from experiments where name = 'MAC Season 6: Sorghum BAP'),
  (select id from sites where sitename = 'MAC Field Scanner Season 6 Range 1 Column 1 E'));
```

When adding a new season for the TERRA REF project, a statement like the following can be used for associating the new season's experiment [or "an experiment for the new season"] with all of the new season's sites. For example, since MAC Field Center sites are consistently named following the format MAC Field Scanner Season x Range a Column b, we could use the following statement to associate the experment named "MAC Season 6: Sorghum BAP" with all Season 6 sites:

```sql
insert into experiments_sites (experiment_id, site_id) 
   select e.experiment_id, s.site_id 
        from (select id as experiment_id from experiments where name = 'MAC Season 6: Sorghum BAP')  as e 
     cross join 
         (select id as site_id from sites where sitename like 'MAC Field Scanner Season 6%') as s;
```

### Step 7: Associate experiments with treatments

```sql
insert into experiments_treatments (experiment_id, treatment_id) 
values ((select id from experiments where name = 'MAC Season 6: Sorghum BAP'),
(select id from treatments where name = 'MAC Season 6: Sorghum'));
```
When adding a new season for the TERRA REF project, a statement like the following can be used to associate all season 6 experiments with all season 6 treatments assuming the experiment and treatment names follow the format convention `MAC Season x: subexperiment name`.

```sql
insert into experiments_treatments (experiment_id, treatment_id) 
   select e.experiment_id, t.treatment_id 
        from (select id as experiment_id from experiments where name like 'MAC Season 6:%')  as e 
     cross join 
         (select id as treatment_id from treatments where name like 'MAC Season 6:%') as s;
```

### Step 8: Associate sites with cultivars

As an example, this statement could be used to associate the site name MAC Field Scanner Season 8 Range 1 Column 1 E with the Sorghum bicolor cultivar Tiburon:

```sql
insert into sites_cultivars (site_id, cultivar_id) 
    values ((select id from sites where sitename = 'MAC Field Scanner Season 8 Range 1 Column 1 E'),
            (select id from cultivars where name = 'Tiburon' and specie_id = 
            (select id from species where scientificname = 'Sorghum bicolor')));
```

### Step 9: Associate sites with citations

```sql
insert into citations_sites (citation_id, site_id)
values ((select id from citations where author = 'Newcomb, Maria' and year = 2016 and title = 'MAC Field Activities'),
(select id from sites where sitename = 'MAC Field Scanner Season 6 Range 1 Column 1 E'));
```

When adding a new season for the TERRA REF project, a statement like the following can be used to associate all citations with author "Newcomb, Maria" with all Season 6 sites since MAC Field Center sites are consistently named following the format `MAC Field Scanner Season x Range a Column b`


```sql
insert into citations_sites (citation_id, site_id) 
   select c.id, s.id 
      from (select id from citations where author = 'Newcomb, Maria') 
     AS c 
      cross join 
         (select id from sites where sitename like 'MAC Field Scanner Season 6%') AS s;
```


## Removing duplicate records
It sometimes happens that multiple rows in a BETYdb table are duplicates, e.g., two species or two sites that were independently added but reference the same entity. A function such as the one that follows could be used to delete a duplicate row and change all references to it to point to a row that we are retaining. (Note that there are serious problems associated with the use of this function, as outlined in [this comment in issue 185](https://github.com/PecanProject/bety/issues/185#issuecomment-530554650){target="_blank"}. We present it here only to outline what might be possible along the lines of partially automating the correction of data errors.)

The function takes three arguments: the name of the table we wish to update (as a string), the id number of the row we wish to remove (the "duplicate"), and the id number of the similar row we wish to retain. For example, if we have two citation rows having essentially the same information having id numbers 286 and 289, we could remove the first and update references to it to point to the second with the statement

```sql
SELECT update_refs_from_to('citations', 286, 289);
```

The following function can be used to combine duplicates or replace an old record with a new one. There are many caveats described in [Issue 185](https://github.com/PecanProject/bety/issues/185){target="_blank"}.

But the basic usage, e.g. to convert all records with `citation_id = 286` to `citation_id = 289`:

```sql
SELECT update_refs_from_to('citations', 286, 289);
```

To make the function available, first run this code:

```sql
CREATE OR REPLACE FUNCTION update_refs_from_to(
  primary_table_name varchar,
  old_id bigint,
  new_id bigint
) RETURNS void AS $$
DECLARE
  foreign_key_col_name varchar;
  referring_table_name varchar;
  update_stmt varchar;
  delete_stmt varchar;
BEGIN
  foreign_key_col_name := regexp_replace(primary_table_name, 's$', '') || '_id';
  FOR referring_table_name IN SELECT table_name FROM information_schema.columns WHERE table_schema = 'public' AND "column_name" = foreign_key_col_name AND is_updatable = 'YES' LOOP

    BEGIN
      update_stmt := 'UPDATE ' || referring_table_name || ' SET ' || foreign_key_col_name || ' = ' || new_id || ' WHERE ' || foreign_key_col_name || ' = ' || old_id;
      RAISE NOTICE 'Attempting to run %', update_stmt;
      EXECUTE update_stmt;
      RAISE NOTICE 'Success!';
    EXCEPTION
      WHEN unique_violation THEN
        RAISE NOTICE 'UPDATE FAILED!!!';
        RAISE NOTICE 'Updating table column % in table % would violate uniqueness constraints', foreign_key_col_name, referring_table_name;
    END;
  END LOOP;
  BEGIN
    delete_stmt := 'DELETE FROM ' || primary_table_name || ' WHERE id = ' || old_id;
      RAISE NOTICE 'Attempting to run %', delete_stmt;
      EXECUTE delete_stmt;
      RAISE NOTICE 'Success!';
  EXCEPTION
    WHEN foreign_key_violation THEN
      RAISE NOTICE 'DELETION FAILED!!!';
      RAISE NOTICE 'Deletion from table % of the row with id % would cause a foreign-key violation', primary_table_name, old_id;
  END;
END
$$ LANGUAGE plpgsql;
```
