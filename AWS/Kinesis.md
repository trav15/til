# Amazon Kinesis

Kinesis makes it easy to collect, process, and analyze real-time, streaming data. Kinesis can ingest real-time data such as video, audio, application logs, website clickstreams, and IoT telemetry data for machine learning, analytics, and other applications

## Kinesis Data Streams

A massively scalable, highly durable data ingestion and processing service optimized for streaming data. You can configure hundreds of thousands of data producers to continuously put data into a Kinesis data stream. Data records are therefore stored in shards in your stream temporarily. The time period from when a record is added to when it is no longer accessible is called the **retention period**. A Kinesis data stream stores records from *24 hours by default* to a maximum of 8760 hours (365 days).

## Kinesis Data Firehose

The easiest way to load streaming data into data stores and analytics tools. Data Firehose is a fully managed service that automatically scales to match the throughput of your data.

It can also batch, compress, and encrypt the data before loading it.
It can capture, transform, and load streaming data into S3, Redshift, Elasticsearch Service, generic HTTP endpoints, and service providers like Datadog, New Relic, MongoDB, and Splunk, enabling near real-time analytics with existing business intelligence tools and dashboards being used today.

## Kinesis Data Analytics

Analyze streaming data, gain actionable insights, and respond to your business and customer needs in real time. You can quickly build SQL queries and Java applications using built-in templates and operators for common processing functions to organize, transform, aggregate, and analyze data at any scale. You can capture streaming data with [Data Streams](#kinesis-data-streams) or [Data Firehose](#kinesis-data-firehose) and use Data Analytics to query and analyze streaming data. Data Analytics can then send processed data to analytics tools so you can create alerts and respond in real-time.

- Kinesis Data Analytics is serverless and takes care of everything required to continuously run your application.
- Kinesis Data Analytics elastically scales applications to keep up with any volume of data in the incoming data stream.
- Kinesis Data Analytics delivers sub-second processing latencies so you can generate real-time alerts, dashboards, and actionable insights.

## Kinesis Video Streams

Amazon Kinesis Video Streams makes it easy to securely stream video from connected devices to AWS for analytics, machine learning (ML), playback, and other processing. Kinesis Video Streams is serverless and automatically provisions and elastically scales all the infrastructure needed to ingest streaming video data from millions of devices. Kinesis Video Streams enforces Transport Layer Security (TLS)-based encryption on data streaming from devices, and encrypts all data at rest using AWS KMS.

## *Resources*

- [Tutorials Dojo Kinesis Cheat Sheet](https://tutorialsdojo.com/amazon-kinesis/)
- [AWS docs Kinesis](https://docs.aws.amazon.com/kinesis/index.html)
- [AWS docs Data Streams](https://docs.aws.amazon.com/streams/latest/dev/introduction.html)
- [AWS docs Data Firehose](https://docs.aws.amazon.com/firehose/latest/dev/what-is-this-service.html)
- [AWS docs Data Analytics](https://docs.aws.amazon.com/kinesisanalytics/latest/dev/what-is.html)
- [AWS docs Video Streams](https://docs.aws.amazon.com/kinesisvideostreams/latest/dg/what-is-kinesis-video.html)