---
title: HTML Drag and Drop API 이해하기
date: 2023-08-01 20:00:00 +0900
categories:
  - JavaScript
tags:
  - HTML
---

## 드래그 앤 드롭이란 무엇인가?

드래그 앤 드롭(Drag and Drop)은 컴퓨터 인터페이스에서 사용자가 마우스나 터치 스크린을 이용해 객체를 다른 위치나 객체 위로 이동시키는 동작을 말합니다. 이 기능은 파일 관리, 텍스트 편집, 그림 그리기 등 다양한 애플리케이션에서 사용됩니다. HTML5에서는 이를 위한 Drag and Drop API를 제공하고 있어, 웹 개발자가 더 쉽게 이러한 기능을 구현할 수 있습니다.

## 기본 동작과 이벤트

드래그 앤 드롭 동작을 수행할 때 발생하는 주요 이벤트에는 `dragstart`, `drag`, `dragenter`, `dragleave`, `dragover`, `drop`, `dragend` 등이 있습니다. 

- `dragstart`: 드래그가 시작될 때 발생
- `drag`: 드래그 중일 때 지속적으로 발생
- `dragenter`: 드래그 대상이 드롭 대상 위로 들어갈 때 발생
- `dragleave`: 드래그 대상이 드롭 대상을 떠날 때 발생
- `dragover`: 드래그 대상이 드롭 대상 위에 있을 때 지속적으로 발생
- `drop`: 실제로 드롭이 실행될 때 발생
- `dragend`: 드래그 앤 드롭 동작이 끝난 후 발생

## 예제 코드 분석

```html
<!DOCTYPE HTML>
<html>
  <body>
    <div id="div1" ondrop="drop(event)" ondragover="allowDrop(event)"></div>
    <img id="drag1" src="img_logo.gif" draggable="true" ondragstart="drag(event)">
  </body>
</html>
```

```javascript
function allowDrop(ev) {
  ev.preventDefault();
}

function drag(ev) {
  ev.dataTransfer.setData("text", ev.target.id);
}

function drop(ev) {
  ev.preventDefault();
  var data = ev.dataTransfer.getData("text");
  ev.target.appendChild(document.getElementById(data));
}
```

이 코드에서 `ondragstart` 이벤트는 드래그가 시작될 때 `drag` 함수를 호출합니다. `setData` 함수를 사용하여 드래그되는 대상의 `id`를 저장합니다. `ondrop`과 `ondragover` 이벤트는 드롭이 실행될 때 `drop` 함수와 `allowDrop` 함수를 호출합니다. `allowDrop` 함수에서 `preventDefault`를 호출하여 기본 드롭을 허용하게 하고, `drop` 함수에서 실제로 드롭을 처리합니다.

## 주의할 점

### Error: Uncaught TypeError: Failed to execute 'appendChild' on 'Node': parameter 1 is not of type 'Node'.

위의 코드에서 드롭 대상(`div1`)이 이미 자식 노드를 가지고 있는 경우, 또는 드래그 대상(`drag1`)이 없는 경우 이 에러가 발생할 수 있습니다. 이는 `appendChild` 함수에 전달되는 파라미터가 유효한 HTML 노드가 아니기 때문입니다. 이 문제를 해결하기 위해선 `getElementById`로 가져온 노드가 실제로 존재하는지 확인하는 코드를 추가할 수 있습니다.

이렇게 HTML Drag and Drop API를 이해하고 사용하면 사용자 경험을 향상시킬 수 있는 다양한 웹 애플리케이션을 개발할 수 있습니다.