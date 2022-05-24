---
layout: post
title:  프로젝트를 Git으로 관리하는 법
date:   2022-05-24 12:38:35 +0300
image:  '/images/JavaScript.jpg'
tags:   [GitHub]
---
<br/>

## 프로젝트를 Git으로 관리하는 법<br/>
*본 포스팅은 윈도우 기준 cmd를 통한 GitHub 업로드방법을 다룹니다.<br/>

___

### 1. Eempty Repository생성<br/>
(1) Visual Studio에서 Ctrl + ` 클릭<br/>
(2) 작업중인 폴더가 Git의 관리 하에 들어가도록 함<br/>
  ```
  git init
  git config --global user.name "내 이름" 입력
  git config --global user.email "메일주소" 입력
  ```
(3) 숨긴파일 보기를 통해 프로젝트 폴더 내 .git 폴더가 생긴 것을 확인<br/>


### 2. 현재시점 저장<br/>
(1) 타임캡슐에 담기지 않은 파일목록 확인<br/>
  ```git status```
(2) 파일목록을 타임캡슐에 포함<br/>
  ```git add -A```
(3) 타입캡슐을 Github에 포함<br/>
  ```git commit -m "설명"```


### 3. 프로젝트 공유를 위한 Github업로드<br/>
(1) Github에서 repository생성<br/>
(2) …or push an existing repository from the command line의 코드블럭을 복사하여 Visual Studio내 cmd에 입력<br/>


### 4. Github Desktop을 통한 프로젝트 관리<br/>
(1) 상단 툴바에 Add local repository클릭<br/>
(2) 변경사항 저장이 필요한 경우, branch에 대한 설명을 작성하여 commit to main<br/>


### 5. 이전 시점으로 돌아가기<br/>
(1) brach확인<br/>
  ```git log```
(2) 이전 시점으로 돌아가기(해당 시점이후 작업 삭제)<br/>
  ```git reset "log일련번호 6자리"```
(2) 이전 시점으로 돌아가기(해당 시점이후 작업 유지)<br/>
  ```git revert "log일련번호 6자리"```

___

*[Git Branch](https://goddaehee.tistory.com/274)