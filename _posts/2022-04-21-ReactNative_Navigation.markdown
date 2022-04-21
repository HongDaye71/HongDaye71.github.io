---
layout: post
title:  React Native Study03_Navigation
date:   2022-04-21 15:01:35 +0300
image:  '/images/ReactNative_Navigation.png'
tags:  [React Native]
---

# React Native Navigation<br/>

### Contents<br/>
1. 네비게이션의 종류와 구조<br/>
2. <br/>
3. <br/>
4. <br/>
5. <br/>

___

### 네비게이션의 종류와 구조<br/>
**종류**<br/>
1. Stack Navigation : 스택 최상위에 위치한 스크린으로 이동<br/>
2. Tab Navigation : 하단 혹은 상단에 위치한 탭바를 통해 스크린 이동<br/>
3. Drawer Navigation : draw gesture를 통해 스크린 이동<br/>

[Navigators_Docs](https://reactnavigation.org/docs/stack-navigator)<br/>

**구조**<br/>
1. Navigation Container : 네비게이션의 모든 구조를 감싸는 최상위 컴포넌트<br/>
2. Navigator : 화면을 관리하는 중간 관리자 역할로, 여러개의 Screen컴포넌트를 자식으로 가짐<br/>
3. Screen : 화면으로 사용되는 컴포넌트로 name(화면이름), component(화면으로 사용 될 컴포넌트)속성을 지정해주어야 함<br/>


___

참고자료 : 
1. [React Native Navigation](https://wix.github.io/react-native-navigation/docs/before-you-start)
2. [[react-native] Stack Navigation - Devlog, Boldly](https://eunbin00.tistory.com/41)


