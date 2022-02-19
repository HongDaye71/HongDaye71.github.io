---
layout: post
title:  React Native Study02_TESLA Mobile App제작
date:   2022-02-13 15:01:35 +0300
image:  '/images/ReactNative.png'
tags:   [React Native, App Development]
---

# Project : React Native를 활용한 TESLA Mobile App제작

## Contents <br/>
1. Render the text<br/>
2. Render the Background Image<br/>
3. Create a separate component for CarItem<br/>

* notJust․dev 유투브 채널의 React Native Tutorial 영상을 바탕으로 공부한 내용을 정리하는 포스팅입니다.<br/>
* [Programming with Mosh 유투브채널 바로가기](https://www.youtube.com/channel/UCYSa_YLoJokZAwHhlwJntIA) <br/>
* [Tutorial Video](https://www.youtube.com/watch?v=iQ_0Fd_N3Mk)<br/>

___

### Render the text<br/>
<img src="/images/Posting/ReactNative/TeslaProject/02.png" alt="Project">
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