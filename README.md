# Docker Kit

Docker kit is a collection of docker-compose that easily to find, copy, and paste.

This really helpful to setup local environment.

## Directory
```
➜  docker-kit git:(master) tree -d    
.
├── auth
│   ├── FusionAuth
│   ├── keycloak
│   ├── Ory
│   ├── permify
│   └── SuperTokens
├── board
│   ├── frappe-crm
│   └── tasks.md
├── broker-queue
│   ├── kafka-zookeeper
│   ├── nats
│   │   └── jetstream-cluster
│   │       ├── nats1
│   │       │   └── jetstream
│   │       │       ├── $G
│   │       │       │   └── streams
│   │       │       │       └── KV_bucket-uk
│   │       │       │           ├── msgs
│   │       │       │           └── obs
│   │       │       └── $SYS
│   │       │           └── _js_
│   │       │               └── _meta_
│   │       │                   ├── msgs
│   │       │                   ├── obs
│   │       │                   └── snapshots
│   │       ├── nats2
│   │       │   └── jetstream
│   │       │       ├── $G
│   │       │       │   └── streams
│   │       │       │       ├── KV_bucket-ob-b
│   │       │       │       │   ├── msgs
│   │       │       │       │   └── obs
│   │       │       │       └── KV_bucket-ob-s
│   │       │       │           ├── msgs
│   │       │       │           └── obs
│   │       │       └── $SYS
│   │       │           └── _js_
│   │       │               └── _meta_
│   │       │                   ├── msgs
│   │       │                   ├── obs
│   │       │                   └── snapshots
│   │       └── nats3
│   │           └── jetstream
│   │               ├── $G
│   │               │   └── streams
│   │               │       ├── KV_bucket-h
│   │               │       │   ├── msgs
│   │               │       │   └── obs
│   │               │       ├── KV_bucket-rt
│   │               │       │   ├── msgs
│   │               │       │   └── obs
│   │               │       └── KV_market-mover
│   │               │           ├── msgs
│   │               │           └── obs
│   │               └── $SYS
│   │                   └── _js_
│   │                       └── _meta_
│   │                           ├── msgs
│   │                           ├── obs
│   │                           └── snapshots
│   ├── nsq
│   ├── rabbitmq
│   ├── redpanda
│   └── sqs
├── ci-cd
│   └── jenkins
├── code-quality
│   └── sonarqube
│       └── asset
├── config-secret
│   └── vault-consul
│       ├── consul
│       │   ├── config
│       │   └── data
│       └── vault
│           ├── config
│           ├── data
│           ├── logs
│           └── policies
├── config-toggle
│   └── unleash
├── data-key-value
│   ├── etcd
│   ├── memcached
│   ├── redis
│   └── redisinsight
├── data-search-engine
│   ├── elasticsearch
│   │   ├── assets
│   │   └── postman
│   ├── meilisearch
│   └── typesense
│       ├── assets
│       └── typesense-playground
│           ├── doc
│           ├── scripts
│           └── seed-data
├── database
│   ├── arangodb
│   ├── cassandra
│   ├── dicedb
│   ├── duckdb
│   ├── mongo
│   ├── mysql
│   ├── postgres
│   └── timescaledb
├── docs
│   ├── docmost
│   ├── paperless-ngx
│   │   ├── consume
│   │   └── export
│   └── pdfding
├── drawing
│   └── excalidraw
├── email-engine
│   └── mailhog
├── messaging-platform
│   └── zulip
└── trace-monitor
    └── jaeger
```

## References
- https://awesome-docker-compose.com