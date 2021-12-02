---
layout: post
title:  Figma Tutorial 01
date:   2021-12-01 15:01:35 +0300
image:  '/images/02.png'
tags:   [Design, Figma]
---

## Contents:<br/>
1. Figma란<br/>
2. Frame & Constraints<br/>
3. Image import & Overlay<br/>
4. 단축키<br/>

___

## Figma란? 
피그마(Figma)는 XD, Sketch처럼 UI 디자인을 위해 유용한 도구 중 하나이며 다음과 같은 여섯가지 특징을 갖습니다.

* 실시간 협업기능<br/>
피그마(Figma)는 여러명이 실시간으로 작업을 공유하고 편집할 수 있는 협업기능을 제공합니다.

* 폰트제공<br/>
공유한 파일에 사용한 폰트가 없을 경우, 폰트가 깨져보이는 경우가 발생합니다. 피그마(Figma)는 많은 폰트를 제공하여 별도의 폰트설치 없이 폰트가 깨져보이는 경우를 줄일 수 있습니다.

* 맥(Mac)과 윈도우(Windows)응용 소프트웨어 지원<br/>
맥과 윈도우 운영체제 모두에서 프로그램이 실행됩니다.

* 무료 프로그램<br/>
개인으로 작업할 경우, 두 명까지는 무료 사용이 가능합니다.

* 벡터 기반의 프로그램<br/>
포토샵은 비트맵 기반으로 작업물에서 픽셀이 깨져보이는 현상이 발생하지만, 피그마(Figma)는 다른 UI프로그램인 XD, Sketch처럼 벡터기반의 프로그램으로 깨짐현상이나 용량을 효율적으로 관리할 수 있습니다.

* 편리한 자동저장<br/>
인터넷에 연결을 한 후, 작업을 하면서 자동으로 저장되는 기능이 있습니다.

Click Figma [Download](https://www.figma.com/downloads/)

___

## Frame & Constraint <br/>
<img src="/images/Posting/Figma/Tutorial01_01.png" alt="Project">

* File명 변경 : 상단 툴바 중앙에서 변경<br/>
* Frame 생성 : 상단 툴바 좌측에서 세 번째 아이콘을 통해 변경<br/>
* Frame Size 및 위치변경 : 우측 Design Pannel의 Frame영역에서 변경<br/>
* Frame View Point 중앙배치 : Shift + 2<br/>
* Frame 이름 변경 : Command(Ctrl)+R <br/>

<img src="/images/Posting/Figma/Tutorial01_02.png" alt="Project">

* Constraints란 : Frame크기에 따라 안에 있는 component의 위치와 크기를 통제할 수 있도록 하는 기능 
(ex.Frame:Iphone의 Background, component:Iphone내 상단 시간과 와이파이,충전표시 요소라고 했을 때 Iphone version에 따라 Frame의 크기가 어떻게 변경되더라도 Component는 정해진 위치에 고정되도록 하는 기능)<br/>

* Constraints기능 :<br/>
1. Horizental or Vertical 설정
2. Left, Right, Left and Right : Frame기준 Component의 고정위치 설정<br/>
3. Center : Frame기준 Component가 중앙에 위치하도록 설정<br/>
4. Scale : Frame기준 Component의 크기조정<br/>

* Constraints사용 : <br/>
1. Component를 Frame내에 배치<br/>
2. Component의 Constraints를 원하는 기능으로 선택 후 사용<br/>

<img src="/images/Posting/Figma/Tutorial01_03.png" alt="Project">

* Constraints사용예제 : <br/>
1. Frame 내에 Imgae1, Image2 배치 <br/>
2. Image1(Apple logo) / Imgae2(Check Icon) : Constraints를 Right, Top으로 설정 / Left, Top으로 설정
3. Frame크기 변경하여 Image1, Imgae2가 Right, Top/ Left, Top에 고정되어 있는 것을 확인

___

## Image import & Overlay<br/>

* Image import의 세 가지 방법 :<br/>
1. Local Image사용 : Desing Pannel -> Fill -> Image<br/>
2. Local Image사용 : Shift + Command(Ctrl)+ K<br/>
3. 무료 이미지 제공 서비스 사용 : Plugin 설치 -> Plugin에서 다운로드 받은 위젯선택 후 원하는 이미지 선택 <br/>

<img src="/images/Posting/Figma/Tutorial01_04.png" alt="Project">
<img src="/images/Posting/Figma/Tutorial01_05.png" alt="Project">

* Image Overlay :<br/>
<img src="/images/Posting/Figma/Tutorial01_05.png" alt="Project">
1. Desing Pannel -> Fill -> 플러스 버튼 클릭 -> 색상지정,Linear선택 -> Frame에서 Overlay방향설정

___

## 단축키 <br/>
1. 복사 : Shift + Option(alt)<br/>
2. 객체 그룹화 : Command(Ctrl) + G<br/>
