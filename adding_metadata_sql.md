## SQL

SQL can also be used for bulk uploads. However, SQL should primarily be used in the following cases:

* fix data errors 
* remove duplicate records
* replace records
* metadata upload requires features that are not available through the web interface or BETYdb-YABA

   * for more information on how to use SQL to add data to BETYdb and specific examples for how to add a new season (TERRA REF project), see the [Metadata Entry Workflow for BETYdb](https://osf.io/v7f9t/wiki/Metadata%20Entry%20Workflow/){target="_blank"}.

### How to insert, update, or delete records

#### Insert a record to a table

* x: name of table

* field1 and field2: names of fields that you want to add data to

* a and b: data values to be added

```sql
insert into x (field1, field2) values (a, b);
```

#### Update a record in a table

* x: name of table

* field1: name of field you would like to update

* a: updated value

* field2: name of conditional field

* b: conditional value

```sql
update x
set field1 = a
where field2 = b;
```

#### Delete a record from a table

* x: name of table

* field1: name of conditional field

* a: conditional value

```sql
delete from x
where field1 = a;
```

#### Remove duplicate records

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
