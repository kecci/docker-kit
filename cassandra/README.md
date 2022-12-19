# cassandra

## Open Cassandra CLI
Open cassandra with docker:
```
$ docker-compose exec cassandra /bin/bash

root@5632e0063892:/#
```

## Run cassandra query 

with command `cqlsh` :
```
root@5632e0063892:/# cqlsh

Connected to citizix at 127.0.0.1:9042
[cqlsh 6.1.0 | Cassandra 4.1.0 | CQL spec 3.4.6 | Native protocol v5]
Use HELP for help.
cqlsh>
```

## Show version
```
$ show version

[cqlsh 6.1.0 | Cassandra 4.1.0 | CQL spec 3.4.6 | Native protocol v5]
```

## Show list keyspaces
```
$ describe keyspaces

system       system_distributed  system_traces  system_virtual_schema
system_auth  system_schema       system_views
```

## Create keyspaces
create new keyspace name `first_app`:
```
$ CREATE KEYSPACE first_app
... WITH REPLICATION = {
...  'class' : 'NetworkTopologyStrategy',
...  'datacenter1' : 1
... } ;
}
```

## Use keyspaces (database)
Use keyspace `first_app`:
```
$ use first_app ;
```

## Describe tables
```
$ describe tables
```

## Create table
create table `users`
```
$ CREATE TABLE users (
... first_name text,
... last_name text,
... email text,
... PRIMARY KEY (email)
... ) ;
)
```

## Query table
```
$ select * from users;

 email | first_name | last_name
-------+------------+-----------

(0 rows)
```



## Exit
```
exit
exit
```