---
title: 일지글 상단 날짜 삽입
---

## 부제에 자동 날짜 삽입

`_posts` 위치 내 게시글들의 날짜들이 `description` 위치에 자동으로 기재되도록, `_layouts/post.html`에서 `_layouts/post_dated.html`를 만들어 `.mainbar > .page-desc` 요소를 수정해 주었다.

| _layouts/post_dated.html
{% raw %}
```html
<div class="mainbar">
  <h1 class="page-title">{{ page.title | default: site.title }}</h1>
  <h3 class="page-desc">{{ page.date | date: "%Y. %m. %d." | default: page.description | default: site.description }}</h3>
  <h3 class="page-desc"></h3>
  <hr>
```
{% endraw %}

## 레이아웃 간략 소개

`_layouts` 위치 내의 html 파일들에 간략 소개 주석을 각각 달아 주었다.

| _layouts/default.html

```html
<!-- /_layouts/default.html -->

<!-- Retains the original header/footer layout in the mainbar div. -->
```

| _layouts/post.html

```html
<!-- /_layouts/post.html -->

<!-- Includes custom header/footer layout of astors-redemption in the mainbar div. -->
<!-- (acts as an actual usage in stead of _layouts/default.html) -->
```

| _layouts/post_dated.html

```html
<!-- /_layouts/post_dated.html -->

<!-- Layout for "dated" posts -->
<!-- Uses the date of the post in the description area of the mainbar -->
<!-- (derived from _layouts/post.html -- other components remain the same) -->
```
<hr style="opacity: 0;">

## 로딩

`link rel="preload"`과 `preconnect`를 사용하여 매번 사용되는 폰트 파일이 가장 먼저 불러다 쓰일 수 있도록 <sup>최적화?</sup> 수정하였다.

| _layouts/default.html | _layouts/post.html | _layouts/post_dated.html
{% raw %}
```html
{% seo %}

<!-- '사용자' 폰트 preload 추가 -->
<link rel="preconnect" href="{{ site.baseurl }}">
<link rel="preload" href="{{ site.baseurl }}{{ '/assets/fonts/NanumSquareL.otf' }}" as="font" crossorigin>
<link rel="preload" href="{{ site.baseurl }}{{ '/assets/fonts/HyliaSerifBeta-Regular.otf' }}" as="font" crossorigin>
<link rel="preload" href="{{ site.baseurl }}{{ '/assets/fonts/NanumSquareEB.otf' }}" as="font" crossorigin>

<!-- 'as' 값 경고로 기존 항목 분리 -->
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link rel="preload" href="https://fonts.googleapis.com/css?family=Open+Sans:400,700&display=swap" as="style">
<link rel="stylesheet" href="https://fonts.googleapis.com/css?family=Open+Sans:400,700&display=swap">
```
{% endraw %}

## 기록

`_posts` 위치 내 아래 글들의 각 내용을 추가하였다.

| 2021-03-15-log-repo-creation.md      | 블로그 개설
| 2021-03-16-sidebar-creation.md       | 왼쪽 목록판 구현
| 2021-03-18-posts-layout-tinkering.md | 레이아웃 추가 구성
| 2021-03-30-post-date-desc-append.md  | 일지글 상단 날짜 삽입

<hr style="opacity: 0;">

<style> .small { font-size: .8em; color: #bebeca; } </style>

<span class="small">4월 1일은 만우절이다. 근데 뭐 중요한 건 아니다.<br>~~잔류 인원들은 대환장 고기 파티를 진행하도록 하자.~~</span>
