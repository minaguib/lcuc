# lcuc
Low-cardinality unique count tool

## About

When you're analyzing data sets on the command line, it's quite common to end up with a pattern like:

```
$ some stream | sort | uniq -c

 10006660 item1
   522353 item2
225788454 item3
```

An observation in the above is that there is low cardinality (only 3 unique items) but a high count (236M).  In the above, the `sort` will likely be the slowest part of the pipeline

This utility offers a more efficient alternative which keeps the counts in-memory in a hash table, avoiding the expensive sort.
