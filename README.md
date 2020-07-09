# lcuc
Low-cardinality unique count tool

## About

When you're analyzing data sets on the command line, it's quite common to end up with a pattern like:

```
$ some stream | sort | uniq -c

1006660 item1
 522353 item2
5576908 item3
```

An observation in the above is that there is low cardinality (only 3 unique items) but a high count (7M).  In the above, the `sort` will likely be the slowest part of the pipeline

This utility offers a more efficient alternative which keeps the counts in-memory in a hash table, avoiding the expensive sort.

## Timing

Vanilla data reading:
```
$ time cat stream > /dev/null

real	0m0.013s
user	0m0.002s
sys	0m0.010s
```

Line count:
```
$ time wc -l stream
 7105921 stream

real	0m0.056s
user	0m0.036s
sys	0m0.016s
```

lcuc unique count:
```
$ time lcuc stream
5576908 item3
522353 item2
1006660 item1

real	0m0.917s
user	0m0.872s
sys	0m0.029s
```

`sort | uniq -c` unique count:
```
$ time cat stream | sort | uniq -c
1006660 item1
522353 item2
5576908 item3

real	1m19.572s
user	1m19.827s
sys	0m0.672s
```
