---
layout: post
title:  React/MouseMoveEvent
date:   2023-01-05 12:38:35 +0300
image:  '/images/Posting/React/TodoList.png'
tags:   [React]
---

# React Project - TodoList

## Description <br/>
* WebAPIs를 기반으로 마우스에 따라 이동하는 원 구현<br/>

___

* 드림코딩 리액트 개념정리-클론코딩 강의의 실전 프로젝트 내용을 정리하는 포스팅입니다.<br/>
* 저작권 이슈로 강의내용은 다루지 않습니다. 실전 프로젝트를 진행하며 스스로 코드를 리뷰하는 포스팅입니다.<br/>

___

<details>
<summary>App.jsx</summary>
<div markdown="1">

```javaScript

import './App.css';
import React, {useState} from 'react';


export default function App() {
    const [x, setX] = useState();
    const [y, setY] = useState(); //초기값은 0으로 설정

    return(
        <div className = 'container' onPointerMove={(event) => 
        {
            setX(event.clientX);
            setY(event.clientY);
        }}>
            <div className = 'pointer' style={% raw %}{{transform: `translate(${x}px, ${y}px)`}}{% endraw %} />
        </div>
    )
}

```
</div>
</details>

<details>
<summary>App.css</summary>
<div markdown="1">

```css

.container {
    width: 100vw;
    height: 100vh;
}

.pointer {
    position: absolute;
    background-color: salmon;
    border-radius: 50%;
    width: 25px;
    height: 25px;
    left: -15px;
    top: -15px;
}

```
</div>
</details>

1. <span style='background-color: #fff5b1'>심볼명 일괄변경</span> : 마우스 우클릭 - Rename Symbol
* Symbol : ES6부터 추가된 타입의 값으로 이름 충돌의 위험없이 속성(Property)의 키(Key)로 쓰기위해 사용할 수 있는 값









