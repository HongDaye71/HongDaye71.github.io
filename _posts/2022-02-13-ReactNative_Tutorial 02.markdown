---
layout: post
title:  React Native Study02_TESLA Mobile App제작
date:   2022-02-13 15:01:35 +0300
image:  '/images/ReactNative_TeslaProject.png'
tags:   [React Native, App Development]
---

# React Native를 활용한 TESLA Mobile App제작

## Contents <br/>
1. Car Item Component<br/>
  (1) Render the text<br/>
  (2) Render the Background Image<br/>
  (3) Create a Separate component for CarItem<br/>
2. Button Component<br/>
  (1) Create Separate Component<br/>
  (2) Receive props<br/>
  (3) Style The button based on 'type' prop<br/>

* notJust․dev 유투브 채널의 React Native Tutorial 영상을 바탕으로 공부한 내용을 정리하는 포스팅입니다.<br/>
* [Programming with Mosh 유투브채널 바로가기](https://www.youtube.com/channel/UCYSa_YLoJokZAwHhlwJntIA) <br/>
* [Tutorial Video](https://www.youtube.com/watch?v=iQ_0Fd_N3Mk)<br/>
* *작업단계 별 부연설명은 Source Code내 주석으로 작성*

___

### 1.1 Car Item Component (Render the text)<br/>
<img src="/images/Posting/ReactNative/TeslaProject/01.png" alt="Project" width="95" height="95">
<details>
<summary>Source Code</summary>
<div markdown="1">

```javascript
import { StatusBar } from 'expo-status-bar';
import { StyleSheet, Text, View } from 'react-native';

export default function App() {
  return (
    <View style={styles.container}>
      <View style={styles.carContainer}>  
        <View style={styles.titles}>
          <Text style={styles.title}>Model S</Text>
          <Text style={styles.subtitle}>Starting at $69,420</Text>
      </View>
      {/*<View></View> = Component를 Group으로 관리*/}
      {/*style={styles.__} = 스타일 지정(스타일은 하단에서 설정))*/}
      </View>

      <StatusBar style="auto" />
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#fff',
    alignItems: 'center',
    justifyContent: 'center',
  },

  carContainer:{
    width:'100%',
    height:'100%',
  },

  titles:{
    marginTop:'30%',
    width:'100%',
    alignItems:'center'
  },

  title:{
    fontSize:40,
    fontWeight:'500',
  },

  subtitle:{
    fontSize:16,
    color:'#5c5e62'
  },
});

```

</div>
</details>

___

### 1.2 Car Item Component(Render the Background Image)<br/>
<img src="/images/Posting/ReactNative/TeslaProject/02.png" alt="Project" width="95" height="95">
<details>
<summary>Source Code</summary>
<div markdown="1">

```javascript
import { StatusBar } from 'expo-status-bar';
import { StyleSheet, Text, View } from 'react-native';

export default function App() {
  return (
    <View style={styles.container}>

      <View style={styles.carContainer}>
        <ImageBackground
          source={require('../assets/images/ModelX.jpeg')}
          style={styles.image}
        />
        
        <View style={styles.titles}>
          <Text style={styles.title}>Model S</Text>
          <Text style={styles.subtitle}>Starting at $69.428</Text>
        </View>
      </View>

      <StatusBar style="auto" />
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#fff',
    alignItems: 'center',
    justifyContent: 'center',
  },

  carContainer:{
    width:'100%',
    height:'100%',
  },

  titles:{
    marginTop:'30%',
    width:'100%',
    alignItems:'center'
  },

  title:{
    fontSize:40,
    fontWeight:'500',
  },

  subtitle:{
    fontSize:16,
    color:'#5c5e62'
  },

  image : {
    width:'100%',
    height:'100%',
    resizeMode:'cover',
    position:'absolute',
  }
});

```
</div>
</details>

___

## 1.3 Car Item Component(Create a Separate component for CarItem)<br/>

<div class="gallery-box">
  <div class="gallery">
    <img src="/images/Posting/ReactNative/TeslaProject/04.png" alt="Project">
    <img src="/images/Posting/ReactNative/TeslaProject/05.png" alt="Project">
    <img src="/images/Posting/ReactNative/TeslaProject/06.png" alt="Project">
  </div>
  <em>App.js / index.js / style.js / <a href="https://unsplash.com/" target="_blank"></a></em>
</div>

- Separate Component 생성 시에 하나의 파일에서 다수 Component의 index & style source code를 작설할 경우, 코드가 지저분해 지므로 Car_Item폴더생성 후 index & style file 별도작성하여 App.js Script에서 사용<br/>

```javascript
import { StatusBar } from 'expo-status-bar';
import React from 'react';
import { StyleSheet, Text, View, ImageBackground } from 'react-native';
import CarItem from './CarItem'; /*CarItem_index.js import*/

export default function App() {
  return (
    <View style={styles.container}>

      <CarItem /> {/*CarItem_index.js code사용*/}
      <StatusBar style="auto" />
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#fff',
    alignItems: 'center',
    justifyContent: 'center',
  },
});

```
</div>
</details>

<details>
<summary>CarItem_index.js Source Code</summary>
<div markdown="1">

```javascript
import React from 'react';
import {View, Text, ImageBackground} from 'react-native';
import StyleButton  from '../StyleButton';
import styles from './styles'

const CarItem = (props) => {
    return (
        <View style={styles.carContainer}>
            <ImageBackground
                source={require('../assets/images/ModelX.jpeg')}
                style={styles.image}
            />
        
            <View style={styles.titles}>
                <Text style={styles.title}>Model S</Text>
                <Text style={styles.subtitle}>Starting at $69.428</Text>
            </View>

            <StyleButton/>
        </View>
    );
};

export default CarItem;
```
</div>
</details>

<details>
<summary>CarItem_styles.js Source Code</summary>
<div markdown="1">

```javascript
 import {StyleSheet} from 'react-native';

 const styles = StyleSheet.create({
    carContainer:{
        width:'100%',
        height:'100%',
      },
    
      titles:{
        marginTop:'30%',
        width:'100%',
        alignItems:'center'
      },
    
      title:{
        fontSize:40,
        fontWeight:'500',
      },
    
      subtitle:{
        fontSize:16,
        color:'#5c5e62'
      },
      
      image : {
        width:'100%',
        height:'100%',
        resizeMode:'cover',
        position:'absolute',
      }
 });

 export default styles;
```
</div>
</details>

___

## 2.1 Button Component(Create a separate component)<br/>
<img src="/images/Posting/ReactNative/TeslaProject/07.png" alt="Project" width="95" height="95">

<div class="gallery-box">
  <div class="gallery">
    <img src="/images/Posting/ReactNative/TeslaProject/08.png" alt="Project">
    <img src="/images/Posting/ReactNative/TeslaProject/09.png" alt="Project">
  </div>
  <em>CarItem_index.js / StyleButton_index.js / StyleButton_style.js / <a href="https://unsplash.com/" target="_blank"></a></em>
</div>

- StyleButton Folder 생성 후 index & style file 별도 작성하여 CarItem_index.js에서 사용<br/>

<details>
<summary>CarItem_index.js Source Code</summary>
<div markdown="1">

```javascript

```
</div>
</details>

<details>
<summary>StyleButton Folder_index.js Source Code</summary>
<div markdown="1">

```javascript

```
</div>
</details>

<details>
<summary>StyleButton Folder_styles.js Source Code</summary>
<div markdown="1">

```javascript
import {StyleSheet} from 'react-native';

const styles = StyleSheet.create({
    container: {
        width:'100%',
        padding:10,
    },

    button: {
        height:40,
        borderRadius:20, /*Button radius설정*/
        justifyContent : 'center', /*vertical기준 : Text Center*/
        alignItems :'center', /*Horizontal기준 : Text Center*/
    },

    text: {
        fontSize:12,
        fontWeight:'500',
        textTransform:'uppercase', /*대문자 세팅*/
    }
});

export default styles;
```
</div>
</details>

___

## 2.2 Button Component(Receive props))<br/>

___

## 2.3 Button Component(Style The Button based on 'type' prop)<br/>
<img src="/images/Posting/ReactNative/TeslaProject/10.png" alt="Project" width="95" height="95">

- Props : Component간 데이터 공유를 위해 사용되는 객체<br/>
- Button Background의 경우, 두 개 버튼의 색상이 다르기 때문에 Style.js에서 지정하지 않고 Props를 통해 별도지정(StyleButton Folder_index.js에서 Type에 따른 Style설정 후 CarItem Folder_index.js에서 type,content,onPress등 설정)<br/>

<details>
<summary>CarItem_index.js Source Code</summary>
<div markdown="1">

```javascript
import React from 'react';
import {View, Text, ImageBackground} from 'react-native';
import StyleButton  from '../StyleButton';
import styles from './styles'

const CarItem = (props) => {
    return (
        <View style={styles.carContainer}>
            <ImageBackground
                source={require('../assets/images/ModelX.jpeg')}
                style={styles.image}
            />
        
            <View style={styles.titles}>
                <Text style={styles.title}>Model S</Text>
                <Text style={styles.subtitle}>Starting at $69.428</Text>
            </View>

            <StyleButton 
                type='primary' 
                content={"Custom Order"} 
                onPress={()=>{
                    console.warn("Custom Order was pressed")
                }}
            />
            {/*Parameter : Type, Content, onPress시 출력 될 텍스트*/}
            <StyleButton 
                type='secondary' 
                content={"Existing Inventory"} 
                onPress={()=>{
                    console.warn("Existing Inventory was pressed")
                }}
            />
        </View>
    );
};

export default CarItem;
```
</div>
</details>

<details>
<summary>StyleButton Folder_index.js Source Code</summary>
<div markdown="1">

```javascript
import React from 'react';
import {View, Text, Pressable} from 'react-native';
import styles from './styles';

const StyleButton = (props) => {

    const {type, content, onPress} = props;
    {/*type, contet, onPress : CarItem_index.js에서 별도지정될 수 있도록 선언*/}

    const backgroundColor = type === 'primary' ? '#171a20CC' : '#FFFFFFA6';
    const textColor = type === 'primary' ? '#FFFFFFA6' : '#171a20CC';
    /*Background Color, Text Color : CarItem_index.js에서 지정한 type에 따라 색상을 어떻게 설정할지 Setting*/

    return (
        <View style={styles.container}>
            <Pressable
                style={[styles.button, {backgroundColor : backgroundColor}]}
                onPress={()=>onPress()}
            >
                <Text style={[styles.text, {color : textColor}]}>{content}</Text>
            </Pressable>
            {/*Background Color, Text Color, Content: 위에서 Setting한 type별 색상이 적용되도록 설정*/}
        </View>
    );
};

export default StyleButton;

```
</div>
</details>