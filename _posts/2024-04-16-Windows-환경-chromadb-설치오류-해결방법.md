---
title: Windows 환경 chromadb 설치오류 해결방법
date: 2024-04-16 16:30:00 +0900
categories: [Information]
tags: [information]     # TAG names should always be lowercase
authors: [LoafingCat]
---


# 목차

1. [메뉴얼 설명 및 오류 내용](#메뉴얼-설명-및-오류-내용)

2. [해결법 1](#해결법-1)

3. [해결법 2](#해결법-2)

4. [해결법 3](#해결법-3)


## 메뉴얼 설명 및 오류 내용

![이미지 22](https://github.com/Loafingcat/Loafingcat.github.io/assets/98324619/7dfe570f-2411-4e0b-9e69-605aaeb37a11)

위 사진에 해당하는 오류를 위한 메뉴얼입니다.

본 메뉴얼은 목차 순서대로 수행하시면 됩니다.

## 해결법 1

아래 링크로 들어가줍니다.

[Visual Studio](https://visualstudio.microsoft.com/ko/visual-cpp-build-tools/)

![이미지 333](https://github.com/Loafingcat/FirstLangChain17/assets/98324619/e9e93530-9d75-4849-9948-263ce2a0db32)

다운 받으시면 아래 사진과 같이 설정하시고 설치하시면 됩니다. 이후 컴퓨터 재부팅 해줍니다.

![이미지 42](https://github.com/Loafingcat/FirstLangChain17/assets/98324619/12b0aab1-6273-4f2b-ab03-647f3ac4502f)


재부팅 하셨으면 다시 우분투를 실행해서 아래 명령어를 입력해줍니다.

    pip install langchain-chroma bs4


만약 오류가 지속된다면 해결법 2로 넘어가주세요.


## 해결법 2

아래 명령어를 터미널에 입력해주시면 됩니다.

    export HNSWLIB_NO_NATIVE=1

이후 아래 명령어를 실행해줍니다.

    pip install langchain-chroma bs4

이래도 설치가 안되시면 해결법 3으로 가주세요.

## 해결법 3

아래 명령어들을 순차적으로 실행시켜줍니다.

    1. sudo apt-get install python3-dev

    2. sudo apt install python3.11

    3. sudo apt install build-essential

    4. pip install hnswlib

    5. pip install langchain-chroma bs4

중간중간 y/n 질문을 하는데 모두 y를 입력해주시면 됩니다.

**만약 이 방법으로도 해결이 안되신다면 저에게 Slack DM 보내주시면 도와드리겠습니다.**






