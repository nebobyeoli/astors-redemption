---
title: 왼쪽 목록판 구현
---

[Jekyll NavBar](https://gist.github.com/pdarragh/c7ca120604c1a1d8b8de){:target="_blank"} gist를 참고하여 왼쪽 목록판을 구현하였다.

`_data/navigation.yml`을 추가해 목록 항목을 표시하고, `_data/navigation.html`에서 반복문으로 각 항목에 접근하도록 해 주었다.

| 참고: [Minimal Mistakes](https://github.com/mmistakes/minimal-mistakes){:target="_blank"} 테마를 사용하는 경우 추가 구현 없이도 [리디렉션 목록판](https://mmistakes.github.io/minimal-mistakes/docs/layouts/#custom-sidebar-navigation-menu){:target="_blank"}을 쓸 수 있다.

<br>

| _data/navigation.yml

```yml
- title: 강낭콩 키우기
  url: /
  sublinks:
    - title: 메인 땅에 헤딩 테스트
      url: /main/
    - title: Another page
      url: /another/

- title: Single Item
  url: /single/

- title: Group of Things
  url: /group/
  sublinks:
    - title: Sub-item 1
      url: /group/si1
    - title: Sub-item 2
      url: /group/si2
    - title: Sub-item 3
      url: /group/si3
```

| _data/navigation.html
{% raw %}
```html
<!-- 아래 내용이 목록판 항목 표시의 핵심이라 할 수 있다. -->

{% for entry in site.data.navigation %}
  {% assign sublinks = entry.sublinks %}
  {% if sublinks %}
    <li {{ current }}>
      <span class="parent">
        {{ entry.title }}
      </span>
      <ul>
        {% for sublink in sublinks %}
          {% if page.url == sublink.url %}
            <li class="active"><a href="{{ site.baseurl }}{{ sublink.url }}">{{ sublink.title }}</a></li>
          {% else %}
            <li><a href="{{ site.baseurl }}{{ sublink.url }}">{{ sublink.title }}</a></li>
          {% endif %}
        {% endfor %}
      </ul>
    </li>
  {% else %}
```
{% endraw %}
<br>

작성된 `_data/navigation.html` 자체를 `_layouts/default.html`에 삽입해, `<body>` 내 하나의 내용 블록과 같이 표시되도록 하였다.

| _layouts/default.html
{% raw %}
```html
<body>
  <header class="page-header" role="banner" style="width: auto !important;">
    <h1 class="project-name">{{ page.title | default: site.title | default: site.github.repository_name }}</h1>
    <h2 class="project-tagline">{{ page.description | default: site.description | default: site.github.project_tagline }}</h2>
    <a href="{{ site.github.repository_url }}" class="btn">View on GitHub</a>
  </header>
  
    <main id="content" class="main-content" role="main">
      <div class="sidebar">
        {% include navigation.html %}
        <!-- 이곳이 목록판이 삽입되는 부분이다. -->
      </div>

      <div class="mainbar">
        {{ content }}
```
{% endraw %}
<br>

`.mainbar`, `.sidebar`, `.parent` 클래스와 기타 변수, 속성을 추가 정의하여 들여쓰기를 기준으로 정렬되어 표시되도록 하였다.

헤더 이미지의 속성을 `cover`로 바꿔, 화면 확대 배율이 달라져도 배경 이미지가 차지하는 공간이 유지될 수 있도록 하였다.

| assets/css/style.scss

```scss
.page-header {
  background: url("../img/titlebg.png") no-repeat fixed;
  background-size: cover;
}
```
