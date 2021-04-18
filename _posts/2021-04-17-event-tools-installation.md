---
title: 이벤트 도구 설치
---

디스코드 검색 결과 NPC의 대화 내용을 수정하는 것에서 나아가, 대화 내용을 더 추가하기 위해서는 해당 NPC의 `msbt` 뿐만 아니라 <b>EventFlow</b>의 대화 노드까지 추가 수정해야 한다는 내용이 있었다.

Wildbits로 `/content/Event/Npc_HatenoVillage001.sbeventpack`를 열었을 때, 그 안의 `EventFlow/` 내 `.bfevfl` 확장자의 EventFlow 파일들을 수정하기 위해서는 다른 보조 도구들이 필요했다.

## 추가 도구 설치

이벤트 편집을 위한 추가 도구들 [`eventeditor`](https://github.com/zeldamods/event-editor){:target="_blank"}, [`botwfstools`](https://github.com/zeldamods/botwfstools){:target="_blank"}를 설치하였다.

[`eventeditor`](https://github.com/zeldamods/event-editor){:target="_blank"}는 `/content/Event/` 폴더에 있는 오브젝트의 EventFlow<sub>(`오브젝트명.sbeventpack/EventFlow/오브젝트명.bfevfl`)</sub>를 노드구조로 표시하고 각 노드(= 이벤트)의 값들을 수정할 수 있게 해 준다.

[`botwfstools`](https://github.com/zeldamods/botwfstools){:target="_blank"}의 `botw-contentfs` 도구는 `/content/` 폴더의 `yaz0` 압축된 팩 파일<sub>(`◆◆.⬤⬤pack`)</sub>들을 임시로 **모두** 압축 해제하여, 압축 단계가 복잡한 파일들을 사용자가 직접 압축 해제하지 않고도 각 내부 파일에 접근할 수 있도록 해 준다. [`fusepy`](https://github.com/fusepy/fusepy){:target="_blank"}와 [`WinFsp`](http://www.secfs.net/winfsp/rel/){:target="_blank"}을 사용하고, 거의 실행 즉시 압축 해제가 완료된다. 이렇게 읽기 모드로 임시 압축 해제된 파일들은 프로그램의 종료와 함께 제거된다.

<br>

## EventEditor 사용

먼저<sub> (모드 폴더 밖의)</sub> 아무 곳에 `아무경로/temp/`의 빈 폴더를 만들어 주고 `botw-contentfs "게임경로/Base,DLC,Update합친폴더/content" "아무경로/temp/content"`를 실행하여 임시 압축 해제 파일들을 생성해 주었다. 다음으로 `아무경로/ArcExtracted/content/` 폴더를 만들어 `아무경로/temp/content/`의 `Actor/`, `Pack/` 폴더를 복사해 주고 `botw-contentfs`를 종료시켰다.
<br><br>
그리고 `%appdata%/eventeditor/eventeditor.ini`의 맨 아래에

```ini
[paths]
rom_root=아무경로/ArcExtracted/content
```
를 추가해, 복사한 파일들을 EventEditor가 참조할 수 있도록 하였다.
<br><br>
EventEditor를 실행<sub>(cmd 또는 윈도우 검색창에 `eventeditor` 실행)</sub>해 `Npc_HatenoVillage001.bfevfl`를 열어 주고, 상단 메뉴 `Flowchart > Add Event > Action` 선택 후, 새로 생긴 이벤트를 더블 클릭해서 각 드랍다운에 `Npc_HatenoVillage001`과 `Demo_Talk`를 선택하고 `Auto fill`을 눌러, 해당 이벤트 종류의 필수 인자(속성)값들이 자동 추가됨을 볼 수 있었다.

![before-autofill]({{ site.baseurl }}{{ '/assets/img/2021-04-17_1.png' }}){:width="720"}
![after-autofill]({{ site.baseurl }}{{ '/assets/img/2021-04-17_2.png' }}){:width="720"}
