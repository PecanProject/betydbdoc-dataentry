## SQL

SQL can also be used for bulk uploads. However, SQL should primarily be used in the following cases:

* fix data errors 

* remove duplicate records

* replace records

* metadata upload requires features that are not available through the web interface or BETYdb-YABA

   * for more information on how to use SQL to add a new season (TERRA REF Project), see the [Metadata Entry Workflow for BETYdb](https://osf.io/v7f9t/wiki/Metadata%20Entry%20Workflow/)

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

