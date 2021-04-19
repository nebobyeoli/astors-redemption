---
title: 대화 문구 추가 시도
---

<style>
    div.language-yaml.highlighter-rouge,
    td {
        width: 35vw;
        display: inline-block;
    }
    
    div.highlight {
        height: 400px;
        overflow-y: scroll;
    }
</style>

## MSBT 문구 추가

일부 대화 문구의 사이에 `control: kind: choice`를 집어 넣어, 중간에 부연 설명이 들어가도록 함을 시도하였다.
<br><br>

| **원본** <b>`(0012 ~ near01)`</b> &nbsp;&nbsp;Npc_HatenoVillage001.msbt | **수정** <b>`(0012 ~ near01)`</b> &nbsp;&nbsp;Npc_HatenoVillage001.msbt
{% raw %}
```yaml
  "0012":
    attributes: ""
    contents:
      - text: Back to the original.
  "0013":
    attributes: ""
    contents:
      - text: Use these clothes.

  near01:
    attributes: Npc_HatenoVillage001
    contents:
      - text: Greetings and saturations!
```
```yaml
  "0012":
    attributes: ""
    contents:
      - text: Back to the original.
  "0013":
    attributes: ""
    contents:
      - text: Use these clothes.

  ## 0014, 0015, 0016 추가
  "0014":
    attributes: ""
    contents:
      - text: Traditional dyeing?
      - control:
          kind: choice
          choice_labels:
            - 16  # 'Long text from Traditional dyeing!\n\nlong long text'
            - 16  # 'Long text from Traditional dyeing!\n\nlong long text'
          selected_index: 0
          cancel_index: 16
          unknown: 16
  "0015":
    attributes: ""
    contents:
      - text: Ancient clothing?
  "0016":
    attributes: Npc_HatenoVillage001
    contents:
      - control:
          kind: pause
          length: long
      - text: "Long text from Traditional dyeing!\n\nlong long text"
  ## 추가 끝

  near01:
    attributes: Npc_HatenoVillage001
    contents:
      - text: Greetings and saturations!
```
{% endraw %}

| **원본** <b>`(talk16)`</b> &nbsp;&nbsp;Npc_HatenoVillage001.msbt | **수정** <b>`(talk16)`</b> &nbsp;&nbsp;Npc_HatenoVillage001.msbt
{% raw %}
```yaml
  talk16:
    attributes: Npc_HatenoVillage001
    contents:

      - control:
          kind: sound
          unknown:
            - 5
            - 6
      - text: "I love the fact that someone so young is\nso interested in our unique "
      - control:
          kind: set_colour
          colour: blue
      - text: Hateno dyes
      - control:
          kind: reset_colour
      - text: ".\n\n"
```
```yaml
  talk16:
    attributes: Npc_HatenoVillage001
    contents:

      ## 부연 텍스트 및 control: kind: choice 추가
      - text: What do you want to know more about?
      - control:
          kind: choice
          choice_labels:
            - 14  # 'Traditional dyeing?'
            - 15  # 'Ancient clothing?'
            - 6   # 'Actually, never mind.'
          selected_index: 0
          cancel_index: 6
          unknown: 10
      ## 추가 끝

      - control:
          kind: sound
          unknown:
            - 5
            - 6
      - text: "I love the fact that someone so young is\nso interested in our unique "
      - control:
          kind: set_colour
          colour: blue
      - text: Hateno dyes
      - control:
          kind: reset_colour
      - text: ".\n\n"
```
{% endraw %}

<hr style="opacity: 0;">

## 변경 내용 저장법

1. **Wildbits**로 `/contents/Pack/Bootup_USen.pack`를 열어 `Message/Msg_USen.product.ssarc` 내 `EventFlowMsg/Npc_HatenoVillage001.msbt` 파일을 `YAML` 탭에서 수정하고 저장한다.
2. `SARC` 탭으로 돌아가 다시 저장하고, `Msg_USen.product.ssarc`에서 `Extract`를 눌러 외부 파일로 저장시킨다.
3. `RSTB` 탭에서 `/contents/System/Resource/`의 RSTB 파일 `ResourceSizeTable.product.srsizetable`을 연다.
4. `Filter RSTB entries`<sup> (주의: 대소문자 구분 **있음**) </sup>에 `Msg_USen`을 검색해, `Message/Msg_USen.product.sarc`의 편집 아이콘을 누르고 `Browse`를 사용해 해당 `RSTB Entry`값을 2단계에서 추출한 `Msg_USen.product.ssarc`의 크기로 설정해 준다.

<br>

## 결과 확인

추가된 선택지 `'Traditional dyeing?'`, `'Ancient clothing?'`, `'Actually, never mind.'` 중 어떤 것을 선택하느냐에 관계없이, `0014`, `0015`, `0016`의 첫 번째 `text` 이후의 문구들은 출력되지 않으며, 선택 후 바로 다시 `talk16`의 나머지 내용으로 넘어간 문구<sup> (`'I love the fact that someone so young is so interested in ~ '`) </sup>가 출력됨을 볼 수 있다.

이와 같은 결과가 나오는 이유는 `msbt` 문구 <sup>추가</sup> 여부에 관계없이 해당 NPC의 `Event` 또는 게임 본체에서 각 대화 문구의 흐름 순서를 지정해 놓았기 때문인 것으로 보인다.

<iframe width="1280" height="360" src="https://www.youtube.com/embed/lqj2n39JatM" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
