git clone https://github.com/wurstmeister/kafka-docker.git

cd kafka-docker

docker-compose up -d

docker exec -it kafka-docker_kafka_1 bash

kafka-topics.sh --create --bootstrap-server localhost:9092 --replication-factor 1 --partitions 1 --topic test

kafka-topics.sh --list --bootstrap-server localhost:9092

kafka-console-producer.sh --broker-list localhost:9092 --topic test

kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic test --from-beginning

