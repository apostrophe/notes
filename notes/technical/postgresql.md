
#### DBeaver Shortcuts
Choose Connection...  Ctrl+9
Tab (in results)      View current row Verticaly


#### Syntax
`::` - cast
https://stackoverflow.com/a/15537761

#### DDL vs DML
Data Manipulation Language - CREATE, DROP, ALTER, TRUNCATE, RENAME
Data Definition Language - SELECT, UPDATE, INSERT, DELETE, MERGE/UPSERT
Data Control Language - GRANT, REVOKE
Transaction Control Language - COMMIT, ROLLBACK, SAVEPOINT

Great SO Post: https://stackoverflow.com/a/44796508

#### Materialized View

A Materialized View is a database object that contains the results of a query. (A form of cache?) 

```sql
ALTER MATERIALIZED VIEW 
```

source: https://docs.oracle.com/en/database/oracle/oracle-database/19/sqlrf/ALTER-MATERIALIZED-VIEW.html