#CleanUpEmptyFilesTool
This tool is designed to look through your HDFS folders to ether identify files with no data in them or delete files with no data in them.

This is hopeful for clusters that have a lot of users with lots of freedom to make mistakes.  

##How to run
 - This will list all files in a director.  This will even work even if you have a million files in one folder.
hadoop jar CleanUpEmptyFilesTool.jar com.cloudera.sa.cap1.largefileutil.CleanUpEmptyFilesTool ls folderName

 - This will list out only files that have zero size
hadoop jar CleanUpEmptyFilesTool.jar com.cloudera.sa.cap1.largefileutil.CleanUpEmptyFilesTool ls-zero folderName

 - This will list out and delete all files of zero size.
hadoop jar CleanUpEmptyFilesTool.jar com.cloudera.sa.cap1.largefileutil.CleanUpEmptyFilesTool rm-zero folderName

##How to test
The following cmd will make a test folder for you to test on

hadoop jar CleanUpEmptyFilesTool.jar com.cloudera.sa.cap1.largefileutil.GenTestFolder 100 folderName

#ReviewTablesTool
This tool is designed to look through your tables and tell you if you could benefit from a compaction

##How to run
hadoop jar CleanUpEmptyFilesTool.jar com.cloudera.sa.cap1.largefileutil.ReviewTablesTool <inputFileForListOfTables> <FileSizeThresholdInMB> <recommendedFileSize>

#WhereAreTheFiles
This tool is designed to look through HDFS and mark which files and folders are in hive tables are not

##How to run
hadoop jar CleanUpEmptyFilesTool.jar com.cloudera.sa.cap1.largefileutil.WhereAreTheFiles <inputFileForListOfTables> <startingHDFSPath>

#CountFilesInHiveTables
This tool with query the hive metastore dump to count number of files and blocks in a table

##Hive to run
spark-submit --class com.cloudera.sa.cap1.spark.CountFilesInHiveTables \ 
--master yarn --deploy-mode client --executor-memory 512MB --num-executors 2 --executor-cores 1 \ 
CleanUpEmptyFilesTool.jar \ 
l \
<inputFolder> \
<inputHiveTable> \
<outputFolder> \
<outputTable>
