# Apache Hadoop with Spark, Pig, and Hive

The docker image Apache hadoop 2.10.0 distribution on Ubuntu 18.04 with Spark 2.4.5, Pig 0.17.0, and Hive 2.3.6

Useful for POC/learning big data.

DO NOT USE IN PRODUCTION (Loose Security)
* 777 permission on HDFS
* NOSASL on Hive

# Build the image

```
docker build -t wqd180067/docker-bigdata:release-1.2 .
```
# Pull the image

```
docker pull wqd180067/docker-bigdata:release-1.2
```

# Start a container

In order to use the Docker image you have just build or pulled use:

```
docker run -it -h localhost -p 10000:10000 -p 10002:10002 -p 50070:50070 -p 50075:50075 -p 8088:8088 -p 8080:8080 wqd180067/docker-bigdata:release-1.2 bash
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

Pyspark Shell

```
pyspark
```

## Python Code Examples

Hive Query

```
from pyhive import hive

host_name = "localhost"
port = 10000

def hiveconnection(host_name, port):
    # "Only NONE, NOSASL, LDAP, KERBEROS, CUSTOM "
    conn = hive.Connection(host=host_name, port=port, auth='NOSASL')
    cur = conn.cursor()
    cur.execute('show databases')
    result = cur.fetchall()

    return result

# Call above function
output = hiveconnection(host_name, port)
print(output)
```

Spark SQL

```
from pathlib import Path
import pandas as pd
import numpy as np

from pyspark.sql import SparkSession
spark = SparkSession.builder.appName('example_app').master('local[*]').getOrCreate()

spark.sql("show databases").show()
```

HDFS

```
from hdfs import InsecureClient

web_hdfs_interface = InsecureClient('http://localhost:50070')

web_hdfs_interface.list('/')
```