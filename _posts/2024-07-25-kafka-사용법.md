---
title: kafka 사용법
date: 2024-07-30 16:30:00 +0900
categories: [Information]
tags: [information]     # TAG names should always be lowercase
authors: [LoafingCat]
---


kafka 테스트 방법

sudo docker exec -it {컨테이너ID} bash

cd /opt/kafka/bin

./kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic topic_GetUserInfo --from-beginning

./kafka-topics.sh --delete --topic topic_GetUserInfo --bootstrap-server 172.31.2.88:9092

./kafka-topics.sh --create --topic topic_GetUserInfo --bootstrap-server 172.31.2.88:9092 --partitions 3 --replication-factor 2

./kafka-topics.sh --create --topic 토픽이름 --bootstrap-server 172.31.2.88:9092 --partitions 3 --replication-factor 2

topic_GetUserInfo

토픽리스트
./kafka-topics.sh --bootstrap-server localhost:9092 --list

토픽생성
./kafka-topics.sh --create --topic topic_currPlayer --bootstrap-server 172.31.5.148:9092 --partitions 3 --replication-factor 2

토픽에 데이터 확인
./kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic topic_currPlayer --from-beginning

토픽삭제
./kafka-topics.sh --delete --topic topic_currPlayer --bootstrap-server 172.31.5.148:9092