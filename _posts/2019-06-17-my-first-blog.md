---
layout: post
title:  "My First Github Blog"
date:   2019-06-17 13:29:15 +0900
categories: [Blog Upgrade]
---
* TOC
{:toc}


# 다른 사람의 글 참고

[지킬로 깃허브에 무료 블로그 만들기](https://nolboo.kim/blog/2013/10/15/free-blog-with-github-jekyll/){: target="_blank" }

# 필요한것들 설치

#### 지킬 설치

```
[sudo] gem install jekyll
```

# 지킬 초기화

```
Jekyll new 깃허브사용자명.github.io
cd 깃허브사용자명.github.com
jekyll serve --watch
```

이제 웹브라우저 주소창에 **localhost:4000**을 입력하면 내 컴퓨터(로컬)에서 디폴트 페이지로 생성된 지킬 사이트를 볼 수 있다.

지킬은 웹서버를 내장하고 있어 아파치나 NgineX와 같은 별도의 웹서버를 띄우지 않고도 사이트를 확인할 수 있다. `--watch`는 사이트를 변경하는 대로 백그라운드에서 제너레이트하여 브라우저에서 변경사항을 바로 확인할 수 있는 옵션이다.

이제 깃허브에 반영해서 로컬이 아닌 `깃허브사용자명.github.io`에서 내 블로그를 볼 수 있게 해보자. `깃허브사용자명.github.io`이란 이름으로 새로운 온라인 저장소를 만든다.

# 첫 글을 작성

```
cd _posts/
cp 2019-06-17-welcome-to-jekyll.markdown 2019-06-17-my-first-post.md
(vim 2019-06-17-my-first-post.md)
```
```
git init
git remote add origin 저장소URL
git add .
git commit -m "Initialize blog"
git push origin master
```

`vim`을 사용해도 되고 다른 에디터를 사용해서 **마크다운**을 이용하여 글을 작성하고 배포하면 끝!!




