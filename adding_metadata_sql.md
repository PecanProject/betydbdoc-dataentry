## SQL

SQL can also be used for bulk uploads. However, SQL should primarily be used when data errors need to be fixed, you need to remove / replace records, or your data upload requires features that are not available through the web interface or BETYdb-YABA.

### How to insert, update, or delete records

#### Insert a record to a table

* x is the name of the table

* field1 and field2 are the names of the fields that you want to add data to

* a and b are the data values to be added

```sql
insert into x (field1, field2) values (a, b);
```
