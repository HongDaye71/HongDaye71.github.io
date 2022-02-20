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
  (3) Create a separate component for CarItem<br/>
2. Button Component<br/>
  (1) Create separate Component<br/>
  (2) Receive props<br/>
  (3) Style The button based on 'type' prop<br/>

* notJust․dev 유투브 채널의 React Native Tutorial 영상을 바탕으로 공부한 내용을 정리하는 포스팅입니다.<br/>
* [Programming with Mosh 유투브채널 바로가기](https://www.youtube.com/channel/UCYSa_YLoJokZAwHhlwJntIA) <br/>
* [Tutorial Video](https://www.youtube.com/watch?v=iQ_0Fd_N3Mk)<br/>

___

### 1.1 Car Item Component (Render the text)<br/>
<img src="/images/Posting/ReactNative/TeslaProject/01.png" alt="Project" width="95%" height="95%">
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

## 1.3 Car Item Component(Create a separate component for CarItem)<br/>

<div class="gallery-box">
  <div class="gallery">
    <img src="/images/Posting/ReactNative/TeslaProject/04.png" alt="Project">
    <img src="/images/Posting/ReactNative/TeslaProject/05.png" alt="Project">
    <img src="/images/Posting/ReactNative/TeslaProject/06.png" alt="Project">
  </div>
  <em>App.js / index.js / style.js / <a href="https://unsplash.com/" target="_blank"></a></em>
</div>

- Separate Component 생성 시에 하나의 파일에서 다수 Component의 index & style source code를 작설할 경우, 코드가 지저분해 지므로 index & style file 별도생성하여 App.js Script에서 사용<br/>

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
<summary>App.js Source Code</summary>
<div markdown="1">

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
## 1.3 Car Item Component(Create a separate component for CarItem)<br/>

<div class="gallery-box">
  <div class="gallery">
    <img src="/images/Posting/ReactNative/TeslaProject/04.png" alt="Project">
    <img src="/images/Posting/ReactNative/TeslaProject/05.png" alt="Project">
    <img src="/images/Posting/ReactNative/TeslaProject/06.png" alt="Project">
  </div>
  <em>App.js / CarItem_index.js / CarItem_style.js / <a href="https://unsplash.com/" target="_blank"></a></em>
</div>

- Separate Component 생성 시에 하나의 파일에서 다수 Component의 index & style source code를 작설할 경우, 코드가 지저분해 지므로 CarItem Folder생성 후 index & style file 별도 작성하여 App.js에서 사용<br/>

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
<img src="/images/Posting/ReactNative/TeslaProject/07.png" alt="Project" width="95" height="95">

<div class="gallery-box">
  <div class="gallery">
    <img src="/images/Posting/ReactNative/TeslaProject/08.png" alt="Project">
    <img src="/images/Posting/ReactNative/TeslaProject/09.png" alt="Project">
  </div>
  <em>App.js / StyleButton_index.js / StyleButton_style.js / <a href="https://unsplash.com/" target="_blank"></a></em>
</div>

<details>
<summary>App.js Source Code</summary>
<div markdown="1">

- StyleButton Folder 생성 후 index & style file 별도 작성하여 App.js에서 사용<br/>

```javascript

```
</div>
</details>

<details>
<summary>CarItem_index.js Source Code</summary>
<div markdown="1">

```javascript

```
</div>
</details>

<details>
<summary>CarItem_styles.js Source Code</summary>
<div markdown="1">

```javascript

```
</div>
</details>
