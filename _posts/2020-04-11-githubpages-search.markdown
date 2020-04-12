---
layout:     post
title:      github blog를 google에서 검색되도록 설정하기
author:     Soo-young Hwang
tags: 		Github-pages
# subtitle:  	
category:  project1
---

### 서론
[지난 포스트](https://swimminghwang.github.io/project1/2020/04/08/githubpages-ga/)에서 내 블로그의 방문자 수 혹은 방문자 유입을 분석해주는 `Google Analytics`를 적용해 보았습니다.    
`Github-pages`를 이용한 블로그는 포털사이트에 검색해도 안 나오더라구요...    
따라서 검색 가능하게 등록을 직접 해 줘야 한답니다 ^ㅗ^    
이번 포스트에선 **포털사이트에 검색했을 때 내 블로그가 나올 수 있도록 등록하는 과정**을 다뤄보았습니다.     
아래의 참고 블로그와 같이, 대표적인 포털 사이트 Google, Daum, Naver 와 같은 검색엔진에 등록해 보았습니다.

### 본론
> Step 1. 사이트맵(sitemap) 만들기

사이트맵(sitemap) 만들기
사이트맵은 페이지 정보를 포털사이트에 알리는 역할을 합니다.    
(내가 등록한 사이트의 모든 정보를 포털사이트에 알리는 역할)    
- sitemap.xml은 웹사이트 내 모든 페이지의 목록을 나열한 파일로 책의 목차와 같은 역할    

그러므로 사이트맵을 만들어서 Google에 등록을 해두면 Google에서 주기적으로 Web상에 있는 contents를 수집합니다. 즉 제 블로그를 등록하면 제 블로그를 수집합니다. 그럼 구글에 관련 검색어로 색인이 되고, 구글링시 제 글을 찾아볼 수 있겠죠!?! 야호 신난당   

참고 블로그에서 Github-pages에서는 보안상의 문제로 플러그인을 사용할 수가 없어서 jekyll plugin을 사용하지 않고 sitemap.xml을 만들어야 한다고 합니다. 사이트를 제너레이트하고 깃헙에 푸시하면 대부분 문제없이 사용할 수 있다고 하네요 

루트 디렉터리에 `sitemap.xml` 을 생성한 후, 아래의 코드를 삽입합니다.

아래 코드에 있는 site.url 변수가 사용될 수 있도록 `.conflg.yml`에 url을 꼭 넣어줘야 합니다.    
있는지 확인해주세요!


{% highlight yml %}
url: "https://swimminghwang.github.io"
{% endhighlight %}


{% highlight xml %}
---
---
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://www.sitemaps.org/schemas/sitemap/0.9 http://www.sitemaps.org/schemas/sitemap/0.9/sitemap.xsd" xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
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
{% endhighlight %}



### 결론

### references
[참고 사이트1](http://jinyongjeong.github.io/2017/01/13/blog_make_searched/)   
[참고 사이트2](http://dveamer.github.io/homepage/Sitemap.html)   
[참고 사이트3](https://honbabzone.com/jekyll/start-gitHubBlog/#step-9-%EA%B5%AC%EA%B8%80-%EA%B2%80%EC%83%89-%EA%B0%80%EB%8A%A5%ED%95%98%EA%B2%8C-%ED%95%98%EA%B8%B0)     
[참고 사이트4](https://wayhome25.github.io/etc/2017/02/20/google-search-sitemap-jekyll/)


http://parkjuwan.dothome.co.kr/webapp/ltgt_conv/
마크다운코드를 하이라이트로