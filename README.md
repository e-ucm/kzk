Kafka And Zookeeper (kzk) Docker image
===

This repository provides everything you need to run Kafka with Zookeeper in Docker.

This Docker image is used in [Rage Analytics](https://github.com/e-ucm/rage-analytics). 
For more information check out the [docker-compose.yml](https://github.com/e-ucm/rage-analytics/blob/master/docker-compose.yml) file.

Why?
---
The main hurdle of running Kafka in Docker is that it depends on Zookeeper.
Compared to other Kafka docker images, this one runs both Zookeeper and Kafka
in the same container. This means:

* No dependency on an external Zookeeper host, or linking to another container
* Zookeeper and Kafka are configured to work together out of the box

Run
---
Optional ENV variables:
 * ADVERTISED_HOST: the external ip for the container, e.g. `docker-machine ip \`docker-machine active\``
 * ADVERTISED_PORT: the external port for Kafka, e.g. 9092
 * ZK_CHROOT: the zookeeper chroot that's used by Kafka (without / prefix), e.g. "kafka"
 * LOG_RETENTION_HOURS: the minimum age of a log file in hours to be eligible for deletion (default is 168, for 1 week)
 * LOG_RETENTION_BYTES: configure the size at which segments are pruned from the log, (default is 1073741824, for 1GB)
 * NUM_PARTITIONS: configure the default number of log partitions per topic

```bash
docker run -p 2181:2181 -p 9092:9092 --env ADVERTISED_HOST=`docker-machine ip \`docker-machine active\`` --env ADVERTISED_PORT=9092 spotify/kafka
```

Aditional Zookeeper Configuration
---
Aditional configuration for Zookeeper is established in the [aditionalZoo.cfg](https://github.com/e-ucm/kzk/blob/master/conf/aditionalZoo.cfg) file.

Public Build
---

https://registry.hub.docker.com/u/e-ucm/kzk/

Build from Source
---

    docker build -t e-ucm/kzk .
