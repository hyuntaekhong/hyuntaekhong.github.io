---
title: "[Design Pattern] 자바 디자인 패턴 - Singleton"
date: 2020-08-16
categories:
  - blog
tags:
  - JAVA
  - Design_Pattern

comments: true
excerpt: 자바 디자인 패턴 - 싱글톤 패턴 
last_modified_at: 2020-08-16
toc: true
---

## 싱글톤 패턴

### 개념

- 생성자가 여러번 호출되더라도 실제로 생성되는 객체는 하나이고 최초로 생성 이후 호출되는 생성자는 이미 생성된 객체를 리턴하는 것을 의미한다.
- 주로 공통된 객체를 여러개 생성해서 사용하는 DBCP(DataBase Connection Pool)와 같은 상황에 많이 사용된다.

### 예제

```java
package basic;
public class HelloSingle {
	
	private static HelloSingle instance = null;	
	private String msg ="안녕 난 싱글턴이야...";
	
	// 기본 생성자 private으로 만들어 생성을 불가능하게 했다.
	// getInstance를 통해서만 생성이 가능하다.
	private HelloSingle() {	}
	
	// getInstance는 내부적으로 생성되지 않았다면 생성하고
	// 기존에 생성된 값이 존재한다면, 기존 인스턴스를 리턴하는 형태를 취한다.
	public static HelloSingle getInstance() {
		if(instance == null) {
			instance = new HelloSingle();
		}
		return instance;
	}
	
	public void prnMsg() {
		System.out.println("msg : " + msg);
	}
}
```

- getInstance는 내부적으로 생성되지 않았다면 생성하고, 기존에 생성된 값이 존재한다면 기존 인스턴스를 리턴하는 형태를 취한다.
- 이와 같은 구조로 인해, 프로그램 전반에 걸쳐 하나의 인스턴스만을 유지한다.
- 인스턴스를 제공하는 메서드와 인스턴스 변수 모두 static으로 선언된 정적 변수 및 메서드이다. 기본생성자를 통해 생성할 수 없기 때문에
외부에서 인스턴스에 접근하려면 클래스 변수 및 메서드에 접근을 허용해야 하기 때문에 두 메서드는 static으로 선언된 것이다.

### 문제점

- 1) 멀티 스레드 환경에서 안전하지 않다는 문제가 발생한다. 여러 스레드가 공유되는 상황에서 아래의 조건문이 동시에 실행될 수 있기 때문에 하나의 인스턴스가 아닌 여러개의 인스턴스가 발생할 위험이 있다.

```java
public static HelloSingle getInstance() {
		if(instance == null) {
			instance = new HelloSingle();
		}
		return instance;
	}
```

- 2) 아래와 같이 count는 각기 다른 스레드에서 공유하고 각기 다른 프로세스에서 처리하고 있기 때문에 값이 일관되지 않을 수 있다.


```java
package basic;
public class HelloSingle {
	private static HelloSingle instance = null;	
	private String msg ="안녕 난 싱글턴이야...";
	private int count= 0;
	
	// 기본 생성자 private으로 만들어 생성을 불가능하게 했다.
	// getInstance를 통해서만 생성이 가능하다.
	private HelloSingle() {	}
	
	// getInstance는 내부적으로 생성되지 않았다면 생성하고
	// 기존에 생성된 값이 존재한다면, 기존 인스턴스를 리턴하는 형태를 취한다.
	public static HelloSingle getInstance() {
		if(instance == null) {
			instance = new HelloSingle();
		}
		return instance;
	}
	
	public void prnMsg() {
		count++;
		System.out.println("msg(호출 횟수) : " + msg + "(" + count + ")" );
	}
}
```


### 해결책

- 멀티스레드 환경에서 싱글톤의 문제점을 해결하는 두가지 방안
	- 1) static 변수에 인스턴스를 만들어 바로 초기화하는 방법
	- 2) 인스턴스를 만드는 메서드에 동기화하는 방법 

- 해결책 1) static 변수에 인스턴스를 만들어 바로 초기화하는 방법
	- static 변수는 객체가 생성되기 전 클래스가 메모리에 로딩할 때 만들어져 초기화가 한 번만 실행된다. 또한 정적 변수는 프로그램이 시작될 때부터 종료될 때까지 없어지지 않고 메모리에 계속 상주하며 클래스에서 생성된 모든 객체에서 참조할 수 있다. 따라서 조건문에서 instance는 null이 될 수 없으므로 기존 생성된 instance를 리턴하게 되는 것이다.
	- 그러나 객체생성 자체는 로드 시점에 결정되어 하나의 객체만을 사용하지만 count에 접근하는 것은 아무 제약없이 동시에 접근이 가능하므로 원치않는 결과를 가져올수도 있다. 
	- 이를 해결하는 방법은 아래의 코드처럼 synchronized를 통해 여러 스레드에서 동시에 접근하는 것을 막는 방법이다.

```java
package basic;
public class HelloSingle {
	private static HelloSingle instance = null;	
	private String msg ="안녕 난 싱글턴이야...";
	private int count= 0;
	
	private HelloSingle() {	}
	
	public static HelloSingle getInstance() {
		if(instance == null) {
			instance = new HelloSingle();
		}
		return instance;
	}
	
	// synchronized를 통해 여러 스레드에서 동시에 접근하는 것을 막는다.
	public sinchronized static void prnMsg() {
		count++;
		System.out.println("msg(호출 횟수) : " + msg + "(" + count + ")" );
	}
}
```

- 이 방법처럼 static을 선언하면 객체를 전혀 생성하지 않고 메서드를 사용할 수 있고 인스턴스 메서드를 사용하는 것보다 성능 면에서 우수하다.


- 해결책 2) 인스턴스를 메서드에 동기화시키는 방법
	- 인터페이스를 구현하는 경우, 인터페이스는 static 메서드를 가질 수 없기 때문에 static을 사용할 수 없는 상황이 발생한다.


**[ Printer.java 인터페이스 ]**

```java
public interface Printer {
	public void prnMsg(String msg);
}
```


**[ RealPrinter.java ]**

```java
public class RealPrinter implements Printer{
	private static Printer printer = null;
    
	private RealPrinter() {
	}

	public synchronized static Printer getInstance() {
		if (printer == null)
			printer = new RealPrinter();
		return printer;
	}

	@Override
	public void print(String msg) {
		System.out.println(msg);
	}
}
```


**[ UsePrinter.java ]**

```java
public class UsePrinter {
	public void doSomething(Printer printer) {
		printer.print("fakeGet");
	}
}
```

**[ FakePrinter.java ]**

```java
public class FakePrinter implements Printer{
	private String msg;

	public void print(String msg) {
		this.msg = msg;
	}

	public String get() {
		return msg;
	}
}
```

**[ UsePrinterTest.java ]**

```java
public class UsePrinterTest {
	public void testdoSomething() {
		FakePrinter fake = new FakePrinter();
		UsePrinter use = new UsePrinter();
		use.doSomething(fake);
		assertEquals("fakeGet", fake.get());
	}
}
```


### 싱글톤의 문제점

- 싱글톤은 프로그램 전체에서 하나의 객체만을 공통으로 사용하고 있기 때문에 각 개체간의 결합도가 높아지고 변경에 유연하게 대처할 수 없다. 싱글톤 객체가 변경되면 이를 참조하고 있는 모든 값들이 변경되어야 한다.
- 멀티스레드 환경에서 대처가 가능하지만 고려해야할 점이 많아 사용이 어렵고, 프로그램 전반에 걸쳐 필요한 부분에만 사용한다면 장점이 존재한다.

