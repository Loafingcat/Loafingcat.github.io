---
title: Feature Store
date: 2024-08-29 16:30:00 +0900
categories: [MLOps]
tags: [mlops]     # TAG names should always be lowercase
authors: [LoafingCat]
---

# 요약

머신러닝에서 Feature Store는 데이터를 효율적으로 가공, 저장 및 관리하기 위한 시스템으로, 데이터 엔지니어와 데이터 과학자 간의 협업을 촉진하는 역할을 한다. Feature는 측정된 현상의 특성 또는 성질로, 원시 데이터를 처리하여 생성된다. 이러한 기능은 머신러닝 문제의 증가에 따라 점점 더 중요해지고 있음.

# Feature Store의 역할

- 데이터 엔지니어와 데이터 과학자 간의 중앙 저장소: 과거에는 모델 개발자가 원시 데이터에서 기능을 추출하고 모델을 학습 및 배포하는 모든 작업을 수행했지만, Feature Store는 이 과정을 효율적으로 나눌 수 있게 함.

- 효율적인 가공 및 관리: 데이터 엔지니어는 대규모 원시 데이터를 관리하고 처리하는데 집중할 수 있고, 데이터 과학자는 이러한 기능을 활용하여 모델 개발 및 분석에 더 많은 시간을 할애할 수 있음.

# 주요 구성 요소

- 원시 데이터 처리 및 가공: 원시 데이터를 기능 형태로 변환하는 작업이 필요함.
- 데이터 웨어하우스: 생성된 기능을 저장하는 중앙 저장소이다.
- 메타데이터 저장소: 각 기능에 대한 메타 정보를 저장한다.
- API: 데이터 과학자가 기능에 접근하기 위한 인터페이스를 제공함.

# 온라인 및 오프라인 Feature Store
- 온라인 Feature Store: 예측 모델이 빠르게 응답할 수 있도록 하기 위해, 낮은 지연 시간을 유지하는 데 필요한 특정 기능만 제공함.
- 오프라인 Feature Store: 배치 작업으로 처리된 기능이 저장됩니다. 이 두 저장소 간의 일관성을 유지하는 것이 중요함.

# MLOps에서의 역할
Feature Store는 MLOps의 핵심 구성 요소 중 하나로, 데이터 관리의 효율성을 높이며, 데이터 과학자들이 더 효과적으로 작업할 수 있도록 돕는다.