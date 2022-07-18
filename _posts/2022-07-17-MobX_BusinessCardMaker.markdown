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
본 포스팅에서는 [직전 포스팅과 동일한 이유로](https://hongdaye71.github.io/blog/mobx-youtubeclone)   

데코레이터를 사용하지 않고 함수형 컴포넌트에 MobX를 적용하는 과정을 다룹니다. <br/>

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

**Login Page**<br/>
  페이지목적: 사용자 로그인<br/>
  세부기능: Google, Github 로그인 연동 (Firebase사용) / 로그인 혹은 PC에 기존 로그인 정보가 남아있는 경우 React Router를 통해 Main Page이동<br/>

**Main Page**
  *Card Maker*<br/>
  페이지목적: 이름, 회사, 이메일, 사진 등 명함 디자인에 필요한 사용자 정보 입력<br/>
  세부기능: 명함생성 및 삭제 / 동일 아이디로 로그인 시 사용자 정보유지(Firebase사용)<br/>
  *Card Preview*<br/>
  페이지목적: Card Maker에서 입력된 정보를 바탕으로 명함 디자인 샘플출력<br/>
  새부기능: 동일 아이디로 로그인 시 명함 디자인 정보유지(Firebase사용)<br/>

<span style='background-color:#fff5b1'>Source Code Structure</span> <br/>

(1) Login Page<br/>
  코드구조: 
  - AuthService Component 생성 (Firebase의 로그인 관련 API기능 포함 / API기능은 service폴더 내 관리)
  - 최상위 Component에서부터 AuthService를 prop으로 전달
  - Login Component는 AuthService를 사용하여 로그인화면 구현

<details>
<summary>auth_service.jsx</summary>
<div markdown="1">

```javascript
import firebase from 'firebase';
import firebaseApp from './firebase'

class AuthService {
    login(providerName) {
        const authProvider = new firebase.auth[`${providerName}AuthProvider`]();
        return firebaseApp.auth().signInWithPopup(authProvider);
    }

    logout() {
        firebase.auth().signOut();
    }

    onAuthChange(onUserChanged) {
        firebase.auth().onAuthStateChanged(user => {
            onUserChanged(user);
        })
    }
}

export default AuthService
```
</div>
</details>

<details>
<summary>login.jsx</summary>
<div markdown="1">

```javascript
import React, { useEffect } from 'react';
import Footer from '../footer/footer';
import Header from '../header/header';
import styles from './login.module.css';
import { useNavigate } from 'react-router-dom';

const Login = ({ authService }) => {
  const navigate = useNavigate();
  const goToMaker = (userId) => {
    navigate(
      '/maker', 
      { state: {id: userId} });
  }

  //사용자 정보변경이 발생하거나, 기존 로그인 정보가 남아있는 경우 MainPage이동 (사용자 아이디 전달)
  useEffect(() => {
    authService.onAuthChange(
      user => {user && goToMaker(user.id) 
    })
  })

  //로그인 시 MainPage이동 (사용자 아이디 전달)
  const onLogin = event => {
    authService 
      .login(event.currentTarget.textContent) 
      .then(data => goToMaker(data.user.uid));
  };

  return (
    <section className={styles.login}>
      <Header />
      <section>
        <h1>Login</h1>
        <ul className={styles.list}>
          <li className={styles.item}>
            <button className={styles.button} onClick={onLogin}>Google</button>
          </li>
          <li className={styles.item}>
            <button className={styles.button} onClick={onLogin}>
              Github
            </button>
          </li>
        </ul>
      </section>
      <Footer />
    </section>
  );
};

export default Login;
```
</div>
</details>


