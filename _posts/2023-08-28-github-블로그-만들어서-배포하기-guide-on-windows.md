---
title: github 블로그 만들어서 배포하기 guide on windows
date: 2023-08-28 16:30:00 +0900
categories: [Guide, Blog]
tags: [guide]     # TAG names should always be lowercase
authors: [LoafingCat]
---

## 목차

[실행환경과 필요한 툴](#0실행환경과-필요한-툴)

[jekyll에 대한 설명 및 Ruby 설치](#1jekyll에-대한-설명-및-ruby-설치)

[jekyll이란](#jekyll이란)

[ruby 설치](#ruby-설치)

[Jekyll 설치](#2jekyll-설치)

[github repository 생성](#3github-repository-생성)

[블로그 테마 선정](#블로그-테마-선정)

[리포지토리 생성](#리포지토리-생성)

[로컬 파일 소스트리에 연결하기](#4로컬-파일-소스트리에-연결하기)

[로컬에서 실행하기](#5로컬에서-실행하기)

[로컬에서 구현한 페이지를 github.io로 배포하기](#6로컬에서-구현한-페이지를-githubio로-배포하기)

[배포 후 블로그 컨텐츠 추가하기](#7배포-후-블로그-컨텐츠-추가하기)

[블로그 테마 변경하기](#8블로그-테마-변경하기)

[주의사항](#9주의사항)


------------------------


## 0.실행환경과 필요한 툴

PC의 OS와 git version입니다.

![KakaoTalk_20230906_012742594_03](https://github.com/Loafingcat/Loafingcat.github.io/assets/98324619/20cf20dd-4a63-4767-94eb-7b784b8bf522)

![이미지 28](https://github.com/Loafingcat/Loafingcat.github.io/assets/98324619/381efbfe-1e84-4aee-aa93-89a963975601)

기본적으로 필요한 툴로는 vscode, git이 있습니다. 없다면 다운을 하시고 이 글을 보시기 바랍니다.


## 1.jekyll에 대한 설명 및 Ruby 설치


### jekyll이란


jekyll이란 정적 웹사이트 생성기 입니다. 서버에 저장된 html, image, javascript 등의 파일이 그대로 전달된 정적인 웹페이지를 보게 됩니다.

Jekyll은 Github에서 개발한 툴로, 핵심 역할은 텍스트 변환 엔진이라고 볼 수 있습니다.

Markdown 형식의 파일을 HTML 파일로 변환해주는 역할을 하기에, 이 문법에 익숙해지면 누구나 쉽게 이용할 수 있습니다.

Jekyll 을 설치하기 위해서는 우선적으로 Ruby Installer를 설치해야 합니다.


### ruby 설치


https://rubyinstaller.org/downloads/ 

이곳에서 설치를 해주면 됩니다. jekyll 자체가 32비트이기 때문에 권장 버전인 3.2.X에서  Ruby+Devkit 3.2.2-1 (x86)를 다운 받도록
하겠습니다.

![KakaoTalk_20230906_012742594_09](https://github.com/Loafingcat/Loafingcat.github.io/assets/98324619/3cb683f0-de03-4c3e-b5bd-6a049a71c04a)

이후는 아래 사진 순서대로 진행해주시면 됩니다.

![KakaoTalk_20230906_012742594_13](https://github.com/Loafingcat/Loafingcat.github.io/assets/98324619/bf9874fa-f801-43a0-beed-33d9d1cb5b0e)

![KakaoTalk_20230906_012742594_14](https://github.com/Loafingcat/Loafingcat.github.io/assets/98324619/ef13ee50-7ab2-41e0-b9f4-7af23ea67c91)

![KakaoTalk_20230906_012742594_16](https://github.com/Loafingcat/Loafingcat.github.io/assets/98324619/c943eee9-2c56-496b-b2fa-75e7f2cb359a)


finish를 누르면 아래 사진처럼 커맨드창이 뜨는데, 절대 끄지마시고 나오는 문구에 따라 엔터를 입력하고 남은 설치를 마쳐줍시다.

![KakaoTalk_20230906_012742594_17](https://github.com/Loafingcat/Loafingcat.github.io/assets/98324619/fea7dc65-297e-4527-b543-9bb094e36233)


이렇게 설치가 다 끝나고 나면 git bash를 실행하여 ruby -v를 입력해봅시다.

버전이 잘 뜨면 성공적으로 설치된 것입니다.


# 2.Jekyll 설치

jekyll의 설치는 ruby에 비하면 매우 간단합니다.

git bash 커맨드창을 열어 아래 커맨드만 입력해주면 설치가 완료됩니다.

gem install jekyll

gem install bundler

bundler라는 것도 같이 설치해야하는데, bundler는 ruby 프로젝트에서 gem 파일의 종속성을 관리하는 도구입니다.

jekyll -v와 bundler -v를 입력하여 각각의 버전이 뜬다면 성공적으로 설치된 것입니다.


# 3.github repository 생성


### 블로그 테마 선정



깃허브 블로그를 만들기 위해서는 우선적으로 자신의 깃허브 블로그를 위한 리포지토리가 필요합니다.

우리는 아래 링크에서 원하는 블로그 테마를 고르고 그것을 적용한 리포지토리를 만들겁니다.

http://jekyllthemes.org/

원하는 테마를 골랐으면 대상의 깃허브 페이지에 들어가서 url을 복사해옵니다.

![이미지 29](https://github.com/Loafingcat/Loafingcat.github.io/assets/98324619/4aac3b67-1389-43fe-8a3f-51bd9efa7881)

![이미지 30](https://github.com/Loafingcat/Loafingcat.github.io/assets/98324619/815a2b47-9ecc-4ff4-9c40-a31b3694057f)



### 리포지토리 생성



이제 리포지토리를 만들 차례입니다. 

새로운 리포지토리를 만들기 위해서는 로그인 이후 좌측에 있는 new 버튼을 누르면 됩니다.

![KakaoTalk_20230906_012742594_05](https://github.com/Loafingcat/Loafingcat.github.io/assets/98324619/618112b9-704f-4e3e-9950-a744d1f7a427)


이후 아래 사진의 지시대로 빨간원을 친 부분을 클릭해줍시다

![KakaoTalk_20230906_012742594_06](https://github.com/Loafingcat/Loafingcat.github.io/assets/98324619/0c0a7428-53db-4d60-b6bf-959618afefd6)

클릭해서 들어가면 아래 사진처럼 clone url을 입력하는 부분과 리포지토리 이름을 입력하는 페이지가 나옵니다

![이미지 36](https://github.com/Loafingcat/Loafingcat.github.io/assets/98324619/2c074d09-cd89-4112-9f63-fcb28a7d47e9)


복사해뒀던 url을 clone url 부분에 붙여넣으시고 리포지토리의 이름은 위 사진처럼 {자신의 깃허브 이름}.github.io의 형식으로 생성하면 됩니다. 빨간 경고가 뜨는 이유는 제가 이미 동일한 이름의 리포지토리를 만들어놨기 때문입니다.

리포지토리를 생성한 뒤 로컬 저장소에 방금 만든 리포지토리를 clone 해줍니다. 이후 로컬에서 소스를 수정하고 다시 배포하기 위해 필요합니다.

만든 리포지토리의 url을 복사해주세요

![이미지 37](https://github.com/Loafingcat/Loafingcat.github.io/assets/98324619/3ca4ad74-510c-40a7-afb5-0e8e5bd36d15)

그리고 원하는 폴더에서 git bash를 열어주시고 git clone {복사한 url} 을 입력해준 후 엔터를 눌러주면 clone 완료입니다.

![이미지 38](https://github.com/Loafingcat/Loafingcat.github.io/assets/98324619/44404cc0-354c-4c93-b7d8-0184f7e7c0ca)




## tip. 
**git bash 커맨드창에선 shift + Ins가 붙여넣기, alt + Ins가 복사입니다.**



# 4.로컬 파일 소스트리에 연결하기

아래 사진과 같은 방법으로 로컬에 저장된 리포지토리 파일을 연동시켜줍니다.

![KakaoTalk_20230906_012742594_10](https://github.com/Loafingcat/Loafingcat.github.io/assets/98324619/d0876cde-3da8-46c3-ad09-a9920ccbd55f)

![KakaoTalk_20230906_012742594_12](https://github.com/Loafingcat/Loafingcat.github.io/assets/98324619/828d69fb-0e78-45b0-9fd9-197e5cdcd72a)

![KakaoTalk_20230906_012742594_11](https://github.com/Loafingcat/Loafingcat.github.io/assets/98324619/78c09940-1d19-4703-9466-17654c861e4b)

클론받은 폴더를 선택해주고 추가 버튼을 눌러주면 성공입니다.



# 5.로컬에서 실행하기

git bash에서 아래 명령어를 순차적으로 입력하기만 하면 됩니다.

    bundle install

    bundle update

    bundle install

설치가 완료 되었다면 

    bundle exec jekyll serve 또는 bundle exec jekyll s

명령어를 입력하여 로컬 서버를 실행하면 됩니다. 

잘 실행이 되었다면 아래와 같은 문구를 확인하실 수 있습니다.

![이미지 32](https://github.com/Loafingcat/Loafingcat.github.io/assets/98324619/f86d9775-9faa-4c4d-896e-940c3a616062)


적혀있는 로컬 주소인 http://127.0.0.1:4000/ 으로 접속해주면 아래 사진과 같이 성공적으로 실행된 것을 볼 수 있습니다.


![이미지 33](https://github.com/Loafingcat/Loafingcat.github.io/assets/98324619/9d369897-c721-4ee6-9b12-73b106a6cfc9)



# 6.로컬에서 구현한 페이지를 github.io로 배포하기

매우 간단합니다. 리포지토리에 존재하는 post 폴더에 들어가줍니다.

![이미지 12](https://github.com/Loafingcat/Loafingcat.github.io/assets/98324619/c11046ad-8e30-4e77-b153-ef988d71182f)

이곳에 배포할 컨텐츠를 작성해줍니다.

![이미지 13](https://github.com/Loafingcat/Loafingcat.github.io/assets/98324619/4b90a80b-9aba-4544-83d7-e43636dbe293)


작성한 파일을 세이브 해줍시다.

![이미지 14](https://github.com/Loafingcat/Loafingcat.github.io/assets/98324619/16f0009d-e9c2-49cc-b0fe-d4e6fb40ee30)


세이브 이후 소스트리에 커밋 버튼을 클릭하여 들어가줍시다.

![이미지 15](https://github.com/Loafingcat/Loafingcat.github.io/assets/98324619/86838388-9c6d-4850-b5bf-8696fd6103c6)


커밋할 파일을 올려주고 주석을 달아준 뒤 커밋 버튼을 눌러줍시다.


![이미지 16](https://github.com/Loafingcat/Loafingcat.github.io/assets/98324619/d9046a92-152b-4909-9e10-283490a271e5)


커밋이 완료되면 push 버튼을 눌러 push를 실행해줍시다.

![이미지 17](https://github.com/Loafingcat/Loafingcat.github.io/assets/98324619/a61610aa-9aff-44b0-823f-09253d112ab6)


이제 나의 원격 리포지토리에 로컬에서 수정한 소스가 업데이트 되고 잠시후 깃허브 페이지에도 업데이트가 적용됩니다.

![이미지 39](https://github.com/Loafingcat/Loafingcat.github.io/assets/98324619/c6c8a700-cfb0-4636-a149-33b90c8aaa0b)

완성된 화면입니다.


# 7.배포 후 블로그 컨텐츠 추가하기

이것 또한 간단합니다. 게시물을 추가하기 위해서는 post 폴더에 알맞은 형식으로 파일을 작성하면 됩니다.

![이미지 19](https://github.com/Loafingcat/Loafingcat.github.io/assets/98324619/f434cc48-62c4-4e4f-b2b1-aa6d9498d9ae)


위 사진처럼 vscode에서 파일을 추가해줍니다. 파일 형식은 .md 입니다(마크다운)

![이미지 20](https://github.com/Loafingcat/Loafingcat.github.io/assets/98324619/f2087d34-518a-4149-b050-7e25bdaa3422)

파일의 이름은 띄어쓰기 부분에 -(하이펀)기호를 입력 해야합니다. 

![이미지 22](https://github.com/Loafingcat/Loafingcat.github.io/assets/98324619/87d1410a-f1f7-4004-a2a4-2e3879615965)

이후 아래 사진처럼 코드를 써주시고 코드 아래의 빈공간에 콘텐츠를 써넣으시면 됩니다.

![이미지 23](https://github.com/Loafingcat/Loafingcat.github.io/assets/98324619/9600a910-fa55-44fb-8ee6-a410b4a356c7)


전부 완료하셨으면 이제 6단계에서 했던 배포를 해주시면 완성입니다.

![이미지 40](https://github.com/Loafingcat/Loafingcat.github.io/assets/98324619/63cca234-2fe3-41ea-a202-14a31a2af1cd)

잠시 후 페이지에 들어가보면 위 사진과 같이 컨텐츠가 추가된 것을 볼 수 있습니다.



# 8.블로그 테마 변경하기

원하는 테마를 가진 리포지토리에 방문해서 그 리포지토리의 모든 파일을 zip 파일로 받는다.

![이미지434311](https://github.com/Loafingcat/Loafingcat.github.io/assets/98324619/d257ac34-b7a7-4dd5-bfae-a10b10fe9e42)

압축을 풀어주고 기존 포스트가 있다면 _post를 제외한 모든 파일을 블로그 폴더에 넣어서 덮어 씌워준다.

![이미지5324312](https://github.com/Loafingcat/Loafingcat.github.io/assets/98324619/4d0f00b8-f0a9-4240-8485-bb3614f1e1bd)

그리고 위 사진처럼 블로그 폴더 경로에서 git bash를 열어 **bundle install** 해주면 블로그 테마가 적용된다.

![이미지111110](https://github.com/Loafingcat/Loafingcat.github.io/assets/98324619/44c40e2d-0878-4485-bfbd-d4052d0319ee)



# 9. 주의사항

마크다운 파일 이름을 지정할 때 단어 사이에 전부 -(하이픈)을 붙여 줘야 합니다.

![이미지 31](https://github.com/FirstBright/LangChain/assets/98324619/62ce4e94-1411-4e41-a704-a51adcdec68f)

