---
layout: post
title:  "Make Category"
date:   2019-06-27 13:29:15 +0900
categories: [Blog Upgrade]
---
* TOC
{:toc}


# 다른 사람의 글 참고

[지킬 블로그 카테고리 만들기](https://devyurim.github.io/development%20environment/github%20blog/2018/08/07/blog-6.html){: target="_blank" }

#  _layouts 폴더에 category.html 파일 생성

category.html은 category 이름에 맞는 포스트들의 타이트들을 리스트로 보여준다. 코드는 아래와 같다.

```
---
layout: default
---
<ul class="posts-list">
  
  {% assign category = page.category | default: page.title %}
  {% for post in site.categories[category] %}
    <li>
      <h3>
        <a href="{{ site.baseurl }}{{ post.url }}">
          {{ post.title }}
        </a>
        <small>{{ post.date | date_to_string }}</small>
      </h3>
    </li>
  {% endfor %}
  
</ul>
```

# _includes 폴더의 index.html 파일 수정

아래의 내용과 같이 수정한다.

```
<header class="site-category">
  <ul>
    
    {% assign pages_list = site.pages %}
    {% for node in pages_list %}
      {% if node.title != null %}
        {% if node.layout == "category" %}
          <li><a class="category-link {% if page.url == node.url %} active{% endif %}"
          href="{{ site.baseurl }}{{ node.url }}">{{ node.title }}</a></li>
        {% endif %}
      {% endif %}
    {% endfor %}
    
</ul>
</header>
```

# category 폴더 생성

(맨 바깥의 디렉토리) 계정명.github.io 폴더 안에 category 폴더를 만들어준 다음 원하는 카테고리 명의 markdown 파일을 추가해준다.

마크다운 파일 내용은 아래와 같다.

```
---

layout: category

title: 여기에 카테고리 이름 입력!

---
```

# 블로그 포스트에 category 추가하기

위의 세가지 셋팅 후 포스트를 작성 시 카테고리 항목만 추가하여 주면 카테고리 지정이 된다.
마크다운 파일 내용은 아래와 같다.

```
---

layout: category

title: [여기에 카테고리 이름 입력](복수 카테고리도 가능하다.)

---
```

주의 해야 할 점은 반드시! category 폴더에 원하는 category를 만들어주고 포스트에 같은 카테고리 명을 입력해야 한다.


