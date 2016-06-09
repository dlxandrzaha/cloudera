# <center> Storage Lab
## <center> HDFS performance
* Find test jar location
`find / -name 'hadoop-*example*.jar'`
* Navigate to test jar location
`cd /opt/cloudera/parcels/CDH-5.7.1-1.cdh5.7.1.p0.11/jars/`
* View available tests
`hadoop jar hadoop-examples.jar`
* Run teragen - generate ~ 1Gb of data
`time hadoop jar hadoop-examples.jar teragen 10000000 /tmp/dlxandrzaha/teragen`

```
16/06/08 10:21:23 INFO client.RMProxy: Connecting to ResourceManager at ip-172-31-34-101.eu-west-1.compute.internal/172.31.34.101:8032
16/06/08 10:21:24 INFO terasort.TeraSort: Generating 10000000 using 2
16/06/08 10:21:24 INFO mapreduce.JobSubmitter: number of splits:2
16/06/08 10:21:24 INFO mapreduce.JobSubmitter: Submitting tokens for job: job_1465387103655_0004
16/06/08 10:21:24 INFO impl.YarnClientImpl: Submitted application application_1465387103655_0004
16/06/08 10:21:24 INFO mapreduce.Job: The url to track the job: http://ip-172-31-34-101.eu-west-1.compute.internal:8088/proxy/application_1465387103655_0004/
16/06/08 10:21:24 INFO mapreduce.Job: Running job: job_1465387103655_0004
16/06/08 10:21:31 INFO mapreduce.Job: Job job_1465387103655_0004 running in uber mode : false
16/06/08 10:21:31 INFO mapreduce.Job:  [###Job Progress###]
16/06/08 10:21:43 INFO mapreduce.Job:  [###Job Progress###]
16/06/08 10:21:46 INFO mapreduce.Job:  [###Job Progress###]
16/06/08 10:21:49 INFO mapreduce.Job:  [###Job Progress###]
16/06/08 10:21:52 INFO mapreduce.Job:  [###Job Progress###]
16/06/08 10:21:53 INFO mapreduce.Job:  [###Job Progress###]
16/06/08 10:21:53 INFO mapreduce.Job: Job job_1465387103655_0004 completed successfully
16/06/08 10:21:53 INFO mapreduce.Job: Counters: 31
        File System Counters
                FILE: Number of bytes read=0
                FILE: Number of bytes written=236118
                FILE: Number of read operations=0
                FILE: Number of large read operations=0
                FILE: Number of write operations=0
                HDFS: Number of bytes read=167
                HDFS: Number of bytes written=1000000000
                HDFS: Number of read operations=8
                HDFS: Number of large read operations=0
                HDFS: Number of write operations=4
        Job Counters
                Launched map tasks=2
                Other local map tasks=2
                Total time spent by all maps in occupied slots (ms)=38973
                Total time spent by all reduces in occupied slots (ms)=0
                Total time spent by all map tasks (ms)=38973
                Total vcore-seconds taken by all map tasks=38973
                Total megabyte-seconds taken by all map tasks=39908352
        Map-Reduce Framework
                Map input records=10000000
                Map output records=10000000
                Input split bytes=167
                Spilled Records=0
                Failed Shuffles=0
                Merged Map outputs=0
                GC time elapsed (ms)=219
                CPU time spent (ms)=21000
                Physical memory (bytes) snapshot=763240448
                Virtual memory (bytes) snapshot=3161993216
                Total committed heap usage (bytes)=640155648
        org.apache.hadoop.examples.terasort.TeraGen$Counters
                CHECKSUM=21472776955442690
        File Input Format Counters
                Bytes Read=0
        File Output Format Counters
                Bytes Written=1000000000

real    0m32.770s
user    0m5.984s
sys     0m0.242s
```
* Perfrom terasort N1
`time sudo -u hdfs hadoop jar hadoop-examples.jar terasort /tmp/dlxandrzaha/teragen/ /tmp/dlxandrzaha/terasort`

```
16/06/08 12:05:51 INFO terasort.TeraSort: starting
16/06/08 12:05:53 INFO input.FileInputFormat: Total input paths to process : 2
Spent 125ms computing base-splits.
Spent 2ms computing TeraScheduler splits.
Computing input splits took 127ms
Sampling 8 splits of 8
Making 3 from 100000 sampled records
Computing parititions took 1166ms
Spent 1296ms computing partitions.
16/06/08 12:05:54 INFO client.RMProxy: Connecting to ResourceManager at ip-172-31-34-101.eu-west-1.compute.internal/172.31.34.101:8032
16/06/08 12:05:55 INFO mapreduce.JobSubmitter: number of splits:8
16/06/08 12:05:55 INFO mapreduce.JobSubmitter: Submitting tokens for job: job_1465387103655_0018
16/06/08 12:05:55 INFO impl.YarnClientImpl: Submitted application application_1465387103655_0018
16/06/08 12:05:55 INFO mapreduce.Job: The url to track the job: http://ip-172-31-34-101.eu-west-1.compute.internal:8088/proxy/application_1465387103655_0018/
16/06/08 12:05:55 INFO mapreduce.Job: Running job: job_1465387103655_0018
16/06/08 12:06:03 INFO mapreduce.Job: Job job_1465387103655_0018 running in uber mode : false
16/06/08 12:06:03 INFO mapreduce.Job:  [###Job Progress###]
16/06/08 12:06:14 INFO mapreduce.Job:  [###Job Progress###]
16/06/08 12:06:25 INFO mapreduce.Job:  [###Job Progress###]
16/06/08 12:06:26 INFO mapreduce.Job:  [###Job Progress###]
16/06/08 12:06:35 INFO mapreduce.Job:  [###Job Progress###]
16/06/08 12:06:36 INFO mapreduce.Job:  [###Job Progress###]
16/06/08 12:06:46 INFO mapreduce.Job:  [###Job Progress###]
16/06/08 12:06:47 INFO mapreduce.Job:  [###Job Progress###]
16/06/08 12:06:58 INFO mapreduce.Job:  [###Job Progress###]
16/06/08 12:07:00 INFO mapreduce.Job:  [###Job Progress###]
16/06/08 12:07:01 INFO mapreduce.Job:  [###Job Progress###]
16/06/08 12:07:12 INFO mapreduce.Job:  [###Job Progress###]
16/06/08 12:07:14 INFO mapreduce.Job:  [###Job Progress###]
16/06/08 12:07:15 INFO mapreduce.Job: Job job_1465387103655_0018 completed successfully
16/06/08 12:07:15 INFO mapreduce.Job: Counters: 50
        File System Counters
                FILE: Number of bytes read=439888140
                FILE: Number of bytes written=878113613
                FILE: Number of read operations=0
                FILE: Number of large read operations=0
                FILE: Number of write operations=0
                HDFS: Number of bytes read=1000001256
                HDFS: Number of bytes written=1000000000
                HDFS: Number of read operations=33
                HDFS: Number of large read operations=0
                HDFS: Number of write operations=6
        Job Counters
                Launched map tasks=8
                Launched reduce tasks=3
                Data-local map tasks=6
                Rack-local map tasks=2
                Total time spent by all maps in occupied slots (ms)=71734
                Total time spent by all reduces in occupied slots (ms)=35644
                Total time spent by all map tasks (ms)=71734
                Total time spent by all reduce tasks (ms)=35644
                Total vcore-seconds taken by all map tasks=71734
                Total vcore-seconds taken by all reduce tasks=35644
                Total megabyte-seconds taken by all map tasks=73455616
                Total megabyte-seconds taken by all reduce tasks=36499456
        Map-Reduce Framework
                Map input records=10000000
                Map output records=10000000
                Map output bytes=1020000000
                Map output materialized bytes=436911106
                Input split bytes=1256
                Combine input records=0
                Combine output records=0
                Reduce input groups=10000000
                Reduce shuffle bytes=436911106
                Reduce input records=10000000
                Reduce output records=10000000
                Spilled Records=20000000
                Shuffled Maps =24
                Failed Shuffles=0
                Merged Map outputs=24
                GC time elapsed (ms)=1187
                CPU time spent (ms)=86550
                Physical memory (bytes) snapshot=6186729472
                Virtual memory (bytes) snapshot=17438625792
                Total committed heap usage (bytes)=6625427456
        Shuffle Errors
                BAD_ID=0
                CONNECTION=0
                IO_ERROR=0
                WRONG_LENGTH=0
                WRONG_MAP=0
                WRONG_REDUCE=0
        File Input Format Counters
                Bytes Read=1000000000
        File Output Format Counters
                Bytes Written=1000000000
16/06/08 12:07:15 INFO terasort.TeraSort: done

real    1m25.259s
user    0m7.867s
sys     0m0.261s
```
* Perfrom terasort N2 (with HDFS Short Circuit Reads)
`time sudo -u hdfs hadoop jar hadoop-examples.jar terasort /tmp/dlxandrzaha/teragen/ /tmp/dlxandrzaha/terasort`

```
16/06/08 12:09:49 INFO terasort.TeraSort: starting
16/06/08 12:09:51 INFO input.FileInputFormat: Total input paths to process : 2
Spent 126ms computing base-splits.
Spent 2ms computing TeraScheduler splits.
Computing input splits took 129ms
Sampling 8 splits of 8
Making 3 from 100000 sampled records
Computing parititions took 1344ms
Spent 1476ms computing partitions.
16/06/08 12:09:52 INFO client.RMProxy: Connecting to ResourceManager at ip-172-31-34-101.eu-west-1.compute.internal/172.31.34.101:8032
16/06/08 12:09:53 INFO mapreduce.JobSubmitter: number of splits:8
16/06/08 12:09:53 INFO mapreduce.JobSubmitter: Submitting tokens for job: job_1465387103655_0019
16/06/08 12:09:54 INFO impl.YarnClientImpl: Submitted application application_1465387103655_0019
16/06/08 12:09:54 INFO mapreduce.Job: The url to track the job: http://ip-172-31-34-101.eu-west-1.compute.internal:8088/proxy/application_1465387103655_0019/
16/06/08 12:09:54 INFO mapreduce.Job: Running job: job_1465387103655_0019
16/06/08 12:10:01 INFO mapreduce.Job: Job job_1465387103655_0019 running in uber mode : false
16/06/08 12:10:01 INFO mapreduce.Job:  [###Job Progress###]
16/06/08 12:10:11 INFO mapreduce.Job:  [###Job Progress###]
16/06/08 12:10:12 INFO mapreduce.Job:  [###Job Progress###]
16/06/08 12:10:22 INFO mapreduce.Job:  [###Job Progress###]
16/06/08 12:10:24 INFO mapreduce.Job:  [###Job Progress###]
16/06/08 12:10:33 INFO mapreduce.Job:  [###Job Progress###]
16/06/08 12:10:43 INFO mapreduce.Job:  [###Job Progress###]
16/06/08 12:10:55 INFO mapreduce.Job:  [###Job Progress###]
16/06/08 12:10:57 INFO mapreduce.Job:  [###Job Progress###]
16/06/08 12:11:08 INFO mapreduce.Job:  [###Job Progress###]
16/06/08 12:11:10 INFO mapreduce.Job:  [###Job Progress###]
16/06/08 12:11:10 INFO mapreduce.Job: Job job_1465387103655_0019 completed successfully
16/06/08 12:11:10 INFO mapreduce.Job: Counters: 50
        File System Counters
                FILE: Number of bytes read=439888140
                FILE: Number of bytes written=878113613
                FILE: Number of read operations=0
                FILE: Number of large read operations=0
                FILE: Number of write operations=0
                HDFS: Number of bytes read=1000001256
                HDFS: Number of bytes written=1000000000
                HDFS: Number of read operations=33
                HDFS: Number of large read operations=0
                HDFS: Number of write operations=6
        Job Counters
                Launched map tasks=8
                Launched reduce tasks=3
                Data-local map tasks=6
                Rack-local map tasks=2
                Total time spent by all maps in occupied slots (ms)=71176
                Total time spent by all reduces in occupied slots (ms)=35917
                Total time spent by all map tasks (ms)=71176
                Total time spent by all reduce tasks (ms)=35917
                Total vcore-seconds taken by all map tasks=71176
                Total vcore-seconds taken by all reduce tasks=35917
                Total megabyte-seconds taken by all map tasks=72884224
                Total megabyte-seconds taken by all reduce tasks=36779008
        Map-Reduce Framework
                Map input records=10000000
                Map output records=10000000
                Map output bytes=1020000000
                Map output materialized bytes=436911106
                Input split bytes=1256
                Combine input records=0
                Combine output records=0
                Reduce input groups=10000000
                Reduce shuffle bytes=436911106
                Reduce input records=10000000
                Reduce output records=10000000
                Spilled Records=20000000
                Shuffled Maps =24
                Failed Shuffles=0
                Merged Map outputs=24
                GC time elapsed (ms)=1402
                CPU time spent (ms)=86490
                Physical memory (bytes) snapshot=6090444800
                Virtual memory (bytes) snapshot=17410887680
                Total committed heap usage (bytes)=6683623424
        Shuffle Errors
                BAD_ID=0
                CONNECTION=0
                IO_ERROR=0
                WRONG_LENGTH=0
                WRONG_MAP=0
                WRONG_REDUCE=0
        File Input Format Counters
                Bytes Read=1000000000
        File Output Format Counters
                Bytes Written=1000000000
16/06/08 12:11:10 INFO terasort.TeraSort: done

real    1m22.138s
user    0m8.006s
sys     0m0.293s
```