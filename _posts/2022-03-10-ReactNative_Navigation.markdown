---
layout: post
title:  React Native Study04_Navigation
date:   2022-03-10 15:01:35 +0300
image:  '/images/ReactNative_Navigation.png'
tags:  [React Native]
---

# React Native_Navigation<br/>

## Contents<br/>
1. Navigation의 종류와 구조<br/>
2. Navigation 환경세팅<br/>

React Native School 유투브 채널의 React Navigation 강좌 내용을 정리하는 포스팅입니다. (영상에 언급되지 않은 내용이 포함되어 있음)

* [Tutorial Video](https://www.youtube.com/watch?v=nQVCkqvU1uE)

___

### Navigation의 종류와 구조 <br/>
**React Navigation Library에서 지원하는 Navigation종류**<br/>
  1) Stack Navigation <br/>
  2) Tab Navigation<br/>
  3) Drawer Navigation<br/>

**Navigation Component**<br/>
<img src="/images/Posting/ReactNative/Navigation/01.png" alt="Project" width="40%" height="40%">

  1) Screen Component : <br/>
  화면으로 사용되는 컴포턴트로 name, component속성을 지정해 주어야 함<br/>
    name : 화면이름<br/>
    component : 화면으로 사용될 컴포넌트<br/>
    ex.) name : Album / component : AlbumScreen => Navigation 외 Script에서 A Component클릭 시 Album으로 이동하겠다는 코드작성 = A Component클릭 시 AlbumScreen 페이지로 이동<br/>

  2) Navigator Component : <br/>
  화면을 관리하는 중간 관리자 역할로, 내비게이션을 구성하며 여러개의 Screen Component를 자식 Component로 갖음<br/>
  
  3) Navigation Container Component<br/>
  Navigation의 계층 구조와 상태를 관리하는 Container역할을 하며, Navigation의 모든 구조를 감사는 최상위 Component<br/>

___

### Navigation 환경세팅<br/>

**React Navigation Library설치**<br/>
```javascript
npm install --save @react-navigation/native
```

