---
title: "[web] 이클립스(eclipse) 톰캣(tomcat) 연동하기"
date: 2020-06-11
categories:
  - blog
tags:
  - github
comments: true
excerpt: Apache Tomcat과 eclipse 연동방법을 알아보겠습니다.
cover: 
last_modified_at: 2020-06-11
toc: true
---

## 1. 개요

### 1) tomcat이란?

- Tomcat은 Apache 재단에서 만든 Java Servlet&JSP 기술 구현을 위한 Open Source 입니다.
- Tomcat은 웹 서버와 연동하여 실행할 수 있는 자바 환경을 제공하여 자바 서버 페이지(JSP)와 자바 서블릿이 실행할 수 있는 환경을 제공합니다.

## 2. 설치방법

tomcat을 eclipse와 연결하기 위해서는 두가지 방법이 있습니다. exe 실행파일을 다운받거나 압축파일을 다운받는 방법이 있습니다. 저는 압축파일 다운로드를 통해 연결해보도록 하겠습니다.

**[Download tomcat](https://tomcat.apache.org/download-90.cgi){: target="blanck"}**

위의 다운로드 링크로 들어가 운영체제에 맞는 압축파일을 다운로드합니다.

![tomcat](\assets\images\web\tomcat.PNG)  

1) 다운받은 압축파일을 압축해제 합니다.

![tomcat](\assets\images\web\tomcat01.png)


<br/>
2) 압축해제한 파일을 eclipse-workstation 폴더로 옮겨줍니다.
(저는 E드라이브에 새로운 eclipse-workstation 폴더를 만들어주고 workspace로 설정해주었습니다)

![tomcat](\assets\images\web\tomcat02.png)


<br/>
3) tomcat 폴더가 있는 worksapce로 경로 설정 후 이클립스를 실행합니다.

![tomcat](\assets\images\web\tomcat03.png)


<br/>
4) window > Show View > Servers 를 클릭합니다.

![tomcat](\assets\images\web\tomcat04.png)


<br/>
5) Apache > Tomcat v9.0 Server(본인이 다운받은 버전)을 선택하고 Next를 클릭합니다.

![tomcat](\assets\images\web\tomcat05.png)


<br/>
6) Tomcat Installation directory 설정을 위해 Browse... 클릭합니다.

![tomcat](\assets\images\web\tomcat14.png)

<br/>
7) Tomcat 폴더를 선택하고 '폴더선택' 후 Finish를 클릭합니다. 

![tomcat](\assets\images\web\tomcat06.png)

<br/>
8) 하단 Servers에 선택한 Tomcat항목이 보이고 이것를 더블클릭합니다.

![tomcat](\assets\images\web\tomcat08.png)

<br/>
9) Port Number를 설정해줍니다. 어떤 포트를 사용하던지 상관없지만, 보통 Tomcat 버전이 v8.0이라면 8888, v9.0이라면 9999를 사용한다고 합니다. 저는 9999로 설정해주었습니다. 그 다음 Server path를 tomcat이 있는 폴더로 설정해주고 `ctrl+s`를 눌러 설정을 저장해줍니다.

![tomcat](\assets\images\web\tomcat10.png)


<br/>
10) 하단의 `Start the Server`를 눌러 서버를 실행합니다. 

![tomcat](\assets\images\web\tomcat15.png)


<br/>
11) 콘솔창에 아래와 같은 메세지가 나오면 성공적으로 tomcat 서버가 연동된 것입니다.

![tomcat](\assets\images\web\tomcat11.png)

<br/>
12) 서버가 연동되었으니 web project를 만들어보겠습니다.  
Project Explorer > New > Dynamic Web Project 를 선택하고 Finish를 클릭해 새로운 web project를 만듭니다.

![tomcat](\assets\images\web\tomcat16.png)

![tomcat](\assets\images\web\tomcat13.png)

<br/>

13) Tomcat - eclipse 연동 환경설정이 완료되었습니다. 

![tomcat](\assets\images\web\tomcat17.png)



