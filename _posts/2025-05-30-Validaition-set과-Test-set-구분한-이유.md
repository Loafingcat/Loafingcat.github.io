---
title: Validation set과 Test set 구분 이유
date: 2025-05-256:30:00 +0900
categories: [머신러닝]
tags: [용어]     # TAG names should always be lowercase
authors: [LoafingCat]
---


Validation set 즉 검증셋은 트레이닝 데이터로 학습한 모델이 제대로 배웠는지 평가하기 위한 용도다. Training set은 교재 보고 학습한거고 검증셋은 모의고사라고 볼 수 있다.

검증셋을 통해 모델 성능을 평가하고 성능이 뛰어난 모델을 분류한다. 이후 마지막에 Test set으로 평가하는데 만약 검증셋이 없다면?

이 모델이 어떤 성능을 낼 지 전혀 알 수가 없다. 왜냐하면 모델은 항상 seen 데이터로 훈련을 했고 useen 데이터를 통해 뭔가를 증명한 적이 없기 때문이다.

따라서 검증셋과 test set이라는 단계는 구분이 필요하다. 트레이닝셋을 통해 훈련된 모델이 검증셋을 통해 성능을 끌어올리고

마지막으로 본 적 없는 데이터를 통해 실제 운영 데이터를 넣었을 때 제 성능을 발휘하는지 평가하기 위해서이기 때문.