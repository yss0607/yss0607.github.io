---
title: React 앱에서 React Testing Library로 DOM 다루기
date: 2023-09-08 20:00:00 +0900
categories:
  - JavaScript
tags:
  - ReactTesting
---

## 소개

이 글에서는 React 앱에서 React Testing Library를 이용하여 DOM을 조작하는 방법에 대해 자세히 알아봅니다. DOM(Document Object Model)이란 웹 페이지를 구성하는 HTML, XML 문서의 프로그래밍 인터페이스입니다. React Testing Library는 사용자의 관점에서 컴포넌트를 테스트하기 쉽게 도와주는 도구입니다.

## React Testing Library의 기본 개념

React Testing Library는 테스트 케이스를 작성할 때 실제로 사용자가 어떻게 인터페이스와 상호작용하는지를 테스트할 수 있게 도와줍니다. `render`와 `fireEvent` 같은 메서드를 제공하여, 코드 상에서 직접적으로 컴포넌트에 이벤트를 발생시키거나, 출력을 확인할 수 있습니다.

## 오류: `TypeError: Cannot destructure property 'asFragment' of 'object null' as it is null.`

주로 이 오류는 `render` 함수가 제대로 동작하지 않아 발생합니다. `render` 함수는 컴포넌트의 렌더링 결과를 반환해야 하는데, 이 때문에 `null`을 반환하면 이런 오류가 발생하게 됩니다.

## 문제 해결 방법

### 1. 의존성 확인
의존성 문제가 있을 수 있으니 `package.json` 파일에서 `@testing-library/react` 패키지의 버전을 확인하세요.

### 2. `cleanup` 사용
테스트가 끝난 후에 이전 테스트의 결과가 다음 테스트에 영향을 주지 않도록 `cleanup` 함수를 사용할 수 있습니다.

### 3. 비동기 처리
비동기적으로 데이터를 불러와야 하는 경우 `waitFor`나 `findBy` 메서드를 사용하여 비동기 처리를 해야 할 수도 있습니다.

## 정리

React 앱에서 DOM을 테스트하기 위해 React Testing Library를 사용하는 것은 매우 효과적입니다. 위에서 언급한 메서드와 오류 해결 방법을 잘 활용한다면 더욱 견고한 앱을 개발할 수 있을 것입니다.