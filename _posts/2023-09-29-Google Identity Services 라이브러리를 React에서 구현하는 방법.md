---
title: Google Identity Services 라이브러리를 React에서 구현하는 방법
date: 2023-09-29 20:00:00 +0900
categories:
  - JavaScript
tags:
  - GoogleIdentity
---

## 시작하기 전에 필요한 것들

React를 사용하여 웹 앱을 개발하고 있다면, 사용자 인증은 중요한 부분입니다. Google Identity Services는 사용자 인증을 간편하게 할 수 있도록 도와주는 라이브러리입니다. 이 라이브러리를 사용하면 사용자의 Google 계정을 활용하여 빠르고 안전한 인증이 가능합니다. 이 글에서는 이를 React 앱에 어떻게 구현할 수 있는지 단계별로 설명합니다.

## 프로젝트 설정

먼저, 프로젝트의 `index.html` 파일에 Google Identity Services 라이브러리를 추가해야 합니다. `<head>` 태그 내에 아래의 코드를 추가하면 됩니다.

```html
<script src="https://accounts.google.com/gsi/client"></script>
```

## 초기화와 설정

React 컴포넌트 내에서 Google Identity Services를 초기화하려면, `useEffect` 훅을 사용할 수 있습니다. 아래는 초기화와 설정에 필요한 코드 예시입니다.

```javascript
useEffect(() => {
  window.google.accounts.id.initialize({
    client_id: 'YOUR_CLIENT_ID',
  });
  window.google.accounts.id.renderButton(
    document.getElementById('buttonDiv'),
    {
      theme: 'outline',
      size: 'large',
    }
  );
}, []);
```

`YOUR_CLIENT_ID` 자리에는 Google API 콘솔에서 생성한 클라이언트 ID를 넣어줍니다. 

## 인증 처리하기

로그인 버튼을 클릭했을 때 인증을 처리하기 위해서는 아래와 같은 코드를 추가합니다.

```javascript
useEffect(() => {
  window.google.accounts.id.prompt((notification) => {
    if (notification.isNotDisplayed() || notification.isSkippedMoment()) {
      // 사용자가 로그인을 거부한 경우
      return;
    }
    // ID 토큰을 받아서 서버에 전송하는 로직
    let id_token = notification.getNotication().getIdToken();
    // 서버로 id_token을 보내 인증을 완료합니다.
  });
}, []);
```

## 문제 해결

오류가 발생할 경우 가장 흔한 오류는 `INVALID_CLIENT_ID`입니다. 이 오류는 클라이언트 ID가 잘못 설정되었을 때 발생합니다. 클라이언트 ID를 다시 확인하고, 필요하다면 Google API 콘솔에서 다시 생성해야 합니다.

## 정리

이 글에서는 Google Identity Services 라이브러리를 React에서 어떻게 구현하는지에 대해 알아보았습니다. 이를 통해 사용자 인증을 더 안전하고 빠르게 처리할 수 있습니다. 초기화와 설정, 그리고 인증 처리 방법까지 상세하게 설명하였으니 참고하여 개발에 활용하시기 바랍니다.