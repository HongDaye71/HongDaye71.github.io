---
layout: post
title:  React Native Study04_Spotify Mobile App Clone
date:   2022-02-13 15:01:35 +0300
image:  '/images/ReactNative_SpotifyProject.png'
tags:  [React Native]
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
- navigation_index.tsx : BottomTabNavigator function수정 (아이콘 및 텍스트 수정) 

[Icon download](https://icons.expo.fyi/)

___

### HomeScreen Setup <br/>
<img src="/images/Posting/ReactNative/Spotify/04.png" alt="Project" width="40%" height="40%">
- HomeScreen 생성 후 navigation_index.tsx의 Home Component변경

___

### Album Component<br/>
<img src="/images/Posting/ReactNative/Spotify/05.png" alt="Project" width="40%" height="40%">
- Album 폴더 생성
- Album_index.tsx : AlbumProps(id, imageUri, artistHeadline정보를 string 입력받음)를 사용하는 Album function생성
- Album_styles.tsx : Album function style지정
- screens_HomeScreen.tsx : Album function사용

___

### Album Category Component <br/>
<img src="/images/Posting/ReactNative/Spotify/06.png" alt="Project" width="40%" height="40%">
- AlbumProps를 types.tsx에 입력하여 타 스크립트에서 불러와 사용할 수 있도록 함<br/>
- 기존 AlbumProps 변경 (id, imageUri, artistHeadline -> types.tsx의 Album import후 사용)<br/>
- screens_HomeScreen.tsx : Album -> AlbumCategory변경 (Album : 단일앨범 / AlbumCategory : 다수앨범 포함 카테고리 )<br/>

* FlatList : 많은 양의 리스트 아이템을 보여주고자 할 때 쓰이는 Component이다. Scroll View와 유사한 기능을 하나 동작 방식에 차이가 있다.<br/>
  (1) ScrollView : 데이터가 화면에 보이지 않을 때 사용자가 Swipe를 통해 가려진 데이터를 볼 수 있도록 한다(출력해야 하는 데이터가 고정적이고 많지 않을 때 사용)<br/>
  (2) FlatList : 모든 데이터를 한 번에 렌더링 하지 않고, 보여지는 부분 혹은 수동으로 설정한 양 만큼의 데이터만을 렌더링 한다. 사용자가 Swipe를 할 때 자동으로 다시 렌더링 한다. (데이터의 길이가 가변적이고 양을 예측할 수 없는 경우에 사용)<br/>

  (3) FlaList Props :<br/>
  - horizontal(boolean) : 리스트를 가로로 보여지게 하는 속성(default:false)<br/>
  - keyExtractor : item에 고유의 키를 주는 속성 (ex. keyExtractor={( item ) => item.id} 을 통해 개별 앨범정보에 키 부여)<br/>
  - data : FlatList의 소스를 담는 공간<br/>
  - renderItem : data로 받은 소스의 item들을 통해 render를 시켜주는 콜백함수<br/>

___

* App Clone목표 :
* 느낀점 : 
* 앞으로의 계획 : 


