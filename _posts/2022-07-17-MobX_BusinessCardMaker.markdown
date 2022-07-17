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
2. Business Card Maker Project구조<br/>
3. Business Card Maker Project에 MobX적용<br/>
    1. useState를 통해 생성한 로컬변수를 전역변수로 변경<br/>
    2. prop 전달 최소화<br/>
___

## :star: 1. 소개<br/>
본 포스팅에서는 데코레이터를 사용하지 않고 함수형 컴포넌트에 MobX를 적용하는 과정을 다룹니다. MobX를 적용할 예제로는 드림코딩의 리액트 강의에서 다루어진 Business Card Maker를 사용하며 MobX적용 전 프로젝트 구조를 먼저 설명하고, 로컬변수를 전역변수로 변경하는 과정을 작성한 뒤에 props전달을 최소화 하는 과정에서 MobX API를 사용한 부분과 사용하지 못한부분, 그리고 그 이유를 작성하고자 합니다.

<span style="color:#D3D3D3">*작성자는 주니어 개발자 입니다. 미흡한 부분이 많으니 잘못된 점은 지적 부탁드립니다*</span>

[데코레이터를 사용하지 않고 MobX를 적용하는 이유](https://hongdaye71.github.io/blog/mobx-youtubeclone)
