
#### IntelliJ
| Action | Steps |
| ------ | ----- |
| Open Database Tool Window | View > Tool Windows > Database     |
| Open a New Query Window   | Database Window > Cmd+(down-arrow) |


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


#### Checkpoints, WAL, etc
Changes to the DB in Postgres work like this:
Example: `update orders set status = 'COMPLETE' where orderId = 529`
- Postgres retreives (from db files[1] into memory) the 8kb block of data that includes data to be modified
- Postgres makes the update in memory
  - this data block is marked as dirty -- ie it hasn't been saved/written to disk
- Postgres writes the transaction to the Write-Ahead Log (WAL) 
  -  the WAL is a transaction log, sequential, so if there's a crash, the WAL can be re-run against the persistant db files on disk without any loss to data
  - When processing a COMMIT, postgres guarantees the WAL has been written to disk
- Checkpoint: Eventually any dirty blocks are written/saved to disk 
  - saved blocks are marked as clean
  - a 'save point'/checkpoint is marked in the WAL, meaning prior logs can be recycled

[1] review storage methods/structure
[2] https://www.postgresql.org/docs/current/wal-intro.html

Source: https://medium.com/@jramcloud1/04-postgresql-17-performance-tuning-checkpoints-explained-4972e78f4e56


#### Indexes

-- index definitions
SELECT indexname, indexdef
FROM pg_indexes
WHERE tablename = 'sales_price'