---
title: 델타 레이크 소개
date: 2021-02-01 11:21:30
category: [Data Engineering, Deltalake]
tags:
---

# 개요

![Deltalake 로고](./delta-lake-logo-tm.png)

Delta Lake는 데이터 레이크에 안정성을 제공하는 오픈 소스 스토리지 계층입니다. ACID 트랜잭션을 제공하고, 확장 가능한 메타데이터를 처리하고, 스트리밍 및 일괄 처리 데이터 처리를 통합합니다. Delta Lake는 기존 데이터 레이크를 기반으로 하여 실행되며 Apache Spark API와 완벽하게 호환됩니다.

![Deltalake Flow](./delta-lake-overview.png)

## Deltalake 주요 특징

아래는 Deltalake의 주요 특징입니다.

### ACID 트랜잭션 on Spark

스파크의 약점아닌 약점은 ACID 트랜잭션이 불가하다는 것입니다. 델타레이크를 사용하면 스파크에서도 데이터에 ACID 트랜잭션을 적용할 수 있습니다. 이를 통해 데이터를 더욱 다채롭게 처리할 수 있습니다.

### 스트리밍 및 배치 통합

델타 레이크의 테이블은 배치 테이블이면서 스트리밍 소스, 싱크로 활용할 수 있습니다. 결론적으로 스트리밍 데이터를 수집하거나 인터렉티브한 쿼리를 수행하는 모든 작업이 기본적으로 가능합니다. 스트리밍 처리에 대해서는 아래 주요기능 & 사용법에서 더 자세하게 살펴보겠습니다.

### 스키마 강제

수집 중에 잘못된 레코드가 삽입되지 않도록 스키마의 변형을 감지하여 처리합니다.

### 시간 여행(Time travel)

데이터의 버전 관리를 통해 롤백(rollback), 전체 기록 감사 추적 및 재현 가능한 기계 학습 실험을 수행 할 수 있습니다.

### Upserts와 Delete

머지, 업데이트, 삭제 명령을 지원하여 변경 데이터 캡처, SCD (slowly-changing-dimension) 작업, 스트리밍 upsert 등과 같은 복잡한 처리를 지원합니다.

## 주요기능 & 사용법

## 사용법

### 1. Run interactively

스파크 쉘을 실행 할 때 —packages 옵션을 통해 델타레이크를 넣으면 쉘에서 코드 스니펫을 수행할 수 있습니다.

### 2.Run as a project

Maven이나 SBT를 통해 프로젝트를 구성하고 델타레이크 의존성을 추가하여 코드 스니펫을 수행하고 프로젝트를 수행할 수 있습니다. 이 페이지에서 [예제](https://github.com/delta-io/delta/tree/master/examples)를 찾을 수 있습니다.

```scala
bin/spark-shell --packages io.delta:delta-core_2.12:0.7.0 --conf "spark.sql.extensions=io.delta.sql.DeltaSparkSessionExtension" --conf "spark.sql.catalog.spark_catalog=org.apache.spark.sql.delta.catalog.DeltaCatalog"
```

## 테이블 생성하기

Delta table은 Dataframe을 delta포맷으로 써서 만들 수 있습니다.

```scala
val data = spark.range(0, 5)
data.write.format("delta").save("/tmp/delta-table")
```

## 데이터 읽기

Delta table 파일의 경로를 명시하여 데이터를 읽을 수 있습니다.

```scala
val df = spark.read.format("delta").load("/tmp/delta-table")
df.show()
```

## 데이터 수정(update)하기

### Overwrite

```scala
val data = spark.range(5, 10)
data.write.format("delta").mode("overwrite").save("/tmp/delta-table")
df.show()
```

### Conditional update without overwrite

Delta lake는 조건부 update, delete, merge(upsert)할 수 있는 API를 제공합니다.

```scala
import io.delta.tables._
import org.apache.spark.sql.functions._

val deltaTable = DeltaTable.forPath("/tmp/delta-table")

// Update every even value by adding 100 to it
deltaTable.update(
  condition = expr("id % 2 == 0"),
  set = Map("id" -> expr("id + 100")))

// Delete every even value
deltaTable.delete(condition = expr("id % 2 == 0"))

// Upsert (merge) new data
val newData = spark.range(0, 20).toDF

deltaTable.as("oldData")
  .merge(
    newData.as("newData"),
    "oldData.id = newData.id")
  .whenMatched
  .update(Map("id" -> col("newData.id")))
  .whenNotMatched
  .insert(Map("id" -> col("newData.id")))
  .execute()

deltaTable.toDF.show()
```

### time travel을 이용한 과거 데이터 조회

time travel을 이용하여 Delta table의 이전 스냅샷을 조회(query)할 수 있습니다. `versionAsOf` 옵션을 사용하세요. time travel에 대한 더 자세한 사항은 [이 페이지](https://docs.delta.io/latest/delta-batch.html#-deltatimetravel)에서 확인할 수 있습니다.

```scala
val df = spark.read.format("delta").option("versionAsOf", 0).load("/tmp/delta-table")
df.show()
```

### 테이블로 스트림 데이터 쓰기

Structured Streaming을 이용해 Delta에 데이터를 쓸 수 있습니다. Delta lake의 트랜잭션 로그는 exactly-once 처리를 보장합니다. 기본적으로 스트림은 append 모드입니다.

```scala
val streamingDf = spark.readStream.format("rate").load()
val stream = streamingDf.select($"value" as "id").writeStream.format("delta").option("checkpointLocation", "/tmp/checkpoint").start("/tmp/delta-table")
```

### 테이블에서 스트림으로 읽기

```scala
val stream2 = spark.readStream.format("delta").load("/tmp/delta-table").writeStream.format("console").start()
```

# References

[https://docs.microsoft.com/ko-kr/azure/databricks/delta/](https://docs.microsoft.com/ko-kr/azure/databricks/delta/)
