---
title: Docker kafka
date: 2024-08-30 16:30:00 +0900
categories: [Kafka]
tags: [kafka]     # TAG names should always be lowercase
authors: [LoafingCat]
---




        version: '3.8'

        volumes:
        kafka_volume:
            driver: local

        services:
        kafka:
            image: apache/kafka:3.7.1
            container_name: kafka1 # instance1의 docker compose 파일
            ports:
            - "9092:9092" # 외부용
            - "9093:9093" # 내부 클러스터용
            environment:
            KAFKA_PROCESS_ROLES: broker,controller
            KAFKA_NODE_ID: 1
            KAFKA_CONTROLLER_QUORUM_VOTERS: 1@172.31.2.88:9093,2@172.31.5.148:9093,3@172.31.9.18:9093
            KAFKA_LISTENERS: PLAINTEXT://0.0.0.0:9092,CONTROLLER://0.0.0.0:9093 # PLAINTEXT 프로토콜로 모든 인스턴스 수신
            KAFKA_ADVERTISED_LISTENERS: PLAINTEXT://172.31.2.88:9092 # 클라이언트는 이 포트로 접근
            KAFKA_LOG_DIRS: /var/lib/kafka/data
            KAFKA_LISTENER_SECURITY_PROTOCOL_MAP: PLAINTEXT:PLAINTEXT,CONTROLLER:PLAINTEXT # 없으면 오류걸림
            KAFKA_INTER_BROKER_LISTENER_NAME: PLAINTEXT
            KAFKA_AUTO_CREATE_TOPICS_ENABLE: "false"
            KAFKA_CONTROLLER_LISTENER_NAMES: CONTROLLER
            KAFKA_LOG_RETENTION_MS: 300000
            volumes:
            - kafka_volume:/var/lib/kafka/data

## PLAINTEXT 프로토콜은 간단하고 빠른 데이터 전송을 가능하게 하지만, 보안이 필요한 경우에는 적합하지 않다. 데이터 보안을 고려할 때는 SSL(Secure Sockets Layer) 또는 SASL(Simple Authentication and Security Layer) 등의 보안 프로토콜을 사용하는 것이 좋음.