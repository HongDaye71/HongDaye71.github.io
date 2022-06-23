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

## :mag: 소개<br/>
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
