---
layout: post
title:  React Native Study04_Spotify Mobile App Clone
date:   2022-02-13 15:01:35 +0300
image:  '/images/ReactNative_TeslaProject.png'
tags:   [React Native, App Development]
---

# React Native_TESLA Mobile App Clone

## Contents <br/>
1. Car Item Component<br/>
  (1) Render the text<br/>
  (2) Render the Background Image<br/>
  (3) Create a Separate component for CarItem<br/>
2. Button Component<br/>
  (1) Create Separate Component<br/>
  (2) Receive props / Style The button based on 'type' prop<br/>
3. Finish Car Item Component
  (1) Use buttons
  (2) Implement props 

___

* notJust․dev 유투브 채널의 React Native Tutorial 영상을 바탕으로 공부한 내용을 정리하는 포스팅입니다.<br/>
* [notJust․dev 유투브채널 바로가기](https://www.youtube.com/channel/UCYSa_YLoJokZAwHhlwJntIA) <br/>
* [Tutorial Video](https://www.youtube.com/watch?v=iQ_0Fd_N3Mk)<br/>
* *작업단계 별 부연설명은 Source Code내 주석으로 작성*

___

## 결과물
<p><iframe src="https://www.youtube.com/embed/qIG1yNURnQ8" frameborder="0" allowfullscreen></iframe></p>
[Source Code Download](https://github.com/HongDaye71/ReactNative-TeslaMobileApp-Clone)

### 1.1 Car Item Component (Render the text)<br/>
<img src="/images/Posting/ReactNative/TeslaProject/01.png" alt="Project" width="40%" height="40%">
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
<img src="/images/Posting/ReactNative/TeslaProject/02.png" alt="Project" width="40%" height="40%">
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

<details>
<summary>App.js  Source Code</summary>
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
<img src="/images/Posting/ReactNative/TeslaProject/07.png" alt="Project" width="40%" height="40%">

<div class="gallery-box">
  <div class="gallery">
    <img src="/images/Posting/ReactNative/TeslaProject/08.png" alt="Project">
    <img src="/images/Posting/ReactNative/TeslaProject/09.png" alt="Project">
  </div>
  <em>CarItem_index.js / StyleButton_index.js / StyleButton_style.js / <a href="https://unsplash.com/" target="_blank"></a></em>
</div>

- StyleButton Folder 생성 후 index & style file 별도 작성하여 CarItem_index.js에서 사용<br/>

<details>
<summary>StyleButton Folder_index.js Source Code</summary>
<div markdown="1">

```javascript
import React from 'react';
import {View, Text, Pressable} from 'react-native';
import styles from './styles';

const StyleButton = (props) => {

    return (
        <View style={styles.container}>
            <Pressable
                style={styles.button}
                onPress={()=> console.warn ('Hey there')}
            >
                <Text style={styles.text}>Custom Order</Text>
            </Pressable>
        </View>
    );
};

export default StyleButton;

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

## 2.2 Button Component(Receive props / Style The Button based on 'type' prop)<br/>
<img src="/images/Posting/ReactNative/TeslaProject/10.png" alt="Project" width="40%" height="40%">

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

___

### 3.1 Finish Car Item Component (Use buttons)<br/>
<img src="/images/Posting/ReactNative/TeslaProject/11.png" alt="Project" width="40%" height="40%">
- 버튼 위치조정 (Style지정 후 CarItem_style.js에서 위치조정)
- CarItem_index.js의 name, tagline, image 요소에 props적용 (앱 스크롤링 시, 화면이동 작업을 용이하게 하기위함)

<details>
<summary>CarItem_index.js</summary>
<div markdown="1">

```javascript
import React from 'react';
import {View, Text, ImageBackground} from 'react-native';
import StyleButton  from '../StyleButton';
import styles from './styles'

const CarItem = (props) => {

    const {name, tagline, taglineCTA, image} = props;
    {/*name, tagline, image : App.js에서 별도 지정할 수 있도록 선언*/}

    return (
        <View style={styles.carContainer}>
            {/*name, tagline, image : App.js에서 별도 지정할 수 있도록 설정*/}
            <ImageBackground
                source={image}
                style={styles.image}
            />
        
            <View style={styles.titles}>
                <Text style={styles.title}>{name}</Text>
                <Text style={styles.subtitle}>
                    {tagline}&nbsp;
                    <Text style={styles.subtitleCTA}>
                        {/*Tochless Delivery 텍스트의 경우, 클릭 가능하도록 별도 스타일 지정*/}
                        {taglineCTA}
                    </Text>
                    </Text>
            </View>

            <View style={styles.buttonsContainer}> 
            {/*Button 위치조정을 위해 하나의 그룹으로 묶어준 뒤 style.js에서 작업*/}
                <StyleButton 
                    type='primary' 
                    content={"Custom Order"} 
                    onPress={()=>{
                        console.warn("Custom Order was pressed")
                    }}
                />
                <StyleButton 
                    type='secondary' 
                    content={"Existing Inventory"} 
                    onPress={()=>{
                        console.warn("Existing Inventory was pressed")
                    }}
                />
            </View>
        </View>
    );
};

export default CarItem;

```
</div>
</details>

<details>
<summary>CarItem_style.js</summary>
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

      subtitleCTA:{
        /*Tochless Delivery 텍스트의 경우, 클릭 가능하도록 별도 스타일 지정*/
        textDecorationLine:'underline',
      },
      
      image : {
        width:'100%',
        height:'100%',
        resizeMode:'cover',
        position:'absolute',
      },

      /*Button 위치조정*/
      buttonsContainer: {
        position: 'absolute',
        bottom: 50,
        width: '100%'
      }
 });

 export default styles;
```
</div>
</details>

<details>
<summary>App.js</summary>
<div markdown="1">

```javascript
import { StatusBar } from 'expo-status-bar';
import React from 'react';
import { StyleSheet, Text, View, ImageBackground } from 'react-native';
import CarItem from './CarItem'; 

export default function App() {
  return (
    <View style={styles.container}>

      <CarItem 
      name={"Model X"}
      tagline={"Order Online For"}
      taglineCTA={"Touchless Delivery"}
      image={require('./assets/images/ModelX.jpeg')}
      /> 
      {/*CarItem_index.js에서 name, tagline, image는 별도 지정하는 것으로 수정하였으므로 해당 스크립트에서 별도지정*/}


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

___

### 3.2 Finish Car Item Component (Implement props)<br/>
<p><iframe src="https://www.youtube.com/embed/qIG1yNURnQ8" frameborder="0" allowfullscreen></iframe></p>

- CarList Folder 생성 후 car & index & style file 별도 작성하여 App.js에서 사용<br/>
  - car.js : 스크롤다운 시 나타날 4개 페이지 내 정보<br/>
  - index.js : car.js 내 한 개의 정보가 CarItem_index.js양식으로 하나씩 랜더링 되도록 코드작성<br/>

<details>
<summary>CarItem_index.js</summary>
<div markdown="1">

```javascript
import React from 'react';
import {View, Text, ImageBackground} from 'react-native';
import StyleButton  from '../StyleButton';
import styles from './styles'

const CarItem = (props) => {

    const {name, tagline, taglineCTA, image} = props.car;

    return (
        <View style={styles.carContainer}>
            <ImageBackground
                source={image}
                style={styles.image}
            />
        
            <View style={styles.titles}>
                <Text style={styles.title}>{name}</Text>
                <Text style={styles.subtitle}>
                    {tagline}&nbsp;
                    <Text style={styles.subtitleCTA}>
                        {taglineCTA}
                    </Text>
                    </Text>
            </View>

            <View style={styles.buttonsContainer}> 

                <StyleButton 
                    type='primary' 
                    content={"Custom Order"} 
                    onPress={()=>{
                        console.warn("Custom Order was pressed")
                    }}
                />
                <StyleButton 
                    type='secondary' 
                    content={"Existing Inventory"} 
                    onPress={()=>{
                        console.warn("Existing Inventory was pressed")
                    }}
                />
            </View>
        </View>
    );
};

export default CarItem;

```
</div>
</details>

<details>
<summary>CarItem_style.js</summary>
<div markdown="1">

```javascript
 import {StyleSheet, Dimensions} from 'react-native';

 const styles = StyleSheet.create({
    carContainer:{
        width:'100%',
        height: Dimensions.get('window').height, 
        /**/
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

      subtitleCTA:{
        textDecorationLine:'underline',
      },
      
      image : {
        width:'100%',
        height:'100%',
        resizeMode:'cover',
        position:'absolute',
      },

      buttonsContainer: {
        position: 'absolute',
        bottom: 50,
        width: '100%'
      }
 });

 export default styles;
```
</div>
</details>

<details>
<summary>CarList_car.js</summary>
<div markdown="1">

```javascript
export default [{
  name: 'Model S',
  tagline: 'Starting at $69,420',
  image: require('../assets/images/ModelS.jpeg'),
}, {
  name: 'Model 3',
  tagline: 'Order Online for',
  taglineCTA: 'Touchless Delivery',
  image: require('../assets/images/Model3.jpeg'),
}, {
  name: 'Model X',
  tagline: 'Order Online for',
  taglineCTA: 'Touchless Delivery',
  image: require('../assets/images/ModelX.jpeg'),
}, {
  name: 'Model Y',
  tagline: 'Order Online for',
  taglineCTA: 'Touchless Delivery',
  image: require('../assets/images/ModelY.jpeg'),
}];

```
</div>
</details>

<details>
<summary>CarList_index.js</summary>
<div markdown="1">

```javascript
import React from 'react';
import {View, FlatList} from 'react-native';

import CarItem from '../CarItem';
import styles from './styles';
import cars from './cars';

const CarsList = (props) => {
    return (
        <View style={styles.container}>
            <FlatList
            /*FlatList : 출력해야 하는 데이터 양이 많은 경우, 모든 데이터를 한 번에 렌더링 하지 않고 보여지는 부분 혹은 수동으로 설정한 양 만큼의 데이터만 렌더링 되도록 하는 Comonent*/
                data={cars}
                renderItem={({item}) => <CarItem car={item} />}
            />
        </View>
    );
};

export default CarsList;
```
</div>
</details>

<details>
<summary>CarList_style.js</summary>
<div markdown="1">

```javascript
import {StyleSheet} from 'react-native';

const styles = StyleSheet.create({
    container:{
        width:'100%',
    }
});

export default styles;
```
</div>
</details>


<details>
<summary>App.js</summary>
<div markdown="1">

```javascript
import { StatusBar } from 'expo-status-bar';
import React from 'react';
import { StyleSheet, View } from 'react-native';
import CarsList from './CarsList'; 

export default function App() {
  return (
    <View style={styles.container}>
      <CarsList />
      {/*기존 CarItem_index.js에서 가져오던 정보를 CarsList_index/js에서 가져오도록 수정 (다수 페이지 생성을 위함)*/}
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

