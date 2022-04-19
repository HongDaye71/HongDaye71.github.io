---
layout: post
title:  Jekyll post not generated Issue_Solution
date:   2022-04-17 12:38:35 +0300
image:  '/images/JavaScript.jpg'
tags:   [Etc.]
---

### :bomb: 문제상황 <br/>
_post에 .md파일을 추가했으나 로컬 서버에만 업데이트 될 뿐, 깃허브 블로그에 포스팅이 게시되지 않음 <br/>

### 해결방법<br/>
**기본적인 부분이 잘못되지 않았는지 확인**<br/>
1. YEAR-MONTH-DAY-title.md 파일 제목 형식확인<br/>
2. 포스팅 날짜가 오기입 되지 않았는지 확인 (파일명과 포스팅 내부 date가 다르지 않은지)<br/>
3. _post 폴더에 맞게 위치해 있는지 확인<br/>

**추가로 시도해볼 수 있는 것들**<br/>
1. _config.yml에 futrue: true추가<br/>
2. 페이지 옵션(타이틀, 카테고리 적는곳)에 published: true 추가<br/>
3. 현재 페이지 강제 리로드(Hard Reload)<br/>
  -> 간혹 페이지를 새로고침해도 캐시에 남아있는 css,image,video등의 파일이 로딩되어 변경된 내용이 바로 반영되지 않는 경우가 있음. 이때는 현재 접속한 페이지의 캐시를 무시하고 강제 리로드 해볼 수 있음<br/>
  -> Window(IE, Chrome, Firefox) : Ctrl + F5<br/>
  -> Mac : ⇧ + ⌘ +R<br/>
4. index.html수정
  -> 간단한 스페이스 추가 만으로 해당 문제를 해결한 사례가 있음



