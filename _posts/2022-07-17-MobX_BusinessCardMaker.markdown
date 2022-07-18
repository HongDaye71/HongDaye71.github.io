---
layout: post
title:  MobX-React | Business Card Maker
date:   2022-05-24 12:38:35 +0300
image:  '/images/MobX.png'
tags:   [MobX]
---
<br/>

# MobX-React | Business Card Maker<br/>
## Contents <br/>
1. 소개<br/>
2. Business Card Maker 구조<br/>
3. Business Card Maker에 MobX적용<br/>
    1. useState를 통해 생성한 로컬변수를 전역변수로 변경<br/>
    2. prop 전달 최소화<br/>
___

## :star: 1. 소개<br/>
본 포스팅에서는 [직전 포스팅과 동일한 이유로](https://hongdaye71.github.io/blog/mobx-youtubeclone)데코레이터를 사용하지 않고 함수형 컴포넌트에 MobX를 적용하는 과정을 다룹니다. <br/>

MobX를 적용할 예제로는 드림코딩의 리액트 강의에서 다루어진 Business Card Maker를 사용하며 MobX적용 전 프로젝트 구조를 먼저 설명하고, 로컬변수를 전역변수로 변경하는 과정을 작성한 뒤에 props전달을 최소화 하는 과정에서 MobX API를 사용한 부분과 사용하지 않은 부분, 그리고 그 이유를 작성하고자 합니다.

<span style="color:#D3D3D3">*작성자는 주니어 개발자 입니다. 미흡한 부분이 많으니 잘못된 점은 지적 부탁드립니다*</span>

___

## :card_index: 2. Business Card Maker 구조<br/>
기존의 Business Card Maker는 아래와 같은 기능 및 구조를 갖는다<br/>

<span style='background-color:#fff5b1'>Project Features</span> <br/>
(1) Sign in with Auth Provider (Using Firebase)<br/>
(2) Add and Delete Card<br/>
(3) Write, Read, Update and Delete data in realtime (Using Firebase)<br/>
(4) Upload image (Using Cloudinary)<br/>

<span style='background-color:#fff5b1'>Project Structure</span> <br/>
(1) App에서 useState를 통해 videos,selectedVideo 상태관리<br/>
    videos: 시작페이지와 비디오 검색 및 시청 시 렌더링되는 비디오 목록<br/>
    selectedVideo: 클릭된 비디오 값<br/>

(2) Youtube파일 생성 후 mostPopular(),search() fetch Web APIs작성<br/>
    mostPopular(): 인기있는 비디오 25개 목록을 받아오는 API fetch<br/>
    search(): 검색한 키워드에 맞추어 비디오 목록을 받아오는 API fetch<br/>

(3) App에서 mostPopular(),search()를 통해 videos,selectedVideo 상태변경<br/>

(4) SearchHeader(), VideoDetail(), VideoItem(), VideoList() 생성<br>
    SearchHeader: 비디오 검색창 HTML생성, 검색키워드를 search함수에 저장<br>
    VideoDetail: 비디오 재생화면 HTML생성<br>
    VideoItem: VideoList를 구성하는 VideoItem HTML생성<br>
    VideoList: videos를 VideoItem에 전달하여 비디오 목록 생성<br>

(5) App에서 SearchHeader() ,VideoDetail(), VideoList()에 상태 및 상태관리 메소드 전달<br>

