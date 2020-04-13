---
title: "[Java] Java 설치와 환경변수 설정 (JDK 8)"
date: 2020-04-11
categories:
  - blog
tags:
  - Java
  - JDK
comments: true
excerpt: "Java 사용을 위해 JDK를 설치하고 환경변수 설정해보겠습니다."
last_modified_at: 2020-04-11T17:35:50-03:00
toc: true
---

## 1. Java JDK

자바 개발 키트(Java Development Kit, JDK)는 자바 컴파일러(Javac), 자바 가상머신(JVM), 다수의 Java Library 등을 포함하고 있어서 자바 개발을 위한 필수 패키지입니다. 

![JDK_1](/assets/images/jdk/jdk09.png){: width="70%" height="70%"}

본인은 이클립스를 통해 Java를 배우고 개발을 진행할 예정입니다. JDK 버전은 Java8, 패키지는 SE(Standard Edition)을 설치할 것입니다. 버전의 경우 현재 시점 최신 릴리즈인 자바 14를 설치해도 무관합니다. 자바의 경우 하위 호환성(Backward Compatibility)을 유지하고 있으므로 최신 버전을 설치하는 것이 합리적이나, 본인이 듣고 있는 교육에서 사용하는 자바 8버전으로 설치를 진행합니다. 

가용 패키지는 자바 EE(Enterprise Edition), SE(Standard Edition), ME(Mobile Edition)가 있습니다. EE나 ME 버전은 보통 SE 버전에 추가적인 유용한 툴을 제공하고 있습니다. 필요한 경우, 다른 JDK로 전환이 가능하기 때문에 개발 초보자라면 JDK SE를 설치하는
것을 추천합니다. 

## 2. Java JDK 설치

먼저 아래의 사이트로 접속해 Java SE를 다운로드하겠습니다. 

**[Java JDK 다운로드]**
["https://www.oracle.com/java/technologies/javase-downloads.html"]("https://www.oracle.com/java/technologies/javase-downloads.html")


- 저는 JDK 8버전을 설치할 것이기 때문에 'Java SE 8u241'을 설치하겠습니다. JDK 8버전 이외에 다른 버전을 설치하실 경우 해당 버전의 JDK Download를 실행하면 됩니다.

  ![JDK 설치](/assets/images/jdk/jdk01.png){: width="90%" height="90%"}

- 각자 운영체제에 맞는 설치파일을 다운로드 합니다. 저는 제 노트북에 맞는 Windows 64x를 설치하겠습니다. 

  ![JDK 설치](/assets/images/jdk/jdk02.png){: width="90%" height="90%"}

- 다운로드 받은 JDK 설치파일을 실행합니다. 

  ![JDK 설치](/assets/images/jdk/jdk03.png){: width="90%" height="90%"}

- 설치파일을 실행하고 아래의 단계를 쭉 따라가시면 됩니다.

  ![JDK 설치](/assets/images/jdk/jdk04.png){: width="90%" height="90%"}


  ![JDK 설치](/assets/images/jdk/jdk05.png){: width="90%" height="90%"}


  ![JDK 설치](/assets/images/jdk/jdk06.png){: width="90%" height="90%"}


  ![JDK 설치](/assets/images/jdk/jdk07.png){: width="90%" height="90%"}


- 경로 지정 단계가 나오는데, 기본값으로 설치를 진행하게 되면 **C:\Program Files\Java\jre1.8.0_241**로 설치됩니다.

  ![JDK 설치](/assets/images/jdk/jdk08.png){: width="90%" height="90%"}

- 마지막 단계에서 'Close'를 클릭하면 JDK 설치가 완료됩니다!

## 3. Java 환경변수 설정

  Cmd 콘솔에서 디렉토리 이동하지 않더라도 어디서든 Java 명령어를 사용하기 위해 환경변수를 설정해줍니다. 단, 이클립스 같은 통합개발환경에서는 알아서 환경변수를 관리하기 때문에 따로 설정이 필요 없습니다!

- '내 PC'를 우클릭해서 '속성'에 들어가 '고급시스템 설정'에 들어갑니다.

  ![JDK 환경설정](/assets/images/jdk/jdk10.png){: width="90%" height="90%"}

  ![JDK 환경설정](/assets/images/jdk/jdk11.png){: width="90%" height="90%"}


- '고급시스템 설정 > 고급 > 환경 변수'를 클릭해줍니다.

  ![JDK 환경설정](/assets/images/jdk/jdk12.png){: width="90%" height="90%"}

- '새로 만들기'를 클릭하면 '사용자 변수 편집' 메뉴창이 뜹니다.

  ![JDK 환경설정](/assets/images/jdk/jdk13.png){: width="90%" height="90%"}

- '사용자 변수 편집'에 아래와 같이 오타없이 작성하고 확인을 눌러줍니다!

  **변수이름 : JAVA_HOME**     

  **변수값   : C:\Program Files\Java\jdk1.8.0_141**

  ![JDK 환경설정](/assets/images/jdk/jdk14.png){: width="90%" height="90%"}

- 그 다음으로 'Path'를 선택하고 '편집'을 클릭합니다.

  ![JDK 환경설정](/assets/images/jdk/jdk15.png){: width="90%" height="90%"}

- '환경 변수 편집'에서 '새로 만들기'를 클릭하면 사진과 같이 입력이 가능하게 됩니다. 

   **%JAVA_HOME%\bin**라고 입력하고 확인을 눌러줍니다!

  ![JDK 환경설정](/assets/images/jdk/jdk17.png){: width="90%" height="90%"}


- 자바 JDK 설치와 환경변수이 완료되었거 CMD콘솔을 실행시켜 잘 설치되었는지 확인해보겠습니다. 콘솔창에서 **java -version** 명령어를 입력해 아래와 같이 JDK 버전과 관련된 정보가 뜨면 정상적으로 설치된 것입니다.

  ![JDK 환경설정](/assets/images/jdk/jdk16.png){: width="90%" height="90%"}


다음에는 **[Java] 이클립스 설치(Eclipse IDE for Java Developers)**에 대해 알아보겠습니다.


### **[[Java] 이클립스 설치(Eclipse IDE for Java Developers)](https://hyuntaekhong.github.io/blog/install-eclipse/)**

