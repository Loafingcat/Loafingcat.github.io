---
title: Pycharm에서 ipynb파일 사용세팅 가이드Pycharm에서 ipynb파일 사용세팅 가이드
date: 2024-04-06 16:30:00 +0900
categories: [Setup]
tags: [setup]     # TAG names should always be lowercase
authors: [LoafingCat]
---

# 목차

[1. Python Virtual Environment](#1-python-virtual-environment)
- [Miniconda 스크립트 파일 다운로드](#miniconda-스크립트-파일-다운로드)
- [스크립트 파일 실행](#스크립트-파일-실행)
- [경로 설정 후 시작](#경로-설정-후-시작)
- [conda 명령어](#conda-명령어)
- [가상환경 생성](#가상환경-생성)

[2. Python Packages]()
- [설치 패키지 목록](#설치-패키지-목록)
- [패키지 설치하기](#패키지-설치하기)

[3. Pycharm에 가상환경 및 jupyter notebook 연동](#3-pycharm에-가상환경-및-jupyter-notebook-연동)

- [파이참에 아나콘다 가상환경 설정하기](#파이참에-아나콘다-가상환경-설정하기)
- [Jupyter notebook 연동](#jupyter-notebook-연동)


------------------------------------

## 1. Python Virtual Environment

### - Miniconda 스크립트 파일 다운로드

아래 명령어를 터미널에 입력합니다.

        wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh

아래의 명령어로 스크립트 파일이 잘 다운로드 받아졌는지 확인할 수 있습니다.

        ll
Miniconda3 스크립트 파일을 확인할 수 있습니다.


![Miniconda3 스크립트](https://quickest-asterisk-75d.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F3ef8dbd9-414c-4cf5-813d-32ecb943cc67%2F3eb551e3-749f-42cf-a7d4-b2b2c7fa6332%2F59.png?table=block&id=8102abf4-e59e-47e7-a11b-a879accfc553&spaceId=3ef8dbd9-414c-4cf5-813d-32ecb943cc67&width=2000&userId=&cache=v2)

### - 스크립트 파일 실행

아래의 명령어를 터미널에 입력해 스크립트 파일을 실행합니다.

        sudo bash Miniconda3-latest-Linux-x86_64.sh

![라이센스](https://quickest-asterisk-75d.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F3ef8dbd9-414c-4cf5-813d-32ecb943cc67%2Fe2fabb50-fce5-4999-9753-e2a65691bd24%2F60.png?table=block&id=5d6219b8-d7e4-4734-837b-d39f3819b2f2&spaceId=3ef8dbd9-414c-4cf5-813d-32ecb943cc67&width=1420&userId=&cache=v2)

 “Do you accept the license terms? [yes|no]” 내용이 나올 때 까지 아래 화살표를 입력합니다.

 ![yes](https://quickest-asterisk-75d.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F3ef8dbd9-414c-4cf5-813d-32ecb943cc67%2F3bccc103-59b2-42aa-8eac-a5f00045c6b1%2F61.png?table=block&id=6517a40d-4afd-409b-a895-dd2bec82e721&spaceId=3ef8dbd9-414c-4cf5-813d-32ecb943cc67&width=2000&userId=&cache=v2)

 yes를 입력합니다.

 ![경로](https://quickest-asterisk-75d.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F3ef8dbd9-414c-4cf5-813d-32ecb943cc67%2F72e26992-2364-4061-b712-d1159620aa29%2F62.png?table=block&id=8027c8dd-fb37-45e7-a0c1-fb0dde759e9a&spaceId=3ef8dbd9-414c-4cf5-813d-32ecb943cc67&width=1420&userId=&cache=v2)

 경로를 “/home/(원하는 이름)/miniconda3”(기본 설정) 설정합니다.

 ![no](https://quickest-asterisk-75d.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F3ef8dbd9-414c-4cf5-813d-32ecb943cc67%2Ff32e6bc4-dd2b-43d8-a7f9-ab36c1375555%2F63.png?table=block&id=311188be-cf05-4cfa-abcf-e2fed6df17eb&spaceId=3ef8dbd9-414c-4cf5-813d-32ecb943cc67&width=1420&userId=&cache=v2)

 중간의 --reverse &SHELL ? 이라는 질문은 no 라고 답합니다.

 ### - 경로 설정 후 시작

 아래 명령어를 순서대로 터미널에 입력합니다.

         # conda 경로 설정
         export PATH="/home/{본인의 유저네임}/miniconda3/bin:$PATH"

        # 설정 즉시 적용, 유저 개인의 alias 및 변수 설정
        source .bashrc 

        # miniconda 시작
        conda init 

#### 적용을 위해 터미널을 종료한 후 다시 실행합니다.(중요)

![적용](https://quickest-asterisk-75d.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F3ef8dbd9-414c-4cf5-813d-32ecb943cc67%2F32699e4e-9f98-4b76-aca2-628fe4d27963%2F65.png?table=block&id=16a7f6ca-19a4-4fab-a3a7-9abeb54c2d13&spaceId=3ef8dbd9-414c-4cf5-813d-32ecb943cc67&width=1420&userId=&cache=v2)

### - conda 명령어

아래의 명령어들을 사용할 수 있습니다.

        # Miniconda 버전 확인
        conda --version 

        # 사용 가능한 가상 환경 확인
        conda env list 

        # 가상 환경 활성화
        conda activate (가상 환경 이름)

        # 가상 환경 비활성화
        conda deactivate (가상 환경 이름) 

명령줄 앞에 (base)가 표시 되어 있으면 가상 환경이 활성화 되어 있는 상태입니다.

![base](https://quickest-asterisk-75d.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F3ef8dbd9-414c-4cf5-813d-32ecb943cc67%2F00c016b2-97c5-4736-8ade-2e651ad51393%2F67.png?table=block&id=ae36ae78-71a5-4d36-a5ca-e44ffb08c830&spaceId=3ef8dbd9-414c-4cf5-813d-32ecb943cc67&width=1310&userId=&cache=v2)

### - 가상환경 생성

사용할 가상환경을 만들어 보겠습니다.

아래의 명령어를 터미널에 입력합니다.

원하는 이름의 파이썬 3.9버전을 사용하는 가상환경을 만들어 줍니다.

        # 원하는 이름을 가진 파이썬 3.9버전을 사용하는 가상환경 생성
        conda create -n (원하는 이름) python=3.9

        cf) ssl 관련 오류 발생 시 입력
        CondaHTTPError: HTTP 000 CONNECTION FAILED
        conda config --set ssl_verify False(no)

Proceed ([y]/n)? 물음에 “y”라고 입력합니다.

![proceed](https://quickest-asterisk-75d.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F3ef8dbd9-414c-4cf5-813d-32ecb943cc67%2F74a26242-5d6b-48a8-b71a-eab54c7f90e7%2F69.png?table=block&id=4a1ebb75-a14f-479f-abe5-c7dd0ff03d26&spaceId=3ef8dbd9-414c-4cf5-813d-32ecb943cc67&width=1420&userId=&cache=v2)
![proceed2](https://quickest-asterisk-75d.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F3ef8dbd9-414c-4cf5-813d-32ecb943cc67%2F895aa4f2-de71-487a-8852-ee3cd342808f%2F70.png?table=block&id=57932bd3-7203-43a4-be51-21a947b39609&spaceId=3ef8dbd9-414c-4cf5-813d-32ecb943cc67&width=1420&userId=&cache=v2)


가상 환경이 올바르게 생성되었는지 확인하겠습니다.

아래의 명령어를 터미널에 입력합니다.

        # 사용 가능한 가상 환경 확인
        conda env list 

        # 해당 가상 환경 활성화
        conda activate (가상환경 이름) 

        # 파이썬 버전 확인cond
        python --version 

        # 파이썬 경로 확인
        which python3 

### 할성화된 가상환경은 명령줄 앞의 (원하는 이름)으로 확인할 수 있고

### conda env list 의 *표 표시로도 확인할 수 있습니다.

![end](https://quickest-asterisk-75d.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F3ef8dbd9-414c-4cf5-813d-32ecb943cc67%2F0edac56e-b666-4359-ba47-284311426b8b%2F71.png?table=block&id=99709bc4-9141-495b-89dc-f0c07e27e198&spaceId=3ef8dbd9-414c-4cf5-813d-32ecb943cc67&width=1910&userId=&cache=v2)

## 2. Python Packages

### - 설치 패키지 목록

**웹 & 데이터 크롤링**

- Requests
- Selenium
- Beautiful Soup 4
- Flask

**데이터 분석**

- Numpy
- Pandas
- Matplotlib
- Seaborn
- PyTorch
- LangChain
- IPython Kernel
- Jupyter Notebook

### - 패키지 설치하기

아래 명령어를 터미널에 입력해주세요.

반드시, 가상 환경이 활성화 된 상태여야 합니다.

        # yeardream 가상 환경 활성화
        conda activate yeardream

        # requests selenium bs4 flask numpy pandas matplotlib seaborn ipykernel notebook 설치
        conda install requests selenium bs4 flask numpy pandas matplotlib seaborn ipykernel notebook -y

        # langchain 설치
        conda install -c conda-forge langchain -y

        # pytorch 설치
        conda install pytorch::pytorch torchvision torchaudio -c pytorch -y

![pakage](https://quickest-asterisk-75d.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F3ef8dbd9-414c-4cf5-813d-32ecb943cc67%2F0c94d5c2-05c1-47a0-bbc8-95958fd600e8%2F76.png?table=block&id=d7c65679-4de4-49ac-b3c2-a601948fd78f&spaceId=3ef8dbd9-414c-4cf5-813d-32ecb943cc67&width=1420&userId=&cache=v2)
![package2](https://quickest-asterisk-75d.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F3ef8dbd9-414c-4cf5-813d-32ecb943cc67%2F843954c9-2c13-4ace-8d8c-024a6ef8a492%2F77.png?table=block&id=6faf2253-e5e2-434d-b5a5-2d8a555fe77e&spaceId=3ef8dbd9-414c-4cf5-813d-32ecb943cc67&width=1420&userId=&cache=v2)

## 3. Pycharm에 가상환경 및 jupyter notebook 연동

### - 파이참에 아나콘다 가상환경 설정하기

![이미지 3](https://github.com/Loafingcat/JungolCodeTestLoafingcat/assets/98324619/5803b85f-4b14-4ecd-aa99-f330f0e77456)

file - new project - Pure Pyhon에 Add Interpreter를 눌러서 뜨는 Add Local interpreter를 눌러줍니다.

![이미지 4](https://github.com/Loafingcat/JungolCodeTestLoafingcat/assets/98324619/50fbe1e7-a1a5-434e-afea-843494ee7e34)

Conda Environment에서 anaconda3를 적용해주면 가상화면 세팅이 완료됩니다.

### - Jupyter notebook 연동

![이미지 5](https://github.com/Loafingcat/JungolCodeTestLoafingcat/assets/98324619/498e9cce-861d-4e74-8e14-2d99c8ca77aa)

view - Tool Windows - Terminal로 들어가줍니다.

![이미지 6](https://github.com/Loafingcat/JungolCodeTestLoafingcat/assets/98324619/41af0cbc-f5fa-4fd6-b8a1-d782efccf2d0)

터미널에 아래 명령어를 입력하면 jupyter notebook에 연동됩니다.

        jupyter notebook

