---
title: 염색 NPC 문구 기록
---

<style>
    div.language-yaml.highlighter-rouge,
    td {
        width: 35vw;
        display: inline-block;
    }
    
    div.highlight {
        height: 480px;
        overflow-y: scroll;
    }
</style>

## 원본 대화 문구 옮기기

텍스트 흐름의 순서 확인 및 `msbt` 텍스트 파일과의 내용 배치 확인 목적으로, 염색 NPC<sup> (영문 이름: **Sayge**) </sup>의 원본 대화 문구의 일부를 텍스트 순서 위주로 텍스트 파일에 기록하였다.

기록은 아래 경로<sup> <b>(압축파일 내장된 파일 포함)</b> </sup>의 대화 텍스트를 순서대로 가져와 일부 축약하는 방식으로 진행하였다.

```fs
/content/Pack/Bootup_USen.pack/Message/Msg_USen.product.ssarc/EventFlowMsg/Npc_HatenoVillage001.msbt
```
<br>

| Npc_HatenoVillage001.msbt.txt | Npc_HatenoVillage001.msbt
{% raw %}
```yaml
# 옮긴 형식
# 게임 내에서 나타나는 형식과 가깝게 표시되도록 기록하였다.

Sayge:

  talk00:
    - Welcome! If you were looking to add
      some color to your wardrobe, you found
      the right place! Hue do you do?
  talk41:
    - These rainy days remind me of the most
      romantic date I ever went on.
    - There we were, standing in the soaking
      rain, and I got down on one knee to
      propose. Couldn't have timed it better!
  [talk14]

  talk42:
    - Hee har ha! If you're not a pigment of
      my imagination, you must be a customer!
  [talk14]

  talk14:
    - Here we go! For <red>20 rupees</red> total, I'll
      dye your <blue>clothes</blue> here to the color of
      your choosing!
    - Or would you like to get back to square
      one and change your clothes back to
      their original color?

    choices:

      0001:
        - Yes, dye!

        talk26:
          - Hrm... You don't have any <blue>clothes that
            can be dyed</blue>! Come back after you
            develop your wardrobe a bit.

        talk06:
          - Wonderful. Now go wait up there.
            I'll just be a minute.
        talk48:
          - Get ready! Because we are going to dye
            all the <red>clothes you're wearing</red> at once!
        talk15:
          - All right, choose your <blue>dye color</blue> or go
            ahead and <blue>change clothes</blue>!

            choices:
            
              0009:
                - Choose a color.

                talk10:
                  - Which dye color would you like?

                talk27:
                  - Hmm... You don't quite have enough
                    ingredients to dye to that color. Sorry!

                talk28:
                  - Choose <red>five</red> ingredients you'd like to use
                    in your dye!
                  talk02:
                    - OK then, that'll be <red>20 rupees</red>!

                    choices:

                      0004:
                        - OK!

                      0005:
                        - Choose again.
                        [talk28]

                talk29:
                  - Did you want to try another color? Or do
                    you want to stop here?

                    choices:

                      0004:
                        - Choose again.

                      0005:
                        - Quit.

                        talk12:
                          - Come back again. Every day is a good
                            day to dye!

              0010:
                - Change clothes.

              0006:
                - Actually, never mind.

      0008:
        - Tell me more.

        talk16:
          - I love the fact that someone so young is
            so interested in our unique <blue>Hateno dyes</blue>.
          - It is indeed part of my duty to keep the
            young people from losing their interest
            in the tradition...
          - Let me give you all the colorful details of
            how the magic works!
        talk21:
          - <blue>Hateno dyeing</blue> is a traditional craft of
            Hateno Village. In days past, we'd
            use our own prepared <blue>dye ingredients</blue>.
          - But these days, there are so many
            <blue>monsters</blue> about, that it's difficult for
            us to gather <blue>ingredients</blue>...
          - That's why we switched to the customer
            bringing us the <blue>dye ingredients</blue>, and in
            return, we have a small service charge.
        talk37:
          - I can also <blue>remove color</blue> from dyed
            fabric so your clothes will be restored to
            their original, if not drab, luster.

      0012:
        - Back to the original.

      0003:
        - No, thanks.

        talk04:
          - Come 'round again! Every day is a good
            day to dye!
```
```yaml
# 원본 형식
# 전체 내용 중 일부
# msbt 내용값들은 게임 진행 순서 상으로는 「순서 없는 나열」이다. ≒ 해시 테이블

# - 중략 -

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
  talk00:
    attributes: Npc_HatenoVillage001
    contents:
      - control:
          kind: sound
          unknown:
            - 7
            - 9
      - text: "Welcome! If you were looking to add\nsome color to your wardrobe, you found\nthe right place! "
      - control:
          kind: pause
          length: short
      - text: Hue do you do?

# - 중략 -

  talk14:
    attributes: Npc_HatenoVillage001
    contents:
      - control:
          kind: sound
          unknown:
            - 7
            - 4
      - text: "Here we go! For "
      - control:
          kind: set_colour
          colour: red
      - text: "20 rupees "
      - control:
          kind: reset_colour
      - text: "total, I'll\ndye your "
      - control:
          kind: set_colour
          colour: blue
      - text: clothes
      - control:
          kind: reset_colour
      - text: " here to the color of\nyour choosing! \nOr would you like to get back to square\none and change your clothes back to\ntheir original color?"
      - control:
          kind: choice
          choice_labels:
            - 1
            - 8
            - 12
            - 3
          selected_index: 0
          cancel_index: 3
          unknown: 10

# - 중략 -

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
      - control:
          kind: sound
          unknown:
            - 6
            - 1
      - text: "It is indeed part of my duty to keep the\nyoung people from losing their interest\nin the tradition..."
      - control:
          kind: pause
          length: short
      - text: "\n"
      - control:
          kind: sound
          unknown:
            - 7
            - 0
      - text: "Let me give you all the colorful details of\nhow the magic works!"

# - 중략 -
```
{% endraw %}
