#Parallel Copying with distcp
1) hadoop distcp file1 file2
2) hadoop distcp dir1 dir2
3) hadoop distcp -update dir1 dir2
4) hadoop distcp -update -delete -p hdfs://namenode1/foo hdfs://namenode2/foo
5) hadoop distcp webhdfs://namenode1:50070/foo webhdfs://namenode2:50070/foo
6) 


