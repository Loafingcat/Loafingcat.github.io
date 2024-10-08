---
title: mlflow 쿠버네티스에 설치
date: 2024-09-07 16:30:00 +0900
categories: [Mlflow]
tags: [mlflow]     # TAG names should always be lowercase
authors: [LoafingCat]
---

		apiVersion: apps/v1
		kind: Deployment
		metadata:
		name: mlflow
		spec:
		replicas: 1
		selector:
			matchLabels:
			app: mlflow
		template:
			metadata:
			labels:
				app: mlflow
			spec:
			containers:
				- name: mlflow
				image: bitnami/mlflow:latest
				ports:
					- containerPort: 8080  
				command: ["mlflow", "ui", "--host", "0.0.0.0", "--port", "8080"]  # MLflow UI 실행
				resources:
					requests:
					memory: "512Mi"  # 요청 메모리
					cpu: "500m"      # 요청 CPU
					limits:
					memory: "1Gi"    # 제한 메모리
					cpu: "1"         # 제한 CPU

		---
		apiVersion: v1
		kind: Service
		metadata:
		name: mlflow
		spec:
		type: NodePort  # LoadBalancer에서 NodePort로 변경
		ports:
			- port: 8080    # 추가된 port 필드
			targetPort: 8080
			nodePort: 30003  # 원하는 포트 번호 (30000~32767 사이)
		selector:
			app: mlflow

helm chart가 아닌 docker image를 이용한 yaml파일을 통해 직접적으로 설치
