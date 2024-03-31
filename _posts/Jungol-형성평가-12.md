---
title: Jungol 리스트3 형성평가 12번
date: 2024-03-31 16:30:00 +0900
categories: [Jungol]
tags: [Jungol]     # TAG names should always be lowercase
authors: [LoafingCat]
---
## 문제
**3행 5열의 2차원 문자리스트에 차례로 대문자를 입력받은 후 소문자로 바꾸어서 출력하는 프로그램을 작성하시오.** 


     입력               출력

        A B C D E           a b c d e
        F G H I J           f g h i j
        K L M N O           k l m n o

### 정답 코드

    L = [['A', 'B', 'C', 'D', 'E'], ['F', 'G', 'H', 'I' ,'J'], ['K', 'L', 'M', 'N', 'O']]

    for i in range(len(L)):
        for j in range(len(L[i])):
             print(L[i][j].lower(), end=' ')
        print()

### 풀이

입력된 리스트 값을 모두 소문자로 만들어주기 위해선 리스트 안의 모든 값을 먼저 불러올 필요가 있다.

        for i in range(len(L)):

이 코드를 통해 리스트 L의 각 행을 반복하게된다. len(L)은 리스트의 길이인 3이 된다.

        for j in range(len(L[i])):

이 코드는 현재 행 L[i] 안에 있는 각 요소에 대한 반복을 실행한다. 

        for j in range(len(L[i])):
             print(L[i][j].lower(), end=' ')

이를 통해 각 요소의 값을 lower() 함수를 통해 소문자로 변환시키고 end = ' '를 통해서 요소 사이에 공백를 추가해서 일단 출력한다.

        for i in range(len(L)):
            for j in range(len(L[i])):
                print(L[i][j].lower(), end=' ')
        print()

그리고 내부 for문이 종료될 때마다 줄바꿈을 해주기 위해서 외부 for문에 print()를 추가해준다.

결과적으로 L의 각 요소가 소문자로 변환되고, 각 행이 공백으로 구분된 한 줄씩 출력된다.