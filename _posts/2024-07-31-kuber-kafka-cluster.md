---
title: kafka cluster in kuber
date: 2024-07-31 16:30:00 +0900
categories: [Kube]
tags: [kube]     # TAG names should always be lowercase
authors: [LoafingCat]
---


작동 안함.. 수정필요

서비스를 통일하는 방안 필요

외부 애플리케이션이랑 통신이 안됨


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
