---
title: 블로그 개설
---

## 초기 설정

Jekyll과 Github Pages를 이용한 개발 일지 블로그를 개설하였다.

| 공식 문서: [Jekyll Quickstart](https://jekyllrb.com/docs/){:target="_blank"}
| Github 로컬 실행 참고 문서: [Testing your GitHub Pages site locally with Jekyll](https://docs.github.com/en/github/working-with-github-pages/testing-your-github-pages-site-locally-with-jekyll){:target="_blank"}

<br>
레포지토리 설정 페이지에서 `Cayman` 테마를 사용하도록 해 주고, 생성된 `_config.yml`에서 기본값 제목 및 보조 문구를 설정해 주었다.

| _config.yml

```yml
theme: jekyll-theme-cayman
title: Astor's Redemption
description: Logs of a long-termed, story-changing BoTW modding project.
```

## 로컬 실행

로컬상에서의 블로그 미리보기가 가능하도록 [`Ruby Devkit`](https://rubyinstaller.org/downloads/){:target="_blank"}을 설치해 주었다.<br>
`Gemfile`을 추가하여 기본 작동 의존성을 가져오도록 해 주었다.

| Gemfile

```Gemfile
source 'https://rubygems.org'
gemspec
```

로컬 빌드 명령은 `bundle exec jekyll serve`, `localhost:4000`으로 연결된다.

## 레이아웃 편집

원본 `Cayman` 테마의 레이아웃 파일을 `_layouts/default.html`로 받아 구성 요소 등 속성을 수정해 주었다.

| Jekyll 사이트의 디렉토리 구조 참고: [Jekyllrb - Directory Structure](https://jekyllrb.com/docs/structure/){:target="_blank"}
| [한글화 문서 (가급적 원어 문서를 추천)](https://jekyllrb-ko.github.io/docs/structure/){:target="_blank"}

<br>
배경 배너 이미지, 글꼴([**Hylia Serif**](http://artsyomni.com/hyliaserif){:target="_blank"}, [나눔스퀘어](https://hangeul.naver.com/font){:target="_blank"}), 색상 계열, 아이콘 등을 설정해 주었다.

- _layouts/
  - default.html
- assets/
  - css/
    - style.scss
  - fonts/
    - HyliaSerifBeta-Regular.otf
    - NanumSquareB.ttf
    - NanumSquareEB.ttf
    - NanumSquareL.ttf
    - NanumSquareR.ttf
  - img/
    - Logo_favicon.png
    - titlebg.png
