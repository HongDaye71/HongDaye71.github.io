---
layout: post
title:  React Native Study04_Navigation
date:   2022-03-10 15:01:35 +0300
image:  '/images/ReactNative_SpotifyProject.png'
tags:  [React Native]
---

# React Native_Navigation<br/>

## Contents<br/>
1. Navigation의 종류와 구조<br/>
2. Navigation 환경세팅<br/>
3. Stack Navigator<br/>

The Net Ninja 유투브 채널의 React Native Tutorial 강좌의 내용을 바탕으로 정리하는 포스팅입니다. 
- 영상에 언급되지 않은 내용이 포함되어 있음
- 본 포스팅은 React Navigation Version 6.x를 기준으로 함

* [Tutorial Video](https://www.youtube.com/watch?v=cS4PgI3zBzY)

___

### Navigation의 종류와 구조 <br/>
**React Navigation Library에서 지원하는 Navigation종류**<br/>
  1) Stack Navigation : 일반적인 스크린 이동 <br/>
  2) Tab Navigation : 탭으로 스크린 이동<br/>
  3) Drawer Navigation : 드로어로 스크린 이동<br/>

**Navigation Component**<br/>
<img src="/images/Posting/ReactNative/Navigation/01.png" alt="Project" width="40%" height="40%">

  1) Screen Component : <br/>
  화면으로 사용되는 컴포턴트로 name, component속성을 지정해 주어야 함<br/>
    name : 화면이름<br/>
    component : 화면으로 사용될 컴포넌트<br/>

  2) Navigator Component : <br/>
  화면을 관리하는 중간 관리자 역할로, 내비게이션을 구성하며 여러개의 Screen Component를 자식 Component로 갖음<br/>
  
  3) Navigation Container Component<br/>
  Navigation의 계층 구조와 상태를 관리하는 Container역할을 하며, Navigation의 모든 구조를 감사는 최상위 Component<br/>

___

### Navigation 환경세팅<br/>

**Installation**<br/>
1) React Native Project에 Navigation에 필요한 패키지 설치<br/>
* Project Template : blank

```javascript
npm install --save @react-navigation/native //react navigation libra
npm install @react-navigation/stack //stack navigation library설치
npm install @react-navigation/drawer //drawer navigation library설치
npm install @react-navigation/bottom-tabs //bottom-tabs navigation library설치

expo install react-native-screens react-native-safe-area-context //dependencies 추가설치(호환되는 라이브러리들의 버전이 설치됨)

```
[React Navigation Docs](https://reactnavigation.org/docs/getting-started)

___

### Stack Navigator<br/>




