---
title: "[Github] 초보 개발자의 Github 사용법"
date: 2020-04-04
categories:
  - blog
tags:
  - github
comments: true
excerpt: "개발자에게 가장 친숙한 프로그램인 **GitHub (깃허브)** 사용법을 알아보도록 하겠습니다."
cover: assets\images\githubcapture_1.png
last_modified_at: 2020-04-04T14:07:54-04:00
toc: true
---

## 1. 개요

첫 포스팅으로 개발자에게 가장 친숙한 프로그램인 **GitHub (깃허브)** 사용법을 알아보도록 하겠습니다.
현업에서 많이 사용되고 있지만, 저와 같은 코딩 초보자에게는 생소한 서비스 중 하나라고 생각합니다.

포스팅을 통해 깃허브 사용법 부터 **Jekyll**을 이용한 깃 블로그 만들기까지 진행해보겠습니다!


## 2. 목차
- GitHub 기초 
- GitHub 계정 가입
- GitHub 사용법

## 3. 내용 

### GitHub 기초
GitHub는 소스코드를 효과적으로 관리하기 위한 서비스로 '분산형 버전 관리 시스템'입니다. 소스코드를 열람하고 변경된 이력을 쉽게 관리할 수 있고, 특점 시점에 저장된 버전과 비교하거나 되돌아갈 수 있어 편리한 버전 관리를 지원합니다.

![why github](\assets\images\why_github.png)


### GitHub 계정 가입


우선 **[GitHub 페이지](github.com/)**에 접속합니다. 그 다음 사용자 이름, 이메일, 비밀번호를 입력합니다. 


![깃허브 캡쳐_1](\assets\images\githubcapture_1.PNG)


다음으로 나오는 Free와 Pro유형 중, Free 플랜을 선택하고 "Finish sign up" 버튼을 클릭합니다.  

![깃허브 캡쳐_2](\assets\images\githubcapture_2.PNG)


가입시 등록한 이메일로 인증 메일이 도착하면 사용자 인증을 하면, GitHub 계정 등록이 완료됩니다.




### GitHub 사용법

가입이 끝났으면 본격적으로 GitHub를 사용해볼 차례인데요. repository 생성 및 삭제, branch 생성 및 삭제, file upload와 commit 메시지 작성 과정을 진행해보겠습니다.


#### GitHub repository 만들기

먼저 저장소인 repository를 만들어보겠습니다. 좌측 상단의 "New"를 클릭합니다.

![깃허브 레포지토리_1](\assets\images\github_repo1.png)

그 다음, Repository Name을 입력하고 "Initailize this repository with a README"를 체크하고 Create repository를 클릭하면 새로운 repository가 생성됩니다!


![깃허브 레포지토리_2](\assets\images\github_repo2.png)



#### GitHub Desktop 설치

다음으로 로컬 저장소에서 작업하기 위해 GitHub Desktop을 설치합니다.

우선  **[GitHub Desktop 설치 URL](desktop.github.com/)** 에 접속합니다. 그 다음 사용자 이름, 이메일, 비밀번호를 입력합니다. 운영체제를 자동으로 인식하여 설치되기 때문에 설치과정을 그대로 따라가면 됩니다!


#### GitHub Desktop Clone Repository

이전에 repository를 만들었기 때문에 로컬 저장소에서 기존의 repository를 가져와야 합니다. File > Clone repository 를 클릭해 방금 만들었던 repository를 clone 합니다. 


"Create a new repository"를 클릭하고 "Name" "Local path"을 설정합니다. "Initialize this repository with a README" 체크박스의 경우 선택사항이고 "Git ignore" "License"는 추후 수정 가능하기에 모두 None으로 설정합니다. 
최종적으로 "Create repository"를 클릭하면 새로운 로컬 저장소가 생성됩니다.

![깃허브 Repository 생성_1](\assets\images\github_desktop_0.png)




Repository를 생성하며 지정한 경로("Local path")로 가보면 아래와 같이 'git_test' 라는 저장소를 확인할 수 있습니다. 


![깃허브 Repository 생성_2](\assets\images\github_repository_2.png)



#### Repository 소스 코드 등록



이제 Git을 사용할 모든 준비가 끝났습니다! 간단하게 'hello_world.html'이라는 코드를 해당 로컬 저장소에 붙여넣기 해줍니다.


![깃허브 코드 등록_2](\assets\images\github_desktop_code_2.PNG)


코드가 GitHub Desktop에서 확인되면 좌측 하단에 보이는 "Commit to master"로 저장소에 'Commit 메시지'를 등록합니다.


![깃허브 코드 등록_3](\assets\images\github_desktop_code_3.PNG)


"History"를 확인해보면, 방금 'Commit'한 정보가 나타납니다. 저는 "Create hello_world.html" 이라는 이름으로 commit을 했네요. 


![깃허브 코드 등록_3-1](\assets\images\github_desktop_code_3-1.PNG)


#### GithHub 원격 저장소 업로드

원격 저장소(GitHub)에 로컬 저장소에서 작업한 사항을 업로드 하기 위해서는 계정 정보를 입력해야 합니다.
GitHub DeskTop의 왼쪽 상단 탭의 File > Options > Accounts에 계정을 로그인합니다. 계정은 처음에 생성했던 GitHub 계정을 입력하시면 됩니다.


![깃허브 코드 등록_4](\assets\images\github_desktop_code_4.PNG)


그리고 File > Options > Git에도 가입시 설정한 Name과 이메일을 입력합니다. 제대로 입력하지 않으면 'GitHub에 commit 메시지'
가 제대로 입력되지 않는 문제가 발생합니다!


![깃허브 코드 등록_5](\assets\images\github_desktop_code_5.PNG)


GitHub DeskTop 상단의 "Publish repository"를 선택하고 GitHub Account(사용자) 정보를 입력합니다. 
GitHub 홈페이지로 이동하면, 로컬 저장소에서 작업한 내용이 잘 업로드 되었음을 확인할 수 있습니다!


![깃허브 원격저장소 확인_1](\assets\images\github_check.PNG)




