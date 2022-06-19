---
layout: post
title:  MobX-React 기초정리
date:   2022-05-24 12:38:35 +0300
image:  '/images/MobX.png'
tags:   [MobX]
---
<br/>

## MobX-React 기초정리<br/>

___

### Contents <br/>
1. MobX-Flux의 이해<br/>
2. MobX구조<br/>
3. 예제실습<br/>

* 나무소리 유투브 채널의 MobX 기초강의 내용을 바탕으로 정리하는 포스팅입니다. <br/>
* 영상에서 언급되지 않은 내용이 포함되어 있음<br/>
* [Tutorial Video](https://youtu.be/NwbZmhE2Blc)<br/>

___

### MobX-Flux의 이해<br/>
#### 1. MobX란? <br/>
MobX는 전역 상태 라이브러리로 모든 상태변화를 자동으로 추적하는 역할을 한다.<br/><br/>

#### 2. MobX를 사용하는 이유 <br/>
React를 구성하는 Component는 State를 이용해 변경 가능한 데이터를 관리할 수 있다. 하지만 다수의 컴포넌트가 각자의 상태를 관리할 경우 데이터 관리 및 제어가 어려우며 데이터 공유가 필요한 경우 제약이 발생한다. MobX는 공통의 데이터 관리영역인 Store를 통해 State를 관리하여 위와 같은 단점을 보완한다.<br/><br/>

#### 3. Flux Architecture <br/>
Flux는 데이터 흐름을 한 방향으로 유지하기 위해 설계된 App 디자인 패턴이다.<br/><br/>

#### 4. MVC와 Flux의 차이<br/>
MVC는 App을 Model,View,Controller로 분리하며 View와 Model사이에 양방향 데이터 이동이 가능하다. MVC는 자신의 역할에 집중할 수 있으며 단순하고 직관적이라는 장점이 있다. 하지만 프로젝트가 커질 경우 Model과 View의 전후관계를 따지기가 힘들어 데이터 관리가 어려워진다. 객체지향 프로그래밍에서 MVC사용 시 발생하는 문제를 해결하기 위해 Flux 디자인 패턴이 나오게 되었다.<br/><br/>

<img src="/images/Posting/MobX/MVC_Flux.png" alt="Project"><br/>

* Model: 로직과 관련된 모든 데이터를 포함<br/>
* View: 사용자에게 데이터를 표현하거나 유저와 상호작용을 처리<br/>
* Controller: 모델과 뷰 구성요소간의 인터페이스 (ex. 클릭이벤트 발생 시 컨트롤러를 통해 Model에 해당 데이터 반영)<br/>

___

### MobX구조<br/>
#### 1. MobX개요 <br/>
- MobX를 이용하면 Component의 State를 Store라는 별도의 영역에서 관리한다.<br/>
- MobX 적용을 위해서는 mobx.js와 mobx-react.js 라이브러리가 필요하다.<br/>
  * <span style='background-color:#fff5b1'>mobx:</span> Store관리를 위한 라이브러리로 observable, action등의 모듈로 구성되어 있음<br/>
  * <span style='background-color:#fff5b1'>mobx-react:</span> Store의 데이터를 React에 적용시키기 위한 라이브러리로 observer등의 모듈로 구성되어 있음<br/>

- MobX는 다수의 Store를 관리할 수 있다.<br/>
- MobX가 제공하는 대표적인 API는 observable, action, observer, computed, inject 이며 API사용은 데코레이터(@)를 이용하는 것이 일반적이다.<br/>
  * <span style='background-color:#fff5b1'>observable:</span> 추적 가능한 state정의<br/>
  * <span style='background-color:#fff5b1'>action:</span> state를 변경하는 메소드<br/>
  * <span style='background-color:#fff5b1'>observer:</span> observable을 통해 관리되는 state를 react component에 적용<br/>
  * <span style='background-color:#fff5b1'>computed:</span> state와 cahce로부터 새로운 결과를 반환<br/>
  * <span style='background-color:#fff5b1'>inject:</span> store를 props에 넣어 component에서 props를 통해 store에 접근할 수 있도록 함<br/>
  
- MobX 라이브러리는 TypeScript가 적용되어 있다.<br/>







#### MVC와 Flux의 차이<br/>

___

#### Etc. <br/>
Component: App을 이루는 최소한의 단위로 React에서는 Class 및 Function Component를 사용한다. <br/>
