---
layout: post
title:  MobX-React 기초정리
date:   2022-05-24 12:38:35 +0300
image:  '/images/MobX.png'
tags:   [MobX]
---
<br/>

# MobX-React 기초정리<br/>
## Contents <br/>
1. MobX-Flux의 이해<br/>
2. MobX구조<br/>
3. 예제실습<br/>

* 나무소리 유투브 채널의 MobX 기초강의 내용을 바탕으로 정리하는 포스팅입니다. <br/>
* 영상에서 언급되지 않은 내용이 포함되어 있음<br/>
* [Tutorial Video](https://youtu.be/NwbZmhE2Blc)<br/>

___

## :mag: MobX-Flux의 이해<br/>
#### 1. MobX란? 
MobX는 전역 상태 라이브러리로 모든 상태변화를 자동으로 추적하는 역할을 한다.<br/><br/>

#### 2. MobX를 사용하는 이유 
React를 구성하는 Component는 State를 이용해 변경 가능한 데이터를 관리할 수 있다. 하지만 다수의 컴포넌트가 각자의 상태를 관리할 경우 데이터 관리 및 제어가 어려우며 데이터 공유가 필요한 경우 제약이 발생한다. MobX는 공통의 데이터 관리영역인 Store를 통해 State를 관리하여 위와 같은 단점을 보완한다.<br/><br/>

#### 3. Flux Architecture
Flux는 데이터 흐름을 한 방향으로 유지하기 위해 설계된 App 디자인 패턴이다.<br/><br/>

#### 4. MVC와 Flux의 차이
MVC는 App을 Model,View,Controller로 분리하며 View와 Model사이에 양방향 데이터 이동이 가능하다. MVC는 자신의 역할에 집중할 수 있으며 단순하고 직관적이라는 장점이 있다. 하지만 프로젝트가 커질 경우 Model과 View의 전후관계를 따지기가 힘들어 데이터 관리가 어려워진다. 객체지향 프로그래밍에서 MVC사용 시 발생하는 문제를 해결하기 위해 Flux 디자인 패턴이 나오게 되었다.<br/><br/>

<img src="/images/Posting/MobX/MVC_Flux.png" alt="Model(로직과 관련된 모든 데이터를 포함), View(사용자에게 데이터를 표현하거나 유저와 상호작용을 처리), Controller(모델과 뷰 구성요소간의 인터페이스 (ex. 클릭이벤트 발생 시 컨트롤러를 통해 Model에 해당 데이터 반영))">

___

##  :pushpin: MobX구조<br/>
#### 1. MobX개요 <br/>
- MobX를 이용하면 Component의 State를 Store라는 별도의 영역에서 관리한다.<br/>
- MobX 적용을 위해서는 mobx.js와 mobx-react.js 라이브러리가 필요하다.<br/>
  * <span style='background-color:#f6f8fa'>mobx:</span> Store관리를 위한 라이브러리로 observable, action등의 모듈로 구성되어 있음<br/>
  * <span style='background-color:#f6f8fa'>mobx-react:</span> Store의 데이터를 React에 적용시키기 위한 라이브러리로 observer등의 모듈로 구성되어 있음<br/>

- MobX는 다수의 Store를 관리할 수 있다.<br/>
- MobX가 제공하는 대표적인 API는 observable, action, observer, computed, inject 이며 API사용은 데코레이터(@)를 이용하는 것이 일반적이다.<br/>
  * <span style='background-color:#f6f8fa'>observable:</span> 추적 가능한 state정의<br/>
  * <span style='background-color:#f6f8fa'>action:</span> state를 변경하는 메소드<br/>
  * <span style='background-color:#f6f8fa'>observer:</span> observable을 통해 관리되는 state를 react component에 적용<br/>
  * <span style='background-color:#f6f8fa'>computed:</span> state와 cahce로부터 새로운 결과를 반환<br/>
  * <span style='background-color:#f6f8fa'>inject:</span> store를 props에 넣어 component에서 props를 통해 store에 접근할 수 있도록 함<br/>

- MobX 라이브러리는 TypeScript가 적용되어 있다.<br/>

___

## :bell: 예제실습<br/>
#### *실습 프로젝트: 버튼클릭을 통해 화면 내 숫자를 증가 및 감소하는 페이지 생성*<br/>

#### 1. yarn create react-app "project name"<br/>
#### 2. mobX 및 Decorator사용을 위한 환경설정<br/>

* <span style='background-color:#fff5b1'>CRA 프로젝트 커스터마이징 방법</span><br/>
(1) eject사용:<br/>
  eject(숨겨져 있던 웹팩 등의 설정을 보여주며 커스터마이징 가능하도록 한다)을 통해 CRA로 생성된 프로젝트를 커스터마이징 할 수 있으나 One Build Dependency(패키지 설치 및 삭제 시 패키지 간 연결 자동관리)의 장점을 잃게 되는 등의 문제가 발생한다.<br/>
(2) react-app-rewired사용:<br/>
  rewired는 eject 없이 CRA의 설정을 커스터마이징을 할 수 있도록 하는 라이브러리이다.<br/>

* <span style='background-color:#fff5b1'>react-app-rewired 사용방법</span><br/>

(1) rewired Library 설치

```
yarn add --dev customize-cra
yarn add --dev react-app-rewired
```

<br/>(2) package.json 수정

```
"scripts": {
	"start": "react-app-rewired start",
    "build": "react-app-rewired build",
    "test": "react-app-rewired test --env=jsdom",
    "eject": "react-scripts eject",
}
```

<br/>(3) 루트폴더에 config-overrides.js추가

```
const { 
  addDecoratorsLegacy, // decorator를 사용할 수 있도록 해주는 config
  disableEsLint,
  override,
} = require("customize-cra");

// 사용자 정의 웹팩 설정
module.exports = {
  webpack: override(
      disableEsLint(),
      addDecoratorsLegacy()
  ),
};
```

<br/>(4) MobX 사용을 위한 플러그인 등 설치

```
// babel 플러그인 설치
yarn add --dev @babel/plugin-proposal-decorators @babel/plugin-proposal-class-properties

// 추가적인 es7 데코레이터 설치
yarn add --dev core-decorators

// mobx 설치
yarn add mobx mobx-react
```

<br/>(5) package.json에 babel 플러그인 추가

```
...
"babel": {
    "presets": [
      "react-app"
    ],
    "plugins": [
      [
        "@babel/plugin-proposal-decorators",
        {
          "legacy": true
        }
      ],
      [
        "@babel/plugin-proposal-class-properties",
        {
          "loose": true
        }
      ]
    ]
  }
 ...
 ```

<br/>

#### 3. 실습을 위한 기본 UI템플릿 설정

<details>
<summary>App.js</summary>
<div markdown="1">

```
import React, { Component } from 'react';
import CounterComponent from './component/CounterComponent';

class App extends Component {
  render(){
    return (
      <div>
        <CounterComponent />
      </div>
  );
  }
}

export default App;
```
</div>
</details>

<details>
<summary>CounterComponent.js</summary>
<div markdown="1">

```
import React, { Component } from 'react';
import { Button, Box } from '@material-ui/core';

class CounterComponent extends Component {

  render(){
    return(
      <div>
        <Button variant='contained' color='primary' size='large'> - </Button>        
        
        <Box component='span' m={5}> 0 </Box>
        
        <Button variant='contained' color='primary' size='large'> + </Button>
      </div>
    )
  }
}

export default CounterComponent;
```
</div>
</details>

<br/>

#### 4. Store생성 및 Observable 변수생성

<details>
<summary>CounterStore.js</summary>
<div markdown="1">

```
import { observable } from 'mobx';

class CounterStore {
    @observable
    _count = 5
}

export default new CounterStore;

/*
1. _count를 store에서 관리할 수 있도록 observable함수의 변수로 할당
    -> 아래 코드를 데코레이터를 통해 작성하면 위 코드와 같이 표현됨
        class CounterStore {
            observable ({
                _count = 5,
            });
        }

2. 데코레이터는 js표준이 아님으로 별도설정 필요
    -> Code - Preferences - settings - experimental decorators검색 - enable체크

3. export시에는 new를 붙여 state사용 시 매번 new를 통해 변수를 새로 생성하지 않도록 작성
*/
```
</div>
</details>

<details>
<summary>index.js</summary>
<div markdown="1">

```
import React from 'react';
import ReactDOM from 'react-dom/client';
import './index.css';
import App from './App';
import reportWebVitals from './reportWebVitals';
import { Provider } from 'mobx-react'
import CounterStore from './store/CounterStore';

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <Provider counterStore={CounterStore}>
    <App />
  </Provider>
);

reportWebVitals();

/*
Store는 컴포넌트에서 사용 가능하도록 Provider를 통해 App 하위에 있는 모든 컴포넌트가 Store를 props와 같이 사용할 수 있도록 설정

* Provider: MobX와 React연결
*/
```
</div>
</details>

<details>
<summary>CounterComponent.js</summary>
<div markdown="1">

```
import React, { Component } from 'react';
import { Button, Box } from '@material-ui/core';
import { inject } from 'mobx-react'

@inject('counterStore')
class CounterComponent extends Component {

  render(){

    const { counterStore } = this.props;

    return(
      <div>
        <Button variant='contained' color='primary' size='large'> - </Button>        
        
        <Box component='span' m={5}> {counterStore._count} </Box>
        
        <Button variant='contained' color='primary' size='large'> + </Button>
      </div>
    )
  }
}

export default CounterComponent;

/*
@inject('counterStore'): 
Provider로 제공되는 Store 중 counterStore를 컴포넌트가 사용할 수 있는 형태로 Props에 주입
*/
```
</div>
</details>

<br/>

#### 5. 숫자의 증가 및 감소 구현

<details>
<summary>CounterStore.js</summary>
<div markdown="1">

```
import { observable, action, makeObservable } from 'mobx';

class CounterStore {

    constructor() {
        makeObservable(this);
    }

    @observable
    _count = 5;

    get count() {
        return this._count;
    }

    @action
    increment() {
        this._count ++;
    }

    @action
    decrement() {
        this._count --;
    }
}

export default new CounterStore;

/*
@action: 
observable data는 action이 붙은 method에서 변경되어야 한다.

get: 
get method 통해 observable data를 외부에 제공하게 되면, 컴포넌트에서 props와 같이 사용가능
-> before: CounterStore._count / after: CounterStore.count
*/
```
</div>
</details>

<details>
<summary>CounterComponent.js</summary>
<div markdown="1">

```
import React, { Component } from 'react';
import { Button, Box } from '@material-ui/core';
import { inject, observer } from 'mobx-react'

@inject('counterStore')
@observer
class CounterComponent extends Component {

  render(){

    const { counterStore } = this.props;

    return(
      <div>
        <Button 
          onClick={() => counterStore.decrement()}
          variant='contained' color='primary' size='large'> - </Button>        
        
        <Box component='span' m={5}> {counterStore.count} </Box>
        
        <Button 
          onClick={() => counterStore.increment()}
          variant='contained' color='primary' size='large'> + </Button>
      </div>
    )
  }
}

export default CounterComponent;

/*
@inject('counterStore'): 
Provider로 제공되는 Store 중 counterStore를 컴포넌트가 사용할 수 있는 형태로 Props에 주입

@observer:
setState와 비슷한 개념으로 observable을 통해 관리되는 state를 react component에 적용
*/
```
</div>
</details>

___

#### Source Code. <br/>
[Github](https://github.com/HongDaye71/mobX_-)