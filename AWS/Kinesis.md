# AWS Kinesis

Kinesis makes it easy to collect, process, and analyze real-time, streaming data. Kinesis can ingest real-time data such as video, audio, application logs, website clickstreams, and IoT telemetry data for machine learning, analytics, and other applications

## Kinesis Data Streams

A massively scalable, highly durable data ingestion and processing service optimized for streaming data. You can configure hundreds of thousands of data producers to continuously put data into a Kinesis data stream. Data records are therefore stored in shards in your stream temporarily. The time period from when a record is added to when it is no longer accessible is called the **retention period**. A Kinesis data stream stores records from *24 hours by default* to a maximum of 8760 hours (365 days).

## Kinesis Data Firehose

The easiest way to load streaming data into data stores and analytics tools. Data Firehose is a fully managed service that automatically scales to match the throughput of your data.

It can also batch, compress, and encrypt the data before loading it.
It can capture, transform, and load streaming data into S3, Redshift, Elasticsearch Service, generic HTTP endpoints, and service providers like Datadog, New Relic, MongoDB, and Splunk, enabling near real-time analytics with existing business intelligence tools and dashboards being used today.

## *Resources*

- [Tutorials Dojo Kinesis Cheat Sheet](https://tutorialsdojo.com/amazon-kinesis/)