---
title: elasticsearch intro
date: 2018-06-11 22:34:17
categories:
  - elasticsearch
tags:
  - elasticsearch
  - ELK
---
## How to use

### Take it easy

**The Mists of Time**

Many years ago, a newly married unemployed developer called Shay Banon followed his wife to London, where she was studying to be a chef. While looking for gainful employment, he started playing with an early version of Lucene, with the intent of building his wife a recipe search engine.

Working directly with Lucene can be tricky, so Shay started work on an abstraction layer to make it easier for Java programmers to add search to their applications. He released this as his first open source project, called Compass.

Later Shay took a job working in a high-performance, distributed environment with in-memory data grids. The need for a high-performance, real-time, distributed search engine was obvious, and he decided to rewrite the Compass libraries as a standalone server called Elasticsearch.

The first public release came out in February 2010. Since then, Elasticsearch has become one of the most popular projects on GitHub with commits from over 300 contributors. A company has formed around Elasticsearch to provide commercial support and to develop new features, but Elasticsearch is, and forever will be, open source and available to all.

Shay’s wife is still waiting for the recipe search…

[«  Getting Started](https://www.elastic.co/guide/en/elasticsearch/guide/current/getting-started.html)  
- [elastic/elasticsearch-definitive-guide: The Definitive Guide to Elasticsearch](https://github.com/elastic/elasticsearch-definitive-guide/)
- [ElasticSearch Cookbook, Second Edition: Alberto Paro: 9781783554836: Amazon.com: Books](https://www.amazon.com/ElasticSearch-Cookbook-Second-Alberto-Paro/dp/1783554835/ref=dp_ob_title_bk?dpID=51w76jr4KML&preST=_SX218_BO1,204,203,200_QL40_&dpSrc=detail)

#### use cases
- Tag Cloud
![1527839724538](/assets/1527839724538.jpg)
- Heatmaps
![1527839786708](/assets/1527839786708.jpg)
- Vector Maps
![1527839847776](/assets/1527839847776.jpg)
- Detect Abnormal
![1527842535887](/assets/1527842535887.jpg)
```
UID: 0000000000600036

// detect abnormal
tags:watchdog_frame AND message: (+0000000000600036)
```
- Wikipedia uses Elasticsearch to provide full-text search with highlighted search snippets, and *search-as-you-type* and *did-you-mean* suggestions.
  - [Wikimedia moving to Elasticsearch – Wikimedia Blog](https://blog.wikimedia.org/2014/01/06/wikimedia-moving-to-elasticsearch/)
  - [Logstash - Wikitech](https://wikitech.wikimedia.org/wiki/Logstash)


- *The Guardian* uses Elasticsearch to combine visitor logs with social-network data to provide real-time feedback to its editors about the public’s response to new articles.
![1527831641278](/assets/1527831641278.jpg)
  - [The Guardian uses the Elastic Stack to deliver real-time visibility of site traffic | Elastic](https://www.elastic.co/use-cases/guardian)
  - [Making Journalism Better With Elasticsearch | Elastic](https://www.elastic.co/elasticon/tour/2015/london/making-journalism-better-with-elasticsearch)
  - [How Elasticsearch Powers the Guardian's Newsroom](https://www.infoq.com/presentations/elasticsearch-guardian)

- Stack Overflow combines full-text search with geolocation queries and uses *more-like-this* to find related questions and answers.
  - [Stack Overflow Uses Facets and Geo-Coding | Elastic](https://www.elastic.co/videos/stack-overflow-uses-facets-and-geo-coding)
  - [How does Stack Overflow implement its search indexing? - Meta Stack Exchange](https://meta.stackexchange.com/questions/187431/how-does-stack-overflow-implement-its-search-indexing/187501#187501)
  - [A new search engine for Stack Exchange - Meta Stack Exchange](https://meta.stackexchange.com/questions/160100/a-new-search-engine-for-stack-exchange)
  - [Nick Craver - Stack Overflow: The Architecture - 2016 Edition](https://nickcraver.com/blog/2016/02/17/stack-overflow-the-architecture-2016-edition/)
  - [StackOverflow Update: 560M Pageviews a Month, 25 Servers, and It's All About Performance - High Scalability -](http://highscalability.com/blog/2014/7/21/stackoverflow-update-560m-pageviews-a-month-25-servers-and-i.html)

- GitHub uses Elasticsearch to query 130 billion lines of code.
![1527833552771](/assets/1527833552771.jpg)
  - [GitHub uses Elasticsearch to index over 8 million code repositories | Elastic](https://www.elastic.co/use-cases/github)
  - [Elasticsearch in Anger: Stories from the GitHub Search Clusters | Elastic](https://www.elastic.co/elasticon/2015/sf/elasticsearch-in-anger-stories-from-the-github-search-clusters)

- [15 Companies Using the ELK Stack](https://logz.io/blog/15-tech-companies-chose-elk-stack/)

#### use Date Range
```
// search log in the defined Range
logtime:[2018-05-01 TO 2018-05-30]

```

#### use tags and message to search frameLog

```
//search tags is watchdog_frame and message contains 82973 (orderId)
tags:watchdog_frame AND message: ( 82973)

// 下发命令
// OrderUpdateOperation(下发订单)
tags:watchdog_frame AND message: (0000000000600042 AND "0x01,0x81")

// TimeAdjustOperation(时间调整)
tags:watchdog_frame AND message: (0000000000600042 AND "0x01,0x04")

// AirConditionerOperation(空调配置)
tags:watchdog_frame AND message: (0000000000600042 AND "0x01,0x06")

// OutputOperation(output控制)
tags:watchdog_frame AND message: (0000000000600042 AND "0x01,0x82")

// OutputOperation(output控制)
tags:watchdog_frame AND message: (0000000000600042 AND "0x01,0x82")

// RealTimeOperation(实时操作)
tags:watchdog_frame AND message: (0000000000600042 AND "0x01,0x84")

// start RealTimeOperation(实时操作)

// 请求上报状态信息报文命令
tags:watchdog_frame AND message: (0000000000600042 AND "0x01,0x84" AND "command=0x00")

// 请求上报版本号命令
tags:watchdog_frame AND message: (0000000000600042 AND "0x01,0x84" AND "command=0x01")

// 远程重启命令
tags:watchdog_frame AND message: (0000000000600042 AND "0x01,0x84" AND "command=0x02")

// reset命令
tags:watchdog_frame AND message: (0000000000600042 AND "0x01,0x84" AND "command=0x03")

// 服务器开门命令
tags:watchdog_frame AND message: (0000000000600042 AND "0x01,0x84" AND "command=0x04")

// 请求位置命令
tags:watchdog_frame AND message: (0000000000600042 AND "0x01,0x84" AND "command=0x05")

// 请求GSM信息命令
tags:watchdog_frame AND message: (0000000000600042 AND "0x01,0x84" AND "command=0x06")

// 设备锁命令
tags:watchdog_frame AND message: (0000000000600042 AND "0x01,0x84" AND "command=0x07")

// end RealTimeOperation(实时操作)

// OutputModeConfiguration(输出模式)
tags:watchdog_frame AND message: (0000000000600042 AND "0x01,0x08")

// MultimediaOperation(多媒体操作)
tags:watchdog_frame AND message: (0000000000600042 AND "0x01,0x83")

// 上报报文

// RoutineStatusReport(空调关)
tags:watchdog_frame AND message: (0000000000600042 AND "0x03,0x03")

// RoutineStatusReport(空调关)
tags:watchdog_frame AND message: (0000000000600042 AND "0x03,0x03" AND "airConditionState" AND "State:Close")

// RoutineStatusReport(空调开)
tags:watchdog_frame AND message: (0000000000600042 AND "0x03,0x03" AND "airConditionState" AND "State:Open")

// RoutineStatusReport(开机报文)
tags:watchdog_frame AND message: (0000000000600042 AND "0x03,0x01")

// RoutineStatusReport(关机报文)
tags:watchdog_frame AND message: (0000000000600042 AND "0x03,0x02")

// RoutineStatusReport(协议看门狗重启报文)
tags:watchdog_frame AND message: (0000000000600042 AND "0x03,0x05")

// UserInputReport(用户输入事件报文)
tags:watchdog_frame AND message: (0000000000600042 AND "0x03,0x21")

// DoorStatusReport(门禁状态)
tags:watchdog_frame AND message: (0000000000600042 AND "0x03,0x22")

// GSMModuleReport(版本信息)
tags:watchdog_frame AND message: (0000000000600042 AND "0x03,0x92")

// SensorAlarmReport(门禁报警)
tags:watchdog_frame AND message: (0000000000600042 AND "0x03,0x31" AND "DoorAlarm")

// SensorAlarmReport(烟雾报警)
tags:watchdog_frame AND message: (0000000000600042 AND "0x03,0x31" AND "SmokeAlarm")

// PowerEventReport(电源事件)
tags:watchdog_frame AND message: (0000000000600042 AND "0x03,0x11")

// GSMModuleReport(GSM卡信息)
tags:watchdog_frame AND message: (0000000000600042 AND "0x03,0x92")

// LocationReport(定位)
tags:watchdog_frame AND message: (0000000000600042 AND "0x03,0x91")

// HeartBeat(心跳包)
tags:watchdog_frame AND message: (0000000000600042 AND "0x04,0xFF")

```

#### search ActionLog

```
logType: WARN
logType: INFO
logType: ERROR
```

#### more

```
// use regex
tags:watchdog_frame AND message: (+0000000000600042 AND 0x0?,0x0?)
```

#### Direct access to the Elasticsearch API
```
// indices setting
$ curl -XPUT https://<endpoint>/blog -d '{
"settings" : { "number_of_shards" : 3, "number_of_replicas" : 1 } }'

// create a post
$ curl -XPOST http://<endpoint>/blog/post/1 -d '{
"author":"jon handler",
"title":"Amazon ES Launch" }'

// bulk create posts
$ curl -XPOST https://<endpoint>/blog/post/_bulk -d '
{ "index" : { "index" : "blog", "type" : "post", "_id" : "2"}}
{"title":"Amazon ES for search", "author": "carl meadows"},
{ "index" : { "index":"blog", "type":"post", "_id":"3" } }
{ "title":"Analytics too", "author": "vivek sriram"}'

// search posts
$ curl -XGET http://<endpoint>/_search?q=ES
{
   "took":16,
   "timed_out":false,
   "shards":{
      "total":3,
      "successful":3,
      "failed":0
   },
   "hits":{
      "total":2,
      "max_score":0.13424811,
      "hits":[
         {
            "index":"blog",
            "type":"post",
            "id":"1",
            "score":0.13424811,
            "source":{
               "author":"jon handler",
               "title":"Amazon ES Launch"
            }
         },
         {
            "index":"blog",
            "type":"post",
            "id":"2",
            "score":0.11506981,
            "_source":{
               "title":"Amazon ES for search",
               "author":"carl meadows"
            },

         }
      ]
   }
}

// Is it running?
http://47.97.104.178:9200/?pretty
{
  "name" : "Vvew76v",
  "cluster_name" : "elasticsearch",
  "cluster_uuid" : "RRMIEU-MQUS-BE5sVOKDKQ",
  "version" : {
    "number" : "6.1.1",
    "build_hash" : "bd92e7f",
    "build_date" : "2017-12-17T20:23:25.338Z",
    "build_snapshot" : false,
    "lucene_version" : "7.1.0",
    "minimum_wire_compatibility_version" : "5.6.0",
    "minimum_index_compatibility_version" : "5.0.0"
  },
  "tagline" : "You Know, for Search"
}

```

- [Query String Query | Elasticsearch Reference [6.x] | Elastic](https://www.elastic.co/guide/en/elasticsearch/reference/6.x/query-dsl-query-string-query.html#query-string-syntax)



## How to view

### Why Elastic

#### Distributed & Scalable

- Resilient; designed for scale-out

- High availability; multitenancy

- Structured & unstructured data

#### Developer Friendly

- Schemaless

- Native JSON

- Client libraries

- Apache Lucene

#### Search & Analytics

- Near Real-time

- Full-text search

- Aggregations

- Geospatial

- Multilingua

### The Elastic Stack
 ![1527665943347](/assets/1527665943347.jpg)

### Architecture
![1527670661895](/assets/1527670661895.jpg)

### Elasticsearch Cluster deploy
![1527836752076](/assets/1527836752076.jpg)


### TERMINOLOGY

| MySQL                   | Elastic Search        |
| ----------------------- | --------------------- |
| Database                | Index                 |
| Table                   | Type                  |
| Row                     | Document              |
| Column                  | Field                 |
| Schema                  | Mapping               |
| Index                   | Everything is indexed |
| Partition               | Shard                 |
| SQL                     | Query DSL             |
| SELECT field, COUNT(*)FROM table GROUP BY field | Facet(Aggregations)          |
| SELECT * FROM table ... | GET http://...        |
| UPDATE table SET ...    | PUT http://...        |

## How to understand

### Basic Concepts

- Cluster:
A cluster consists of one or more nodes which share the same cluster name. Each cluster has a single master node which is chosen automatically by the cluster and which can be replaced if the current master node fails


- Node:
A node is a running instance of ElasticSearch which belongs to a cluster. Multiple nodes can be started on a single server for testing purposes, but usually you should have one node per server. At startup, a node will use unicast for multicast, if specified) to discover an existing cluster with the same cluster name and will try to join that cluster.

- Index:
An index is like a database in a relational database. It has a mapping which defines multiple types. An index is a logical namespace which maps to one or more primary shards and can have zero or more replica shards.

- Type:
A type is like a table in a relational database. Each type has a list of fields that can be specified for documents of that type. The mapping defines how each field in the document is analyzed.

- Document:
A document is a SON document which is stored in ElasticSearch. it is like a row in a table in a relational database. Each
 document is stored in an index and has a type and an id a document is a JSON object(also known in other languages as a hash/hashmap/associative array) which contains zero or more fields, or key-value pairs. The original JSON document that is indexed will be stored in the `_source` field, which is returned by default when getting or searching for a document.

- Field:
A document contains a list of fields, or key-value pairs. The value can be a simple(scalar) value (eg a string, integer, date),or a nested structure like an array or an object. A field is similar to a column in a table in a relational database. The mapping for each field has a field type (not to be confused with document type)which indicates the type of data that can be stored in that field, eg integer, string, object. The mapping also allows you to define (amongst other things) how the value for a field should be analyzed.

- Mapping:
A mapping is like a 'schema definition' in a relational database. Each index has a mapping, which defines each type within the index, plus a number of index-wide settings A mapping can either be defined explicitly, or it will be generated automatically when a document is indexed.

- Facets(Aggregations):
Faceted search refers to a way to explore large amounts of data by displaying summaries about various partitions of the data and later allowing to narrow the navigation to a specific partition.
In Elasticsearch, `facets` are also the name of a feature that allowed to compute these summaries. `facets` have been replaced by [aggregations](https://www.elastic.co/guide/en/elasticsearch/reference/6.1/search-aggregations.html) in Elasticsearch 1.0, which are a superset of facets.

- Shard:
A shard is a single Lucene instance. It is a low-level "worker" unit which is managed automatically by ElasticSearch. An index is a logical namespace which points to primary and replica shards.
ElasticSearch distributes shards amongst all nodes in the cluster, and can move shards automatically from one node to another in the case of node failure, or the addition of new nodes
  - [lucene - need elasticsearch index sharding explanation - Stack Overflow](https://stackoverflow.com/questions/47003336/need-elasticsearch-index-sharding-explanation?rq=1)

- Primary Shard:
Each document is stored in a single primary shard. When a document is send for indexing, it is indexed first on the primary shard, then on all replicas of the primary shard. By default, an index has 5 primary shards. You can specify fewer or more primary shards to scale the number of documents that your index can handle.

- Replica Shard:
Each primary shard can have zero or more replicas. A replica is a copy of the primary shard, and has two purposes:
a. increase failover: a replica shard can be promoted to a primary shard if the primary fails.
b. increase performance: get and search requests can be handled by primary or replica shards.
- Identified by "\_index/\_type/\_id"

### Configuration

- cluster.name:
Cluster name identifies duster for auto-discovery If production environment has multiple clusters on the same network, duster name must be unique.
- node.name:
Node names are generated dynamically on startup. But user can specify a name to node manual.
- node.master&node.data:
Every node can be configured to allow or deny being eligible as the master, and to allow or deny to store the data, Master allow this node to be eligible as a master node(enabled by default)and Data allow this node to store data (enabled by default)

Following are the settings to design advanced duster topologies.

1. If a node to never become a master node, only to hold data. This will be the" workhorse"of the duster.
`node master: false, node data: true`

2. If a node to only serve as a master and not to store data and to have free resources. This will be the "coordinator" of the cluster.
`node master: true, node data: false`

3. If a node to be neither master nor data node, but to act as a"search load balancer"(fetching data from nodes, aggregating, etc)
`node master: false, node data: false`

- Index:
A number of options(such as shard/replica options, mapping or analyzer definitions, translog settings, .) can be set for indices globally, in this file.
Note, that it makes more sense to configure index settings specifically for a certain index, either when creating it or by using the index templates API..
example.
`index.number_of_shards: 5, index.number_of_replicas: 1`

- Discovery:
ElasticSearch supports different types of discovery, which makes multiple ElasticSearch instances talk to each other.
The default type of discovery is multicast. Unicast discovery allows to explicitly control which nodes will be used to discover the duster. it can be used when multicast is not present, or to restrict the duster communication-wise.

**Index Versus Index Versus Inverted Index**

![invertedIndex](/assets/invertedIndex.jpg)

You may already have noticed that the word *index* is overloaded with several meanings in the context of Elasticsearch. A little clarification is necessary:

- Index (noun)

  As explained previously, an *index* is like a *database* in a traditional relational database. It is the place to store related documents. The plural of *index* is *indices* or *indexes*.

- Index (verb)

  *To index a document* is to store a document in an *index (noun)* so that it can be retrieved and queried. It is much like the `INSERT` keyword in SQL except that, if the document already exists, the new document would replace the old.

- Inverted index

  Relational databases add an *index*, such as a B-tree index, to specific columns in order to improve the speed of data retrieval. Elasticsearch and Lucene use a structure called an *inverted index* for exactly the same purpose. By default, every field in a document is *indexed* (has an inverted index) and thus is searchable. A field without an inverted index is not searchable. We discuss inverted indexes in more detail in [Inverted Index](https://www.elastic.co/guide/en/elasticsearch/guide/current/inverted-index.html).
  - [A first take at building an inverted index](https://nlp.stanford.edu/IR-book/html/htmledition/a-first-take-at-building-an-inverted-index-1.html)
  - [Th30z (Matteo Bertozzi Code): Python: Inverted Index for dummies](http://th30z.blogspot.com/2010/10/python-inverted-index-for-dummies.html)

### Cluster Architecture
  ![1527670820582](/assets/1527670820582.jpg)
  - Partitioning your documents into different containers or shards, which can bestored on a single node or on multiple nodes.
  - Balancing these shards across the nodes in your cluster to spread the indexing andsearch load.
  - Duplicating each shard to provide redundant copies of your data, to prevent dataloss in case of hardware failure.
  - Routing requests from any node in the cluster to the nodes that hold the data you’reinterested in.
  - Seamlessly integrating new nodes as your cluster grows or redistributing shards torecover from node loss.

### Index Request
![1527845763041](/assets/1527845763041.jpg)  
```
Request :
PUT test/cities/1 {
"rank": 3,
"city": "Hyderabad",
"state": "Telangana", "population2014": 7750000, "land_area": 625, "location":
{
"lat": 17.37,
"lon": 78.48 },
"abbreviation": "Hyd" }
Response : { "_index": "test", "_type": "cities", "_id": "1", "_version": 1, "created": true }
```
### Search Request
![1527845880572](/assets/1527845880572.jpg)
```
Request :
GET test/cities/1?pretty
Response : {
"_index": "test", "_type": "cities", "_id": "1", "_version": 1, "found": true, "_source": {
"rank": 3,
"city": "Hyderabad",
"state": "Telangana", "population2014": 7750000, "land_area": 625, "location": {
"lat": 17.37,
"lon": 78.48 },
"abbreviation": "Hyd" }
}
```
### Updating a document
```
Request :
PUT test/cities/1 {
"rank": 3,
"city": "Hyderabad",
"state": "Telangana", "population2013": 7023000, "population2014": 7750000, "land_area": 625,
"location":
{
"lat": 17.37,
"lon": 78.48 },
"abbreviation": "Hyd" }
Response : {"_index": "test", "_type": "cities", "_id": "1", "_version": 2, "created": false}
```
### Searching
- Search across all indexes and all types
`http://localhost:9200/_search`

- Search across all types in the test index.
`http://localhost:9200/test/_search`

- Search explicitly for documents of type cities within the test index.
`http://localhost:9200/test/cities/_search`

## Reference:
  - [Database index - Wikipedia](https://en.wikipedia.org/wiki/Database_index)
  - [Inverted index - Wikipedia](https://en.wikipedia.org/wiki/Inverted_index)
  - [B+ tree - Wikipedia](https://en.wikipedia.org/wiki/B%2B_tree)
  - [Aggregation features, Elasticsearch vs. MySQL (vs. MongoDB) - Ulf WendelUlf Wendel](http://blog.ulf-wendel.de/2016/aggregation-features-elasticsearch-vs-mysql-vs-mongodb/)
  - [ElasticSearch-Head](https://github.com/mobz/ElasticSearch-head)
  - [Marvel](http://www.elastic.co/guide/en/marvel/current/#_marvel_8217_s_dashboards)
  - [Paramedic](https://github.com/karmi/ElasticSearch-paramedic)
  - [Bigdesk](https://github.com/lukas-vlcek/bigdesk/)
