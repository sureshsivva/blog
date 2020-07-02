---
title: Spark User Classpath First
author: Suresh Siva
date: 2020-06-25 08:00:00 +0800
categories: [Spark, Setup]
tags: [spark, pyspark, classpath, issues, library, spark-submit]
math: true
---

## Properties

```shell
spark.driver.userClassPathFirst=true
spark.executor.userClassPathFirst=true
```

The above 2 properties help us to give the precedence to the user submitted libraries as the first things to be used while initializing the Spark context.

This option helps us more when there is a conflict between the Spark's internal jars and user submitted jars or theirs dependencies. It may happen mostly on older Spark clusters where we happened to use some recent versions of the third party jars.

>
[Note: This approach is still in **experimental** phase and used in **cluster mode only** by the time of writing, use it wisely]

## Demo

## Environment

- Spark : 2.2.0
- Spark-Cosmosdb-Connector : 2.4.0_2.11-3.0.5

I happened to be in a situation to use more recent version of the `spark-cosmosdb-connector` connector to get most of the recent features from a Spark cluster which's version lags behind.

The `spark-cosmosdb-connector` 3.0.5 version expects a recent version of the `httpclient` library which conflicts with the Spark cluster's `httpclient` version `4.2.5`. The command I used is,

```shell
pyspark2 --master yarn \
         --conf "spark.dyanmicAllocation.enabled=true" \
         --conf "spark.dynamicAllocation.maxExecutors=25" \
         --executor-memory 8g \
         --executor-cores 4 \
         --driver-memory 4g \
         --driver-cores 1 \
         --queue queue_name \
         --jars "hdfs://CLUSTER/path/to/jars/azure-cosmosdb-spark_2.4.0_2.11-3.0.5.jar,hdfs://CLUSTER/path/to/jars/azure-documentdb-2.4.7.jar,hdfs://CLUSTER/path/to/jars/java-uuid-generator-4.0.1.jar,hdfs://CLUSTER/path/to/jars/httpclient-4.5.12.jar"

```

The error I was getting is,

![HttpClient Error]({{ "/assets/img/posts/20200625_http_client_error.png" | relative_url }})

When tracing the root cause, it became obvious that the Spark cluster's `httpclient` is way older than the the `httpclient` version expected by the `azure-cosmos-connector`, hence this was blocking the execution.

## Fix

Using the `spark.{driver,executor}.userClassPathFirst` configurations on Spark command has helped fixing this issue.

The working Spark command I was using is,

<script src="https://gist.github.com/suresiva/22b9d3b27da18135c284d6a01d2ef8af.js"></script>

Hope this helps!!
