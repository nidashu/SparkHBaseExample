<h3>HBase Snapshot to Spark Example</h3>
<p>
This project shows how to analyze an HBase Snapshot using Spark. I used the the HBase <a href="https://hbase.apache.org/apidocs/org/apache/hadoop/hbase/mapreduce/TableSnapshotInputFormat.html">TableSnapshotInputFormat</a> class, which allows allows a MapReduce job to run over a table snapshot.
<br>
<br>
Currently, there are a few different ways to process HBase Snapshots (using Hive, Spark, etc), but many of these methods cannot analyze the timestamps at the variable-level. This code shows how to filter/analyze the snapshot timestamps (and all the fields) at a granular level.
<br>
<br>Build project: <code>mvn package</code>
<br>
<br>Spark: <code>spark-submit --class com.github.zaratsian.SparkHBase.SparkHBase --master yarn-client /tmp/SparkHBaseExample-0.0.1-SNAPSHOT.jar props</code>
<br>
<br>
<b>HBase Table</b>: This is the sample table that was used for this project. From here, I took a snapshot and sent it into HDFS using this syntax: <code>hbase org.apache.hadoop.hbase.snapshot.ExportSnapshot -snapshot customer_info_ss -copy-to hdfs://localhost:8020/tmp/ -mappers 1</code>.
<img src="screenshots/hbase_records.png" class="inline"/>
<br>
<br>
<b>Output from Spark RDD</b>: This screenshot shows the Spark output. I read in the HBase Snapshot into Spark, parsed the individual fields, and this is the raw Spark RDD output.
<img src="screenshots/hbase_spark_output_raw.png" class="inline"/>
<br>
<br>
<b>Filtered Output from Spark</b>: This is a filtered list of records that are more recent (newer) than the user-defined timestamp/threshold value (in this example, I'm keeping all records newer than "2016-08-12 11:46:26:800").
<img src="screenshots/hbase_spark_output.png" class="inline"/>
<br>
The RDD will be writted to HDFS at /tmp/hbase_data_from_spark.
<br>
<br>
<br><b>Versions:</b>
<br>This code was tested using <a href="http://hortonworks.com/products/data-center/hdp/">Hortonworks HDP</a> 2.4.2.0-258 
<br>HBase version 1.1.2.2.4.2.0-258
<br>Spark version 1.6.1
<br>Scala version 2.10.5 (Java HotSpot(TM) 64-Bit Server VM, Java 1.8.0_40) 
</p>
