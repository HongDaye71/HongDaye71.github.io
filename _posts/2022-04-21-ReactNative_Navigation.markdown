---
layout: post
title:  React Native Study03_Navigation
date:   2022-04-21 15:01:35 +0300
image:  '/images/ReactNative_Navigation.png'
tags:  [React Native]
---

# React Native Navigation<br/>

### Contents<br/>
1. Getting started<br/>
2. Hello React Navigation<br/>
3. <br/>
4. <br/>
5. <br/>

* React Navigation 공식문서를 바탕으로 공부한 내용을 정리한 포스팅 입니다.<br/>
* [React Natvigation Docs](https://reactnavigation.org/docs/getting-started)<br/>

___

### :fire: Getting started<br/>
React Native Navigation은 React Native와 함께 사용되는 하나의 모듈이다. 웹이나 앱에서 스크린 이동을 구현하기 위해 사용된다.<br/>

**Minimum requirements**<br/>
react-native = 0.63.0<br/>
expo = 41 (사용하는 경우)<br/>
typescript = 4.1.0 (사용하는 경우)<br/>

**Installation**
React Native project 내 패키지 설치

```javascript
npm install @react-navigation/native
expo install react-native-screens react-native-safe-area-context //install versions of library
npm install react-native-screens react-native-safe-area-context
```

**Wrapping your app in NavigationContainer**
전체 앱을 NavigationContainer로 Wrapping 

```javascript
/*index.js 혹은 App.js와 같은 entry file Wrapping*/

import * as React from 'react';
import { NavigationContainer } from '@react-navigation/native';

export default function App() {
  return (
    <NavigationContainer>{/* Rest of your app code */}</NavigationContainer>
  );
}
```

___

### :fire: Hello React Navigation<br/>

웹 브라우저 : <a>태그를 통해 스크린 이동구현 (ex. When the user presses the back button, the browser pops the item from the top of the history stack)

