---
title: 로컬에서 Flink dashboard 띄우기
date: 2024-06-30 16:30:00 +0900
categories: [Information]
tags: [information]     # TAG names should always be lowercase
authors: [LoafingCat]
---


## 경로 

cd /usr/local/flink/conf/config.yaml

## 수정

![이미지 5](https://github.com/Loafingcat/JungolCodeTestLoafingcat/assets/98324619/407cd4c5-bcac-42bd-9516-662d46523bf3)

bind address를 0.0.0.0으로 바꾼다.

port 주석을 풀어준다.

## 참고

    sudo lsof -i :8081

위 명령어로 8081 포트가 사용중인지 확인한다.

사용중이라면 아래 명령어로 포트 연결을 끊고 다시 시도한다.

    sudo kill -9 "PID"