---
title: kafka exporter
date: 2024-07-31 16:30:00 +0900
categories: [Kafka]
tags: [kafa]     # TAG names should always be lowercase
authors: [LoafingCat]
---


        docker run -d --name kafka-exporter \
        --network work_default \
        -e KAFKA_SERVER=172.31.2.88:9092,172.31.5.148:9092,172.31.9.18:9092 \
        -p 9308:9308 \
        danielqsj/kafka-exporter

카프카의 매트릭 정보를 위해서는 필수적으로 있어야함

매트릭 정보를 프로메테우스에 보내주고, 그걸 그라파나로 시각화 하는것이 가능하다.