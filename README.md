# Apache Hadoop distribution on Ubuntu with Spark, Pig, and Hive

The docker image Apache hadoop 2.10.0 distribution on Ubuntu 18.04 with Spark 2.4.5, Pig 0.17.0, and Hive 2.3.6

Added Rstudio Server on port 8787.

Forked From: [https://hub.docker.com/r/suhothayan/hadoop-spark-pig-hive](https://hub.docker.com/r/suhothayan/hadoop-spark-pig-hive)

# Build the image

```
docker build -t wqd180067/docker-bigdata:1.0 .
```
# Pull the image

```
docker pull wqd180067/docker-bigdata:1.0
```

# Start a container

In order to use the Docker image you have just build or pulled use:

```
docker run -it -p 50070:50070 -p 8088:8088 -p 8080:8080 -p 8787:8787 wqd180067/docker-bigdata:1.0 bash
```

## Testing

You can run one of the hadoop examples:

```
# run the mapreduce
yarn jar $HADOOP_HOME/share/hadoop/mapreduce/hadoop-mapreduce-examples-2.9.2.jar grep input output 'dfs[a-z.]+'

# check the output
hdfs dfs -cat output/*
```

## Run 

### Hive 

```
hive
```

or 

```
 beeline -u jdbc:hive2://
```

### Pig 

```
pig
```

### Spark 

Scala 

```
spark-shell
```

Python

```
pyspark
```



