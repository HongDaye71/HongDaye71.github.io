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
1. react-native = 0.63.0<br/>
2. expo = 41 (사용하는 경우)<br/>
3. typescript = 4.1.0 (사용하는 경우)<br/>

**Installation**<br/>
React Native project 내 패키지 설치<br/>
```javascript
npm install @react-navigation/native
expo install react-native-screens react-native-safe-area-context //install versions of library
npm install react-native-screens react-native-safe-area-context
```

**<br/>Wrapping your app in NavigationContainer**<br/>
전체 앱을 NavigationContainer로 Wrapping <br/>

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

Web browser : a 태그를 통해 스크린 이동구현 (ex. When the user presses the back button, the browser pops the item from the top of the history stack)<br/>

React Native : Stack Navigator를 통해 Navigation History관리 및 스크린 이동구현  
  * 한 개의 Stack Navigator만을 사용할 경우
    - Web browser와의 공통점 : 개념적으로 Web browser와 동일하게 스크린 이동구현<br/>
    - Web browser와의 차이점 : Animation 혹은 gesture를 통해 스크린 이동구현 가능<br/>


**Installing the native stack navigator**<br/>
React Native project 내 설치<br/>
```javascript
npm install @react-navigation/native-stack
```


**<br/>Creating a native stack navigator<br/>**
<img src="/images/Posting/ReactNative/Navigation/01.png" alt="Project" width="40%" height="40%">
createNativeStackNavigator : Screen, Navigator properties를 포함하는 function<br/>

<details>
<summary>App.js</summary>
<div markdown="1">

```javascript
{ % raw % }
import { StatusBar } from 'expo-status-bar';
import { StyleSheet, Text, View } from 'react-native';
import { NavigationContainer } from '@react-navigation/native'
import { createNativeStackNavigator } from '@react-navigation/native-stack';

function HomeScreen() {
  return (
    <View style={{ flex: 1, alignItem: 'center', justifyContent: 'center'}}>
      {/*flex: 비율을 통해 크기설정(ex. 1:전체화면에서 1의 비율차지 / 1:1 전체 화면에서 반반 만큼의 공간차지)*/}
      <Text>HomeScreen</Text>
    </View>
  );
}

const Stack = createNativeStackNavigator();
//const : 변수선언 키워드로 ES6이후, var/let/const가 사용됨

function App() {
  return (
    <NavigationContainer>
      {/*NavigationContainer is a component which manages our navigation tree and contains the navigation state. This component mush wrap all navigators structure*/}
      <Stack.Navigator>
        <Stack.Screen name = "Home" component={HomeScreen} />
      </Stack.Navigator>
    </NavigationContainer>
  );
}

export default App;
{ % endraw % }
```
</div>
</details>


**<br/>Configuring the navigator<br/>**
Stack이 두 개의 루트(Home, Details)를 갖도록 코드추가<br/>

<details>
<summary>App.js</summary>
<div markdown="1">

```javascript
{ % raw % }
import { StatusBar } from 'expo-status-bar';
import { StyleSheet, Text, View } from 'react-native';
import { NavigationContainer } from '@react-navigation/native'
import { createNativeStackNavigator } from '@react-navigation/native-stack';

function DetailScreen() {
  return(
    <View style={{flex: 1, alignItems: 'center', justifyContent: 'center'}}>
      <Text>Details Screen</Text>
    </View>
  );
}

function HomeScreen() {
  return (
    <View style={{ flex: 1, alignItem: 'center', justifyContent: 'center'}}>
      {/*flex: 비율을 통해 크기설정(ex. 1:전체화면에서 1의 비율차지 / 1:1 전체 화면에서 반반 만큼의 공간차지)*/}
      <Text>HomeScreen</Text>
    </View>
  );
}

const Stack = createNativeStackNavigator();
//const : 변수선언 키워드로 ES6이후, var/let/const가 사용됨

function App() {
  return (
    <NavigationContainer>
      {/*NavigationContainer is a component which manages our navigation tree and contains the navigation state. This component mush wrap all navigators structure*/}
      <Stack.Navigator>
        <Stack.Screen name = "Home" component={HomeScreen} />
        <Stack.Screen name = "Details" component={DetailScreen} />
      </Stack.Navigator>
    </NavigationContainer>
  );
}

export default App;
{ % endraw % }
```
</div>
</details>

___

### Appendix<br/>
Navigation 외 발생했던 문제들 :
1. Android emulator reload failed 
  오류 : warn No apps connected. Sending "reload" to all React Native apps failed
  원인 : 
    1. 기기연결 불안정
  해결 : 
    1. adb reverse tcp:8081 tcp:8081 (연결 재설정)