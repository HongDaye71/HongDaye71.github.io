---
layout: post
title:  MobX-React | Youtube Clone
date:   2022-05-24 12:38:35 +0300
image:  '/images/MobX.png'
tags:   [MobX]
---
<br/>

# MobX-React|Youtube Clone<br/>
## Contents <br/>
1. 소개<br/>
2. Youtube Clone Project구조<br/>
3. Video Store생성<br/>
4. Store생성<br/>
5. Observable Data사용<br/>
6. Warning, Error수정<br/>

* 본 포스팅은 드림코딩의 리액트 강의에서 다루어진 Youtube Clone Project에 MobX 상태관리 라이브러리를 적용하는 과정을 다룹니다

___

## :star: 소개<br/>
리액트를 사용해서 프론트 개발을 할 때에는 클래스형과 함수형 컴포넌트를 사용할 수 있다. 과거에는 함수형 컴포넌트에서 상태관리 및 라이프사이클 메소드가 제공되지 않았기 때문에 클래스 컴포넌트를 주로 사용했으나 2019년 v16.8부터 리액트에서 함수형 컴포넌트에 훅(hook)을 지원해주면서 현재는 공식 문서에서 함수형 컴포넌트와 훅을 함께 사용할 것을 권장하고 있다. 개발자들 또한 클래스 보다는 함수형 컴포넌트를 사용하는데, 이유는 아래와 같다.<br/>

1. <span style='background-color:#fff5b1'>코드가 간결하다</span> <br/>
    클래스 컴포넌트는 클래스와 렌더함수 선언 및 extend를 통한 컴포넌트 상속 등 선언 방식부터 함수형 컴포넌트에 비해 작성할 코드가 많다.

```javascript
//Function Component
import { useState} from 'react';

function App() {
    const [state, setState] = useState([]);
    return(
        <div>
            <OtherFunction
                state={state}>
            />
        </div>
    );
}
```
<br/>

```javascript
//Class Component
import React, {Component} from 'react'

class App extends Component{
    state = {
        state: null,
    };
    
    render() {
        return (
        <div>
            <OtherFunction
                state={this.state.state}>
            />
        </div>
        );
    }
}
```

<br/>

2. <span style='background-color:#fff5b1'>함수형 컴포넌트는 렌더링 결과를 보장받는다</span> <br/>
    함수형 컴포넌트는 immutable하지만, 클래스 컴포넌트는 this를 사용하기 때문에 mutable하다. 아래 예제는 this의 변경 가능한 특징으로 인해 발생할 수 있는 문제이다. 

```javascript
//Function Component
function DeleteComment(props) {
  const showAlert = () => {
    alert(`${props.user}`의 댓글을 삭제합니다.);
  };

  const handleClick = () => {
    setTimeout(showAlert, 5000);
  };

  return (
    <button onClick={handleClick}>삭제</button>
  );
}
```

<br/>

```javascript
//Class Component
class DeleteComment extends React.Component {
  showAlert = () => {
    alert(`${this.props.user}`의 댓글을 삭제합니다.);
  };

  handleClick = () => {
    setTimeout(this.showAlert, 5000);
  };
  render() {
  return (
    <button onClick={this.handleClick}>삭제</button>
  )};
}
```

<br/>
    클래스형 컴포넌트의 실행과정을 아래와 같다.










MobX를 공부하면서 대부분의 예제들이 클래스기반의 데코레이터를 사용하는 것을 확인했습니다. 


- 현재는 클래스 컴포넌트 + 데코레이터를 다루는 예제가 많음
- 클래스 컴포넌트의 단점 / 데코레이터는 클래스 컴포넌트에서만 사용 가능하다는 점 /데코레이터가 레거시라는 점
- 따라서 본 포스팅에서는 데코레이터를 사용하지 않고 Function Component에 MobX를 적용해 보도록 함

___

## :mag: Youtube Clone Project구조<br/>
- 기존의 Youtube Clone Project는 --한 구조로 되어있음
- 현재는 상태가 많지 않아 굳이 MobX를 통해 관리하지 않아도 되지만, 후에 프로젝트가 복잡해지면 props로 -- 하는 것은 -- 하다는 문제가 있음

___

## :mag: Video Store생성<br/>
- Observable Data를 관리하는 Video Store생성 후 MostPopular, SelectVideo와 같은 Function을 이동시킴
- youtube도 이동시킴
- 데코레이터를 사용하지 않기 때문에 --함 (runInAction제외)

```javascript
```

* [MobX 기초정리]()<br/>
포스팅 흐름 참고: https://hyeok999.github.io/2020/04/16/mobx-hooks-market/#a3

___

## :mag: Store생성<br/>
- 폴더에 생길 모든 스토어들을 한 곳을 통해서 불러들이게끔 하기 위해서 custom Hook을 다음과 같이 작성 (현재 프로젝트에서는 반드시 필요하지 않으나 프로젝트가 커질경우 이와 같이 관리하는 것이 좋음)

```javascript
```
___

## :mag: Observable Data사용<br/>
- App에서 Observable Data 사용

___

## :mag: Warning, Error수정<br/>
- 아래와 같은 경고문구 발생 / 해결과정
since strict-mode is enabled, changing (observed) observable values without using an action is not allowed 

- 영상 클릭시 오류 발생 / 원인
___

#### Source Code. <br/>
* [Github](https://github.com/HongDaye71/YoutubeClone)<br/>
* [Github(MobX)](https://github.com/HongDaye71/MobX_YoutubeClone)<br/>
