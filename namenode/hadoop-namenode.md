# NameNode

1) The nameNode manages the filesystem namespace. 
2) It maintains the filesystem tree and the metadata for all the files and directories in the tree.
3) This information is stored persistently on the local disk in the form of two files:
   1) The namespace image
   2) The edit log

#secondary nameNode
1) It is also possible to run a secondary nameNode, which despite its name does not act 
as a namenode. 
2) Its main role is to periodically merge the namespace image with the edit log to prevent the edit log from becoming too large.
3) The secondary namenode usually runs on a separate physical machine because it requires plenty of CPU and as much memory as the namenode to perform the merge. It keeps a copy of the merged namespace image, which can be used in the event of the namenode failing.
4) 


#HDFS Federation

The namenode keeps a reference to every file and block in the filesystem in memory, which means that on very large clusters with many files, memory becomes the limiting factor for scaling (see How Much Memory Does a Namenode Need?). HDFS federation, introduced in the 2.x release series, allows a cluster to scale by adding namenodes, each of which manages a portion of the filesystem namespace. For example, one namenode might manage all the files rooted under /user, say, and a second namenode might handle files under /share.
Under federation, each namenode manages a namespace volume, which is made up of the metadata for the namespace, and a block pool containing all the blocks for the files in the namespace. Namespace volumes are independent of each other, which means namenodes do not communicate with one another, and furthermore the failure of one namenode does not affect the availability of the namespaces managed by other namenodes. Block pool storage is not partitioned, however, so datanodes register with each namenode in the cluster and store blocks from multiple block pools.

To access a federated HDFS cluster, clients use client-side mount tables to map file paths to namenodes. This is managed in configuration using ViewFileSystem and the viewfs:// URIs.


#HDFS High Availability
he combination of replicating namenode metadata on multiple filesystems and using the secondary namenode to create checkpoints protects against data loss, but it does not provide high availability of the filesystem. The namenode is still a single point of failure (SPOF).


The new namenode is not able to serve requests until it has (i) loaded its namespace image into memory, (ii) replayed its edit log, and (iii) received enough block reports from the datanodes to leave safe mode. On large clusters with many files and blocks, the time it takes for a namenode to start from cold can be 30 minutes or more.

#active-standby


# quorum journal manager (QJM)
The QJM runs as a group of journal nodes, and each edit must be written to a majority of the journal nodes.

# failover controller
The transition from the active namenode to the standby is managed by a new entity in the system called the failover controller


# Client

A client accesses the filesystem on behalf of the user by communicating with the namenode and datanodes. 


# Important configuration

1) fs.defaultFS
2) dfs.replication
3) 