---
title: JavaScript에서 화면 표시 전 DOM 트리 조작하기
date: 2023-09-19 20:00:00 +0900
categories:
  - JavaScript
tags:
  - DOM트리조작
---

## 소개
JavaScript와 jQuery를 사용하여 웹 페이지가 브라우저에 표시되기 전에 DOM(Document Object Model) 트리를 조작하는 방법에 대해 알아보겠습니다. DOM 트리는 웹 페이지의 구조를 나타내는 표현 방식입니다. 이를 통해 웹 페이지의 여러 요소를 쉽게 제어할 수 있습니다.

## `DOMContentLoaded` 이벤트 사용하기
`DOMContentLoaded` 이벤트는 HTML 문서가 완전히 로드된 직후 발생합니다. 이 시점에는 외부 스크립트와 스타일시트가 아직 로드되지 않은 상태일 수 있습니다. 이 이벤트를 사용하면 화면 표시 전에 DOM을 조작할 수 있습니다.

```javascript
document.addEventListener("DOMContentLoaded", function() {
  // 여기에 DOM 조작 코드를 작성합니다.
});
```

## jQuery `$(document).ready()` 사용하기
jQuery를 사용하는 경우 `$(document).ready()` 메서드를 이용할 수 있습니다. 이 메서드도 `DOMContentLoaded` 이벤트와 유사한 역할을 합니다.

```javascript
$(document).ready(function() {
  // 여기에 DOM 조작 코드를 작성합니다.
});
```

## `defer` 속성 활용하기
`<script>` 태그에 `defer` 속성을 추가하면, 스크립트는 문서 파싱이 완료된 후에 실행됩니다. 이 방법을 사용하면 외부 스크립트 로딩이 DOM 조작에 방해되지 않습니다.

```html
<script defer src="your-script.js"></script>
```

## 주의사항
화면 표시 전에 DOM을 조작할 때는 몇 가지 주의할 점이 있습니다.

1. **호환성**: 모든 브라우저가 위에 언급된 메서드나 이벤트를 지원하지 않을 수 있습니다.
2. **코드 순서**: DOM을 조작하는 코드가 먼저 실행되어야 합니다. 그렇지 않으면 원하는 결과를 얻을 수 없습니다.
3. **비동기 처리**: AJAX 호출 같은 비동기 작업이 있는 경우, 해당 작업이 완료되기를 기다린 후에 DOM을 조작해야 할 수도 있습니다.

## 결론
화면 표시 전에 DOM을 조작하려면 `DOMContentLoaded` 이벤트, jQuery의 `$(document).ready()` 메서드, 또는 `defer` 속성을 활용할 수 있습니다. 각 방법에는 장단점이 있으므로 상황에 따라 적절한 방법을 선택하면 됩니다. 이러한 기술을 활용하면 웹 페이지의 사용성과 반응성을 향상시킬 수 있습니다.