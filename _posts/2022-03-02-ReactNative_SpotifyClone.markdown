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
<summary>navigation_index.tsx (프로젝트 초기생성 후 수정된 부분)</summary>
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
```
</div>
</details>




<details>
<summary>screens_HomeScreen (Search, Library, Premium 유사)</summary>
<div markdown="1">

```javascript
import { StyleSheet, TouchableOpacity } from 'react-native';

import { Text, View } from '../components/Themed';
import { RootStackScreenProps } from '../types';

export default function NotFoundScreen({ navigation }: RootStackScreenProps<'NotFound'>) {
  return (
    <View style={styles.container}>
      <Text style={styles.title}>This screen doesn't exist.</Text>
      <TouchableOpacity onPress={() => navigation.replace('Root')} style={styles.link}>
        <Text style={styles.linkText}>Go to home screen!</Text>
      </TouchableOpacity>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    alignItems: 'center',
    justifyContent: 'center',
    padding: 20,
  },
  title: {
    fontSize: 20,
    fontWeight: 'bold',
  },
  link: {
    marginTop: 15,
    paddingVertical: 15,
  },
  linkText: {
    fontSize: 14,
    color: '#2e78b7',
  },
});
```
</div>
</details>


<details>
<summary>types.tsx</summary>
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
  /*TypeScript에 BottomTap추가*/
  Home: undefined;
  Search: undefined;
  Library: undefined;
  Premium:undefined;
};

export type RootTabScreenProps<Screen extends keyof RootTabParamList> = CompositeScreenProps<
  BottomTabScreenProps<RootTabParamList, Screen>,
  NativeStackScreenProps<RootStackParamList>
>;
```
</div>
</details>
___

### Home Screen Setup<br/>
<details>
<summary>screens_HomeScreen.tsx</summary>
<div markdown="1">

```javascript
import { StyleSheet, Text, View } from 'react-native';
import { RootTabScreenProps } from '../types';

export default function HomeScreen({ navigation }: RootTabScreenProps<'Home'>) {
  return (
    <View style={styles.container}>
      <Text style={{color:'white'}}>Hello</Text>
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

### Album Component<br/>
<img src="/images/Posting/ReactNative/TeslaProject/03.png" alt="Project" width="40%" height="40%">
- Album folder생성 후 index.tsx / style.ts script작성
- screens_HomeScreen.tsx에서 album내 component작성 및 Album import

<details>
<summary>Album_index.tsx</summary>
<div markdown="1">

```javascript
import React from 'react';
import {View, Image, Text} from 'react-native';
import styles from './styles';

export type AlbumProps = {
    album: {
        id:string;
        imageUri:string;
        artistsHeadline:string;
    }
}

const Album = (props:AlbumProps)=>(
    <View style={styles.container}>
        <Image source={{uri:props.album.imageUri}} style={styles.image}/>
        <Text style={styles.text}>{props.album.artistsHeadline}</Text>
    </View>
)

export default Album;
```

</div>
</details>

<details>
<summary>Album_syltes.ts</summary>
<div markdown="1">

```javascript
import { StyleSheet } from "react-native";

const styles = StyleSheet.create({
    container: {
        width:200,
    },
    
    image: {
        width:'100%',
        height:200,
    },

    text: {
        color:'grey',
        marginTop:10,
    }
})

export default styles;
```

</div>
</details>

</div>
</details>

<details>
<summary>screens_HomeScreen.ts</summary>
<div markdown="1">

```javascript
import React from 'react';
import { StyleSheet, Text, View } from 'react-native';
import Album from '../components/Album';

const album = {
  /*album내 component작성*/
  id: '1',
  imageUri:'https://user-images.githubusercontent.com/81608287/155875578-be0f8c69-b72e-45d7-a8de-8a7b144b2056.jpg',
  artistsHeadline:'Taylor Swift, Cardi Objective C, Avicii'
}

export default function HomeScreen() {
  return (
    <View style={styles.container}>
      <Album album={album}/>  {/*Album import*/}
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

### Album Category Component<br/>
<p><iframe src="https://www.youtube.com/embed/Noz3zuQMam8" frameborder="0" allowfullscreen></iframe></p>
- Album Category 폴더생성 후 index.tsd, styles.ts 작성 <br/>
- Album Component type(id,image, artistHeadline의 type을 string으로 지정하는 것)은 types.tsx에 작성하여 clone과 같이 사용 <br/>

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
  /*TypeScript에 BottomTap추가*/
  Home: undefined;
  Search: undefined;
  Library: undefined;
  Premium:undefined;
};

export type RootTabScreenProps<Screen extends keyof RootTabParamList> = CompositeScreenProps<
  BottomTabScreenProps<RootTabParamList, Screen>,
  NativeStackScreenProps<RootStackParamList>
>;

export type Album={ /*Album Component Type작성(Clone과 같이 사용될 수 있도록)*/
  id:string;
  imageUri:string;
  artistsHeadline:string;
}

```
</div>
</details>

<details>
<summary>Album Category_index.tsx</summary>
<div markdown="1">

```javascript
import React from 'react';
import {FlatList, Text, View} from 'react-native';
import {Album} from "../../types";
import AlbumComponent from '../Album';
import styles from "./styles";

export type AlbumCategoryProps = {
    title:string, 
    albums:[Album],
}

const AlbumCategory=(props:AlbumCategoryProps)=>(
    <View style={styles.container}>
        {/*Title of Category*/}
        <Text style={styles.title}>{props.title}</Text>

        {/*List of albums*/}
        <FlatList 
        /*많은 양의 리스트 아이템을 스크롤로 내리면서 보여주고자 할 때 사용하며 parameter로는 data, renderItem, keyExtractor가 있다*/
            data={props.albums}
            /*data : 만들고자 하는 리스트의 데이터*/
            renderItem={({ item }) => <AlbumComponent album={item} />}
            /*renderItem : data로 받은 데이터를 item에 각각 render*/
            keyExtractor={( item ) => item.id}
            /*keyExtractor : 각 요소 구별*/
            horizontal
            showsHorizontalScrollIndicator={false}
        />
    </View>
)

export default AlbumCategory;
```

</div>
</details>

<details>
<summary>Album Category_style.ts</summary>
<div markdown="1">

```javascript
import React from 'react';
import {FlatList, Text, View} from 'react-native';
import {Album} from "../../types";
import AlbumComponent from '../Album';
import styles from "./styles";

export type AlbumCategoryProps = {
    title:string, 
    albums:[Album],
}

const AlbumCategory=(props:AlbumCategoryProps)=>(
    <View style={styles.container}>
        {/*Title of Category*/}
        <Text style={styles.title}>{props.title}</Text>

        {/*List of albums*/}
        <FlatList 
        /*많은 양의 리스트 아이템을 스크롤로 내리면서 보여주고자 할 때 사용하며 parameter로는 data, renderItem, keyExtractor가 있다*/
            data={props.albums}
            /*data : 만들고자 하는 리스트의 데이터*/
            renderItem={({ item }) => <AlbumComponent album={item} />}
            /*renderItem : data로 받은 데이터를 item에 각각 render*/
            keyExtractor={( item ) => item.id}
            /*keyExtractor : 각 요소 구별*/
            horizontal
            showsHorizontalScrollIndicator={false}
        />
    </View>
)

export default AlbumCategory;
```
</div>
</details>

<details>
<summary>HomeScreen.tsx</summary>
<div markdown="1">

```javascript
import React from 'react';
import { StyleSheet, Text, View } from 'react-native';
import AlbumCategory from '../components/AlbumCategory';

const albumCategory = {
  id:'1',
  title:'Happy Vibes',
  albums: 
  [
    {
      id:'1',
      imageUri:'https://user-images.githubusercontent.com/81608287/156109216-cd427b41-efb0-4b72-af57-e56b2a9e261a.jpg',
      artistsHeadline:'the mamas & the papas'
    }, 
    {
      id:'2',
      imageUri:'https://user-images.githubusercontent.com/81608287/156109488-d1346086-53d5-4428-aa95-b3cd1f3509e4.jpg',
      artistsHeadline:'Don McLean'
    },
    {
      id:'3',
      imageUri:'https://user-images.githubusercontent.com/81608287/156109573-2137d151-2f76-42fa-bf90-55455ba3a82d.jpg',
      artistsHeadline:'Madeleine Peyroux'
    },
    {
      id:'4',
      imageUri:'https://user-images.githubusercontent.com/81608287/156109687-d4f0ee5d-514b-4eef-8f92-ea8d306be0ae.jpg',
      artistsHeadline:'Roy Orbison'
    }
  ]
}

export default function HomeScreen() {
  return (
    <View style={styles.container}>
      <AlbumCategory 
        title={albumCategory.title} 
        albums={albumCategory.albums}
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

### Data (Album Categories : Array)<br/>
<img src="/images/Posting/ReactNative/TeslaProject/04.png" alt="Project" width="40%" height="40%">
- Spotify Mobile App 내 전체 Album Categories생성 후 개별 페이지에서 사용 <br/>
- data folder 생성 후 Album Categories data작성<br/>

<details>
<summary>data_albumCategories</summary>
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
        imageUri: 'https://cache.boston.com/resize/bonzai-fba/Globe_Photo/2011/04/14/1302796985_4480/539w.jpg',
        artistsHeadline: 'Taylor Swift, Kygo Objective C, Avicii'
      }, {
        id: '6',
        imageUri: 'https://cdn6.f-cdn.com/contestentries/1485199/27006121/5ca3e39ced7f1_thumb900.jpg',
        artistsHeadline: 'Post Malone, Drake, Eminem'
      },
      {
        id: '7',
        imageUri: 'https://images-na.ssl-images-amazon.com/images/I/61F66QURFyL.jpg',
        artistsHeadline: 'Journey, Escape, Avicii'
      },
    ]
  },{
    id: '3',
    title: 'Shows to try',
    albums: [
      {
        id: '8',
        imageUri: 'https://cache.boston.com/resize/bonzai-fba/Globe_Photo/2011/04/14/1302796985_4480/539w.jpg',
        artistsHeadline: 'Taylor Swift, Kygo Objective C, Avicii'
      }, {
        id: '9',
        imageUri: 'https://cdn6.f-cdn.com/contestentries/1485199/27006121/5ca3e39ced7f1_thumb900.jpg',
        artistsHeadline: 'Post Malone, Drake, Eminem'
      },
      {
        id: '10',
        imageUri: 'https://images-na.ssl-images-amazon.com/images/I/61F66QURFyL.jpg',
        artistsHeadline: 'Journey, Escape, Avicii'
      },
    ]
  }, {
    id: '4',
    title: 'Workout',
    albums: [
      {
        id: '11',
        imageUri: 'https://cache.boston.com/resize/bonzai-fba/Globe_Photo/2011/04/14/1302796985_4480/539w.jpg',
        artistsHeadline: 'Taylor Swift, Kygo Objective C, Avicii'
      }, {
        id: '12',
        imageUri: 'https://cdn6.f-cdn.com/contestentries/1485199/27006121/5ca3e39ced7f1_thumb900.jpg',
        artistsHeadline: 'Post Malone, Drake, Eminem'
      },
      {
        id: '13',
        imageUri: 'https://images-na.ssl-images-amazon.com/images/I/61F66QURFyL.jpg',
        artistsHeadline: 'Journey, Escape, Avicii'
      },
    ]
  },
  ]
```

</div>
</details>

<details>
<summary>screens_HomeScreen</summary>
<div markdown="1">

```javascript
import React from 'react';
import { StyleSheet, FlatList, View } from 'react-native';
import AlbumCategory from '../components/AlbumCategory';
import albumCategories from '../data/albumCategories';

export default function HomeScreen() {
  return (
    <View style={styles.container}>
      <FlatList 
        data={albumCategories}
        /*data_albumCategories(App내 전체 앨범데이터)를 만들고자 하는 데이터 리스트로 설정*/
        renderItem={({item}) => (
          /*renderItem : data로 받은 데이터를 item에 각각 render*/
          <AlbumCategory 
            title={item.title}
            albums={item.albums}
            keyExtractor={(item) => item.id}
            /*keyExtractor : 각 요소 구별*/
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

### Album Screen<br/>
<img src="/images/Posting/ReactNative/TeslaProject/05.png" alt="Project" width="40%" height="40%">
- Home화면 앨범 클릭 시, 나타나는 페이지 제작 (screens 폴더 내 AlbumScreen.tsx생성)
- Navigation_index.tsx 수정하여 Home화면 앨범 클릭 시 AlbumScreen페이지로 이동 되도록 설정

<details>
<summary>Source Code</summary>
<div markdown="1">

```javascript
```

</div>
</details>




