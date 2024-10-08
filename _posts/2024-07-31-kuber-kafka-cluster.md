---
title: kafka cluster in kuber
date: 2024-07-31 16:30:00 +0900
categories: [Kube]
tags: [kube]     # TAG names should always be lowercase
authors: [LoafingCat]
---


    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: kafka-1
    spec:
      replicas: 1
      selector:
        matchLabels:
          app: kafka
          instance: kafka-1
      template:
        metadata:
          labels:
            app: kafka
            instance: kafka-1
        spec:
          containers:
          - name: kafka
            image: apache/kafka:3.7.1
            ports:
            - containerPort: 9092
            - containerPort: 9093
            env:
            - name: KAFKA_PROCESS_ROLES
              value: "broker,controller"
            - name: KAFKA_NODE_ID
              value: "1"
            - name: KAFKA_CONTROLLER_QUORUM_VOTERS
              value: "1@kafka-1:9093,2@kafka-2:9093,3@kafka-3:9093"
            - name: KAFKA_LISTENERS
              value: "PLAINTEXT://0.0.0.0:9092,CONTROLLER://0.0.0.0:9093"
            - name: KAFKA_ADVERTISED_LISTENERS
              value: "PLAINTEXT://192.168.124.174:9092"
            - name: KAFKA_LOG_DIRS
              value: "/var/lib/kafka/data"
            - name: KAFKA_LISTENER_SECURITY_PROTOCOL_MAP
              value: "PLAINTEXT:PLAINTEXT,CONTROLLER:PLAINTEXT"
            - name: KAFKA_INTER_BROKER_LISTENER_NAME
              value: "PLAINTEXT"
            - name: KAFKA_AUTO_CREATE_TOPICS_ENABLE
              value: "false"
            - name: KAFKA_CONTROLLER_LISTENER_NAMES
              value: "CONTROLLER"
            - name: KAFKA_LOG_RETENTION_MS
              value: "300000"
            - name: KAFKA_MESSAGE_MAX_BYTES
              value: "2000000000"  # 2GB로 설정
            - name: KAFKA_REPLICA_FETCH_MAX_BYTES
              value: "2000000000"  # 2GB로 설정
            - name: KAFKA_MAX_PARTITION_FETCH_BYTES
              value: "2000000000"  # 2GB로 설정
            volumeMounts:
            - name: kafka-storage
              mountPath: /var/lib/kafka/data
          volumes:
          - name: kafka-storage
            emptyDir: {} # 파드 삭제되면 데이터도 날아감. Persistent Volum 쓰면 좋음.

    ---
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: kafka-2
    spec:
      replicas: 1
      selector:
        matchLabels:
          app: kafka
          instance: kafka-2
      template:
        metadata:
          labels:
            app: kafka
            instance: kafka-2
        spec:
          containers:
          - name: kafka
            image: apache/kafka:3.7.1
            ports:
            - containerPort: 9092
            - containerPort: 9093
            env:
            - name: KAFKA_PROCESS_ROLES
              value: "broker,controller"
            - name: KAFKA_NODE_ID
              value: "2"
            - name: KAFKA_CONTROLLER_QUORUM_VOTERS
              value: "1@kafka-1:9093,2@kafka-2:9093,3@kafka-3:9093"
            - name: KAFKA_LISTENERS
              value: "PLAINTEXT://0.0.0.0:9092,CONTROLLER://0.0.0.0:9093"
            - name: KAFKA_ADVERTISED_LISTENERS
              value: "PLAINTEXT://192.168.124.173:9092"
            - name: KAFKA_LOG_DIRS
              value: "/var/lib/kafka/data"
            - name: KAFKA_LISTENER_SECURITY_PROTOCOL_MAP
              value: "PLAINTEXT:PLAINTEXT,CONTROLLER:PLAINTEXT"
            - name: KAFKA_INTER_BROKER_LISTENER_NAME
              value: "PLAINTEXT"
            - name: KAFKA_AUTO_CREATE_TOPICS_ENABLE
              value: "true"
            - name: KAFKA_CONTROLLER_LISTENER_NAMES
              value: "CONTROLLER"
            - name: KAFKA_LOG_RETENTION_MS
              value: "300000"
            - name: KAFKA_MESSAGE_MAX_BYTES
              value: "2000000000"  # 2GB로 설정
            - name: KAFKA_REPLICA_FETCH_MAX_BYTES
              value: "2000000000"  # 2GB로 설정
            - name: KAFKA_MAX_PARTITION_FETCH_BYTES
              value: "2000000000"  # 2GB로 설정
            volumeMounts:
            - name: kafka-storage
              mountPath: /var/lib/kafka/data
          volumes:
          - name: kafka-storage
            emptyDir: {}

    ---
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: kafka-3
    spec:
      replicas: 1
      selector:
        matchLabels:
          app: kafka
          instance: kafka-3
      template:
        metadata:
          labels:
            app: kafka
            instance: kafka-3
        spec:
          containers:
          - name: kafka
            image: apache/kafka:3.7.1
            ports:
            - containerPort: 9092
            - containerPort: 9093
            env:
            - name: KAFKA_PROCESS_ROLES
              value: "broker,controller"
            - name: KAFKA_NODE_ID
              value: "3"
            - name: KAFKA_CONTROLLER_QUORUM_VOTERS
              value: "1@kafka-1:9093,2@kafka-2:9093,3@kafka-3:9093"
            - name: KAFKA_LISTENERS
              value: "PLAINTEXT://0.0.0.0:9092,CONTROLLER://0.0.0.0:9093"
            - name: KAFKA_ADVERTISED_LISTENERS
              value: "PLAINTEXT://192.168.78.213:9092"
            - name: KAFKA_LOG_DIRS
              value: "/var/lib/kafka/data"
            - name: KAFKA_LISTENER_SECURITY_PROTOCOL_MAP
              value: "PLAINTEXT:PLAINTEXT,CONTROLLER:PLAINTEXT"
            - name: KAFKA_INTER_BROKER_LISTENER_NAME
              value: "PLAINTEXT"
            - name: KAFKA_AUTO_CREATE_TOPICS_ENABLE
              value: "true"
            - name: KAFKA_CONTROLLER_LISTENER_NAMES
              value: "CONTROLLER"
            - name: KAFKA_LOG_RETENTION_MS
              value: "300000"
            - name: KAFKA_MESSAGE_MAX_BYTES
              value: "2000000000"  # 2GB로 설정
            - name: KAFKA_REPLICA_FETCH_MAX_BYTES
              value: "2000000000"  # 2GB로 설정
            - name: KAFKA_MAX_PARTITION_FETCH_BYTES
              value: "2000000000"  # 2GB로 설정
            volumeMounts:
            - name: kafka-storage
              mountPath: /var/lib/kafka/data
          volumes:
          - name: kafka-storage
            emptyDir: {}

    ---
    apiVersion: v1
    kind: Service
    metadata:
      name: kafka-1
    spec:
      ports:
      - name: plaintext
        port: 9092
        targetPort: 9092
        protocol: TCP
      - name: controller
        port: 9093
        targetPort: 9093
        protocol: TCP
      selector:
        app: kafka
        instance: kafka-1

    ---
    apiVersion: v1
    kind: Service
    metadata:
      name: kafka-2
    spec:
      ports:
      - name: plaintext
        port: 9092
        targetPort: 9092
        protocol: TCP
      - name: controller
        port: 9093
        targetPort: 9093
        protocol: TCP
      selector:
        app: kafka
        instance: kafka-2

    ---
    apiVersion: v1
    kind: Service
    metadata:
      name: kafka-3
    spec:
      ports:
      - name: plaintext
        port: 9092
        targetPort: 9092
        protocol: TCP
      - name: controller
        port: 9093
        targetPort: 9093
        protocol: TCP
      selector:
        app: kafka
        instance: kafka-3

NodePort 또는 LoadBalancer 타입으로 외부 접근 가능하게 하기?

## 접근 방법

1. LoadBalancer로 서비스 생성

2. 서비스가 생성된 후 kubectl get services 명령어를 사용하여 외부 IP 주소 확인. EXTERNAL-IP 열에 로드 밸런서의 IP가 표시될거임.

4. 그 외부 아이피를 http://<외부 IP>:9092 이런 형식으로 접근.

Deployment: 어플리케이션 배포 및 관리

Service: pod간의 통신, 외부 접근허용