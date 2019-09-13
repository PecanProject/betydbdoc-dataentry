## SQL

SQL can also be used for bulk uploads. However, SQL should primarily be used when data errors need to be fixed, you need to remove duplicate records / replace records, or your data upload requires features that are not available through the web interface or BETYdb-YABA.

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

