---
title: "[Java] 이클립스 간단한 사용방법"
date: 2020-04-12
categories:
  - blog
tags:
  - Java
  - Eclipse
comments: true
excerpt: "이클립스를 이용해 Java Project, Package, Class를 만들어보겠습니다."
last_modified_at: 2020-04-12T22:45:50-03:00
toc: true
---

## 1. Java Project 생성

- 먼저 지난 시간에 설치한 이클립스를 실행하고 Workspace를 설정하고 Launch를 클릭해 실행해줍니다. 딱히 설정할 Workspace 경로가 없다면 기본값으로 진행하면 됩니다.

	![이클립스 사용법_1](/assets/images/eclipse/eclipse08.png)

- 메인화면이 나오면 File > New > Java Project 를 실행합니다.(해당 명령의 단축키는 'Ctrl + n' 입니다)

	![이클립스 사용법_2](/assets/images/eclipse/eclipse10.png)

- Project name은 'test'로 만들어보겠습니다. Finish를 누르면 Java project가 만들어집니다.

	![이클립스 사용법_3](/assets/images/eclipse/eclipse11.png)

- test라는 project가 만들어진 것을 확인할 수 있습니다.

	![이클립스 사용법_4](/assets/images/eclipse/eclipse12.png)


## 2. Package 생성

- test > src 아이콘을 우클릭하고 'New > Package'를 클릭해 Package를 만듭니다.

	![이클립스 사용법_5](/assets/images/eclipse/eclipse13.png)

- Source folder : 'test/src'  Name : 'testPackge' 로 설정하고 Finish를 클릭하면 패키지가 만들어집니다.

	![이클립스 사용법_6](/assets/images/eclipse/eclipse14.png)

## 3. Class 생성

- test > src > testPackage 아이콘을 우클릭하고 'New > Class'를 클릭합니다.

	![이클립스 사용법_7](/assets/images/eclipse/eclipse15.png)

- Source folder : 'test/src' Package : 'testPackage  Name : 'testJava' 로 설정하고 Finish를 클릭하면 클래스파일이 만들어집니다.

	![이클립스 사용법_8](/assets/images/eclipse/eclipse16.png)

- 클래스까지 모두 만들어졌으니 테스트를 해보겠습니다. 아래 이미지와 같이 "Hello Wolrd!!"를 출력해보겠습니다.

	![이클립스 사용법_9](/assets/images/eclipse/eclipse17.png)

- Run > Run (단축키 : Ctrl + F11)을 클릭해 해당 문구를 출력해봅니다.

	![이클립스 사용법_10](/assets/images/eclipse/eclipse18.png)

- Hello World!! 라고 정상적으로 출력됩니다!

	![이클립스 사용법_11](/assets/images/eclipse/eclipse19.png)


이클립스에서 Java Project, Package, Class를 만들어보았습니다. 다음 포스팅에서는 Java 문법을 차근차근 정리하도록 하겠습니다.