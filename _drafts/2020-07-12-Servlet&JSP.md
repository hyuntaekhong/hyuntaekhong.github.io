---
title: "[WEB] Servlet과 JSP"
date: 2020-07-12
categories:
  - blog
tags:
  - WEB
  - Servlet
  - JSP
  
comments: true
excerpt: Servlet과 JSP
last_modified_at: 2020-07-12
toc: true
---

![WAS](/assets/images/linux/was02.png) <br/>

지난 시간 Web Server와 WAS에 대해 공부했다. 오늘은 WAS 내부에 Web Container 내부에 있는 JSP, Servlet에 대해 살펴보자. 


## 1. Servlet

### 1) 개념  
	-	웹프로그래밍에서 클라이언트의 요청을 처리하고 그 결과를 다시 클라이언트에게 전송하는 Setvlet 클래스의 구현 규칙을 지킨 자바프로그래밍 기술
	-	즉, 자바를 사용해서 웹을 만들기 위해 필요한 기술로 클라이언트가 요청에 결과를 응답해주는 자바 프로그램이다..
	- 예를 들어, 로그인 시 사용자는 아이디와 비밀번호를 입력하고, 로그인을 한다. 이때 서버는 클라이언트의 아이디와 비밀번호를확인하고, 다음 프로세스를 진행해야 하는데, 이러한 역할을 수행하는 것이 바로 Servlet이다.
  - Servlet을 자바로 구현된 CGI라고도 한다.

### 2) 특징
  


