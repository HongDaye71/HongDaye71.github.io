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
    1. useState를 통해 생성한 지역변수를 전역변수로 변경<br/>
    2. props 전달 최소화<br/>

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
<span style='background-color:#f6f8fa'>Login Page</span><br/>
  페이지목적: 사용자 로그인<br/>
  세부기능: Google, Github 로그인 연동 (Firebase사용) / 로그인 혹은 PC에 기존 로그인 정보가 남아있는 경우 React Router를 통해 Main Page이동<br/>

<span style='background-color:#f6f8fa'>Main Page</span><br/>
  *Card Maker*<br/>
  페이지목적: 이름, 회사, 이메일, 사진 등 명함 디자인에 필요한 사용자 정보 입력<br/>
  세부기능: 명함생성 및 삭제 / 동일 아이디로 로그인 시 사용자 정보유지(Firebase사용)<br/>
  *Card Preview*<br/>
  페이지목적: Card Maker에서 입력된 정보를 바탕으로 명함 디자인 샘플출력<br/>
  새부기능: 동일 아이디로 로그인 시 명함 디자인 정보유지(Firebase사용)<br/>

<span style='background-color:#fff5b1'>Source Code Structure</span> <br/>
<span style='background-color:#f6f8fa'>Login Page</span><br/>
AuthService Component 생성 (Firebase의 로그인 관련 API기능 포함)<br/>
최상위 Component에서부터 AuthService를 prop으로 전달<br/>
Login Component는 AuthService를 사용하여 로그인화면 구현<br/>

<details>
<summary>auth_service.jsx</summary>
<div markdown="1">

```
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

```
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

<br/>

<span style='background-color:#f6f8fa'>Main Page<span>

*Card Maker*<br/>
Maker에서 cards, userId 상태생성 및 카드추가, 삭제기능 생성하여 Editor에 props로 전달<br/>
Editor는 위 props를 Card_edit_form과 CardAddForm에 map을 통해 전달<br/>
Card_edit_form와 CardAddForm은 전달받은 props를 통해 Card Maker UI생성<br/>

*Card Preview*<br/>
Maker에서 Preview에 cards를 props로 전달<br/>
Preview는 위 props를 Card에 map을 통해 전달<br/>
Cards는 전달받은 props를 통해 Card Preview UI생성<br/>

<details>
<summary>maker.jsx</summary>
<div markdown="1">

```
import { useState } from 'react';
import Header from '../header/header'
import Footer from '../footer/footer'
import React, { useEffect } from 'react';
import styles from './maker.module.css';
import { useNavigate, useLocation } from 'react-router-dom';
import Editor from '../editor/editor';
import Preview from '../preview/preview';

const Maker = ({ FileInput, authService, cardRepository }) => {
    const location = useLocation();
    const [cards, setCards] = useState({});
    const [userId, setUserId] = useState(location.state.id);

    const navigate = useNavigate();

    const onLogout = () => {
        authService.logout();
    };

    //사용자 아이디 변경시 마다 DB정보 업데이트
    useEffect(() => {
        if(!userId) {
            return;
        }
        const stopSync = cardRepository.syncCards(userId, cards => {
            setCards(cards);
        })
        return () => stopSync();
    }, [userId]);

    //로그인 구현
    useEffect(() => {
        authService.onAuthChange(user => {
            if(user) {

            } else {
                navigate('/');
            }
        });
    });

    //카드생성
    const createOrUpdateCard = card => {
        setCards(cards => {
            const updated = { ...cards };
            updated[card.id] = card; 
            return updated; 
            });
        cardRepository.saveCard(userId, card); 
    }

    //카드삭제
    const deleteCard = card => {
        setCards(cards => {
            const updated = { ...cards };
            delete updated[card.id] 
            return updated; 
            });
        cardRepository.removeCard(userId, card);
    }

    return(
        <section className={styles.maker}>
            <Header onLogout={onLogout}/>
            <div className={styles.container}>
                <Editor 
                    FileInput={FileInput}
                    cards={cards} 
                    addCard={createOrUpdateCard} 
                    updateCard={createOrUpdateCard} 
                    deleteCard={deleteCard}/>
                <Preview cards={cards}/>
            </div>
            <Footer />
        </section>
    )
}

export default Maker;
```
</div>
</details>

<details>
<summary>editor.jsx</summary>
<div markdown="1">

```
import React from 'react';
import CardAddForm from '../card_add_form/card_add_form';
import Card_edit_form from '../card_edit_form/card_edit_form';
import styles from './editor.module.css'

const Editor = ({ FileInput, cards, addCard, updateCard, deleteCard }) => 
    <section className={styles.editor}>
        <h1 className={styles.title}>Card Maker</h1>
        {Object.keys(cards).map(key => (
            <Card_edit_form 
            key={key} 
            FileInput={FileInput}
            card={cards[key]} 
            updateCard={updateCard} 
            deleteCard={deleteCard}/>
        ))}
        <CardAddForm FileInput={FileInput} onAdd={addCard}/>
    </section>

export default Editor;
```
</div>
</details>

<details>
<summary>card_edit_form.jsx</summary>
<div markdown="1">

```
import React, { useRef } from 'react';
import Button from '../button/button';
import styles from './card_edit_form.module.css'

const Card_edit_form = ({ FileInput, card, updateCard, deleteCard }) => {
    const nameRef = useRef();
    const companyRef = useRef();
    const themeRef = useRef();
    const titleRef = useRef();
    const emailRef = useRef();
    const messageRef = useRef();

    const {
        name,
        company,
        theme,
        title,
        email,
        message,
        fileName,
    } = card;
    
    const onFileChange = file => {
        updateCard({
            ...card,
            fileName: file.name,
            fileURL: file.url,
        })
    }
    
    const onChange = (event) => {
        if (event.currentTarget == null) {
            return;
        }
        event.preventDefault();
        updateCard({ 
            ...card, /
            [event.currentTarget.name]: event.currentTarget.value,})}

    const onSubmit = (event) => {deleteCard(card);}

    return (
        <form className={styles.form}>
            <input className={styles.input} type="text" name="name" ref={nameRef} value={name} onChange={onChange}/>
            <input className={styles.input} type="text" name="company" ref={companyRef} value={company} onChange={onChange}/>
            <select className={styles.select} name="theme" ref={themeRef} value={theme} onChange={onChange}>
                <option value="light">light</option>
                <option value="dark">dark</option>
                <option value="colorful">colorful</option>
            </select>
            <input className={styles.input} type="text" name="title" ref={titleRef} value={title} onChange={onChange}/>
            <input className={styles.input} type="text" name="email" ref={emailRef} value={email} onChange={onChange}/>
            <textarea className={styles.textarea} name="message" ref={messageRef} value={message} onChange={onChange}></textarea>
            <div className={styles.fileInput}>
                <FileInput name={fileName} onFileChange={onFileChange}/>
            </div>
            <Button name='Delete' onClick={onSubmit} />
        </form>
    );
};

export default Card_edit_form;

```
</div>
</details>

<details>
<summary>card_add_form.jsx</summary>
<div markdown="1">

```
import React, { useRef, useState } from 'react';
import Button from '../button/button';
import styles from './card_add_form.module.css'

const CardAddForm = ({ FileInput, onAdd }) => {
    const formRef = useRef();
    const nameRef = useRef();
    const companyRef = useRef();
    const themeRef = useRef();
    const titleRef = useRef();
    const emailRef = useRef();
    const messageRef = useRef();
    const [file, setFile] = useState({ fileName: null, fileURL: null });

    const onFileChange = file => {
        setFile({
            fileName: file.name,
            fileURL: file.url,
        });
    }

    const onSubmit = (event) => {
        event.preventDefault();
        const card = {
            id: Date.now(),
            name : nameRef.current.value || '',
            company : companyRef.current.value || '',
            theme : themeRef.current.value,
            title : titleRef.current.value || '',
            email : emailRef.current.value || '',
            message : messageRef.current.value || '',
            fileName: file.fileName || '',
            fileURL: file.fileURL || '',
        };
        formRef.current.reset(); 
        setFile({ fileName: null, fileURL: null })
        onAdd(card);
    }

    return (
        <form ref={formRef} className={styles.form}>
            <input ref={nameRef} className={styles.input} type="text" name="name" placeholder="Name" />
            <input ref={companyRef} className={styles.input} type="text" name="company" placeholder="Company" />
            <select  ref={themeRef} className={styles.select} name="theme" placeholder="Theme">
                <option placeholder="light">light</option>
                <option placeholder="dark">dark</option>
                <option placeholder="colorful">colorful</option>
            </select>
            <input ref={titleRef} className={styles.input} type="text" name="title" placeholder="Title" />
            <input ref={emailRef} className={styles.input} type="text" name="email" placeholder="Email" />
            <textarea ref={messageRef} className={styles.textarea} name="message" placeholder="Message"></textarea>
            <div className={styles.fileInput}>
                <FileInput name={file.fileName} onFileChange={onFileChange}/>
            </div>
            <Button name='Add' onClick={onSubmit} />
        </form>
    );
};

export default CardAddForm;
```
</div>
</details>


<details>
<summary>preview.jsx</summary>
<div markdown="1">

```
import React from 'react';
import styles from './preview.module.css';
import Card from '../card/card';

const Preview = ({ cards }) => 
    <section className={styles.preview}>
        <h1 className={styles.title}>Card Preview</h1>
        <ul className={styles.cards}>
            {Object.keys(cards).map(key => (
                <Card             
                key={key} 
                card={cards[key]}  />
            ))}
        </ul>
    </section>

export default Preview;
```
</div>
</details>

<details>
<summary>card.jsx</summary>
<div markdown="1">

```
import React from 'react';
import styles from './card.module.css'

const DEFAULT_IMAGE = '/images/default_logo.png'

const Card = ({ card }) => {
    const {name, company, title, email, message, theme, fileName, fileURL} = card;
    const url = fileURL || DEFAULT_IMAGE; //fileURL이 없다면 DEFAULT_IMAGE사용

    return(
        <li className={`${styles.card} ${getStyles(theme)}`}>
            <img className={styles.avatar} src={url} alt="profile photo" />
            <div className={styles.info}>
                <h1 className={styles.name}>{name}</h1>
                <p className={styles.company}>{company}</p>
                <p className={styles.title}>{title}</p>
                <p className={styles.email}>{email}</p>
                <p className={styles.message}>{message}</p>
            </div>
        </li>
    );
};

function getStyles(theme) {
    switch (theme) {
        case 'dark':
            return styles.dark;
        case 'light':
            return styles.light;
        case 'colorful':
            return styles.colorful;
        default:
            throw new Error(`unkown theme: ${theme}`);
    }
}

export default Card;
```
</div>
</details>

<br/>

*전체 소스코드는 하단의 깃허브 링크를 통해 확인가능*

___

## :books: 3. Business Card Maker에 MobX적용
기존의 예제는 Maker에서 cards, userId, 카드추가, 삭제기능을 생성하여 Editor와 Preview에 props로 전달한다. 이후 Editor와 Preview는 Card_edit_form, CardAddForm, Card에 다시 props를 전달한다. 이와같이 props를 반복적으로 전달하여 사용할 경우, 데이터 공유가 필요한 경우에 제약이 발생할 뿐만 아니라 프로젝트의 규모가 커질수록 최하위 컴포넌트에 prop 한 개를 전달하기 위해 최상위 컴포넌트에서 부터 반복적으로 prop을 전달하는 코드가 추가되어 코드 가독성이 떨어진다.

따라서 기존에 Maker에서 지역변수로 관리하던 cards, userId, 카드추가, 삭제기능을 MobX를 통해 전역변수로 관리하고자 한다. 추가로 Login에서 지역변수로 관리하던 userId 또한 전역변수로 관리하고자 한다. 

### :mag: 3.1 useState를 통해 생성한 지역변수를 전역변수로 변경<br/>

<span style='background-color:#fff5b1'>Store Folder 내 MakerStore생성하여 cards, userId, 카드추가, 삭제기능 작성<span>

```
import { runInAction, observable  } from "mobx";

const makerStore = observable({
    cards : {}, 
    userId : '',

    createOrUpdateCard (card) {
        runInAction(() => {
            const updated = { ...this.cards };
            updated[card.id] = card; 
            this.cards = updated
        })
    },

    deleteCard (card) {
        runInAction(() => {
            const updated = { ...this.cards };
            delete updated[card.id] 
            this.cards = updated
        })
    },
    
    stopSync (cards) {
        this.cards = cards
        console.log(this.cards)
    },

    
});

export { makerStore };
```

<br/>

<span style='background-color:#fff5b1'>Store Folder 내 LoginStore생성하여 userId 관리<span> <br/>

```
import { runInAction, observable  } from "mobx";

const loginStore = observable({
    id : '',
    
    setLoginStore (event) {
        runInAction(() => {
            this.id = event
        })
    },

});

export { loginStore };
```

<br/>

<span style='background-color:#fff5b1'> Store Folder에 생길 모든 store들을 한 곳에서 사용하도록 함<span>

```
import { makerStore } from "./makerStore";
import { loginStore } from "./loginStore";

const useStore = () => {
    return { makerStore, loginStore }
};

export default useStore;
```

<br/>

### :mag: 3.2 props 전달 최소화<br/>

<span style='background-color:#fff5b1'>Editor에서 MakerStore에 접근하여 cards, userId, 카드추가, 삭제기능을 Card_edit_form, CardAddForm에 전달<span><br/>

*Card_edit_form, CardAddForm에서 MakerStore에 접근하면 props를 전달하는 과정을 한 단계 더 줄일 수 있으나 Editor에서 map을 통해 개별 컴포넌트에 cards, userId, 카드추가, 삭제기능을 부여해야 함으로 위와같이 작성하였다*

```
import React from 'react';
import CardAddForm from '../card_add_form/card_add_form';
import Card_edit_form from '../card_edit_form/card_edit_form';
import styles from './editor.module.css'
import { useObserver  } from 'mobx-react';
import useStore from '../../store/store';

const Editor = ({ FileInput, cardRepository }) => {
    const { makerStore } = useStore();
    const { loginStore } = useStore();
    const cards = makerStore.cards;

    //카드생성 및 업데이트 
    const createOrUpdateCard = card => {
        makerStore.createOrUpdateCard(card);
        cardRepository.saveCard(loginStore.id, card); 
    }

    //카드삭제
    const deleteCard = card => {
        makerStore.deleteCard(card);
        cardRepository.removeCard(loginStore.id, card);
    }

    return useObserver(() => (
    <section className={styles.editor}>
        <h1 className={styles.title}>Card Maker</h1>
        {Object.keys(cards).map(key => (
            <Card_edit_form 
            key={key} 
            FileInput={FileInput}
            card={cards[key]} 
            updateCard={createOrUpdateCard} 
            deleteCard={deleteCard}/>
        ))}
        <CardAddForm 
            FileInput={FileInput} 
            cardRepository={cardRepository}/>
    </section>
    ))
}

export default Editor;
```


