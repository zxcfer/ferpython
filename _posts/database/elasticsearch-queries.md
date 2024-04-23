---
layout: post
title: "ElasticSearch Queries"
tags: ["elasticsearch"]
---

```bash
bin/elasticsearch-setup-passwords interactive
```

you should enamble X-Pack in `config/elasticsearch.yml`

```
xpack.security.enabled: true
```

# Cofniguration

`elasticsearch.yml` set the cluster name `cluster.name`

in the case of nodes set `node.name`

```bash
curl -XGET 'localhost:9200/_cluster/health?pretty'
curl -XGET 'localhost:9200/_cluster/state?pretty'
curl -XGET 'localhost:9200/_cluster/stats?pretty'
curl -XGET 'localhost:9200/_nodes/stats?pretty'
curl -XGET 'localhost:9200/_nodes/?pretty'
curl -XGET 'localhost:9200/_nodes/plugins'
curl -XGET 'localhost:9200/_nodes/node-1/stats?pretty'
curl -XGET 'localhost:9200/_nodes/stats/indices?pretty'
curl -XGET 'localhost:9200/_nodes/stats/ingest?pretty'
curl -XGET 'localhost:9200/_nodes/stats/ingest,fs?pretty'
curl -XGET 'localhost:9200/_nodes/stats/_all?pretty'
curl -XGET 'localhost:9200/_nodes/stats?metric=_all?pretty'
```

```bash
curl -XGET 'localhost:9200/_cluster/pending_tasks?pretty'
curl -XGET 'localhost:9200/_tasks'
curl -XGET 'localhost:9200/_tasks?nodes=node1,node2&actions=cluster:*&pretty'
curl -XGET 'localhost:9200/_tasks/43r315an3xamp13'
```


### POST `employees/_search`

```json
{
  "query": {
    "match": {
      "phrase": {
        "query" : "heuristic"
      }
    }
  }
}
```

### PUT `_cluster/settings`

```json
{
  "persistent": {
    "cluster.routing.allocation.exclude._name": null
  }
}
```

