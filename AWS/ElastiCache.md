# ElastiCache

Amazon ElastiCache allows you to seamlessly set up, run, and scale popular open-Source compatible in-memory data stores in the cloud. Build data-intensive apps or boost the performance of your existing databases by retrieving data from high throughput and low latency in-memory data stores. Amazon ElastiCache is a popular choice for real-time use cases like Caching, Session Stores, Gaming, Geospatial Services, Real-Time Analytics, and Queuing.

## ElastiCache for Redis

Amazon ElastiCache offers fully managed Redis and Memcached for most demanding applications that require sub-millisecond response times. However, ***Redis is the only service in Elasticache that supports replication***.

Using `Redis AUTH` command can improve data security by requiring the user to enter a password before they are granted permission to execute Redis commands on a password-protected Redis server. 

To require that users enter a password on a password-protected Redis server, include the parameter `--auth-token` with the correct password when you create your replication group or cluster and on all subsequent commands to the replication group or cluster.

## *Resources* 

- https://tutorialsdojo.com/amazon-elasticache/
- https://aws.amazon.com/elasticache/redis-vs-memcached/