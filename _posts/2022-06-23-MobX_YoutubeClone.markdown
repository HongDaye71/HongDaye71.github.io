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
3. Youtube Clone Project에 MobX적용<br/>
    1. Video Store생성<br/>
    2. Store생성<br/>
    3. Observable Data사용<br/>

* 본 포스팅은 드림코딩의 리액트 강의에서 다루어진 Youtube Clone Project에 MobX 상태관리 라이브러리를 적용하는 과정을 다룹니다

___

## :star: 1. 소개<br/>
리액트를 사용해서 프론트 개발을 할 때에는 클래스형과 함수형 컴포넌트를 사용할 수 있다. 과거에는 함수형 컴포넌트에서 상태관리 및 라이프사이클 메소드가 제공되지 않았기 때문에 클래스 컴포넌트를 주로 사용했으나 2019년 v16.8부터 리액트에서 함수형 컴포넌트에 훅(hook)을 지원해주면서 현재는 공식 문서에서 함수형 컴포넌트와 훅을 함께 사용할 것을 권장하고 있다. 개발자들 또한 클래스 보다는 함수형 컴포넌트를 사용하는데, 이유는 아래와 같다.<br/>

1. <span style='background-color:#fff5b1'>코드가 간결하다</span> <br/>
    클래스 컴포넌트는 클래스와 렌더함수 선언 및 extend를 통한 컴포넌트 상속 등 선언 방식부터 함수형 컴포넌트에 비해 작성할 코드가 많다.

```javascript
//Class Component
import React, {Component} from 'react'

class App extends Component{
    state = {
        state: null,
    };
    
    render() {
        return (
        <div>
            <OtherFunction
                state={this.state.state}> />
        </div>
        );
    }
}
```
<br/>

```javascript
//Function Component
import { useState} from 'react';

function App() {
    const [state, setState] = useState([]);
    return(
        <div>
            <OtherFunction
                state={state}>/>
        </div>
    );
}
```
<br/>


2. <span style='background-color:#fff5b1'>함수형 컴포넌트는 렌더링 결과를 보장받는다</span> <br/>
    함수형 컴포넌트는 immutable하지만, 클래스 컴포넌트는 this를 사용하기 때문에 mutable하다. 아래 예제는 this의 변경 가능한 특징으로 인해 발생할 수 있는 문제이다. <br/>

    클래스형 컴포넌트의 실행과정을 아래와 같다<br/>
    (1) Kich란 계정에서 삭제 버튼을 클릭하여 this.handleClick()을 실행시킨다<br/>
    (2) handleClick()은 콜백함수로 5초 뒤 showAlert()를 실행시킨다<br/>
    (3) 이때 5초가 지나기 전에 Kitty의 프로필로 들어가면 this.props.user는 Kitty로 변경된다<br/>
    (4) 따라서 showAlert()는 의도치 않게 업데이트된 this.props.user를 가지고 실행된다<br/>
    (5) 사용자는 Kich계정을 삭제했으나, Kitty의 계정을 삭제했다는 안내창을 받게된다<br/>

    * 비동기 함수인 콜백함수가 실행되는 순간 showAlert()는 this에 묶여 고정된 porps를 갖지못한 불안한 상태를 가지게 되는 것이다

```javascript
//Class Component
class DeleteComment extends React.Component {
  showAlert = () => {
    alert(`${this.props.user}`의 계정을 삭제합니다.);
  };

  handleClick = () => {
    setTimeout(this.showAlert, 5000);
  };
  render() {
  return (
    <button onClick={this.handleClick}>삭제</button>
  )};
}
```
<br/>

```javascript
//Function Component
function DeleteComment(props) {
  const showAlert = () => {
    alert(`${props.user}`의 댓글을 삭제합니다.);
  };

  const handleClick = () => {
    setTimeout(showAlert, 5000);
  };

  return (
    <button onClick={handleClick}>삭제</button>
  );
}
```

<br/>

위와 같은 이유로 작성자 또한 프로젝트 진행 시 함수형 컴포넌트를 주로 사용하고자 한다. 하지만 이번에 MobX를 공부하면서 대부분의 예제들이 클래스기반의 데코레이터를 사용하는 것을 확인했다. 따라서 본 포스팅에서는 데코레이터를 사용하지 않고 함수형 컴포넌트에 MobX를 적용하는 과정을 다뤄본다. MobX를 적용할 예제로는 드림코딩의 리액트 강의에서 다루어진 Youtube Clone Project를 사용한다.

<span style="color:#D3D3D3">*작성자는 주니어 개발자 입니다. 미흡한 부분이 많으니 잘못된 점은 지적 부탁드립니다*</span>

___

## :closed_book: 2. Youtube Clone Project<br/>
기존의 Youtube Clone Project는 아래와 같은 기능 및 구조를 갖는다<br/>

<span style='background-color:#fff5b1'>Project Features</span> <br/>
(1) Watch popular videos in real time using the YouTube API<br/>
(2) Search a video using the YouTube API<br/>

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

<details>
<summary>Source Code</summary>
<div markdown="1">

<details>
<summary>App.jsx</summary>
<div markdown="1">

```javascript
import { useState, useEffect, useCallback } from 'react';
import styles from './app.module.css';
import SearchHeader from './components/search_header/search_header';
import VideoList from './components/video_list/video_list';
import VideoDetail from './components/video_detail/video_detail';

function App({ youtube }) {
  const [videos, setVideos] = useState([]);
  const [selectedVideo, setSelectedVideo] = useState(null);

  const selectVideo = video => {
    setSelectedVideo(video);
  }
  
  const search = useCallback(query => {
    youtube
      .search(query)
      .then(videos => 
        setVideos(videos));
        setSelectedVideo(null);
  },[]);

  useEffect(()=> {
    youtube
      .mostPopular()
      .then(videos => setVideos(videos));
  }, []);

  return (
  <div className={styles.app}>
    <SearchHeader onSearch={search}/> 
    <section className={styles.content}>
    {selectedVideo && (
      <div className={styles.detail}>
        <VideoDetail video={selectedVideo} />
      </div>
    )}
      <div className={styles.list}>
        <VideoList 
          videos={videos} 
          onVideoClick={selectVideo}
          display={selectedVideo ? 'list' : 'grid'}
        />
      </div>
    </section>
  </div>
  );
}

export default App;
```
</div>
</details>

<details>
<summary>youtube.js</summary>
<div markdown="1">

```javascript
class Youtube {
    constructor(key) {
        this.key = key;
        this.getRequestOptions = {
            method: 'GET',
            redirect: 'follow'
        };
    }

    async mostPopular() {          
        const response = await fetch(`https://youtube.googleapis.com/youtube/v3/videos?part=snippet&chart=mostPopular&maxResults=25&key=${this.key}`, this.getRequestOptions);
        const result_1 = await response.json();
        return result_1.items; 
    }

    async search(query) {
        const response = await fetch(`https://youtube.googleapis.com/youtube/v3/search?part=snippet&maxResults=25&q=${query}&type=video&key=${this.key}`, this.getRequestOptions);
        const result_1 = await response.json();
        return result_1.items.map(item => ({ ...item, id: item.id.videoId }));
        /*
        key warning error: 
        search api사용 시, id가 오브젝트 형태로 들어가있어 비디오가 고유의 key를 갖지 않는다는 warning message가 출력됨
        따라서 setVideos를 통해 result.items을 videos에 넣기 전, item복사 후 id를 추가하는 별도 작업 필요
        */
    }
}

export default Youtube;
```
</div>
</details>

<details>
<summary>search_header.js</summary>
<div markdown="1">

```javascript
import styles from './search_header.module.css'
import React, {useRef} from 'react';

const SearchHeader = React.memo (({ onSearch }) => {
    const inputRef = useRef();

    const handleSearch = () => {
        const value = inputRef.current.value;
        onSearch(value); //검색 이벤트가 발생하면, onSearch 콜백함수 및 검색된 결과값 호출
    }

    const onClick = () => {
        handleSearch();
    };

    const onKeyPress = (event) => {
        if (event.key === 'Enter') {
            handleSearch();
        }
    };

    return (
    <header className={styles.header}>
        <div className={styles.logo}>
            <img className={styles.img} src="./images/logo.png" alt="logo" />
            <h1 className={styles.title}>Youtube</h1>
        </div>
        <input
            ref={inputRef} 
            className={styles.input} 
            type="search" 
            placeholder='Search...' 
            onKeyPress={onKeyPress} 
        />
        <button className={styles.button} type="submit" onClick={onClick}>
            <img className={styles.buttonImg}src="./images/search.png" alt="search" />
        </button>
    </header>
    );
});

export default SearchHeader;
```
</div>
</details>

<details>
<summary>video_detail.js</summary>
<div markdown="1">

```javascript
import React from 'react';
import styles from './video_detail.module.css'

const videoDetail = ({video}) => (
    <section className={styles.detail}>
        <iframe 
            className={styles.video}
            type="text/html" 
            title="youtube video player"
            width="100%" 
            height="500px"
            src={`https://www.youtube.com/embed/${video.id}`}
            frameBorder="0" 
            allowFullScreen>
        </iframe>
        <h2>{video.snippet.title}</h2>
        <h3>{video.snippet.channeltitle}</h3>
        <pre className={styles.description}>{video.snippet.description}</pre>
    </section>
);

export default videoDetail;

```
</div>
</details>

<details>
<summary>video_item.js</summary>
<div markdown="1">

```javascript
import React from 'react';
import styles from './video_item.module.css';

const VideoItem = React.memo(({video, video: {snippet}, onVideoClick, display}) => {
    const displayType = display === 'list' ? styles.list : styles.grid;

    return (
    <li className={`${styles.container} ${displayType}`} onClick={()=> onVideoClick(video)}>
        <div className={styles.video}>
            <img 
                className={styles.thumbnails}
                src={snippet.thumbnails.medium.url} 
                alt="video thumbnail"/>
            <div>
            <p className={styles.title}>{snippet.title}</p>
            <p className={styles.channel}>{snippet.channelTitle}</p>
            </div>
        </div>
    </li>
    );
});

export default VideoItem;
```
</div>
</details>

<details>
<summary>video_list.js</summary>
<div markdown="1">

```javascript
import React from 'react';
import VideoItem from '../video_item/video_item';
import styles from './video_list.module.css';

const VideoList = ({videos, onVideoClick, display}) => (
    <ul className={styles.videos}>
    {videos.map(video => (
        <VideoItem 
            key={video.id} 
            video={video} 
            onVideoClick={onVideoClick}
            display={display}
        />
    ))}
    </ul>
    );

export default VideoList;
```
</div>
</details>

</div>
</details>

*전체 소스코드는 하단의 깃허브 링크를 통해 확인가능*

___

## :books: 3. Youtube Clone Project에 MobX적용
### :mag: 3.1 Video Store생성<br/>
1. observable data를 관리하는 videoStore생성
2. 기존 App에 위치해 있던 상태 및 상태관리 메소드 이동
3. 본 포스팅에서는 데코레이터를 사용하지 않으므로 클래스가 아닌 객체 형태와 메소드로 스토어를 작성하고 observable API로 감싸줌
3. fetch Web APIs사용을 위해 기존 App에 위치해있던 youtube 생성코드 이동 
4. observable data는 action이나 runInAction을 통해 변경되어야 함으로 state변경이 이루어지는 부분은 runInAction API로 감싸줌
    * <span style="color:#D3D3D3">action vs runInAction: <br/>
    action API는 첫 번째로 불리는 awit코드 전까지만 실행된다. 이후 await의 return값에 의해 observable값을 변경하려면 다른 action으로 감싸야 한다. runInAction을 사용하면 불필요한 action함수 생성을 줄이면서 좀 더 가독성 높은 비동기 코드를 만들 수 있다</span>

```javascript
import { runInAction, observable } from 'mobx';
import Youtube from '../service/youtube';

const youtube = new Youtube(process.env.REACT_APP_YOUTUBE_API_KEY);

const videoStore = observable({
    videos : [],
    selectedVideo : null,

    mountMostPopular() {
            youtube
            .mostPopular()
            .then(result => runInAction((() => {this.videos = result})))
    },

    mountSelectVideo(event) {
        runInAction((() => {
            this.selectedVideo = event
        }))
    },  

    mountSearch(query) {
        youtube
        .search(query)
        .then(videos => runInAction((() => {this.videos = videos})))
        runInAction((() => {this.setSelectedVideo = null}));
    }
});

export { videoStore };
```
<br/>

___

### :mag: 3.2 useStore생성<br/>
스토어 폴더에 생길 모든 store들을 한 곳에 불러들이게끔 하기 위해 Custom hook을 다음과 같이 작성<br/>

* Custom hook: 개발자가 직접 만든 hook으로 반복되는 메서드를 하나로 묶어 사용한다. Custom Hook의 이름은 use로 시작해야 한다.

```javascript
import { videoStore } from './videoStore';

const useStore = () => {
    return { videoStore };
};

export default useStore;
```

___

### :mag: 3.3 Observable Data사용<br/>
App에서 Observable Data 사용<br/>

1. useStore를 videoStore라는 이름으로 호출<br/>
2. 비디오 검색, 선택 등의 액션이 발생했을 때 videoStore의 mostPopular(),search() 호출<br/>
3. 함수 컴포넌트에서 Observer를 사용하는 방법은 아래와 같음
    (1) useObserver import<br/>
    (2) return시 useObserver반환<br/>

```javascript
import { useEffect, useCallback } from 'react';
import styles from './app.module.css';
import SearchHeader from './components/search_header/search_header';
import VideoList from './components/video_list/video_list';
import VideoDetail from './components/video_detail/video_detail';
import { useObserver  } from 'mobx-react';
import useStore from './store/store';

function App() {
  const { videoStore } = useStore();

  useEffect(()=> {
    videoStore.mountMostPopular();
  }, []);

  const selectVideo = video => {
    videoStore.mountSelectVideo(video);
  }

  const search = useCallback(query => {
      videoStore.mountSearch(query);
      videoStore.mountMostPopular();
      videoStore.mountSelectVideo(null);
  },[]);

  return useObserver(() => (
    <div className={styles.app}>
    <SearchHeader onSearch={search}/> 
    <section className={styles.content}>
    {videoStore.selectedVideo && (
      <div className={styles.detail}>
        <VideoDetail video={videoStore.selectedVideo} />
      </div>
    )}
      <div className={styles.list}>
        <VideoList 
          videos={videoStore.videos} 
          onVideoClick={selectVideo}
          display={videoStore.selectedVideo ? 'list' : 'grid'}
        />
      </div>
    </section>
  </div>
  ))
}

export default App;
```

___

#### Project Eror <br/>
오류메세지: www-embed-player.js:792 GET https://googleads.g.doubleclick.net/pagead/id net::ERR_UNSAFE_REDIRECT
원인: PC에 광고차단 확장프로그램이 설치되어 있는 경우, 비디오 재생 시 GET요청을 차단하여 발생하는 오류

#### Source Code. <br/>
* [Github](https://github.com/HongDaye71/YoutubeClone)<br/>
* [Github(MobX)](https://github.com/HongDaye71/MobX_YoutubeClone)<br/>

#### Etc. <br/>
* 메소드와 함수의 차이점<br/>
    (1) 함수는 메소드를 아우르는 포괄적인 용어이다<br/>
    (2) 함수는 객체로부터 독립적이며, 메소드는 객체에 종속적이다<br/>
    (3) 메소드는 아래 두 가지 포인트에서 함수와 다르다<br/>
        - 메소드는 호출된 객체에 암시적으로 전달된다<br/>
        - 메소드는 클래스 안에 있는 데이터를 조작할 수 있다<br/>

* async/await: 작업의 순차성을 강제해주는 것으로 아래와 같이 사용될 수 있다 <br/>
```javascript
async function getApple() {
  await delay(3000);	//3초 기다리고 실행
  return "apple";
}
````
