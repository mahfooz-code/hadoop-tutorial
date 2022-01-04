# DataNode

1) DataNodes are the workhorses of the filesystem.
2) They store and retrieve blocks when they are told to (by clients or the namenode), and they report back to the namenode periodically with lists of blocks that they are storing.
3) 


#Block Caching
Normally a datanode reads blocks from disk, but for frequently accessed files the blocks may be explicitly cached in the datanode’s memory, in an off-heap block cache. By default, a block is cached in only one datanode’s memory, although the number is configurable on a per-file basis.

Job schedulers (for MapReduce, Spark, and other frameworks) can take advantage of cached blocks by running tasks on the datanode where a block is cached, for increased read performance.
