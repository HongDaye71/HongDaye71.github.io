---
layout: post
title:  React Native Study03_Spotify App Clone
date:   2022-04-18 15:01:35 +0300
image:  '/images/ReactNative_SpotifyProject.png'
tags:  [React Native, App Development]
---

# React Native_Spotify Mobile App Clone

## Contents <br/>
1. Initialise the expo project<br/>
2. Bottom Tab Navigator<br/>
3. Home Screen Setup<br/>
4. Album Component<br/>
5. Album Category Component<br/>
6. Data :<br/>
    - Album Categories : Array<br/>
7. Album Scrren<br/>
___

* notJust․dev 유투브 채널의 React Native Tutorial 영상을 바탕으로 공부한 내용을 정리하는 포스팅입니다.<br/>
* [notJust․dev 유투브채널 바로가기](https://www.youtube.com/channel/UCYSa_YLoJokZAwHhlwJntIA) <br/>
* [Tutorial Video](https://www.youtube.com/watch?v=Ho41KNKvoBc&list=PLY3ncAV1dSVBejIDGrcbNRs148uHowYfx)<br/>
* *작업단계 별 부연설명은 Source Code내 주석으로 작성*
* Techinologies : <br/>
    (1)Front End : React Native, Expo, TypeScript, React Navigation<br/>
    (2)Backend End : AWS Amplify, AWS AppSync, GraphQL<br/>

___

## 결과물
<p><iframe src="" frameborder="0" allowfullscreen></iframe></p>
[Source Code Download]()

___ 

### Initialise the expo project<br/>
<img src="/images/Posting/ReactNative/Spotify/01.png" alt="Project" width="40%" height="40%">
<img src="/images/Posting/ReactNative/Spotify/02.png" alt="Project" width="40%" height="40%">
- tabs(TypeScript) template선택하여 프로젝트 생성<br/>
    (1) blank : 처음부터 expo를 시작하고 싶을 때 선택<br/>
    (2) blank(TypeScript) : TypeScript 사용 시 선택<br/>
    (3) tabs(TypeScript) : NavigationTab과 같은 Tab사용 시 선택<br/>
[Click To View React Navigation Posting](https://hongdaye71.github.io/blog/reactnative-navigation-copy)

___

### Bottom Tab Navigator <br/>
<img src="/images/Posting/ReactNative/Spotify/03.png" alt="Project" width="40%" height="40%">
- types.tsx : RootTabParamList수정 (TabOne/TabTwo -> Home/Search/Library/Premium)<br/>
- index.tsx : BottomTabNavigator function수정 (아이콘 및 텍스트 수정) 

[Icoone download](https://icons.expo.fyi/)

<details>
<summary>type.tsx</summary>
<div markdown="1">

```javascript
import { BottomTabScreenProps } from '@react-navigation/bottom-tabs';
import { CompositeScreenProps, NavigatorScreenParams } from '@react-navigation/native';
import { NativeStackScreenProps } from '@react-navigation/native-stack';

declare global {
  namespace ReactNavigation {
    interface RootParamList extends RootStackParamList {}
  }
}

export type RootStackParamList = {
  Root: NavigatorScreenParams<RootTabParamList> | undefined;
  Modal: undefined;
  NotFound: undefined;
};

export type RootStackScreenProps<Screen extends keyof RootStackParamList> = NativeStackScreenProps<
  RootStackParamList,
  Screen
>;

export type RootTabParamList = {
  Home: undefined;
  Search: undefined;
  Library: undefined;
  Premium: undefined;
};

export type RootTabScreenProps<Screen extends keyof RootTabParamList> = CompositeScreenProps<
  BottomTabScreenProps<RootTabParamList, Screen>,
  NativeStackScreenProps<RootStackParamList>
>;

```
</div>
</details>

<details>
<summary>navigation_index.tsx(수정된 부분)</summary>
<div markdown="1">

```javascript
/*Bottom Tab Navigator에서 사용할 아이콘 불러오기*/
import { 
  FontAwesome,
  Entypo, 
  EvilIcons, 
  MaterialIcons , 
  FontAwesome5 } 
  from '@expo/vector-icons';

/*화면상의 아이콘 및 텍스트 변경*/
const BottomTab = createBottomTabNavigator<RootTabParamList>();

function BottomTabNavigator() {
  const colorScheme = useColorScheme();

  return (
    <BottomTab.Navigator
      initialRouteName="Home"
      screenOptions={{
        tabBarActiveTintColor: Colors[colorScheme].tint,
      }}>
      <BottomTab.Screen
        name="Home"
        component={TabOneScreen}
        options={{
          tabBarIcon: ({ color }) => <Entypo name="home" size={30} style={{marginBottom:-3}} color={color} />,
        }}
      />
      <BottomTab.Screen
        name="Search"
        component={TabTwoScreen}
        options={{
          tabBarIcon: ({ color }) => <EvilIcons name="search" size={30} style={{marginBottom:-3}} color={color} />,
        }}
      />
      <BottomTab.Screen
        name="Library"
        component={TabTwoScreen}
        options={{
          tabBarIcon: ({ color }) => <MaterialIcons name="library-music" size={30} style={{marginBottom:-3}} color={color} />,
        }}
      />
      <BottomTab.Screen
        name="Premium"
        component={TabTwoScreen}
        options={{
          tabBarIcon: ({ color }) => <FontAwesome5 name="spotify" size={30} style={{marginBottom:-3}} color={color} />,
        }}
      />
    </BottomTab.Navigator>
  );
}
```
</div>
</details>

___

### HomeScreen Setup <br/>
<img src="/images/Posting/ReactNative/Spotify/04.png" alt="Project" width="40%" height="40%">
- HomeScreen 생성 후 index.tsx의 Home Component변경

<details>
<summary>HomeScreen.tsx</summary>
<div markdown="1">

```javascript
import { StyleSheet } from 'react-native';

import EditScreenInfo from '../components/EditScreenInfo';
import { Text, View } from '../components/Themed';
import { RootTabScreenProps } from '../types';

export default function TabOneScreen({ navigation }: RootTabScreenProps<'Home'>) {
  return (
    <View style={styles.container}>
      <Text style={styles.title}>Home</Text>
      <View style={styles.separator} lightColor="#eee" darkColor="rgba(255,255,255,0.1)" />
      <EditScreenInfo path="/screens/TabOneScreen.tsx" />
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    alignItems: 'center',
    justifyContent: 'center',
  },
  title: {
    fontSize: 20,
    fontWeight: 'bold',
  },
  separator: {
    marginVertical: 30,
    height: 1,
    width: '80%',
  },
});

```
</div>
</details>

<details>
<summary>index.tex(수정된 부분)</summary>
<div markdown="1">

```javascript
/*HomeScreen import*/
import HomeScreen from '../screens/HomeScreen';

      <BottomTab.Screen
        name="Home"
        component={HomeScreen}
        options={{
          tabBarIcon: ({ color }) => <Entypo name="home" size={30} style={{marginBottom:-3}} color={color} />,
        }}
      />
```
</div>
</details>

___

### ---- <br/>
<img src="/images/Posting/ReactNative/Spotify/04.png" alt="Project" width="40%" height="40%">

<details>
<summary>type.tsx</summary>
<div markdown="1">

```javascript

```
</div>
</details>

___

* App Clone목표 :
* 느낀점 : 
* 앞으로의 계획 : 
