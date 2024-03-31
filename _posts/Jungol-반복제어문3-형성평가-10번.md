---
title: Jungol 반복제어문3 형성평가 10번
date: 2024-03-31 16:30:00 +0900
categories: [Jungol]
tags: [Jungol]     # TAG names should always be lowercase
authors: [LoafingCat]
---

## 문제

**자연수 n을 입력받아 각 문제의 출력예와 같이 출력되는 프로그램을 작성하시오.**

        입력            출력

        3               1 3 5
                        7 9 1
                        3 5 7

#### 정답 코드

        n = 3

        num = -1
        for i in range(n):
            for j in range(n):
               num = (num + 2) % 10
              print(num, end=' ')
         print()

#### 풀이

        for i in range(n):

외부 for문은 몇 행까지 출력해서 보여줄지를 결정한다. n이 3이기 때문에 0, 1, 2으로 3개의 행 까지만 반복하게 될 것이다.

        for j in range(n):

내부 for문이다. 이 부분은 앞으로 출력될 값을 한 행에 몇 개까지 보여줄지를 결정하는 부분이다. n이 3이니 외부 for문과 마찬가지로 3개까지 보여주게 될 것이다.

        num = (num + 2) % 10

num 값을 -1로 초기화시켜 놓았기 때문에 첫 num은 1이 될 것이다. 그리고 2씩 증가하여 10 이하의 홀수 값만 출력되게 된다.

        print(num, end=' ')

1, 3, 5, 7, 9, 1, 3, 5, 7, 9, ...를 한 칸의 공백으로 나누어 출력하는 부분이다.

        for i in range(n):
            for j in range(n):
                num = (num + 2) % 10
                print(num, end=' ')
        print() 

내부 for문이 종료되면 print() 함수가 호출되어서 줄 바꿈을 해준다.

결과적으로 3 X 3 크기의 행렬이 출력되고 그 안의 요소는 10이하의 홀수가 된다.