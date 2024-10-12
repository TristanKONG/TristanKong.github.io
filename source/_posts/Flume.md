# Flume

## Source

### Exec

get data by running external command

```
.type = exec
.command = cat/tail -F

```

### SpoolDir

```
.type = spooldir
.spoolDir
.deletePolicy = nevet/immediate
```

### Netcat

```
.type = netcat
.bind = localhost
.port = 9999
```

Unix utility

read,write data on network

### protocal

TCP

UDP

### TailDir

```
.type = TAILDIR
.filegroups = f1
.filegroups.f1 = (localtion of f1)
.positionFile = (localtion of json file)
```

### Kafka

```
.type = org.apache.flume.source.kafka.KafkaSource
```

### HTTP

accept events by POST and GET

### "handler"

implement interface "HTTPSourceHandler"

take

HTTPServletRequest

return

a list of Flume events





## Channel

### Memory Channel

fast

events are stored  in an in-memory queue

```
.type = memory
.capacity = 1000
.transactionCapacity = 1000
```



### File Channel

reliable

events are written in the disk

```
.checkpointDir = (checkpoint file)
.dataDir = (log file)
```



## Sink

### HDFS

```
.hdfs.path
.hdfs.fileType = DataStream/SequenceFile/CompressedStream
.hdfs.filePrefix
.hdfs.fileSuffix
.hdfs.rollCount = (events in a file, 10 lines by default)
.hdfs.rollSize = (size of a file, 1024 byte by default,if 0 then no limit)
.hdfs.rollInterval = (Maximum waiting time for data, 30 sec by default)
.hdfs.useLocalTimeStamp = true (使用本地时间戳，便于HDFS排序和查找)
```

### HBase

```
.type = hbase2
.table
.columnFamily
.serializer = org.apache.flume.sink.hbase2.RegexHBaseEventSerializer
```

