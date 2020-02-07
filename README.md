git clone https://github.com/wurstmeister/kafka-docker.git

cd kafka-docker

docker-compose up -d

docker exec -it kafka-docker_kafka_1 bash

cd /opt/kafka/bin


./kafka-topics.sh --create --bootstrap-server localhost:9092 --replication-factor 1 --partitions 1 --topic test

./kafka-topics.sh --list --bootstrap-server localhost:9092

./kafka-console-producer.sh --broker-list localhost:9092 --topic test

./kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic test --from-beginning

./kafka-producer-perf-test.sh   --topic test   --num-records 50000   --record-size 100   --throughput -1   --producer-props acks=1   bootstrap.servers=localhost:9092   buffer.memory=67108864   batch.size=1000

*** kafka streams - ksql - ksqldb ***
➜  ~ docker ps
CONTAINER ID        IMAGE                                          COMMAND                  CREATED             STATUS                 PORTS                                        NAMES
f0eb72bf97e0        confluentinc/ksqldb-cli:0.6.0                  "/bin/sh"                5 hours ago         Up 5 hours                                                          ksqldb-cli
7a8b43821e52        confluentinc/ksqldb-server:0.6.0               "/usr/bin/docker/run"    5 hours ago         Up 5 hours             0.0.0.0:8088->8088/tcp                       ksqldb-server
3baeed3de2ed        confluentinc/cp-kafka-connect:5.4.0-beta1      "/etc/confluent/dock…"   5 hours ago         Up 5 hours (healthy)   0.0.0.0:8083->8083/tcp, 9092/tcp             kafka-connect
a4161a2c2d27        confluentinc/cp-schema-registry:5.4.0-beta1    "/etc/confluent/dock…"   5 hours ago         Up 5 hours             0.0.0.0:8081->8081/tcp                       schema-registry
9d5597f757db        confluentinc/cp-enterprise-kafka:5.4.0-beta1   "/etc/confluent/dock…"   5 hours ago         Up 5 hours             0.0.0.0:9092->9092/tcp                       kafka
7839ea56d01f        postgres:11.2                                  "docker-entrypoint.s…"   5 hours ago         Up 5 hours             0.0.0.0:5432->5432/tcp                       postgres
6a6a7108267a        confluentinc/cp-zookeeper:5.4.0-beta1          "/etc/confluent/dock…"   5 hours ago         Up 5 hours             2888/tcp, 0.0.0.0:2181->2181/tcp, 3888/tcp   zookeeper

docker exec -it ksqldb-cli bash

ksql http://ksqldb-server:8088

