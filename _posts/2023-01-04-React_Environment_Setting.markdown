---
layout: post
title:  React/환경설정
date:   2023-01-04 12:38:35 +0300
image:  '/images/React.png'
tags:   [React]
---

# React 환경설정

## Contents <br/>
1. 설치해야 하는 툴 <br/>
2. 툴 설명 <br/>
3. 리액트 시작하기 <br/>

___

### 1. 설치해야 하는 툴
리액트 시작을 위해 필요한 기본 툴은 아래와 같다 <br/>
1. Visual Studio [download](https://code.visualstudio.com/)<br/>
2. Terminal (선택사항)<br/>
3. Node.js [download](https://nodejs.org/en/)<br/>
  - LTS(Long Term Support) 버전설치<br/>
  - 터미널에 node -v, npm -v 입력하여 정상설치 여부 확인<br/>
4. Git [download](https://git-scm.com/)<br/>
  - 터미널에 git --version 입력하여 정상설치 여부 확인<br/>
5. Yarn [download](https://yarnpkg.com/)<br/>
  - 터미널에 yarn -v 입력하여 정상설치 여부 확인<br/>

___

### 2. 툴 설명
1. Node.js <br/>
  - 정의 : 브라우저 밖에서 JS의 실행을 돕는 JS런타임 (node.js전에는 브라우저 환경에서만 JS를 사용할 수 있었으나, node.js이후 백엔드를 위해서도 JS를 사용할 수 있게 됨)
  - 장점 : npm자동설치 
2. Yarn <br/>
  - 정의 : JS패키지 매니저로 npm과 동일한 기능을 한다
  - 장점 : npm에 비해 속도가 빠르다(npm은 패키지를 순차적으로 설치하는 반면, yarn은 동시에 설치하도록 되어있다), 보안성이 높다(npm은 패키지에 포함된 다른 패키지 코드를 자동으로 실행해 시스템 상 취약성을 발생시킨다)

___

### 3. 리액트 시작하기
1. CRA(Create React App)을 통해 프로젝트 셋업
  - 정의 : CRA는 Webpack, Babel 등 리액트에서 사용되는 도구 및 설정을 포함하고 있다. 따라서 CRA를 사용하면 복잡한 설정없이 리액트 개발환경을 구성하고 이용할 수 있다
  - 사용법 : 
    1. 폴더생성 : 터미널에 mkdir foldername 입력
    2. 폴더접근 : cd foldername 입력
    3. 프로젝트생성 : yarn create react-app projectname 입력