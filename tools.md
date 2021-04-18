---
title: Tools & Resources
description: 모딩 자료 및 도구들
---
<style>
   .small { font-size: .8em; color: #819198; }
   ins { text-decoration: underline 2px; text-underline-offset: 3px; }
   strong a:hover { text-decoration: none; }
</style>

# Documents

## [ZeldaMods](https://zeldamods.org/wiki/Main_Page){:target="_blank"}

해당 게임의 구성 요소에 대한 연구 및 모딩 안내 문서 전용 위키

## [BoTW Modding Hub Discord Server](https://discord.com/invite/vPzgy5S){:target="_blank"}

Wii U, Cemu(Wii U 에뮬레이터), Nintendo Switch 플랫폼에 대한 해당 게임의 모딩 중심지<br>(the Modding Hub for Breath of the Wild on Wii U, Cemu and Nintendo Switch)

## [GameBanana > BoTW(Wii U)](https://gamebanana.com/games/5866){:target="_blank"}

완성된 모드작<sub>**(Mods)**</sub>들이 공유되는 곳으로, 모드를 다운로드하고 뜯어 봄을 통해 효과 대체 등에 있어 참고 자료로 사용할 수 있음

# Tools

<ul class="small">
   <li>아래 도구들 대부분은 Python 3.7대 또는 Visual Studio C++ 2019 재배포판을 필요로 한다.</li>
   <li>아래 모든 도구들은 닌텐도에서 제공한 것이 아니라 이전에 모딩을 시도한 사람들이 직접 제작한 것들이다.<br>이들 중 대부분은 역공학(reverse engineering)과 파일 디코딩 작업에 숙련되어 있다.</li>
   <li>기존/초기 원본 도구들 및 자세한 정보는 모딩 허브 디스코드의 #tutorials-tools-resources 채널에서 확인할 수 있다.</li>
</ul>

## [Switch Toolbox](https://github.com/KillzXGaming/Switch-Toolbox){:target="_blank"}

많은 기능이 있지만 대표적으로 **Yaz0 (해당 게임에서 사용하는 인코딩 기법)** 으로 인코딩된 모델과 텍스처 <sub>(texture)</sub> `.sbfres` 파일, 그리고 핵심 구성요소(사용자 캐릭터, dialogue, 로고/인벤토리 아이콘 등)를 포함하는 `.pack` 파일들을 디코딩하고 대체, 속성을 수정하는 데 사용된다.

## [Wildbits](https://github.com/NiceneNerd/Wild-Bits){:target="_blank"}

Switch Toolbox와 유사한 기능을 수행하나, 주로 JSON 형태에서 인코딩된 텍스트 요소들을 수정하는 데 사용되며 GUI도 VSCode와 유사하게, 용이한 편집을 위한 방향으로 구성되어 있다. `ResourceSizeTable.product.srsizetable`의 항목별 값들을 수정하는 도구로 가장 잘 알려져 있다. Wii U와 Nintendo Switch는 하나의 오브젝트를 불러올 때마다 그 오브젝트가 필요한 크기만큼 메모리를 먼저 할당해 주는 과정을 거치는데, 이 각각의 크기값들이 명시되어 있는 데이터 파일이 바로 **ResourceSizeTable (RSTB)** 이다. 모드 실행이 종종 실패하는 가장 큰 이유가 이 RSTB 값이 잘못되었거나, 수정된 파일이 이전보다 너무 커진 것에서 나온다. (이러한 실패는 쉐이더 캐시 컴파일링이 끝난 직후나 이후 시작 화면이 열렸을 때 게임이 닫히는 경우, 또는 세이브 로드 시 무한 로딩이 되는 상황으로 나타난다.)

## [BCML (BoTW Cross-platform Mod Loader)](https://github.com/NiceneNerd/BCML){:target="_blank"}

가장 큰 목적은 여러 개의 모드를 한꺼번에 적용시켜 플레이할 수 있게끔 하는 것이다. Wildbits와 같이 RSTB를 수정하는 기능을 갖고 있으나 모드 경로 내 파일들을 원본, 다른 모드 내 파일들과 대조하여 큰 파일의 할당값으로 수정하는 과정이 자동화되도록 작성되었다. RSTB 외에도 각종 `.pack` 파일간의 불일치성이 있을 때 정보를 합치거나 일치화해 주는 기능도 가진다. 이 때문에 모드 산출물을 보다 정규화하거나 만든 모드의 할당 오류를 고치는 데에 이 도구를 사용하기도 하고, 기능 중 한 가지로 모드 폴더를 [`.bnp`<sup>**(BCML Nano Patch)**</sup>](https://gamebanana.com/news/21580) 배포용 파일로 묶어주는 것이 있다.

## [Ice Spear](https://ice-spear-tools.gitlab.io/){:target="_blank"}

오버월드 및 던전 <sub>(Shrine)</sub> 요소들을 편집하는 데 쓰인다. 맵의 모든 오브젝트는 **정적(Static)** 또는 **동적(Dynamic)** 중 하나의 방법으로 로드된다. 정적 로드 유닛은 해당 구역의 환경 오브젝트(terrain)가 로드될 때 로드되며, `#Link` 시스템을 이용해 상호 인과관계에 의한 로딩을 구현할 수 있다. 동적 로드 유닛은 플레이어 좌표와의 거리에 따라 동적으로 로드되며, MainField나 AoC <sup>(Add-on content -- DLC)</sup> 의 오픈 월드 구역에 한해 유효성을 가진다. 정적 유닛에는 `_Static`, 동적 유닛에는 `_Dynamic`의 접미사가 붙는다.


## [Event Editor](https://github.com/zeldamods/event-editor){:target="_blank"}

`/content/Event/` 폴더에 있는 오브젝트의 EventFlow<sub>(`오브젝트명.sbeventpack/EventFlow/오브젝트명.bfevfl`)</sub>를 노드구조로 표시하고 각 노드(= 이벤트)의 값들을 수정할 수 있게 해 준다.

## [BoTW FS<sup> (File System) </sup> Tools](https://github.com/zeldamods/botwfstools){:target="_blank"}

[`botwfstools`](https://github.com/zeldamods/botwfstools){:target="_blank"}의 `botw-contentfs` 도구는 `/content/` 폴더의 `yaz0` 압축된 팩 파일<sub>(`◆◆.⬤⬤pack`)</sub>들을 임시로 **모두** 압축 해제하여, 압축 단계가 복잡한 파일들을 사용자가 직접 압축 해제하지 않고도 각 내부 파일에 접근할 수 있도록 해 준다. [`fusepy`](https://github.com/fusepy/fusepy){:target="_blank"}와 [`WinFsp`](http://www.secfs.net/winfsp/rel/){:target="_blank"}을 사용하고, 거의 실행 즉시 압축 해제가 완료된다. 이렇게 읽기 모드로 임시 압축 해제된 파일들은 프로그램의 종료와 함께 제거된다.


## [Breath of the Wow](https://www.reddit.com/r/breathofthewow/comments/6b70uk/version_2_of_the_memory_editor/){:target="_blank"}

**[<ins>(원본 설명 링크)</ins>](https://www.reddit.com/r/cemu/comments/67qy8p/introducing_breath_of_the_wow_a_zelda_inventory/){:target="_blank"}**

Cemu로의 게임 실행 중, 게임 프로세스의 메모리를 스캔허고 수정하는 방법으로 기존 또는 임의로 추가한 의상/아이템을 스스로에게 제공하거나 물량/제한/사용자 좌표 항목 등을 변경할 수 있다. 주로 추가/편집한 아이템이 게임 내에서 제대로 표시되는지 시험해 보는 데 사용된다.

#### [Google](https://www.google.com/){:target="_blank"}
<span class="small">기타 용어에 대한 의미나, 도구 프로그램에서 처리 오류가 났을 때 해결법을 찾아보는 데 사용한다.<br>`구글이 답이다. 구글을 애용하자.`</span>

#### [Blender](https://www.blender.org/download/releases/2-81/){:target="_blank"}
<span class="small">3D 모델링/애니메이션 관련 복합 오픈소스 도구로 모델 파일을 교체/수정/보완하는 데 사용한다.</span>

#### [Krita](https://krita.org/){:target="_blank"}
<span class="small">이미지 제작 및 편집 도구로 텍스쳐/아이콘/배경/로고 등의 이미지 요소들을 편집하는 데 사용한다.</span>
