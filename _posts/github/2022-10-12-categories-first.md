---
title: "[Github 블로그 - Jekyll] 블로그 시작하기(1) - chruby, ruby 설치"
excerpt: "Repository생성 및 chruby, ruby 설치하기"

categories:
- Jekyll
tags:
- [Github, Jekyll]

permalink: /Github/first/

toc: true
toc_sticky: true

date: 2022-10-12
last_modified_at: 2022-10-12
---

## 📍 Why, Github로 블로그를 만들었냐면!
### 1. 마크다운 (Markdown) 못잃어!
평소 메인으로 사용하는 메모 및 기록 툴이 노션이다.  
마크다운 기반으로 만들어졌기 때문에 작성 후 네이버나 티스토리에 붙여 넣으면 레이아웃이 다 깨져버린다.
더불어, 마크다운 문법에 익숙해져버린 나의 손가락들... 
티스토리에서 마크다운 문법을 사용할 수 있게 커스텀이 가능하다고 하지만 다 설정해줘야하기 때문에 애초에 문법을 사용하는 블로그를 선택했다. 

### 2. 카테고리별 정리 가능 !
마크다운이 좋으면 벨로그를 사용하면 되는게 아닌가?   
벨로그 UI랑 편리함이 세상 저리가라 너무 좋았다. 하지만... 카테고리 분류가 어려웠다.   
나는 상위 카테고리별로 분류하여 정리하는걸 좋아하기 때문에 벨로그는 아쉬움이 많았다.   
그래서 다양한 테마와 커스텀이 가능한 깃허브로 블로그를 만들어보기로 결심!! 

### 3. 도전하게 만든다.
깃허브 블로그 할게 많다.  
테마 고르기부터, 내 입맛에 맞게 하려면 HTML,CSS 수정도 해야하고, 루비도 깔아야하고,   
따로 설정할게 많기 때문에 재밌어보인다. 

---
# 깃허브 블로그 만들기 Start!

<aside>
💡 MacOS, M1 기반으로 작성되었기에 설정법이 다를 수 있습니다.
</aside>

### 1. Github Repository 생성
![](/assets/images/posts_img/github-first/repository.png)

[`username.github.io`](http://username.github.io) 로 생성한다.

Jekyll를 사용하려면 Ruby 개발환경이 필요하다.   
공식문서에서 추천하는 `chruby`를 사용하여 `Ruby`를 설치한다.

### 2. Homebrew로 설치
<aside>
💡 기존에 Homebrew가 설치되어있기때문에 설치 방법은 생략하였지만, 아래 토글로 확인 할 수 있습니다.
</aside>
<details>
<summary>Homebrew 설치하기</summary>
<div markdown="1">

```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

</div>
</details>  

### 1. `chruby`, `ruby` 설치

```bash
brew install chruby ruby-install
```


### 2.`ruby` 최신 버전 설치

```bash
ruby-install ruby
```

하지만 오류 발생..^^
![](/assets/images/posts_img/github-first/스크린샷%202022-10-11%20오후%209.56.50.png)

현재 14인치 맥북프로 (M1 Pro) 인데,    
M1이라 그런지 위에 방법으론 설치가 안됐다. 그래서 폭풍 검색 후 해결 방법을 찾았다.
> 회사 컴퓨터는 M1이고, 집에서 쓰는 맥북프로는 Intel이다.   
> Intel 맥에서는 `ruby-install ruby` 로 실행했을때 정상적으로 설치된다. 

<details>
<summary>Apple Silicon Mac (M1/M2) 일때 루비 설치 방법</summary>
<div markdown="1">

Apple Silicon Mac(M1 또는 M2)을 사용하는 경우 CLT(Apple Command Line Tools) 또는
Xcode의 버전을 확인하기

```bash
brew config
```

아래쪽에서 `CLT:`와 `Xcode:`로 시작하는 줄을 찾는다.   
둘 중 하나가 `14`로 시작하는 경우 다음과 같이 Ruby를 설치해야한다.

![](/assets/images/posts_img/github-first/스크린샷%202022-10-11%20오후%2010.04.45.png)
```bash
ruby-install ruby -- --enable-shared
```

해당 방법으로 하니 설치가 완료됐다.

![](/assets/images/posts_img/github-first/스크린샷%202022-10-11%20오후%209.52.55.png)

</div>
</details>  

<br>
### 3. 자동으로 chruby를 사용하더록 쉘 구성

```bash
echo "source $(brew --prefix)/opt/chruby/share/chruby/chruby.sh" >> ~/.zshrc
echo "source $(brew --prefix)/opt/chruby/share/chruby/auto.sh" >> ~/.zshrc
echo "chruby ruby-3.1.2" >> ~/.zshrc
```

<br>
### 4. 루비 버전 확인   
- 3.1.2p20 (2022-04-12 revision 4491bb740a) or 최신버전으로 나와야한다.

```bash
ruby -v
```

![](/assets/images/posts_img/github-first/스크린샷%202022-10-11%20오후%2011.25.12.png)

<br>
### 5. Install Jekyll 

```bash
gem install jekyll
```
---
#### 참고
- [Jekyll DOCS](https://jekyllrb.com/docs/installation/macos/)
- [The fastest and easiest way to install Ruby on a Mac in 2022](https://www.moncefbelyamani.com/how-to-install-xcode-homebrew-git-rvm-ruby-on-mac/)