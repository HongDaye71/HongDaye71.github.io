---
layout: post
title:  React Native Study04_Spotify Mobile App Clone
date:   2022-04-19 12:38:35 +0300
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
8. Home Screen<br/>
9. Navigation to Album Screen<br/>
10. Album Scrren - Song List<br/>

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
{% raw %}
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
{% endraw %}
```
</div>
</details>

___

### HomeScreen Setup <br/>
<img src="/images/Posting/ReactNative/Spotify/04.png" alt="Project" width="40%" height="40%">
- HomeScreen 생성 후 navigation_index.tsx의 Home Component변경

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
<summary>navigation_index.tex(수정된 부분)</summary>
<div markdown="1">

```javascript
{% raw %}
/*HomeScreen import*/
import HomeScreen from '../screens/HomeScreen';

      <BottomTab.Screen
        name="Home"
        component={HomeScreen}
        options={{
          tabBarIcon: ({ color }) => <Entypo name="home" size={30} style={{marginBottom:-3}} color={color} />,
        }}
      />
{% endraw %}
```
</div>
</details>

___

### Album Component<br/>
<img src="/images/Posting/ReactNative/Spotify/05.png" alt="Project" width="40%" height="40%">
- Album 폴더 생성
- Album_index.tsx : AlbumProps(id, imageUri, artistHeadline정보를 string 입력받음)를 사용하는 Album function생성
- Album_styles.tsx : Album function style지정
- screens_HomeScreen.tsx : Album function사용

<details>
<summary>Album_index.tsx</summary>
<div markdown="1">

```javascript
{% raw %}
import React from 'react';
import {View, Image, Text} from 'react-native';
import styles from './styles';

export type AlbumProps = {
    album : {
        id : string;
        imageUri : string;
        artistHeadline : string;
    }
}

const Album=(props:AlbumProps) => (
    <View style={styles.container}>
        <Image source={{uri:props.album.imageUri}} style={styles.images}/>
        <Text>{props.album.artistHeadline}</Text>
    </View>
)

export default Album;
{% endraw %}
```
</div>
</details>

<details>
<summary>Album_styles.tsx</summary>
<div markdown="1">

```javascript
import { StyleSheet } from "react-native";

const styles = StyleSheet.create({
    container:{
        width:200,
    },
    images:{
        width:'100%',
        height:200,
    },
    text:{
        color:'grey',
        marginTop:10,
    }
})

export default styles;
```
</div>
</details>


<details>
<summary>screens_HomeScreen.tsx</summary>
<div markdown="1">

```javascript
import * as React from 'react';
import {StyleSheet, Text, View} from 'react-native';

import Album from '../components/Album'

const album = {
  id:'1',
  imageUri : 'https://user-images.githubusercontent.com/81608287/163757044-767912f2-5cdf-4553-b029-b47c67d82ce8.jpg',
  artistHeadline :'Dennis Brown'
}

export default function HomeScreen() {
  return(
    <View style={styles.container}>
      <Album album={album}/>
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

<details>
<summary>type.tsx(추가한 부분)</summary>
<div markdown="1">

```javascript
export type Album = {
  id : string;
  imageUri : string;
  artistHeadline : string;
}
```
</div>
</details>

<details>
<summary>Album_index.tsx</summary>
<div markdown="1">

```javascript
{% raw %}
import React from 'react';
import {View, Image, Text} from 'react-native';
import styles from './styles';
import {Album} from '../../types';

/*기존 AlbumProps 변경 (id, imageUri, artistHeadline -> types.tsx의 Album import후 사용)*/
export type AlbumProps = {
    album : Album,
}

const Album=(props:AlbumProps) => (
    <View style={styles.container}>
        <Image source={{uri:props.album.imageUri}} style={styles.images}/>
        <Text style={styles.text}>{props.album.artistHeadline}</Text>
    </View>
)

export default Album;
{% endraw %}
```
</div>
</details>

<details>
<summary>AlbumCategory_index.tsx</summary>
<div markdown="1">

```javascript
import React from 'react';
import {FlatList, View, Text} from 'react-native'
import {Album} from '../../types';
import styles from './styles';
import AlbumComponent from '../Album';

export type AlbumCategoryProps = {
    title: string,
    albums: [Album],
}

const AlbumCategory = (props:AlbumCategoryProps) => (
    <View>
        <Text style={styles.title}>{props.title}</Text>
        <FlatList
            data ={props.albums}
            renderItem = {({ item }) => <AlbumComponent album={item}/>}
            keyExtractor={( item ) => item.id}
            horizontal        
        />
    </View>
)

export default AlbumCategory;
```
</div>
</details>

<details>
<summary>AlbumCategory_styles.tsx</summary>
<div markdown="1">

```javascript
import {StyleSheet} from 'react-native';

const styles = StyleSheet.create({

    container : {
        margin : 10,
    },

    title:{
        color : 'white',
        fontSize : 28,
        fontWeight : 'bold',
        margin:10
    }
})

export default styles;
```
</div>
</details>


<details>
<summary>screen_HomeScreen.tsx(수정된 부분)</summary>
<div markdown="1">

```javascript
import * as React from 'react';
import {StyleSheet, Text, View} from 'react-native';

import AlbumCategory from '../components/AlbumCategory'

const albumCategory = {
  id:'1',
  title:'Happy Vibes',
  albums:[
    {
      id: '1',
      imageUri: 'https://cache.boston.com/resize/bonzai-fba/Globe_Photo/2011/04/14/1302796985_4480/539w.jpg',
      artistHeadline: 'Taylor Swift, Kygo Objective C, Avicii'
    }, {
      id: '2',
      imageUri: 'https://cdn6.f-cdn.com/contestentries/1485199/27006121/5ca3e39ced7f1_thumb900.jpg',
      artistHeadline: 'Post Malone, Drake, Eminem'
    },
    {
      id: '3',
      imageUri: 'https://images-na.ssl-images-amazon.com/images/I/61F66QURFyL.jpg',
      artistHeadline: 'Journey, Escape, Avicii'
    },
    {
      id: '4',
      imageUri: 'https://i.pinimg.com/originals/a2/0d/37/a20d37791f8ad5cd54734cd3af559cc9.jpg',
      artistHeadline: 'Bob Marley, Cardi B, Stas Mihailov'
    },
  ]
};

export default function HomeScreen() {
  return(
    <View style={styles.container}>
      <AlbumCategory 
      title={albumCategory.title} 
      albums={albumCategory.albums}
      />
    </View>
  );
}

```
</div>
</details>

___

### Home Screen <br/>
<img src="/images/Posting/ReactNative/Spotify/07.png" alt="Project" width="40%" height="40%">
- 앨범정보를 HomeScreen.tsx에 저장하지 않고, albumbumCategories.ts 파일에 별도저장<br/>

<details>
<summary>albumbumCategories.ts</summary>
<div markdown="1">

```javascript
export default [{
    id: '1',
    title: 'Happy Vibes',
    albums: [
      {
        id: '1',
        imageUri: 'https://cache.boston.com/resize/bonzai-fba/Globe_Photo/2011/04/14/1302796985_4480/539w.jpg',
        artistsHeadline: 'Taylor Swift, Kygo Objective C, Avicii'
      }, {
        id: '2',
        imageUri: 'https://cdn6.f-cdn.com/contestentries/1485199/27006121/5ca3e39ced7f1_thumb900.jpg',
        artistsHeadline: 'Post Malone, Drake, Eminem'
      },
      {
        id: '3',
        imageUri: 'https://images-na.ssl-images-amazon.com/images/I/61F66QURFyL.jpg',
        artistsHeadline: 'Journey, Escape, Avicii'
      },
      {
        id: '4',
        imageUri: 'https://i.pinimg.com/originals/a2/0d/37/a20d37791f8ad5cd54734cd3af559cc9.jpg',
        artistsHeadline: 'Bob Marley, Cardi B, Stas Mihailov'
      },
    ]
  }, {
    id: '2',
    title: 'Popular Playlists',
    albums: [
      {
        id: '5',
        imageUri: 'https://user-images.githubusercontent.com/81608287/164179481-f14d8b74-ade8-4cc0-be99-642b0d04b745.jpg',
        artistsHeadline: 'Black Match'
      }, {
        id: '6',
        imageUri: 'https://user-images.githubusercontent.com/81608287/164178197-baa4ed0f-a0f1-486e-8681-1ff6ae17ecbe.png',
        artistsHeadline: 'Bruno Mars'
      },
      {
        id: '7',
        imageUri: 'https://user-images.githubusercontent.com/81608287/164178414-37069212-9d42-4d80-b53a-c0c57b9ec27e.jpg',
        artistsHeadline: 'Lauv'
      },
    ]
  },{
    id: '3',
    title: 'Shows to try',
    albums: [
      {
        id: '8',
        imageUri: 'https://user-images.githubusercontent.com/81608287/164178562-74b4c793-6ce0-4c94-a779-e3702e2a60a2.jpg',
        artistsHeadline: 'Betta Lemme'
      }, {
        id: '9',
        imageUri: 'https://user-images.githubusercontent.com/81608287/164178803-76329fd2-fc24-4892-a6bb-84f34a4b4ae2.jpg',
        artistsHeadline: 'Milk & Bone, Alex Lustig'
      },
      {
        id: '10',
        imageUri: 'https://user-images.githubusercontent.com/81608287/164179050-384577aa-adee-4429-9907-7bc20cd7de2e.jpg',
        artistsHeadline: 'The Greeting Committee'
      },
    ]
  }, {
    id: '4',
    title: 'Workout',
    albums: [
      {
        id: '11',
        imageUri: 'https://user-images.githubusercontent.com/81608287/164179218-9e3810a7-1ae0-4b29-9bb2-f484d7614a15.jpg',
        artistsHeadline: 'Peter Manos'
      }, {
        id: '12',
        imageUri: 'https://user-images.githubusercontent.com/81608287/164177887-f618f57b-be43-4d2d-a687-5b01fdb3acb4.jpg',
        artistsHeadline: 'Barrie'
      },
      {
        id: '13',
        imageUri: 'https://user-images.githubusercontent.com/81608287/164179319-eff98448-f098-42b0-80f2-e9bc17e531c4.jpg',
        artistsHeadline: 'William Bell'
      },
    ]
  },
  ]
```
</div>
</details>

<details>
<summary>HomeScreen.tsx</summary>
<div markdown="1">

```javascript
import * as React from 'react';
import {FlatList, StyleSheet, Text, View} from 'react-native';

import AlbumCategory from '../components/AlbumCategory'
import albumCategories from '../data/albumCategories';

export default function HomeScreen() {
  return(
    <View style={styles.container}>
      <FlatList 
        data={albumCategories}
        /*renderItem will be one Albumcategory*/
        renderItem={({item}) => (
          <AlbumCategory 
            title={item.title}
            albums={item.albums}
            keyExtractor={( item ) => item.id}
          />
          )}
      
      />
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

___

###  Navigation to Album Screen <br/>
<img src="/images/Posting/ReactNative/Spotify/08.png" alt="Project" width="40%" height="40%">
- AlbumScreen.tsx생성
- BottomTabNavigator.tsx / index.tsx : 초기 파일생성 시, default code가 튜토리얼과 상이하여 동일하게 변경
- BottomTabNavigator.tsx : TabOne Navigator()에 AlbumScreen추가
- Album_index.tsx : Home화면에서 앨범 클릭 시 Album Screen페이지로 이동하도록 수정

<details>
<summary>BottomTabNavigator.tsx</summary>
<div markdown="1">

```javascript

```
</div>
</details>

<details>
<summary>index.tsx</summary>
<div markdown="1">

```javascript

```
</div>
</details>

<details>
<summary>Album Screen</summary>
<div markdown="1">

```javascript

```
</div>
</details>

<details>
<summary>Album_index.tsx</summary>
<div markdown="1">

```javascript

```
</div>
</details>

___

###  Album Scrren - Song List <br/>
<img src="/images/Posting/ReactNative/Spotify/09.png" alt="Project" width="40%" height="40%">

<details>
<summary>type.tsx</summary>
<div markdown="1">

```javascript

```
</div>
</details>

___

###  ___ <br/>
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



