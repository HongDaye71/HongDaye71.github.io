---
layout: post
title:  React/좌표찾아007
date:   2022-08-11 12:38:35 +0300
image:  '/images/React/좌표찾아007.jpg'
tags:   [Programmers]
---

# React Project - 좌표찾아007

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

* 드림코딩 브라우저101 강의의 실전 프로젝트 내용을 정리하는 포스팅입니다.<br/>
* 저작권 이슈로 강의내용은 다루지 않습니다. 실전 프로젝트를 진행하며 스스로 코드를 리뷰하는 포스팅입니다.<br/>

___

<details>
<summary>HTML</summary>
<div markdown="1">

```javascript

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

1. <span style='background-color: #fff5b1'>meta charset="문자셋"</span></br>
HTML문서의 문자 인코딩 방식을 명시함. 유니코드(Unicode)를 위한 문자셋인 UTF-8이 일반적으로 사용됨 
* 유니코드 : 전 세계의 모든 문자를 컴퓨터에서 일관되게 표현하고 다룰 수 있도록 설계된 산업 표준

2. <span style='background-color: #fff5b1'>meta name='viewport'</span></br>
현재 사용자가 보고 있는 컴퓨터 화면의 영역을 나타냄

3. <span style='background-color: #fff5b1'>클래스 자동생성</span></br>
.Line.horizontal 입력 후 Tab키를 클릭하면 자동생성 됨 (img태그로 target클래스를 생성하고 싶은 경우, img.target 입력 후 Tab키를 클릭)










