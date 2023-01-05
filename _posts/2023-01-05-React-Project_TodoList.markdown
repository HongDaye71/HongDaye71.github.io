---
layout: post
title:  React/TodoList
date:   2023-01-05 12:38:35 +0300
image:  '/images/Posting/React/TodoList.png'
tags:   [React]
---

# React Project - TodoList

## Description <br/>
* 하루목표를 작성하고 관리할 수 있는 웹서비스 구현<br/>

## Description <br/>
1. 리스트 구현하기 <br/>
2. 추가하기 구현하기 <br/>
3. 삭제하기 구현하기 <br/>
4. 필터 적용하기 <br/>
5. 스타일링 적용하기 <br/>
6. 다크모드 구현하기 <br/>
7. 아이템 저장하기 <br/>
___

* 드림코딩 리액트 개념정리-클론코딩 강의의 실전 프로젝트 내용을 정리하는 포스팅입니다.<br/>
* 저작권 이슈로 강의내용은 다루지 않습니다. 실전 프로젝트를 진행하며 스스로 코드를 리뷰하는 포스팅입니다.<br/>

___

### 1. 리스트 구현하기

<details>
<summary>App.jsx</summary>
<div markdown="1">

```javaScript

import './App.css';
import TodoList from './components/TodoList/TodoList';

function App() {
    return <div> 
        <TodoList />
    </div>
}

```
</div>
</details>

<details>
<summary>TodoList.jsx</summary>
<div markdown="1">

```javaScript

import React, {useState} from 'react';

export default function TodoList() {
    const [todos, setTodos] = useState([
        {id: '123', text: '장보기', status: 'active'},
        {id: '124', text: '공부하기', status: 'active'}
        ])
    return <section> 
        <ul>
            {
                todos.map((item) => (
                    <li key={item.id}>{item.text}</li>
                ))
            }
        </ul>
    </section>
}


```
</div>
</details>

1. Components 폴더생성 <br/>
2. TodoList 폴더생성 - TodoList 파일생성 <br/>
    - PostCSS를 통해 컴포넌트별로 스타일이 적용될 예정으로 App을 구성하는 요소를 별도 컴포넌트로 관리 <br/>
3. App에서 TodoList컴포넌트 출력 <br/>
4. TodoList에서 배열생성 및 출력 <br/>

* ES7 React/Redux/GraphQL/React-Native snippets 확장자 설치 후 'rfc-엔터'를 통해 컴포넌트 기본 툴 생성가능
* useState()에서 배열을 만들기 위해 useState([])사용 - 배열을 구성하는 리스트를 {}로 입력
* section태그 : 주제별 영역들을 그룹화하기 위해 사용한다. 주로 `<ul> <ol> <li> <h1> <p>` 등의 태그를 포함한다. 일반적인 구조는 아래와 같다 <br/>

```html
<section> 
    <h1>상품소개</h1>
    <ul> 
        <li>상품1<li>
        <li>상품2<li>
        <li>상품3<li>
    </ul>
    <p>상품이 실제 이미지와 다를 수 있습니다</p>
</section>
```
___

[Git]()









