---
title: "[Java 02] 자바 기초"
date: 2020-04-14
categories:
  - blog
tags:
  - Java
comments: true
excerpt: "자바의 특징과 프로그램 실행과정을 배워보았습니다."
last_modified_at: 2020-04-14T
toc: true
---

## 자바의 특징

자바 언어는 다음과 같은 특징을 가지고 있습니다.

1. 운영체제와 독립적으로 실행이 가능
   하나의 소스파일로 자바 실행 환경(JRE: Java Runtime Environment)이 설치된 모든 운영체제에서 실행이 가능합니다.

2. 객체지향 언어
	부품에 해당하는 객체를 먼저 만들고, 이것들을 하나씩 조립 및 연결해서 전체의 프로그램을 완성하는 객체 지향 프로그래밍 언어입니다.

3. 메모리 자동관리(GC: Garbage Collector)
	객체 생성 시 자동으로 메모리 영역을 찾아서 할당하고 사용이 완료되면 GC를 실행시켜 자동적으로 사용하지 않는 객체를 제거시켜줍니다.

## 자바 가상 머신(JVM)

자바 프로그램은 완전한 기계어가 아닌, 중간 단계의 바이트 코드(bytecode)이기 때문에 운영체제에서 이를 해석하고 실행하기 위해서는 가상의 운영체제인 자바 가상 머신(JVM)이 필요합니다. 

이처럼 운영체제와 자바 프로그램을 중계하는 JVM을 두어 여러 운영체제에서 동일한 실행 결과를 나오도록 설계한 것입니다. 따라서 JVM은 자바 프로그램을 운영체제가 이해하는 기계어로 번역하여 실행해야 하기 때문에 운영체제에 맞는 JVM을 설치해야 합니다.  

![자바기초](\assets\images\java\javabase01.png)

## 자바 소스 작성과 실행

자바 공부를 위해 이클립스를 설치했지만, 그 전에 작성한 소스파일이 JVM에서 구동되는 과정 **`소스파일(Hello.java) -> 바이트코드 파일(Hello.class) -> JVM을 통한 기계어 번역(java.exe) 실행`** 을 살펴보겠습니다.

![자바기초](\assets\images\java\javabase08.png)


먼저 소스 파일을 작성해줍니다. 메모장을 열고 **`파일 > 다른 이름으로 저장 > 저장 위치는 'C:\Temp 디렉토리' > 파일명은 'Hello.java' > 저장`**

![자바기초](\assets\images\java\javabase02.png)

![자바기초](\assets\images\java\javabase03.png)
<br/>
<br/>


다음과 같이 "Hello Java!!"를 출력하는 소스 파일을 작성합니다. 

```
public class Hello { 
	public static void main(String[] args) {
		System.out.println("Hellow Java!!");
	}
}
```
<br/>
<br/>


CMD 명령창을 실행하고 C:\Temp 디렉토리로 이동하기 위해 아래와 같이 작성하고 엔터를 누릅니다.

``` 
cd C:\temp 
```
<br/>
<br/>


해당 디렉토리 Hello.java 소스 파일을 확인하는 명령어를 실행합니다.

```
dir
```
<br/>
<br/>

결과는 아래와 같이 나옵니다. 

![자바기초](\assets\images\java\javabase04.png)
<br/>
<br/>


컴파일러로 Hello.java 소스 파일을 컴파일합니다. 작성한 소스 파일(Hello.java)을 통해 바이트 코드 파일(Hello.class)을 만드는 과정입니다.

```
javac Hello.java
```
<br/>
<br/>


결과는 아래와 같이 나옵니다.

![자바기초](\assets\images\java\javabase05.png)
<br/>
<br/>



Temp폴더를 확인해보면 'Hello.java'파일과 'Hello.class'파일이 생성된 것을 확인할 수 있습니다.

![자바기초](\assets\images\java\javabase06.png)
<br/>
<br/>


Hello.class를 실행하기 위해 JVM 구동 명령어인 java.exe를 아래처럼 입력하고 실행합니다. 

```
java Hello
```
<br/>
<br/>


아까 작성했던 "Hello Java!!"가 정상적으로 출력되었습니다.  

![자바기초](\assets\images\java\javabase07.png)





