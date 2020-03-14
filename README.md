Demonstration : Kafka Monitoring Suite (Prometheus / Grafana)
==============================================================

This repository demonstrates how to use Prometheus and Grafana  for monitoring an Apache Kafka cluster.

## Getting Started

### Start Confluent Plateform using Docker

**1. Clone the Kafka Monitoring Suite repository.**
```
git clone https://github.com/streamthoughts/kafka-monitoring-suite-demo-prometheus.git
cd kafka-monitoring-suite-demo-prometheus
```
**2. Start Confluent/Kafka cluster.**

Deploy Kafka, Prometheus and Grafana services using Docker. Depending on your network speed, this may take few minutes to download all images.

```bash
./monitoring-suite-start
```

**3. Create topic.**

Create `demo-topic` with 6 partitions and 3 replicas.

```bash
$KAFKA_HOME/bin/kafka-topics --create --partitions 6 --replication-factor 3 --topic demo-topic
```

**4. Produce messages.**

Open a new terminal window, generate some message to simulate producer load. 

* [Kafka Benchmark Commands](https://gist.github.com/jhidalgo3/014f2626fff717c0650583467b50f20c)

```bash
$KAFKA_HOME/bin/kafka-producer-perf-test \
  --topic test \
  --num-records 5000\
  --record-size 100 \
  --throughput -1 \
  --producer-props acks=1 \
  bootstrap.servers=localhost:9092 \
  buffer.memory=67108864 \
  batch.size=8196

```

**5. Consume messages.**

Open a new terminal window, generate some message to simulate consumer load.

```bash
$KAFKA_HOME/bin/kafka-producer-perf-test --throughput 500 --num-records 100000000 --topic demo-topic --record-size 100
```

**6. Open Grafana.**

Open your favorite web browser and open provided Grafana dashboard : Kafka Cluster / Global Healthcheck

(see [Accessing Grafana Web UI](#accessing-grafana-web-ui))

![kafka-cluster-healthcheck](./assets/kafka-cluster-healthcheck.png)

**7. Stop all containers.**

Cleanup all containers.

```bash
./monitoring-suite-stop
```

### Accessing Grafana Web UI

Grafana is accessible at the address : [http://localhost:3000](http://localhost:3000)

Security are : 
* user : `admin`
* password : `kafka`

### Accessing Prometheus Web UI

Prometheus is accessible at the address : [http://localhost:9090](http://localhost:9090) 

## Contributions

Any feedback, bug reports and PRs are greatly appreciated!

## Licence

Licensed to the Apache Software Foundation (ASF) under one or more contributor license agreements. See the NOTICE file distributed with this work for additional information regarding copyright ownership. The ASF licenses this file to you under the Apache License, Version 2.0 (the "License"); you may not use this file except in compliance with the License. You may obtain a copy of the License at

[http://www.apache.org/licenses/LICENSE-2.0](http://www.apache.org/licenses/LICENSE-2.0)

Unless required by applicable law or agreed to in writing, software distributed under the License is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the License for the specific language governing permissions and limitations under the License