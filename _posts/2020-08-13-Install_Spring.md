---
title: "[Spring] Spring Framework install"
date: 2020-08-13
categories:
  - blog
tags:
  - WEB
  - SPRING

comments: true
excerpt: Spring Framework 환경설정
last_modified_at: 2020-08-13
toc: true
---

## Spring 설치

### 1. 설치환경

- OS : WINDOWS 10
- IDE : Eclipse EE
- JRE : jre 1.8.0_251
- JDK : jdk-14.0.2

### 2. Spring 설치 및 환경설정

- 1) Apache Maven Project 사이트 http://maven.apache.org/ 접속

![Spring](/assets/images/spring/install01.png)

- 2) apache-maven-3.6.3-bin.zip 다운로드

![Spring](/assets/images/spring/install02.png)

- 3) 압축풀기 위치는 tomcat이 설치된 eclipse-workspace

![Spring](/assets/images/spring/install03.png)

- 4) 시스템 환경변수 설정 : 내 pc > 속성 > 고금 시스템 설정 > 시스템 속성_환경 변수

![Spring](/assets/images/spring/install04.png)

- 5) 환경변수 만들기
  - 시스템 변수 새로 만들기

  ![Spring](/assets/images/spring/install05.png)
  
  ![Spring](/assets/images/spring/install04-5.png)


  - 사용자 변수 만들기

  ![Spring](/assets/images/spring/install04-7.png)
  
  ![Spring](/assets/images/spring/install04-6.png)

- 6) 설치된 메이븐 확인
 
  ![Spring](/assets/images/spring/install08-1.png)


- 7) spring-workspace 만들기
  - 원하는 경로에 spring-workspace 폴더를 만든다.
  - spring-workspace 폴더 아래 maven-repository 폴더를 만든다
 
  ![Spring](/assets/images/spring/install08.png)


- 8) eclipse-workspace > apache-maven-3.6.3 > settings.xml 파일 경로 수정
  - 7)에서 만들어준 maven-workspace 폴더를 절대경로로 잡아준다.

  ![Spring](/assets/images/spring/install09.png)

- 9) 이클립스를 실행하고 새로운 maven project를 생성한다.
  
  ![Spring](/assets/images/spring/install10.png)
  
  ![Spring](/assets/images/spring/install11.png)


- 10) https://mvnrepository.com/ 사이트에서 'spring conterxt'를 검색 후 4.3.28.RELEASE를 클릭한다

  ![Spring](/assets/images/spring/install12.png)
  
  ![Spring](/assets/images/spring/install13.png)


- 11) 하단 텍스트박스의 내용을 복사한다.

  ![Spring](/assets/images/spring/install14.png)

- 12) 복사한 내용을 이클립스 프로젝트 내의 pom.xml에 붙여넣기 한다

  ![Spring](/assets/images/spring/install15.png)