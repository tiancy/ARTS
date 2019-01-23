# Technique

## Hbase

$ hbase shell

```hbase
// TABLE
list
// scan where status = 1
scan 't1', {COLUMNS => 'info:status', FILTER => "(ValueFilter(=, 'binary:1'))"}
```
