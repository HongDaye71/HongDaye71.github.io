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

___

### Navigation의 종류와 구조 <br/>
React Navigation Library에서 지원하는 Navigation종류<br/>
  1) Stack Navigation <br/>
  2) Tab Navigation<br/>
  3) Drawer Navigation<br/>

Navigation Component<br/>
  1) Screen Component : <br/>
  화면으로 사용되는 컴포턴트로 name, component속성을 지정해 주어야 함<br/>
    name : 화면이름<br/>
    component : 화면으로 사용될 컴포넌트<br/>
    ex.) name : Album / component : AlbumScreen => Navigation 외 Script에서 A Component클릭 시 Album으로 이동하겠다는 코드작성 = A Component클릭 시 AlbumScreen 페이지로 이동<br/>
  2) Navigator Component
  3) Navigation Container Component