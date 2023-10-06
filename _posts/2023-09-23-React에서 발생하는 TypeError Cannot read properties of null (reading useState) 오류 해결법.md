---
title: React에서 발생하는 TypeError Cannot read properties of null (reading useState) 오류 해결법
date: 2023-09-23 20:00:00 +0900
categories:
  - JavaScript
tags:
  - React에러
---

## 오류 개요

"TypeError: Cannot read properties of null (reading 'useState')" 오류는 React에서 상태 관리를 위해 `useState` 훅을 사용할 때 특정 조건 하에 발생하는 문제입니다. 이 오류는 `useState`가 null 객체에서 호출되려고 할 때 나타납니다. 이 글에서는 이 오류를 어떻게 해결할 수 있는지 구체적인 방법을 설명합니다.

## 오류 발생 원인

이 오류의 주요 원인은 다음과 같습니다:

1. **훅 호출 위치**: 훅은 함수 컴포넌트의 최상위 레벨에서만 호출되어야 합니다.
2. **조건부 렌더링**: 조건부 렌더링을 사용할 때 `useState`를 조건문 안에서 호출하면 안됩니다.

## 해결 방안 1: 훅 호출 위치 확인

훅이 함수 컴포넌트 바깥이나 일반 자바스크립트 함수 안에서 호출되는 경우, 이 오류가 발생할 수 있습니다. 훅을 반드시 함수 컴포넌트의 최상위에서 호출해야 합니다.

```javascript
// 올바른 예
function App() {
  const [state, setState] = useState(0);
  return <div>{state}</div>;
}

// 잘못된 예
function example() {
  const [state, setState] = useState(0); // 이 위치에서는 사용할 수 없습니다.
}
```

## 해결 방안 2: 조건부 렌더링 수정

`useState`를 조건문 안에서 호출하면 React가 훅의 순서를 추적할 수 없어 오류가 발생합니다. 따라서, 조건문 바깥에서 훅을 호출하고, 필요한 로직은 그 이후에 처리해야 합니다.

```javascript
// 올바른 예
function App() {
  const [state, setState] = useState(0);
  if (state > 5) {
    // 로직 처리
  }
  return <div>{state}</div>;
}

// 잘못된 예
function App() {
  if (something) {
    const [state, setState] = useState(0); // 이 위치에서는 사용할 수 없습니다.
  }
}
```

이러한 방법들을 통해 "TypeError: Cannot read properties of null (reading 'useState')" 오류를 효과적으로 해결할 수 있습니다. 코드를 살펴보고 이 문제가 어디에서 발생하는지 확인하면, 적절한 해결책을 빠르게 찾을 수 있을 것입니다.