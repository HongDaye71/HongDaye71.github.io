---
layout: post
title:  React Native Study03_Spotify App Clone
date:   2022-03-02 15:01:35 +0300
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
- tabs(TypeScript) template선택하여 프로젝트 생성<br/>
    (1) blank : 처음부터 expo를 시작하고 싶을 때 선택<br/>
    (2) blank(TypeScript) : TypeScript 사용 시 선택<br/>
    (3) tabs(TypeScript) : NavigationTab과 같은 Tab사용 시 선택<br/>

___

### Bottom Tab Navigator <br/>
<img src="/images/Posting/ReactNative/Spotify/02.png" alt="Project" width="40%" height="40%">
- Backdground Color : app.json script의 userInterfaceStyle변수변경<br/>
- navigation_index.tsx에서 Home, Search, Your Library, Premium 버튼생성<br/>
- screens folder에서 각 버튼 페이지 생성
- types.tsx의 RootTabParamList에 각 버튼명 추가


<details>
<summary>navigation_index.tsx</summary>
<div markdown="1">

```javascript
import { Entypo, EvilIcons, MaterialCommunityIcons, FontAwesome5, FontAwesome } from '@expo/vector-icons';
/*Bottom Tab Icon Site Import*/

import { createBottomTabNavigator } from '@react-navigation/bottom-tabs';
import { NavigationContainer, DefaultTheme, DarkTheme } from '@react-navigation/native';
import { createNativeStackNavigator } from '@react-navigation/native-stack';
import * as React from 'react';
import { ColorSchemeName, Pressable } from 'react-native';

import Colors from '../constants/Colors';
import useColorScheme from '../hooks/useColorScheme';
import ModalScreen from '../screens/ModalScreen';
import NotFoundScreen from '../screens/NotFoundScreen';

import HomeScreen from '../screens/HomeScreen';
import SearchScreen from '../screens/SearchScreen';
import LibraryScreen from '../screens/LibraryScreen';
import PremiumScreen from '../screens/PremiumScreen';
/*Bottom Tab 클릭시, 나타날 페이지 import*/
import { RootStackParamList, RootTabParamList, RootTabScreenProps } from '../types';
import LinkingConfiguration from './LinkingConfiguration';

export default function Navigation({ colorScheme }: { colorScheme: ColorSchemeName }) {
  return (
    <NavigationContainer
      linking={LinkingConfiguration}
      theme={colorScheme === 'dark' ? DarkTheme : DefaultTheme}>
      <RootNavigator />
    </NavigationContainer>
  );
}

const Stack = createNativeStackNavigator<RootStackParamList>();

function RootNavigator() {
  return (
    <Stack.Navigator>
      <Stack.Screen name="Root" component={BottomTabNavigator} options={{ headerShown: false }} />
      <Stack.Screen name="NotFound" component={NotFoundScreen} options={{ title: 'Oops!' }} />
      <Stack.Group screenOptions={{ presentation: 'modal' }}>
        <Stack.Screen name="Modal" component={ModalScreen} />
      </Stack.Group>
    </Stack.Navigator>
  );
}

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
        component={HomeScreen} /*Home Button 클릭 시 나타나는 페이지*/
        options={({ navigation }: RootTabScreenProps<'Home'>) => ({
          title: 'Home',
          tabBarIcon: ({ color }) => <Entypo name="home" size={30} style={{marginBottom:-3}} color={color} />,
          headerRight: () => (
            <Pressable
              onPress={() => navigation.navigate('Modal')}
              style={({ pressed }) => ({
                opacity: pressed ? 0.5 : 1,
              })}>
              <FontAwesome
                name="info-circle"
                size={25}
                color={Colors[colorScheme].text}
                style={{ marginRight: 15 }}
              />
            </Pressable>
          ),
        })}
      />
      <BottomTab.Screen
        name="Search"
        component={SearchScreen} /*Search Button 클릭 시 나타나는 페이지*/
        options={{
          title: 'Search',
          tabBarIcon: ({ color }) => <EvilIcons name="search" size={30} style={{marginBottom:-3}} color={color} />,
        }}
      />
      <BottomTab.Screen
        name="Library"
        component={LibraryScreen} /*Library Button 클릭 시 나타나는 페이지*/
        options={{
          title: 'Library',
          tabBarIcon: ({ color }) => <MaterialCommunityIcons name="music-box-multiple" size={30} style={{marginBottom:-3}} color={color} />,
        }}
      />
      <BottomTab.Screen
        name="Premium"
        component={PremiumScreen} /*Library Button 클릭 시 나타나는 페이지*/
        options={{
          title: 'Premium',
          tabBarIcon: ({ color }) => <FontAwesome5 name="spotify" size={30} style={{marginBottom:-3}} color={color} />,
        }}
      />
    </BottomTab.Navigator>
  );
}

function TabBarIcon(props: {
  name: React.ComponentProps<typeof FontAwesome>['name'];
  color: string;
}) {
  return <FontAwesome size={30} style={{ marginBottom: -3 }} {...props} />;
}
```
</div>
</details>






