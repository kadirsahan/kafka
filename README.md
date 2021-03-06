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

| __NAMES__ |
|--------------|
| ksqldb-cli |
| ksqldb-server |
| kafka-connect  |
| schema-registry |
| kafka |
| postgres 
| zookeeper |






docker exec -it ksqldb-cli bash

ksql http://ksqldb-server:8088


in zookeeper

kafka-topics --zookeeper localhost:2181 --create --partitions 1 --replication-factor 1 --topic USERS

kafka-topics --zookeeper localhost:2181 --create --partitions 1 --replication-factor 1 --topic USERACCOUNTS

in kafka

kafka-console-producer --broker-list localhost:9092 --topic USERS

in another session

kafka-console-producer --broker-list localhost:9092 --topic USERACCOUNTS

CREATE STREAM users (userid INT, firstname VARCHAR, lastname VARCHAR)  WITH (VALUE_FORMAT = 'DELIMITED', KAFKA_TOPIC = 'USERS');

CREATE STREAM users_accounts (accountid INT, userid INT, accountname VARCHAR, balance VARCHAR)  WITH (VALUE_FORMAT = 'DELIMITED', KAFKA_TOPIC = 'USERACCOUNTS');
