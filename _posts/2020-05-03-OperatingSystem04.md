---
title: "[운영체제 04] 병행 프로세스"
date: 2020-05-04
categories:
  - blog
tags:
  - Operating System
comments: true
excerpt: "운영체제(OS : Operating System) 4장 병행 프로세스"
last_modified_at: 2020-05-04
toc: true
---

## 목차
1. 병행 프로세스
2. 동기화와 임계영역
3. 동기화 도구
4. 프로세스의 상호협력
5. 프로세스 간의 통신

## 병행 프로세스

### 병행성

- 여러 개의 프로세스 또는 스레드가 동시에 실행되는 시스템의 특성을 의미
- CPU 개수에 따라 병행 프로세스 실행 형태가 달라진다.

| 한개의 CPU | 각 프로세스가 짧은 시간 간격으로 번갈아 실행되는 인터리빙 형식으로 진행 |
| 여러개의 CPU | 각 프로세스가 각 CPU에서 온전히 실행되는 병행 처리 형식으로 진행 |


#### 메모리 구조에 따른 병행프로세스 실행 형태


![병행프로세스](\assets\images\os\os19.png)


**(1) 강결합(tightly-coupled) 멀티프로세서 시스템**
- 여러 CPU 간에 하나의 기억장치를 공유하며 하나의 운영체제가 모든 CPU와 시스템 하드웨어를 제어
- master/slave 환경이나 SMP(symmetric multi processing, 대칭구조)가 해당
  
**(2) 약결합(loosely-coupled) 멀티프로세서 시스템**
- 2개 이상의 독립된 컴퓨터 시스템을 통신선을 통하여 연결
- 각 시스템은 자신의 운영체제와 기억장치를 가지고 있으며 독립적으로 운영되고 필요할 때만 통신을 한다.
- 시스템 간의 통신은 메시지 전달(message passing)이나 원격 프로시저 호출방식(remote processing calls, RPC)을 사용
클러스터 구조가 해당


#### 프로세스 처리의 병행성 문제

<br/>

**1. 단일프로세스 내의 병행성**

우선순위 그래프, Fork/Join 구조, 병행문 등에 의해 설명이 가능하다.

**(1) 우선순위 그래프**

- 어떤 연산의 일부분이 가지는 우선순위 제약조건을 정의하는 데 유용한 방법

![병행프로세스](\assets\images\os\os20.png)

> S3는 S1과 S2가 완료된 후에 실행될 수 있다.  
> S4는 S3이 완료된 후에 실행될 수 있다.


**(2) Fork/Join 구조**

![병행프로세스](\assets\images\os\os22.png)

우선순위 그래프의 예제를 통해 Fork/Join 구조를 설명해보자면, 

**Fork**

- fork L 명령어는 프로그램 내에서 2개의 병행 수행을 만든다. 
- 하나는 L로 레이블이 붙여진 문장에서 수행 시작, 다른 하나는 fork 명령어 다음 문장을 계속 수행 
- fork L1문이 수행될 때, b:=z+1;이 시작되고, 이 연산은 a:=x+y;와 동시에 수행 

![병행프로세스](\assets\images\os\os21.png)

**Join**
- join 명령어는 병행하는 2개의 연산을 하나로 재결합시키는 방법 제공
- 어느 하나가 먼저 join을 실행하게 될 경우에, join을 수행한 연산이 먼저 종료되고 반면에 두 번째 연산은 계속된다.



**(3)병행문**

- 1개의 프로세스가 여러 가닥의 병렬 프로세스로 분할되었다가 다시 한 가닥의 프로세스로 결합하는 것
- 병행성을 식별하는 고급 언어 구조는 parbegin/parend 문에서 볼 수 있으며 다음과 같은 형태 갖는다.  

`parbegin S1; S2; ...; Sn; parend`  

- 아래의 그림처럼 parbegin과 parend 사이에 있는 모든 문장은 병행하여 수행이 가능하고 parend 다음 문장은 모든 문장이 끝난 후에만 실행이 가능하다.

![병행프로세스](\assets\images\os\os23.png)



**2. 프로세스 간의 병행성**

- 프로세스 간의 병행성은 프로세스가 서로 완전히 독립하여 수행되거나 다른 프로세스와 가끔 협력하면서 기능을 수행하는 방법으로 구분이 가능하다.
- 프로세스 간의 병행성에서 상호 협력하는 경우를 비동기적(asynchronous) 이라고 말하며, 때때로 자원을 공유해야 되기 때문에 다소 복잡하다.
- 여기서 비동기 병행 프로세스는 어떤 프로세스가 실행 중인 다른 프로세스에 영향을 주는 유기적 프로세스이다.
- 다음의 그림은 유기적 프로세스 간에 일어날 수 있는 문제점이다.


![병행프로세스](\assets\images\os\os24.png)


| 잔고가 50,000원인 하나의 통장에 A는 30,000원을 입금하고 B는 20,000원을 입금하는 상황이다. |
| A와 B가 동시에 엔터를 눌러 입금을 한다면, A는 잔고 50,000원을 읽어가 30,000원을 입금해 80,000원을 잔고에 갖다 놓는다 |
| B는 잔고 50,000원을 읽어가 20,000원을 입금해 70,000원을 잔고에 갖다 놓는다 |
| 그러면 최종 잔고는 70,000원이 되어 정상적인 처리 결과인 100,000원과 다르게 된다. |

이와 같은 문제점을 해결하기 위한 방법이 **동기화와 임계영역**이다


<br/>


## 동기화와 임계영역

### 1. 프로세스 동기화  

- 2개 이상의 프로세스에 대한 처리순서를 결정하는 것  
- 동시에 사용할 수 없는 공유자원이 있는 경우 프로세스 동기화의 성공 여부는 **(a)하나의 자원이 사용되는 동안(임계영역)**에 **(b)다른 프로세스에서는 사용이 불가능(상호배제)**하도록 만드는 운영체제에 달려있음  
- 한 프로세스의 처리 결과에 따라 다른 프로세스의 처리가 영향을 받는 경우에도 프로세스 동기화가 명확할 필요성이 있다.  

※ 임계자원 : 프린터처럼 둘 이상의 프로세스가 공유할 수 없는 자원

<br/>

**(a) 임계영역(critical section)**
- 프로그램에서 각 프로세스는 임계영역이라 불리는 코드 세그먼트를 갖는데, 이 세그먼트에서 프로세스는 공용변수를 읽고, 테이블을 갱신하고, 파일에 쓰는 등의 일을 한다.   
- 시스템의 가장 중요한 특징은 하나의 프로세스가 임계영역에서 수행 중일 때 다른 어떠한 프로세스도 이 임계영역에서 수행될 수 없다는 것  
- 프로세스에 의한 임계영역의 수행은 상호배제, 즉 어떤 프로세스가 임계영역에 있을 경우 다른 프로세스는 그 임계영역에 들어갈 수 없고 배타적으로 수행되도록 프로토콜을 설계  


<br/>

**(b) 상호배제(mutual exclusion)가 요구되는 이유?**
- 유기적 프로세스 간의 문제는 2개 이상의 프로세스가 공유 메모리나 공유 파일을 사용하는 경우에 발생할 수 있으며, 그로 인한 데이터 값의 부정확성은 전체 데이터를 신뢰할 수 없게 만들 수 있다.


앞서 보았던 통장 예시로 다시 돌아가보면, 임계영역은 바로 잔고를 읽고 입금액만큼 더한 잔고를 다시 쓰는 부분이다. 이 임계영역에 대한 상호배제가 지켜지지 않으면 앞서 본 것처럼 잔고 계산이 잘못될 수 있는 것이다.


<br/>

### 2. 임계영역을 갖는 프로세스의 일반적 구조  

![병행프로세스](\assets\images\os\os25.png)


**(1) 진입코드 영역, 진입영역(entry section)**  
- 각 프로세스는 그 임계영역에 들어갈 수 있는지의 여부를 미리 요청, 이런 요구를 구현하는 코드 영역	

**(2) 해제영역(exit section)**  
- 임계영역의 수행을 마치고 다음에 진입할 프로세스를 선택하는 것

**(3) 잔류영역(remainder section)**  
- 나머지 코드, 임계영역을 마치고 나와서 나머지 작업을 수행


<br/>

### 3. 임계영역 문제 해결을 위한 요구 3가지    


 
**(1) 상호배제**  

프로세스가 임계영역에서 수행 중일 때 다른 어떤 프로세스도 임계영역에서 수행될 수 없다.  

**(2) 진행**  

임계영역에서 수행되는 프로세스가 없고 여러 개의 프로세스가 임계영역에 들어오고자 할 때에는 그중에서 다음에 임계영역에서 실행될 대상으로 적절히 한 프로세스를 결정해여 하며 이 결정은 무한정 미루어질 수 없다.  

**(3) 제한된 대기**  

한 프로세스가 임계영역에 대한 요청 후부터 요청이 수락되기까지의 기간 내에 다른 프로세스가 임계영역을 수행할 수 있는 횟수에는 제한이 있어야 한다.


<br/>


## 동기화(synchronization) 도구

동기화는 절대영역에서 일할 수 있는 프로세스에 앞서 ‘lock-and-key’를 실행한다. 이것은 키를 요구하는데, 일단 키를 가지면 절대영역에 들어간 프로세스가 일을 마치고 키를 반환할 때까지 모든 다른 프로세스는 잠기게 된다. 

| 프로세스는 먼저 키가 사용 가능한 상태인가를 확인한다. |
| 사용 가능하다면 키를 차지해 잠금을 걸어 다른 프로세스가 접근할 수 없도록 하는 순차적 행위로 구성 |

이러한 방법을 수행하는 방법에는 대표적으로 'Test-and-Set'과 '세마포어' 방식이 있다.


### 1. Test-and-Set

- 상호배제의 하드웨어적 해결 방법으로 분리가 불가능한 단일 기계 명령어로서, 간단히 ‘TS’라고 한다.  
- 단일 기계 사이클로 동작하여 프로세서는 lock을 사용할 수 있을지 여부를 확인한 후 사용할 수 있으면 다른 프로세스가 사용할 수 없도록 '사용할 수 없음(unavailable)으로 세팅
- 구현의 열쇠는 메모리 속에 있는 하나의 비트, 사용하고 있지 않으면(free) 0의 값을, 사용 중(busy)이면 1의 값을 갖는다.
- 중요한 특징은 원자적으로 수행된다는 점, 원자적이란 인터럽트되지 않는 하나의 단위로 처리됨을 의미한다. 즉, 하나의 명령 사이클 내에서 이루어진다.


![testandset](\assets\images\os\os26.png)

<br/>

| 1. 프로세스 P1은 절대영역에 들어가기 전에 TS 명령어를 이용하는 조건 코드를 검사 |
| 2. 다른 프로세스가 절대영역에 없다면 P1은 수행되는 것을 허락받고 조건 코드는 0에서 1로 변경 |
| (만약 P1이 busy 상태 코드를 발견하게 된다면 조건 코드를 계속 검사하면서 들어갈 수 있을 때까지 기다리는 대기 루프에 머무른다) |
| 3. 프로세스 수행 후, P1이 절대영역을 빠져나갈 때 0으로 다시 리셋(reset)해서 다른 프로세스가 들어갈 수 있도록 세팅 |

<br/>


시스템이 Test_and_Set 명령을 제공한다면, 상호배제는 false로 초기화한 boolean 변수 lock을 선언함으로써 다음과 같이 구현된다.

![testandset](\assets\images\os\os27.png)


Test-and-Set은 두가지 결점을 가지고 있다.  

1. 결점이 많은 프로세스가 절대 영역에 들어가기를 원할 때 기아가 발생한다. 그 이유는 프러세스가 임의의 접근을 시도하기 때문이다. FCFS 정책이 정해지지 않는다면 어떤 프로세스가 실행되지 못할 수도 있다.   
2. 대기 프로세스는 비생산적이고 자원만을 소비하는 busy waiting 일어나게 된다.


<br/>


### 2. 세마포어(Semaphore)

세마포어의 예는 철도에서 열차의 진행 가능 여부를 나타내는 신호기이다. 신호기가 올라가면 장애물이 있다는 표시로 열차는 신호기가 내려갈 때까지 기다려야 한다.

![testandset](\assets\images\os\os28.png)


세마포어 s는 정수값을 가지며 두 표준단위 연산(atomic operation) P와 v엥 의해서만 접근되는 정수형 공용변수로서 P는 네덜란드 어로 검사, V는 증가를 나타낸다. P, V 연산이 세마포어 변수를 수정하는 것은 개별적으로 수행된다. 즉, 한 프로세스가 세마포어의 변수 s를 수정할 때 다른 어떤 프로세스가 동시에 같은 변수 값을 수정할 수 없다. 


![testandset](\assets\images\os\os29.png)


## 프로세스의 상호협력

몇 개의 프로세스가 공통작업을 수행하기 위하여 서로 협동하는 경우가 있는데, 가장 대표적인 예가 '생산자와 소비자', '판독기와 기록기'의 예이다. 각각은 양쪽에 상호배제와 동기화를 요구하며 세마포어를 이용하여 실행한다.  



### 생산자/소비자 문제

생산자/소비자 문제는 유한버퍼(bounded buffer) 문제라고도 한다. 고정된 크기를 가진 버퍼를 사이에 두고 버퍼가 비어있다면 소비자가 기다리게 되고 버퍼가 가득 차면 생산자가 기다린다. 


![testandset](\assets\images\os\os30.png)


생산자와 소비자는 같은 버퍼에 접근하므로 생산자는 소비자가 버퍼를 소비하는 동안 버퍼에 데이터를 채워 넣을 수 있으나 버퍼가 꽉 찼는데도 계속 생산하게 되면 소비자는 버퍼가 찼는데도 데이터를 가져올 수 없다.

이런 프로세스가 버퍼를 통해 협동한다면 생산자는 버퍼가 가득 찼을 때에는 더이상 정보를 생산하지 말아야 하고, 생산자는 버퍼가 비어 있을 때에는 더 이상 소비를 하면 안된다. 즉, 버퍼가 비어 있으면 소비자가 기다리고, 버퍼가 가득 차면 생산자가 기다려야 하므로 생산자와 소비자는 동기화되야 한다.

**생산자 프로세스에 대한 코드**

```c++
repeat
    ...
    nextp에 데이터 항목을 생산함
    ...
    P(empty)  // 비어있는 버퍼의 수가 1만큼 감소
    P(mutex)  
    ...
    nextp를 버퍼에 넣음
    ...
    V(mutex)
    V(full)  // 비어있는 버퍼의 수가 1만큼 증가
until false;
```


**소비자 프로세스에 대한 코드**

```c++
repeat
    ...
    P(full)  // 차있는 버퍼의 수가 1만큼 감소
    P(mutex)  
    ...
    버퍼에서 데이터 항목을 꺼내 nextc에 넣음
    ...
    V(mutex)
    V(empty)  // 차있는 버퍼의 수가 1만큼 증가
    ...
    nextc에 있는 데이터 항목을 소비함
    ...
until false;
```

<br/>


### 판독기/기록기 문제

데이터 객체(data object, 파일이나 레코드 같은 것)는 여러 병행 프로세스 간에 공유될 수 있다. 이런 프로세스 중 일부는 다른 것이 공유객체의 내용을 읽기를 원할 때, 공유객체의 갱신(읽기, 쓰기)을 원할 수 있다. 읽고자 하는 프로세스는 판독기, 쓰고자 하는 프로세스는 기록기라고 구분한다.

2개의 판독기가 동시에 공유 데이터 객체에 접근할 때는 아무런 문제가 일어나지 않는다. 그러나 기록기와 또 다른 프로세스(판독기 또는 기록기)가 동시에 공유객체에 접근한다면 문제가 발생해 병행성 조건을 침해하게 된다. 이러한 형태의 문제가 발생하지 않도록 기록기가 공유객체에 대해 배타적 접근(한 순간에 한 프로세스만 접근)을 하도록 해야 한다. 
  

**동기화 문제를 판독기/기록기 문제**

(1) 제 1 판독기/기록기 문제
- 기록기가 이미 공유객체를 사용하도록 허가되지 않았다면 판독기는 대기하지 않는다. 다시 말해서 어떠한 판독기도 기록기가 대기중이라는 이유로 다른 판독기가 끝나기를 기다리지 않는다.
- 기록기가 기아상태일 수 있다.

(2) 제 2 판독기/기록기 문제
- 일단 기록기가 준비되었다면 기록을 가능한 한 빨리 수행할 수 있도록 하는 것이다. 다시 말해서 기록기가 객체에 접근하기 위하여 대기 중일 때에는 어떠한 새로운 판독기도 읽기를 시작할 수 없다.
- 판독기가 기아상태일 수 있다.


※ 판독기/기록기 문제 해결 방법은 추후 보충



## 프로세스 간의 통신 

앞서 여러 가지 문제가 동기화 문제로 제시되었는데, 결국에 이들은 협력하려는 프로세스 간의 통신을 허락하는 문제의 예라고 할 수 있다.
원칙적으로 2개의 상호 보완적인 통신 프로세스가 통신하는 기법에는 두 가지가 있다. 공유기억장치 기법과 메시지 시스템 기법이다.

### 공유기억장치 기법(shared memory)

- 통신하는 프로세스 간에 어떤 변수를 공유하도록 하여 프로세스가 이런 공유변수를 이용하여 정보를 교환하도록 하는 것
- 앞에서 설명한 유한 버퍼가 예이다.
- 고속통신이 가능
- 통신 기능을 제공하는 책임은 응용 프로그래머에게 달려 있고 운영체제는 단지 공유 기억장소만을 제공


### 메시지 시스템 기법(message system)

- 메시지 시스템 기법은 메시지 교환방식을 이용함으로써 프로세스가 공유변수에 의존하지 않고도 서로 통신할 수 있게 하는 것
- 프로세스 간의 통신기능은 기본적으로 send(message)와 receive(message) 연산자 형태로 제공되고, 보다 소량의 데이터 교환하는 데 유효한 방식
- 통신을 제공하는 책임은 운영체제 자체에 있다.
- 프로세스 P와 Q가 통신하기를 원한다면 서로 메시지를 주고받아야 하는데 그러기 위해서는 통신 링크(communication link)가 그들 사이에 이루어져야 한다.








