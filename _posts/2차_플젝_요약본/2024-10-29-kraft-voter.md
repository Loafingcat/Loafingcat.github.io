---
title: 투표자가 홀수여야 하는 이유
date: 2024-10-02 16:30:00 +0900
categories: [Kafka]
tags: [kafka]     # TAG names should always be lowercase
authors: [LoafingCat]
---

KRaft 모드에서 투표자가 홀수여야 하는 이유와 브로커가 5개일 때 투표자가 3명이어야 하는 이유는 주로 장애 조치(failover) 와 합의 알고리즘에 관련이 있습니다.

### 투표자가 홀수여야 하는 이유

과반수 원칙: 분산 시스템에서는 장애가 발생했을 때 새로운 리더(컨트롤러)를 선출하기 위해 과반수 이상의 투표자가 동의해야 합니다. 홀수 개의 투표자가 있을 경우, 장애가 발생하더라도 항상 과반수를 유지할 수 있습니다.
장애 발생 시 안정성: 예를 들어, 투표자가 5명일 때, 3명이 동의해야 새로운 리더를 선출할 수 있습니다. 만약 2명이 장애가 나더라도 나머지 3명이 과반수를 유지할 수 있습니다.

        apiVersion: apps/v1
        kind: StatefulSet
        metadata:
        name: kafka  # Kafka StatefulSet의 이름
        spec:
        serviceName: kafka  # 서비스 이름
        replicas: 1  # 복제본 수 (여기서는 1)
        selector:
            matchLabels:
            app: kafka  # 선택기 레이블
        template:
            metadata:
            labels:
                app: kafka  # 파드 레이블
            spec:
            nodeSelector:
                type: worker  # 워커 노드에서 실행
            initContainers:  # 초기화 컨테이너
            - name: init-permissions
                image: busybox  # 초기화 작업을 위한 이미지
                command: ["sh", "-c", "if [ -d /var/lib/kafka/data/lost+found ]; then rm -rf /var/lib/kafka/data/lost+found; fi && chown -R 1000:1000 /var/lib/kafka/data"]
                volumeMounts:
                - name: kafka-storage  # 볼륨 마운트
                mountPath: /var/lib/kafka/data  # 마운트 경로
            containers:
            - name: kafka  # Kafka 컨테이너
                image: apache/kafka:3.7.1  # Kafka 이미지
                ports:
                - containerPort: 9092  # Kafka 클라이언트 연결 포트
                env:
                - name: KAFKA_PROCESS_ROLES
                value: "broker,controller"  # Kafka 역할 설정
                - name: KAFKA_NODE_ID
                value: "0"  # 노드 ID 설정
                - name: KAFKA_CONTROLLER_QUORUM_VOTERS
                value: "0@kafka-0:9093,1@kafka-1:9093,2@kafka-2:9093"  # 컨트롤러 쿼럼 설정

### 브로커가 5개일 때 투표자가 3명이어야 하는 이유
과반수 유지: 브로커가 5개일 때 투표자가 3명인 경우, 1명이 장애가 발생해도 2명이 남아 과반수(2명)를 유지할 수 있습니다. 그러나 2명이 장애가 발생하면 1명만 남게 되어 과반수를 유지하지 못하게 됩니다.
안정적인 리더 선출: 3명의 투표자가 있다면, 장애가 발생하더라도 새로운 리더를 안정적으로 선출할 수 있는 구조가 됩니다.

### 브로커가 5개 이상일 때 투표자 수
일반적인 규칙: 브로커 수가 홀수일 때는 보통 전체 브로커 수의 절반보다 1명이 더 많은 수의 투표자를 설정하는 것이 좋습니다. 예를 들어:
브로커가 7개일 경우: 투표자는 5명 (과반수는 4명)
브로커가 9개일 경우: 투표자는 5명 (과반수는 5명)
결론
KRaft 모드에서 투표자는 항상 홀수여야 하며, 브로커가 5개일 때는 투표자를 3명으로 설정하는 것이 안정성을 높입니다. 브로커가 5개 이상일 경우에도 동일한 원칙을 적용하여 투표자를 결정하면 됩니다. 이를 통해 시스템의 신뢰성과 가용성을 높일 수 있습니다.

### 그럼 브로커 다섯개 일 때 투표자를 다섯명으로 하는게 더 안전하지 않나?

브로커가 5개일 때, 투표자를 5명으로 설정하는 것이 직관적으로 더 안전해 보일 수 있지만, 실제로는 문제가 발생할 수 있습니다.

브로커가 5개일 때 투표자가 5명인 경우의 문제

**과반수 원칙**

투표자가 5명일 경우, 새로운 리더를 선출하기 위해서는 3명 이상의 투표자가 동의해야 합니다.
만약 3명이 장애가 발생하면, 남은 2명만으로는 과반수를 유지할 수 없게 되어 새로운 리더를 선출할 수 없습니다.

**장애 발생 시 시나리오**

모든 브로커가 장애가 발생하는 경우: 예를 들어, 5명의 투표자가 모두 브로커이면서 장애가 발생하면, 시스템은 리더를 선출할 수 없는 상태에 빠질 수 있습니다.

2명 이상의 장애: 만약 2명이 장애가 발생하면, 남은 3명 중에서 1명이라도 더 장애가 나면 과반수가 유지되지 않게 됩니다.

### 규칙

투표자 수는 몇 개의 장애를 감내할 수 있는지의 구조를 가지게 된다.

3명이면 1개의 장애

5명이면 2개의 장애

7명이면 3개의 장애
...

투표자는 브로커의 과반수를 넘지 않는것이 좋나보다..