## R and SQL

SQL can also be used for bulk uploads. However, these should primarily be used when data errors need to be fixed, or your data upload requires features that are not available through the web interface or BETYdb-YABA. 

### SQL 

Here is an example workflow that you can use to add your metadata:

1.) Add experiments

```sql
insert into experiments (name, start_date, end_date, user_id) 
values ('MAC Season 6: Sorghum BAP', '2018-04-06', '2018-08-01', 'some text', 'some text', 6000000004)
```

2.) Add sites

```sql
insert into sites (city, state, country, sitename) 
values ('Maricopa', 'Arizona', 'USA', 'MAC Field Scanner Season 7 Range 9 Column 15')
```

3.) Add treatments


```sql
insert into treatments (name, definition, control) 
values ('MAC Season 6: Sorghum', 'some text', 't')
```

4.) Add cultivars

```sql
insert into cultivars (name, specie_id) 
values ('RIL-CS27_(TX2910/(Macia/R07007)-CS44)-CSF1-PRF2-CS27', 2588)
```

5.) Add citations

```sql
insert into citations (author, year, title) 
values ('Newcomb, Maria', 2016, 'Maricopa Agricultural Center Field Activities')
```

6.) Associate experiments with sites

```sql
insert into experiments_sites (experiment_id, site_id) values ((select id from experiments where name = 'MAC Season 6: Sorghum BAP'),
(select id from sites where sitename = 'MAC Field Scanner Season 6 Range 1 Column 1 E'))
```

7.) Associate sites with cutlivars

```sql
insert into sites_cultivars (site_id, cultivar_id) 
values ((select id from sites where sitename = 'MAC Field Scanner Season 8 Range 1 Column 1 E'),
(select id from cultivars where name = 'Tiburon' and specie_id = 2588))
```

8.) Associate sites with citations

```sql
insert into citations_sites (citation_id, site_id)
values ((select id from citations where author = 'Newcomb, Maria' and year = 2016 and title = 'MAC Field Activities'),
(select id from sites where sitename = 'MAC Field Scanner Season 6 Range 1 Column 1 E'))
```
