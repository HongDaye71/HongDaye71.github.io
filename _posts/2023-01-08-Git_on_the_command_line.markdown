---
layout: post
title:  CLI로 Git관리하기
date:   2023-01-08 12:38:35 +0300
image:  '/images/Posting/React/TodoList.png'
tags:   [Git]
---

# CLI로 Git관리하기

## Description <br/>
1. CLI 명령어 <br/>
2. Git 명령어 <br/>
3. 기타 <br/>

___

### CLI 명령어
#### 1. 폴더이동
```
pwd : 현재 폴더 위치 (cmd에서는 작동하지 않음)
ls : 현재 위치의 모든 파일 표시 (cmd에서는 작동하지 않음)
dir : 현재 위치의 모든 파일 표시 
cd 폴더경로 : 폴더이동
cd.. : 이전 폴더로 이동
```

#### 2. 파일생성 및 삭제
```
mkdir 폴더명 : 폴더 생성
rm -r 폴더명 : 폴더 삭제
cp -r 폴더명 폴더위치 : 폴더 복사
mv 폴더명 변경폴더명 : 폴더명 변경

touch 파일명 : 파일 생성
rm 파일명 : 파일 삭제
cp 파일명 파일위치 : 파일 복사
mv 파일명 변경파일명 : 파일명 변경
```

### Git 기본 명령어
#### Git 폴더 초기화 - init/pull
```
git init : 현재 폴더를 git에 관리하에 둠
git pull : 현재 폴더에 모든 파일을 git hub에 업데이트
```

#### Git 상태확인 - status/log
```
git status : 현재 상태 출력
git log : commit로그 등 출력
```

#### Github업로드 - add/commit/push
```
//1. 업로드할 파일 추가
git add 파일명
git add * 

//2. 커밋
git commit -m "comment"

//3. 업로드
git push 저장소명 브랜치명
git push origin main

//최신 commit 코멘트 수정
git commit --amend

//히스토리 유지
git revert 원복할 commitID
```

* init된 폴더 내부로 이동해서 명령어를 실행해야 됨 <br/> 
* 업로드 시에 대부분의 기본 저장소와 브랜치는 origin/main임 <br/>
* 폴더 열려있으면 오류남 <br/>
* Git업로드는 아래의 과정으로 이루어짐 <br/>
    1. add : 다음 변경을 기록할 때 까지 변경분을 모아놓기 위해 사용<br/>
    2. commit : 변경된 사항을 로컬 저장소에 기록 (ex. 내 컴퓨터)<br/>
    3. upload : 변경된 사항을 원격 저장소에 기록 (ex. 깃허브)<br/>

#### Branch 확인,생성,이동
```
//저장소 확인
git remote

// 브랜치
git branch 모든 브랜치를 확인하며 현재 브랜치는 색이 다르게 출력되어 확인할 수 있음
git branch 브랜치명 : 새로운 브랜치 생성
git checkout 브랜치명 : 브랜치 이동
git merge 합쳐질브랜치명 : 명령어를 실행하는 브랜치에 합쳐질 브랜치가 합쳐짐
```

### 기타
* CLI(Command Line Interface) : GUI와 반대되는 개념으로 문자를 통해 컴퓨터와 상호작용한다.
* CMD(Command Prompt) : 명령 프롬프트로 문자를 통해 상호작용하는 CLI를 기반으로 한다
* Bash : Brain Fox가 개발한 CLI로써 오픈소스이다. 리눅스와 맥에서는 Bash가 기본 Shell이다. 터미널을 사용해 Bash에 접근할 수 있다
* 맥 주소 : 고유한 주소를 부여해 통신할 수 있도록 만든 일종의 하드웨어 주소다. CMD에서 ipconfig/all을 입력해 물리적 주소를 확인하면 된다.
* 터미널 : 컴퓨터 시스템에서 데이터를 입출력 하는 인터페이스이다. 터미널은 인터페이스일 뿐이고 명령을 처리하고 결과를 출력하는 것은 쉘이 담당한다.
    * CMD는 윈도우에서 명령어를 입력하기 위한 CLI이고, 터미널은 유닉스 운영체제에서 명령어를 입력하기 위한 CLI이다.
