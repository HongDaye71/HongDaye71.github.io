---
layout: post
title:  Github블로그 포스팅이슈_해결방법
date:   2022-04-17 12:38:35 +0300
image:  '/images/GitHub.png'
tags:   [Etc]
---

<img src="/images/Posting/Etc/03.png" alt="Project">
<br/>

## 문제상황 <br/>
_post에 .md파일을 추가했으나 로컬 서버에만 업데이트 될 뿐, 깃허브 블로그에 포스팅이 게시되지 않음 <br/>

___

## 해결방법<br/>
**기본적인 부분이 잘못되지 않았는지 확인**<br/>
[ x ] YEAR-MONTH-DAY-title.md 파일 제목 형식확인<br/>
2. 포스팅 날짜가 오기입 되지 않았는지 확인 (파일명과 포스팅 내부 date가 다르지 않은지)<br/>
3. _post 폴더에 맞게 위치해 있는지 확인<br/><br/>

**추가로 시도해볼 수 있는 것들**<br/>
1. _config.yml에 futrue: true추가<br/>
2. 페이지 옵션(타이틀, 카테고리 적는곳)에 published: true 추가<br/>
3. 현재 페이지 강제 리로드(Hard Reload)<br/>
  * 간혹 페이지를 새로고침해도 캐시에 남아있는 css,image,video등의 파일이 로딩되어 변경된 내용이 바로 반영되지 않는 경우가 있음. 이때는 현재 접속한 페이지의 캐시를 무시하고 강제 리로드 해볼 수 있음<br/>
  * Window(IE, Chrome, Firefox) : Ctrl + F5<br/>
  * Mac : ⇧ + ⌘ +R<br/>
4. index.html수정<br/>
  * 간단한 스페이스 추가 만으로 해당 문제를 해결한 사례가 있음

___

나의 경우, 위 방법을 모두 시도해보았으나 문제가 해결되지 않아 반나절을 허비했다. <br/>
Github_repository의 pages build fail message를 확인하지 않은 탓이였다. <br/>

아래 이미지에 표기해둔 순서대로 error message를 확인해본 결과, 아래와 같은 문제로 포스팅이 게시되지 않는 것을 확인했다.<br/>

<img src="/images/Posting/Etc/01.png" alt="Project">

**에러 메세지** <br/>
Liquid Exception: Liquid syntax error<br/>

**원인**<br/>
Jekyll에서 사용되는 liquid는 {% raw %}{{, }}{% endraw %}를 escape 문자로 사용하는데, md문서에 {% raw %}{{{% endraw %}, {% raw %}}}{% endraw %}가 있는 경우 에러 메시지를 출력한다.<br/>

**해결방법**
<img src="/images/Posting/Etc/02.png" alt="Project">
<br/>중괄호 앞 뒤로 raw와 endraw를 추가한다.

___

### 참고자료<br>
1. [jekyll-post-not-generated](https://stackoverflow.com/questions/30625044/jekyll-post-not-generated)
2. [github-pages-are-not-updating](https://stackoverflow.com/questions/20422279/github-pages-are-not-updating)
3. [jekyll-not-generating-posts](https://stackoverflow.com/questions/16990138/jekyll-not-generating-posts)
4. [[Github Blog]깃허브 블로그 포스팅 게시 안됨 해결](https://devyuseon.github.io/github%20blog/githubblog-post-not-shown/)
5. [[Github블로그/Jekyll] Liquid Exception: Liquid syntax error 해결](https://iamheesoo.github.io/blog/gitblog-sol-jekyll02)