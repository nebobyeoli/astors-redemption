---
title: 레이아웃 추가 구성
---

## Header-Footer 삽입 레이아웃 추가

기본 레이아웃인 `_layouts/default.html`을 `_layouts/post.html`로 추가해 바꾸어 주었다.

게시글들의 머리와 끝의 `header`와 `footer`에는 각각 페이지 제목 - 날짜, 사이트 제목 - 부제 및 첫 화면 링크가 표시되고, `page-header`의 배너 위치에는 페이지가 아닌 사이트의 제목 - 부제가 표시되어 보다 일관적으로 나타나도록 수정하였다.

| 참고: [Github Metadata](https://jekyll.github.io/github-metadata/site.github/){:target="_blank"} 및 [Jekyll Front Matter](https://jekyllrb.com/docs/front-matter/){:target="_blank"} 항목들

<hr style="opacity: 0;">

| _layouts/post.html
{% raw %}
```html
<div class="mainbar">
  <!-- header: 페이지 제목-날짜 -->
  <h1 class="page-title">{{ page.title | default: site.title }}</h1>
  <h3 class="page-desc">{{ page.description | default: site.description }}</h3>
  <h3 class="page-desc"></h3>
  <hr>
  
  {% if page.content != empty %}
    {{ content }}<br><br><br><hr>
  {% endif %}

  <h1>
    <a href="{{ site.baseurl }}" class="a-footing">
      <!-- footer: 사이트 제목-부제 -->
      <span class="big-url">{{ site.title }}</span>
      <span class="small-url"> - 홈 화면으로</span>
    </a>
  </h1>
  <h4 class="page-desc foot-desc">{{ site.description }}</h4>
```
{% endraw %}
<br>

## 날짜글 링크 자동 삽입

`_posts` 위치 내의 일별 작성글들을 가리키는 링크가 자동으로 리디렉션 목록판에 나타나도록 `_includes/navigation.html`에 추가 구현해 주었다.

| 말이 자동이지 그냥 반복문 한 번 더 돌리는 것이다.
| _includes/navigation.html
{% raw %}
```html
<!-- 아래 내용이 추가된 내용 중 핵심이라 할 수 있다. -->
<!-- 'active' 클래스는 현재 열려 있는 페이지가, 반복자가 가리키는 해당 문서와 일치함을 의미한다. -->

<ul>
  {% for post in site.posts %}

    {% if page.url == post.url %}
      {% assign class = 'active' %}
    {% else %}
      {% assign class = 'hasUrl' %}
    {% endif %}

    <li class="{{ class }}">
      <a href="{{ post.url }}" style="font-size: .76em;">
        <sub>{{ post.date | date: "%m.%d." }}&nbsp;</sub>
        {{ post.title }}
      </a>
    </li>

  {% endfor %} <!-- for post in site.posts -->
</ul>
```
{% endraw %}
<br>

## 색상

목록판의 <sup>(임시? 배경 이미지 무설정의)</sup> 색상 계열을 지정해 주었다.

각 헤더 및 링크 헤더, 목록판 항목들에 대한 적절 색상 변수들 <sup>(마우스 hover 효과나 현재 페이지 링크 강조 등)</sup> 을 지정해 주었다.

| _sass/variables.scss

```scss
// 일부는 기존값에서 수정, 나머지는 새로 추가된 변수들이다.
// 이 외 !default 표기된 변수들은 현재 새로 수정된 색상을 무시 처리하라는 의미로, 사용자가 수정하기 편하게 놓인 항목들이다.

// Headers
$header-heading-color: #f9f7dc;
$header-bg-color: #645f8a;
$header-bg-color-secondary: #39477b;

// Sidebar
$sidebar-bg-color: #f5e7ec;
$sidebar-font-size: 1.4em;
$sidebar-indent: 1rem;
$sidebar-pre-left: 16px;
$sidebar-width: 300px;
$sidebar-padding: 1.8rem;
$sidebar-padding-each: .5rem;

// Text
$section-h1-color: #7e1355;
$section-h2-color: #aa3c6f;

$sidebar-active-color: #d3c1da;
$sidebar-hover-color: #dedae7;
$body-link-pink: #9b0c2b;
$body-link-blue: #1e6bb8;
```
