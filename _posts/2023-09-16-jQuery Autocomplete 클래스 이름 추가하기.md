---
title: jQuery Autocomplete 클래스 이름 추가하기
date: 2023-09-16 20:00:00 +0900
categories:
  - JavaScript
tags:
  - Autocomplete
---

## 문제 상황

jQuery의 Autocomplete 기능을 사용할 때, 목록에 특정 클래스 이름을 추가하고 싶다는 문제가 제기되었습니다. StackOverflow에서 해당 질문이 나왔고, 다양한 해결 방법이 제안되었습니다.

## Autocomplete란 무엇인가?

Autocomplete는 사용자가 입력란에 텍스트를 입력하면, 이에 맞는 여러 가지 옵션을 미리 보여주는 기능입니다. 이는 주로 검색어 제안, 주소 입력 등에서 많이 사용됩니다.

## 해결 방법

### jQuery를 이용한 클래스 추가

```javascript
$( ".selector" ).autocomplete({
  open: function() {
    $('.ui-autocomplete').addClass('your-class-name');
  }
});
```

이 코드를 사용하면, Autocomplete 목록이 열릴 때 `ui-autocomplete` 클래스에 `your-class-name` 클래스가 추가됩니다.

### `open` 이벤트 활용

`open` 이벤트는 Autocomplete 목록이 열릴 때 발생합니다. 이 이벤트 내에서 `.addClass()` 메소드를 사용하여 클래스를 추가할 수 있습니다.

### `ui-autocomplete` 클래스의 중요성

`ui-autocomplete`는 jQuery UI 라이브러리에서 자동으로 생성하는 클래스입니다. 이 클래스가 적용된 요소는 Autocomplete 목록을 스타일링하는 데 사용됩니다. 따라서 이 클래스에 추가적인 클래스를 부여하면, 원하는 대로 스타일을 변경할 수 있습니다.

## 마무리

jQuery의 Autocomplete 기능을 사용하여 목록에 클래스를 추가하는 방법은 다양합니다. 위의 예시 코드를 활용하면 쉽고 빠르게 원하는 클래스를 추가할 수 있습니다. 이를 통해 Autocomplete 목록의 스타일을 개인화할 수 있으며, 사용자 경험을 향상시킬 수 있습니다.