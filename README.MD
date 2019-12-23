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

You can set breakpoints at the classes mentioned below to learn how ingestion work.

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







