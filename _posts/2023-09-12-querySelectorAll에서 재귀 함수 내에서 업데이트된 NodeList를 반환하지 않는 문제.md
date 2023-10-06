---
title: querySelectorAll에서 재귀 함수 내에서 업데이트된 NodeList를 반환하지 않는 문제
date: 2023-09-12 20:00:00 +0900
categories:
  - JavaScript
tags:
  - querySelectorAll
---

## 문제 정의

개발자들이 자주 마주치는 문제 중 하나는 `querySelectorAll`을 사용하여 웹 페이지의 특정 요소들을 선택할 때, 이 함수가 재귀(자기 자신을 다시 호출하는 함수) 내에서 업데이트된 NodeList를 반환하지 않는 경우가 있다. 이 문제는 특히 동적으로 페이지의 요소가 변경되는 상황에서 더욱 복잡해질 수 있다.

## 원인과 해결 방안

### 원인: Static NodeList

`querySelectorAll`은 "Static NodeList"를 반환합니다. 'Static'은 고정적이라는 뜻으로, 반환된 NodeList는 초기 상태를 계속 유지하게 됩니다. 따라서 후에 DOM이 변경되더라도, `querySelectorAll`로 얻은 NodeList는 업데이트되지 않습니다.

### 해결 방안: 다시 쿼리하기

재귀 함수 내에서는 DOM이 업데이트 될 가능성이 있으므로, 재귀 호출마다 `querySelectorAll`을 다시 실행해야 합니다. 이렇게 하면 최신 상태의 NodeList를 얻을 수 있습니다.

### 해결 방안: Live NodeList 사용

`getElementsByClassName` 또는 `getElementsByTagName` 같은 메서드들은 "Live NodeList"를 반환합니다. 'Live'는 실시간이라는 뜻으로, DOM이 변경될 때 자동으로 업데이트됩니다. 이를 활용하면 문제를 해결할 수 있습니다.

## 예제 코드

```javascript
function recursiveFunction() {
  // querySelectorAll로 얻은 Static NodeList
  const elements = document.querySelectorAll('.some-class');
  
  // 동작
  // ...

  // 다시 쿼리하여 최신 NodeList 얻기
  const updatedElements = document.querySelectorAll('.some-class');

  // 재귀 호출
  if (someCondition) {
    recursiveFunction();
  }
}
```

## 주의사항

이러한 해결 방법들은 각각의 상황에 따라 장단점이 있으므로, 사용 전에 어떤 방법이 더 적합한지 잘 고려해야 합니다. 예를 들어, "Live NodeList"는 실시간으로 업데이트되므로 성능에 영향을 줄 수 있습니다. 

## 결론

`querySelectorAll` 함수가 재귀 함수 내에서 업데이트된 NodeList를 반환하지 않는 문제는 주로 "Static NodeList"의 특성 때문입니다. 이를 해결하기 위해선 재귀 호출마다 다시 쿼리를 실행하거나 "Live NodeList"를 사용하는 방법이 있습니다.