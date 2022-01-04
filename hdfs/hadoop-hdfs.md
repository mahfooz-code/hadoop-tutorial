#How to know the block size of hadoop file?

1) hadoop fs -stat %o /filename
2) hdfs getconf -confKey dfs.blocksize
3) hadoop fsck /path/to/file -files -blocks
4) hdfs dfs -stat %o /tmp/testfile_64

#HDFS’s fsck command understands blocks.
hdfs fsck / -files -blocks

# Copy file from local to hdfs
 
    hadoop fs -copyFromLocal input/docs/quangle.txt \
    hdfs://localhost/user/tom/quangle.txt

    hadoop fs -copyToLocal quangle.txt quangle.copy.txt

#creating directory in hdfs
    
     hadoop fs -mkdir books

#Permission
    dfs.permissions.enabled

# Accessing local file system
    hadoop fs -ls file:///

# Hdfs proxy
    
    


