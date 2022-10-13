---
title: "[Github 블로그 - Jekyll] 블로그 시작하기(3) - Jekyll Local에서 사용하기, LiveReload 적용 "
excerpt: "Local 환경 세팅, LiveReload 적용"

categories:
  - Blog
tags:
  - [Github, Jekyll]
header:
  teaser: "/assets/images/posts_img/blogsearch/3.png"
permalink: /Github/blog3/

toc: true
toc_sticky: true

date: 2022-10-12
last_modified_at: 2022-10-12
---
![](/assets/images/posts_img/blogsearch/3.png)
## 📍 Jekyll Local 환경 세팅

이전글에서 블로그를 사용할 세팅이 끝났다.  
이제 글만 쓰면 된다! 하지만 내 로컬 환경에서 글을 작성하고 테스트를 해보려면 어떻게 해야할까?
깃허브로 `push` 하고 해당 `url`에 들어가서 확인해야한다면 너무 비효율적일것이다.

### 🔎 그러면 어떻게 로컬에서 확인 할 수 있을까?
로컬에서 Jekyll를 실행하면 된다!!!  
spring 처럼 빌드 후 서버를 실행하면 내 로컬에서 확인하고 작업할 수 있다.

**실행 명령어**
```bash
jekyll serve
```

하지만 역시 쉽게 된다면 경기도 오산..
#### ⚠️ 첫번째 오류 발생   
- `Could not find gem 'jekyll-admin' in locally installed gems. (Bundler::GemNotFound)`
- 찾아보니 `GemNotFound` 오류는 `Bundler` 라고 입력만 하면 쉽게 해결된다고 한다.


#### ⚠️ 두번째 오류 발생
- `: cannot load such file -- webrick (LoadError)`
- 위에와 다른 오류가 발생했다. 

#### 🚨 해결방법
`Ruby 3.0.0` 부터는 `webrick`이 빠졌기 때문에 추가로 설치해줘야 한다고 한다.
![](/assets/images/posts_img/github-2/Untitled.png) 

아래 명령어를 통해 설치한다.
```bash
bundle add webrick
```

이제 다시 `jekyll serve` 를 입력하니깐 잘 된다!
![](/assets/images/posts_img/github-2/Untitled2.png)

---
또 다른 이슈 발생.
수정사항이 생겼을때 매번 서버를 종료 후 재시동 해야지만 반영이 됐다.   
실시간으로 반영해주는 플러그인이 있지 않을까?  

### LiveReload
```bash
bundle exec jekyll serve --livereload
```
혹은
```bash
jekyll serve --livereload 
```
를 해주면 실시간으로 `html, css` 수정사항이 반영된다.

---
**참고**
- [https://www.ruby-lang.org/en/news/2020/12/25/ruby-3-0-0-released/](https://www.ruby-lang.org/en/news/2020/12/25/ruby-3-0-0-released/)
- [jekyll 실행 시킬 때 `require': cannot load such file -- webrick (LoadError) 오류가 난다면 bundle add webrick](https://junho85.pe.kr/1850)