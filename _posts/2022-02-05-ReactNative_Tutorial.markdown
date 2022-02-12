---
layout: post
title:  React Native Study 01
date:   2022-02-04 15:01:35 +0300
image:  '/images/ReactNative.png'
tags:   [React Native, App Development]
---

## Contents <br/>
1. React Native란?<br/>
2. React Native설치<br/>
3. 


* 스피드잡의 채널의 리액트 네이티브 기본강좌 강의자료를 바탕으로 공부한 내용을 정리하는 포스팅입니다 (채널에서 언급되지 않은 내용이 일부 포함되어 있음)

* [스피드잡스 유투브채널 바로가기](https://www.youtube.com/channel/UCoIGXCqf2U1dTetloCYF46Q)

* [Tutorial Video](https://www.youtube.com/watch?v=Sr5UOR4llXY&list=PL60Uti4nULBN7EQYmgjksXJXnkufo0m-9)

___

## React Native란?<br/>
React Native는 페이스북에서 만든 오픈소스 모바일 어플리케이션 프레임워크이다. JavaScript로 개발이 가능하며 하나의 프로그래밍 언어로 IOS와 Android 모바일 앱을 동시에 개발할 수 있다.<br/>

풀어서 설명하면, 모바일 어플리케이션 개발을 위해 Android에서는 Kotlin과 Java를 사용하고 IOS는 Objective-C와 Swift를 일반적으로 사용한다. 이렇게 모바일 플랫폼 회사에서 정식으로 권장하는 기본 언어와 프레임워크로 개발한 앱을 Native App이라 하는데, 이는 각각의 OS에 최적화 되어 있어 속도가 빠르고 개발자가 원하는 모든 기능을 구현할 수 있다는 장점이 있지만 회사 입장에서 두 배의 개발자가 필요하다는 단점이 있다. <br/>

이를 해결하기 위해 등장한 것이 Hybrid App이다. 이는 React Native와 같은 프레임워크를 통해 개발된 앱으로 개발자가 하나의 프로그래밍 언어(JavaScript)로 앱을 개발하면 IOS와 Android에서 자동으로 Object-C나 Kotlin등으로 변환하여 앱을 구동시킨다. <br/>

Hybrid App을 위한 프레임워크에는 React Native외에도 Xamarin, Native Script, Flutter 등이 있다.

___

## React Native설치<br/>
- Expo CLI를 사용하여 설치<br/>
    * Expo :  React Native사용 시 개발,구축,배포 과정이 빠르게 진행될 수 있도록 도와주는 툴<br/>

    1. Node.js 설치<br/>
        (1) [사이트 접속 후 LTS Ver Download](https://nodejs.org/en/)<br/>
        (2) node -v (설치여부 확인)<br/>

        * Node.js : V8엔진으로 빌드된 JavaScript런타임<br/>
            * (런타임 : 프로그래밍 언어가 구동되는 환경)<br/><br/>

    2. Expo설치 <br/>
        (1) npm install -g expo-cli<br/>

        * NPM : Node Package Manager의 약자로, Node.js에서 사용 가능한 모듈을 패키지화 하여 모아놓고 개발자가 프로젝트에 사용하는 모듈을 편하게 install하고 관리할 수 있도록 돕는 패키지 매니저<br/><br/>

    3. 프로제트 실행<br/>
        (1) 프로젝트 설치경로 지정 : 

            ```
            dir #현재경로 확인
            cd Expo #경로지정

            ``` 

        (2) 프로젝트 생성 및 실행 : 
        
            ```
            pip init expoTest
            #프로젝트 폴더 생성
            #이후 blank, blank(TypeScript), tabs 을 선택하라는 화면이 뜨면 택1 (본인은 blank선택)

            cd expoTest 
            npm strart
            #프로젝트 폴더에 들어간 뒤 실행

            ``` 
    <br/><br/>
    
    4. 휴대폰으로 연결<br/>
        (1) 휴대폰과 PC를 동일한 네트워크에 연결<br/>
        (2) 휴대폰 내 Expo go 어플 설치 후 회원가입<br/>
        (3) PC_Expo 좌측 하단에 QR코드 스캔하여 휴대폰으로 접속<br/><br/>


    5. 안드로이드 화면 가상실행<br/>
        * 본인은 Iphone 사용자로 Android 화면은 가상으로 실행하여 확인

        (1) [Android Studion Download](https://developer.android.com/studio?gclid=Cj0KCQiA0p2QBhDvARIsAACSOOMW9pVBHxCyXdLhzdMIvCRSPOleHFa4Wj3sUoD3zzRYkq4Ot4QOezcaAgZZEALw_wcB&gclsrc=aw.ds)<br/>
        (2)


        
            
