---
title: "[운영체제 02] 프로세스의 개요와 구성" 
date: 2020-05-01
categories:
  - blog
tags:
  - Operating System
comments: true
excerpt: "운영체제(OS : Operating System) 2장 프로세스의 개요"
last_modified_at: 2020-05-01
toc: true
---

## 목차

1. 프로세스 개요와 구성
2. 스레드와 스케줄링

## 프로세스

- 프로세스란 실행중인 프로그램을 의미하고 프로세스는 사용자가 실행시킨 프로그램 뿐만 아니라 스풀링과 같은 시스템 테스크도 각각 하나의 프로세스로 취급한다.
- 프로그램 자체는 디스크 내 파일로 존재하고 동작을 하지 않는 정적이며 수동적인 개체여서, 프로그램을 실행시키려면 운영체제로부터 프로그램이 동장작하는데 필요한 CPU, 메모리, 입출력장치, 파일 등의 자원을 할당받아 동장을 시작해야 한다.


![프로세스 설명](\assets\images\os\os05.png)


### 프로세스의 상태 변화

1. 생성상태 -> 준비상태
- 미리 정의된 정책에 따라 스케줄러에 의해 호출, 이때 메모리의 이용 가능성과 어떤 장치가 요구되는지를 검사한다.

2. 준비상태 -> 실행상태
- 사전에 정의된 알고리즘(FCFS, SJF, SRT, RR등)에 따라 스케줄러에 의해 처리된다. 이 과정을 디스패치라고 한다.

3. 실행상태 -> 준비상태
- 할당시간의 만료나 우선순위 알고리즘을 택하고 있는 시스템에서 높은 우선순위의 프로세스가 오는 경우 스케줄러에 의해 처리된다.

4. 실행상태 -> 대기상태
- READ, WRITE 또는 다른 I/O 요구, 페이지 교환을 요구하는 작업 같은 명령 등에 의하여 일어난다.
- 이러한 작업은 상대적으로 오랜 시간이 걸리기 때문에 그동안 CPU를 다른 프로세스에 할당하여 활용하기 위함이다.

5. 대기상태 -> 준비상태
- I/O 장치 관리자의 신호에 의해 일어난다.
- 페이지 교환의 경우 페이지 인터럽트 핸들러가 메모리에 그 페이지가 있다는 신호를 보내게 되며, 프로세스는 준비 큐에 놓이게 된다.

6. 실행상태 -> 종료상태
- 프로세스를 성공적으로 끝마친 경우, 혹은 운영체제가 에러 발생을 감지하고 프로세스를 강제로 종료시킨 경우에 스케줄러에 의해 실행된다.


### 프로세스 제어 블록(Process Control Block, PCB)

- 프로세스의 관리를 위해 운영체제는 프로세스 제어블록에 정보를 보관한다.


![프로세스 설명](\assets\images\os\os06.png)

**1. 프로세스 상태**
- 프로세스의 현재 상태

**2. 프로세스 번호(PID)**
- 프로세스의 구분 기준이 되는 ID를 나타낸다.

**3. 프로그램 카운터(PC)**
- 프로세스 수행을 위한 다음 명령의 주소를 표시한다.

**4. 레지스터(register)**
- 실행상태에서 다른 상태로 전이되는 경우 CPU의 레지스터 정보를 이곳에 저장시켜서 나중에 다시 실행상태로 전이될 때 복구 시켜 프로세스의 정확한 수행을 이어나간다.

**5. 메모리**
- 프로세스가 저장된 주소와 가상 메모리를 사용하는 경우에는 가상주소와 실제주소의 사상(mapping) 정보, 기준 레지스터(base register)와 경계 레지스터(bound register) 등의 정보를 포함한다.

**6. 프로세스 우선순위**
- 시스템에 의해 이용, 스케줄링 시 어떤 작업을 선택할 것인가를 결정

**7. 회계정보**
- 성능 측정과 순위에 대한 목적을 위한 정보이다.
- CPU 사용시간, 프로세스의 시스템 존재 시간, 메모리 사용량, 보조기억장치 사용량, 그리고 기타 시스템 프로그램의 사용 실태 등의 다양한 정보를 포함한다. 


### 프로세스의 생성과 종료

**1. 프로세스 생성**

- 부모 프로세스는 실행과정 동안 프로세스 생성 시스템의 호출을 이용하여 여러개의 자식 프로세스를 생성한다.
- 프로세스 생성과 관련된 작업인 프로세스의 이름을 결정하고 프로세스 준비 큐에 삽입하여 프로세스에 초기 우선순위를 부여하고 프로세스에 대한 플세스 제어 블록을 만든다.
- 프로세스는 작업을 수행하기 위해 자원이 필요한데 자식 프로세스가 생성되면 운영체제로부터 직접 자원을 얻거나 부모 프로세스 자원의 일부를 얻는다.(과도한 서브 프로세스 생성으로 인한 과부하 방지)
- 프로세스 생성시 물리적, 논리적 자원을 얻는 것 이외에도 몇몇 초기화 데이터가 부모에 의해 자식 프로세스로 전달된다. 


**2. 프로세스 종료**

- 프로세스는 마지막 문장이 실행을 마쳤을 때 종료된다. 이때 프로세스는 부모 프로세스에게 실행결과를 되돌려 준다.
- 부모 프로세스가 자식 프로세스 실행 종료시킬 수 있는 경우
  a) 자식 프로세스가 할당된 자원의 사용을 초과했을 경우  
  => 이는 부모 프로세스가 자식 프로세스 상태를 조사할 수 있는 메커니즘이 필요하다.
  b) 자식 프로세스에게 할당된 작업이 더 이상 필요하지 않은 경우


### 프로세스 간의 관계

**1. 독립적 프로세스**

- 시스템에서 실행중인 다른 프로세스의 영향을 받지도 주지도 않는 프로세스를 의미한다.
- 프로세스 상태는 다른 프로세스와 공유되지 않는다.
- 프로세스 실행은 결정적(deterministic)이다. 즉, 실행결과는 입력상태에 의해서만 결정된다.
- 프로세스의 실행은 재생가능(reproducible)하다. 즉, 실행결과는 같은 입력에 대하여 항상 동일하다.
- 프로세스 실행은 타 프로세스와 무관하게 중단되거나 재시작될 수 있다.

**2. 유기적 프로세스**

- 시스템에서 실행중인 다른 프로세스의 영향을 주고 받으며 동작하는 프로세스를 의미한다.
- 프로세스의 상태는 다른 프로세스와 공유된다.
- 프로세스의 실행은 비결정적(nondeterministic)이다. 즉, 실행결과는 실행순서에 좌우되기 땨문에 미리 예측할 수 없다.
- 프로세스의 실행은 재생 불가능(irreproducible)하다. 즉, 실행결과는 동일한 입력에 대하여 항상 동일하지는 않는다.


## 스레드(Thread)
- 스레드는 프로세스 내에서의 다중처리를 위하여 제안된 개념으로 실행 단위를 프로세스에서 한 단계 낮추어 규정한 것이다. 
일반적으로 다중 프로세싱 시스템에서 기본적인 처리단위는 프로세스이다. 


![프로세스 설명](\assets\images\os\os07.png)

스레드는 제어의 흐름을 의미하며 프로세스에서 실행의 개념만을 분리한 것으로 실행에 필요한 최소한의 정보만을 가지고 프로그램 수행 시 자신이 속해있는 프로세스의 실행환경을 공유한다.
대부분의 기존 프로그램은 하나의 프로세스가 하나의 스레드를 갖는 형태이나 처리효율을 극대화하는 방법으로 프로세스 내에서의 병렬적 수행을 위하여 다중 스레딩을 이용한다.


## 스케줄링

### 스케줄링 단계

![프로세스 설명](\assets\images\os\os08.png)

**1. 상위단계 스케줄링**
- 시스템에 들어오는 작업들을 선택하여 프로세스를 생성한 후 프로세스 준비 큐에 전달하는 역할이다.
- 이때 선택 기준은 시스템의 자원을 효율적으로 이용할 수 있도록 하는 것으로, 보통 입출력 중심 작업과 연산 중심 작업을 균형있게 선택하도록 작업 순서를 결정한다.

**2. 하위단계 스케줄링**
- 사용 가능한 CPU를 준비상태의 어느 프로세스에 배당할지를 결정하는 것이다. 이 결정을 통하여 CPU를 배당받은 프로세스는 결국 실행상태가 되면서 프로세스가 처리된다.
- 이 결정을 통하여 CPU를 배당받은 프로세스는 결국 실행상태가 되어 처리되는데 이를 디스패처라고 한다.

**3. 중간단계 스케줄링**
- 프로세스를 일시적으로 메모리에서 제거하여 중지시키거나 다시 활성화시켜서 시스템에 대한 단기적인 부하를 조절한다.
- 시스템 과부하가 되는 경우 어떤 프로세스를 메모리에서 제거해야 부하가 줄어들지를 결정하고 실제 중지를 실행하여 최고의 성능을 유지한다.


### 스케줄링 정책
- 운영체제가 프로세스를 스케줄링할 때 고려하는 기본적인 목표 두가지는 '공정성'과 '균형'이다.
  a) 공정성 : 모든 프로세스가 적정 수준에서 CPU 작업을 할 수 있게 하는 것
  B) 균형 : 시스템의 자원들을 충분히 활용하는 것

- 이외에도 일괄처리 운영체제는 처리량 극대화, 반환시간 최소화, CPU 활용의 극대화를 스케줄링 목표로 한다.
- 대화형 운영체제는 빠른 응답시간과 과다한 대기시간 방지를 목표로 한다. 

**1. 선점 스케줄링 정책**

- 진행중인 작업에 인터럽트를 걸고 다른 작업에 CPU를 할당하는 스케줄링 전략
- 시간 할당 방식에서 주로 사용한다.
- 높은 우선순위의 프로세스가 긴급할 경우에 유용하다.
- 단점은 경비가 많이 들고 오버헤드를 초래한다. 또한 문맥교화의 문제가 발생한다.

※ 문맥교환(context switching)
- 문맥 교환이란 CPU가 현재 실행하고 있는 프로세스의 문맥(상태)을 프로세스 제어 블록(PCB)에 저장하고, 다음 프로세스의 PCB로부터 문맥을 복원하는 작업이다.
- CPU의 모든 레스스터와 기타 운영체제에 따라 요구되는 프로세스의 상태를 문맥(context)이라고 부르는데, 프로세스가 종료되지 않은 상태에서 선점 스케줄링 정책에 따라 CPU가 다른 프로세스에 할당되려면 문맥 교환이 필요하다.

**2. 비선점 스케줄링 정책**

- 프로세스가 CPU를 할당받아 실행이 시작되면 프로세스 자체가 I/O 인터럽트를 걸거나 프로세스를 종료할 때까지 실행상태에 있는다.
- 비선점 스케줄링은 우선순위와 관계없이 모든 프로세스가 공정하게 순서에 따라 실행되도록 관리된다.