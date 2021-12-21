# Indexes

A feature provided my the db to speed up queries. It should not be overused.

## Explain Analyze

Add `EXPLAIN ANALYZE` before the query you want to explain.  
It will show what is happening under the hood in a given query.  

## Create Index
Types of Indexes  

- Standard single-column index
`CREATE INDEX index_name ON table (col)`

- Unique index
`CREATE UNIQUE INDEX index_name ON table (col)`

- Multi-column index
`CREATE INDEX index_name ON table (col1, col2...)` _beware when adding many columns, possible performance hit_  

## Delete Index
`DROP INDEX index_name`
