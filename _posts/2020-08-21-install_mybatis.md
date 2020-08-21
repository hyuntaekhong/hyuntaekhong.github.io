---
title: "[SPRING] 2020.08.21_이클립스에 mybatis 설치"
date: 2020-08-21
categories:
  - blog
tags:
  - WEB
  - SPRING
  - MYBATIS

comments: true
excerpt: 이클립스 spring mybatis 설치 및 환경설정
last_modified_at: 2020-08-21
toc: true
---

## 1. mybatis 설치

### 1) mybatis 홈페이지 접속

<a href="https://mybatis.org/mybatis-3/ko/getting-started.html " >mybatis 홈페이지 링크</a>

![Spring](/assets/images/spring/mybatis/mybatis_install01.PNG)

### 2) mybatis-3.5.5.zip 다운로드

![Spring](/assets/images/spring/mybatis/mybatis_install02.PNG)


### 3) 압출풀기 후 mybatis-3.5.5.jar 파일 확인

![Spring](/assets/images/spring/mybatis/mybatis_install03.PNG)


### 4) 이클립스 접속 후 Java Project 만들기

- mybatis 실습할 java Project를 만든다. (java 콘솔로 실습 후 web으로 넘어갈 예정)
- 'mybatis-study' 라는 프로젝트 생성

![Spring](/assets/images/spring/mybatis/mybatis_install04.png)


### 5) mybatis-study 프로젝트 아래에 lib 이라는 폴더 생성하고 jar 파일 붙여넣기

- 해당 폴더에 mybatis.jar 와 ojdbc.jar 파일을 넣어줄 예정이다.
- 폴더를 만든 다음 압출 풀어놓은 mybatis-3.5.5.jar 파일만 lib폴더로 복사 붙여넣기

![Spring](/assets/images/spring/mybatis/mybatis_install05.PNG)


### 6) mybatis-study 프로젝트를 우클릭 후 Build Path > Configure Build Path 클릭

- 붙여넣은 jar 파일을 라이브러리에 추가하기 위한 과정

![Spring](/assets/images/spring/mybatis/mybatis_install06.png)

### 7) libraries > add JARs... 클릭 후 lib 폴더 아래의 mybatis-3.5.5.jar를 선택하고 OK 클릭

- 해당 폴더에 mybatis.jar 와 ojdbc.jar 파일을 넣어줄 예정이다.
- 폴더를 만든 다음 압출 풀어놓은 mybatis-3.5.5.jar 파일만 lib폴더로 복사 붙여넣기

![Spring](/assets/images/spring/mybatis/mybatis_install07.PNG)


### 8) libraries에 추가된 것을 확인하고 apply and close 클릭

- DB 연결을 위해 ojdbc8.jar도 추가했다.

![Spring](/assets/images/spring/mybatis/mybatis_install08.PNG)


### 9) 새로 추가된 Referenced Libraries 아래 jar파일이 생성되었는지 확인

- 잘 생성되었다면, mybatis 기본적인 설치가 완료된 것이다.

![Spring](/assets/images/spring/mybatis/mybatis_install09.PNG)

