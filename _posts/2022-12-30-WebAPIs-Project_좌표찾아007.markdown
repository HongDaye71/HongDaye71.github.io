---
layout: post
title:  WebAPIs/좌표찾아007
date:   2022-08-11 12:38:35 +0300
image:  '/images/Posting/React/coordinateImg.jpg'
tags:   [Programmers]
---

# WebAPIs Project - 좌표찾아007

## Description <br/>
* WebAPIs를 기반으로 윈도우 내 마우스 좌표를 출력하는 웹서비스 구현<br/>
* 좌표는 가로,세로 선과 함께 마우스를 따라 이동함<br/>

___

* 드림코딩 브라우저101 강의의 실전 프로젝트 내용을 정리하는 포스팅입니다.<br/>
* 저작권 이슈로 강의내용은 다루지 않습니다. 실전 프로젝트를 진행하며 스스로 코드를 리뷰하는 포스팅입니다.<br/>

___

<details>
<summary>HTML</summary>
<div markdown="1">

```HTML

<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Coordinates</title>
    <script src="main.js" defer></script>
    <link rel="stylesheet" href="style.css" />
  </head>
  <body>
    <body>
      <div class="Line horizontal"></div>
      <div class="Line vertical"></div>
      <img class="target" src="img/target.png" alt="target">
      <span class="tag">Temp</span>
  </body>
  </body>
</html>

```
</div>
</details>

1. <span style='background-color: #fff5b1'>meta charset="문자셋"</span> : HTML문서의 문자 인코딩 방식을 명시함. 유니코드(Unicode)를 위한 문자셋인 UTF-8이 일반적으로 사용됨 
* 유니코드 : 전 세계의 모든 문자를 컴퓨터에서 일관되게 표현하고 다룰 수 있도록 설계된 산업 표준

2. <span style='background-color: #fff5b1'>meta name='viewport'</span> : 현재 사용자가 보고 있는 컴퓨터 화면의 영역을 나타냄

3. <span style='background-color: #fff5b1'>클래스 자동생성</span> : .Line.horizontal 입력 후 Tab키를 클릭하면 자동생성 됨 (img태그로 target클래스를 생성하고 싶은 경우, img.target 입력 후 Tab키를 클릭)

4. <span style='background-color: #fff5b1'>코드설명</span> : 웹서비스를 구성하는 가로 선, 세로 선, 이미지, 좌표텍스트 클래스 생성


___


<details>
<summary>CSS</summary>
<div markdown="1">

```CSS

body {
    background-color: black;
}

.Line {
    position: absolute;
    background-color: white;
}

.horizontal {
    width: 100%;
    height: 1px;
    top: 50%;
}

.vertical {
    height: 100%;
    width: 1px;
    left: 50%;
}

.target {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
}

.tag {
    color: white;
    position: absolute;
    top: 50%;
    left: 50%;
    font-size: 30px;
    transform: translate(20px, 20px);
}

```
</div>
</details>

1. <span style='background-color: #fff5b1'>transform: translate(-50%, -50%);</span> : 자신을 기준으로 자신이 가진 가로, 세로 너비의 몇 퍼센트만큼 어느 방향으로 이동할지 설정
* transform : Flash, JavaScript를 사용하지 않고 요소를 애니메이션 하거나 상호작용의 효과를 적용하고자 할 때에 사용</br>
* translate : X,Y축을 따라 지정된 거리만큼 요소를 이동시킬 때 사용 (Y축은 생략할 수 있으며 자동으로 0값이 설정됨 / translateX, translateY 함수존재)


___


<details>
<summary>JavaScript</summary>
<div markdown="1">

```JavaScript

const horizontal = document.querySelector('.horizontal');
const vertical = document.querySelector('.vertical');
const target = document.querySelector('.target');
const tag = document.querySelector('.tag');

document.addEventListener('mousemove', (event)=> {
    const x = event.clientX;
    const y = event.clientY;
    console.log(`${x} ${y}`);

    vertical.style.left = `${x}px`;
    horizontal.style.top = `${y}px`;
    target.style.left = `${x}px`;
    target.style.top = `${y}px`;
    tag.style.left = `${x}px`;
    tag.style.top = `${y}px`;
    tag.innerHTML = `${x}px, ${y}px`;
});

```

</div>
</details>

1. <span style='background-color: #fff5b1'>document.querySelector()</span> : CSS선택자를 통해 JavaScript의 DOM요소 선택 (querySelector는 Document method로 CSS의 첫 번째 선택자를 리턴)
* Document : 브라우저에 로드된 모든 웹페이지를 나태내며 DOM Tree의 진입점 역할을 함</br>

2. <span style='background-color: #fff5b1'>Element.innerHTML</span></br>
Element내에 포함된 HTML 또는 XML마크업을 가져오거나 설정함
* Element : DOM Tree는 node의 계층구조로 이루어져 있음. element는 node의 유형 중 하나로 html문서에서 ```<div> <p> <title>```과 같은 태그를 사용해 작성된 노드임

___

[Github](https://github.com/HongDaye71/WebAPIs_Coordinate/tree/main)








