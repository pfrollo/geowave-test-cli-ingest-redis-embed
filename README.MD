# Introduction

The motivation behind the project was to provide a quick way
 to build and run basic elements of GeoWave without all the baggage
 the GeoWave projects brings in and help people learning GeoWave.
 This project builds and starts in seconds versus minutes. One can set breakpoints
 to learn about GeoWave implementation.
 
 
The project currently contains only the essential dependencies needed to ingest GDELT data
 into embedded REDIS in memory storage. If you examine `pom.xml` you can see these
 essential dependencies.
 
 
Later you can add more dependencies into the project for further exploration of GeoWave. 

Create a GitHub issue or a pull request with a fix if there is an issue with this project or have questions.

 
## Run Configurations 
If you are using IntelliJ IDEA you can take advantage of several built in run configurations:
* Start REDIS store
* Add REDIS store to GeoWave
* Add data index to GeoWave
* Ingest GDELT data

These configurations are stored at `.idea\runConfigurations`.


These run configurations where created using GeoWave documentation. You should start first
with setting up of a standalone GeoWave instance and then running through their
[GeoWave Quickstart Guide - Vector Demo](https://locationtech.github.io/geowave/walkthrough-vector.html#)
 so that you understand the process and obtain GDELT data this project works with.  

 
If you are using a different IDE then you can create your own run configurations.


## Exercises and Important Classes

You can set breakpoints at the classes mentioned below to learn how the ingestion process works.

* `org.locationtech.geowave.core.ingest.operations.LocalToGeowaveCommand` class is responsible for ingestion
data from the local file system, S3, or HDFS. See `geowave help ingest` or `geowave help ingest localtogw`
for more information.

* Ingestion test is at `org.locationtech.geowave.format.gdelt.GDELTIngestTest`.

* `org.locationtech.geowave.format.gdelt.GDELTIngestPlugin#toGeoWaveDataInternal` responsible for conversion
 of data files to GeoWave data format.

* `org.locationtech.geowave.core.store.ingest.AbstractLocalFileIngestDriver#write` is responsible
 for writing `GeoWaveData`, the GeoWave representation of ingested data, into the data storage.
 `GeoWaveData` represents `SimpleFeature` one row of data read from a zip ingested file.
 The writer used here is selected based on adapterId and specified index. When you ingest GDELT data
 you will discover that `IndexCompositeWriter` is used to write the data to the storage. 
 


## Notes
Q: Where the GeoWave configuration file is stored?

A: It is stored in the user's directory `~/.geowave/${project.parent.version}-config.properties`.
This is where for example information about REDIS and GDELT is stored:
```
store.default-redis.opts.address=redis\://127.0.0.1\:6379
store.default-redis.opts.gwNamespace=geowave.default
store.default-redis.type=redis
store.default-rocksdb.opts.gwNamespace=default
store.default-rocksdb.type=rocksdb
store.gdelt.opts.address=redis\://127.0.0.1\:6379
store.gdelt.opts.aggregationMaxRangeDecomposition=-2147483648
store.gdelt.opts.compression=SNAPPY
store.gdelt.opts.dataIndexBatchSize=-2147483648
store.gdelt.opts.enableBlockCache=true
store.gdelt.opts.enableSecondaryIndexing=false
store.gdelt.opts.enableServerSideLibrary=true
store.gdelt.opts.gwNamespace=geowave.gdelt
store.gdelt.opts.maxRangeDecomposition=-2147483648
store.gdelt.opts.persistDataStatistics=true
store.gdelt.type=redis
```
---
Q: What is the purpose of ${project.parent.version}-config.properties.key configuration file?

A:  

---
Q: Which driver is used to ingest data?

A: `org.locationtech.geowave.core.ingest.local.LocalFileIngestCLIDriver.LocalFileIngestCLIDriver`

--- 
Q: How can I speed up the data ingestion?

A: Number of ingestion threads can be increased with `-t, --threads` parameter.\
The thread pool is created at `org.locationtech.geowave.core.store.ingest.AbstractLocalFileIngestDriver.startExecutor`

---
