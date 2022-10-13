---
title: "[Github 블로그 - Jekyll] 블로그 시작하기(4) - 블로그 구글 검색 노출 시키기(Google Search Console)"
excerpt: "Google Search Console 설정법"

categories:
  - Blog
tags:
  - [Github, Jekyll, GoogleSearchConsole ]

permalink: /Github/blog3/

toc: true
toc_sticky: true

date: 2022-10-13
last_modified_at: 2022-10-13
---

블로그를 만들었다면 혼자 보고 만족하는게 아닌,

다른 사람들과 공유하고 소통하길 원할것이다! 그렇다면 검색에 노출되게 기능을 추가해야한다.

## 📍 Google Search Console

[https://search.google.com/search-console/about](https://search.google.com/search-console/about)

위에 링크로 들어가면 아래 내용들을 확인할 수 있다.

![Untitled](/assets/images/posts_img/blogsearch/Untitled.png)

Search Console에 대한 영상 자료도 공유되고 있다.

![Untitled](/assets/images/posts_img/blogsearch/Untitled%201.png)

해당 서비스를 이용하면 아래와 같은 서비스를 만나볼 수 있다고 한다.

![Untitled](/assets/images/posts_img/blogsearch/Untitled%202.png)

## ✅ Google Search Console 시작하기

시작하기를 누르면 아래와 같은 이미지가 나온다.

![Untitled](/assets/images/posts_img/blogsearch/Untitled%203.png)

도메인을 따로 사용하지 않고 깃허브에서 제공되는 url을 사용할 것이기 때문에
`URL 접두어` 에 블로그 주소를 입력한다.

URL 확인이 완료되면 소유권 확인을 위한 창이 나타난다.

`minimal-mistakes` 테마의 `_config`에선 `content` 값으로만 설정할 수 있기 때문에 다른확인방법에서  HTML 태그를 복사한다.

![Untitled](/assets/images/posts_img/blogsearch/Untitled%204.png)

그 이외에 다른 확인 방법 들도 있다.

- HTML 파일
- Google 애널리틱스
- Google 태그 관리자
- 도메인 이름 공급업체

해당 방법은 환경에 따라 다르기때문에 목적에 맞게 사용하는걸 권장한다.

## ✅  HTML 태그 세팅하기

`_config.yml`에서 `google_site_verification:` 을 검색하면 해당 부분이 나온다.

복사한 `meta 태그` 에서 `content` 부분만 복사 후 해당 위치에 붙여넣어준다.

```bash
<meta name="google-site-verification" content="REGEjUQ1lanH_8Lgj1oCQDfiBi--------------" />
```

![Untitled](/assets/images/posts_img/blogsearch/Untitled%205.png)

google 이외에도, bing, yandex, naver 에 대한 검색 인증 코드를 넣을 수 있도록 세팅되어있다.

[**minimal-mistakes 테마 공식문서 참고**](https://mmistakes.github.io/minimal-mistakes/docs/configuration/)

![Untitled](/assets/images/posts_img/blogsearch/Untitled%206.png)

설정이 완료되었으면 `commit & push` 후 반영되길 기다린다.

다시 Google Search Console로 돌아와 확인을 누르면!

![Untitled](/assets/images/posts_img/blogsearch/Untitled%207.png)

소유권 확인이 된다고 뜬다!

이젠 진짜 구글이 검색 URL 정보를 크롤링할 수 있도록 추가로 설정해줘야 한다.

## ✅  sitemap.xml 만들기

```bash
---
layout: null
---

<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:schemaLocation="http://www.sitemaps.org/schemas/sitemap/0.9 http://www.sitemaps.org/schemas/sitemap/0.9/sitemap.xsd"
        xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
    {% for post in site.posts %}
    <url>
        <loc>{{ site.url }}{{ post.url }}</loc>
        {% if post.lastmod == null %}
        <lastmod>{{ post.date | date_to_xmlschema }}</lastmod>
        {% else %}
        <lastmod>{{ post.lastmod | date_to_xmlschema }}</lastmod>
        {% endif %}

        {% if post.sitemap.changefreq == null %}
        <changefreq>weekly</changefreq>
        {% else %}
        <changefreq>{{ post.sitemap.changefreq }}</changefreq>
        {% endif %}

        {% if post.sitemap.priority == null %}
        <priority>0.5</priority>
        {% else %}
        <priority>{{ post.sitemap.priority }}</priority>
        {% endif %}

    </url>
    {% endfor %}
</urlset>
```

해당 파일을 _config.yml 파일과 동일한 위치에 넣어준다.

Google 크롤러가 주기적으로 나의 URL을 체크할 수 있도록 해주는 파일이다.

git push 하기 전에 로컬 서버 실행 후 확인 해본다.

아래처럼 나오면 확인 완료!

![Untitled](/assets/images/posts_img/blogsearch/Untitled%208.png)

## ✅  robots.txt 생성

`_config.yml` 와 같은 위치에 아래 파일을 넣어준다.

검색엔진 크롤러들이 홈페이지를 크롤링하는데 도움을 주는 파일이다.

```bash
User-agent: *
Allow: /
Sitemap: {{ '/sitemap.xml' | relative_url | prepend: site.url }}
```

## ✅  Sitemap 제출

이제 나의 사이트맵을 제출해주면 끝이난다.

`sitemap.xml` 을 아래 URL 입력 부분에 넣어주면 된다.

![Untitled](/assets/images/posts_img/blogsearch/Untitled%209.png)

**참고**

- [https://mmistakes.github.io/minimal-mistakes/docs/configuration/](https://mmistakes.github.io/minimal-mistakes/docs/configuration/)
- [https://velog.io/@eona1301/Github-Blog-검색창-노출시키기](https://velog.io/@eona1301/Github-Blog-%EA%B2%80%EC%83%89%EC%B0%BD-%EB%85%B8%EC%B6%9C%EC%8B%9C%ED%82%A4%EA%B8%B0)
- [https://khs613.github.io/github/google-search-sitemap/](https://khs613.github.io/github/google-search-sitemap/)