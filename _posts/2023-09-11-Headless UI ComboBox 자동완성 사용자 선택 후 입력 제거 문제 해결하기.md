---
title: Headless UI ComboBox 자동완성 사용자 선택 후 입력 제거 문제 해결하기
date: 2023-09-11 20:00:00 +0900
categories:
  - JavaScript
tags:
  - HeadlessUI
---

## 문제 상황

Headless UI ComboBox를 사용할 때 자동완성 기능이 있는데, 문제는 사용자를 선택한 후에도 입력이 자동으로 제거되지 않는다는 것입니다. 이 문제는 사용자 경험에 좋지 않으며, 웹사이트에서는 이러한 문제가 없어야 합니다. 

## 원인: State 관리 문제

이 문제의 주된 원인은 React의 State 관리와 관련이 있습니다. ComboBox 컴포넌트가 현재 입력값을 관리하지 못하고 있기 때문에 사용자가 선택을 하더라도, 그 정보가 즉시 반영되지 않습니다. 

## 해결 방법: `useState` 사용하기

React의 `useState` 훅을 사용하여 입력값을 관리할 수 있습니다. 예를 들어, 사용자가 선택한 항목을 저장할 수 있는 새로운 상태 변수를 만들고, 그 변수를 업데이트할 수 있습니다.

```javascript
const [selectedUser, setSelectedUser] = useState(null);
```

선택이 이루어지면, 이 상태 변수를 업데이트하여 입력값을 제거할 수 있습니다.

```javascript
const handleSelect = (user) => {
  setSelectedUser(user);
  // 입력값 제거 로직
}
```

## 추가 팁: `useEffect` 활용하기

`useEffect` 훅을 사용하여 `selectedUser` 상태 변수가 변경될 때마다 자동으로 입력값을 제거하는 로직을 추가할 수 있습니다. 

```javascript
useEffect(() => {
  if (selectedUser) {
    // 입력값 제거 로직
  }
}, [selectedUser]);
```

이렇게 하면 사용자가 선택을 하면 자동으로 입력값이 제거되므로 사용자 경험이 향상됩니다.

## 요약

Headless UI ComboBox에서 자동완성 기능을 사용할 때 입력이 제거되지 않는 문제는 주로 React의 State 관리 문제에서 발생합니다. `useState`와 `useEffect` 훅을 사용하여 이 문제를 쉽게 해결할 수 있습니다. 이렇게 하면 웹사이트의 사용자 경험을 크게 향상시킬 수 있습니다.