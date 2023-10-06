---
title: 브라우저에서 navigator.mediaDevices.enumerateDevices가 audioinput만 표시하고 videoinput을 표시하지 않는 문제 해결하기
date: 2023-09-22 20:00:00 +0900
categories:
  - JavaScript
tags:
  - navigator
---

## 원인 파악

이 문제가 발생하는 주된 원인은 보안 문제와 권한 문제입니다. HTTPS 환경에서만 `navigator.mediaDevices.enumerateDevices` 함수가 제대로 작동하며, 사용자가 카메라 접근을 허용하지 않은 경우 이 함수는 비디오 디바이스를 나열하지 않을 수 있습니다.

## 해결 방안 1: HTTPS 환경 확인

웹 사이트가 HTTPS를 사용하고 있는지 확인하세요. HTTPS는 'HyperText Transfer Protocol Secure'의 약자로, 보안이 강화된 웹 통신 프로토콜입니다. 만약 HTTP 환경에서 작동하고 있다면, 이를 HTTPS로 변경해야 합니다.

## 해결 방안 2: 사용자 권한 확인

`navigator.mediaDevices.getUserMedia` 함수를 이용하여 사용자로부터 카메라 접근 권한을 명시적으로 요청할 수 있습니다. 사용자가 허용하면 `enumerateDevices` 함수는 `videoinput`을 제대로 나열해 줄 것입니다.

```javascript
navigator.mediaDevices.getUserMedia({ video: true })
  .then(stream => {
    // 여기에서 스트림을 사용하거나 닫을 수 있습니다.
    stream.getTracks().forEach(track => track.stop());
  })
  .catch(err => {
    // 에러 처리
    console.error("Error: ", err);
  });
```

## 해결 방안 3: 브라우저 캐시와 쿠키 삭제

이전에 웹 사이트에 접속했을 때의 설정이 현재 문제를 일으킬 수도 있습니다. 브라우저의 캐시와 쿠키를 삭제한 후 다시 시도해 보세요.

## 결론

`navigator.mediaDevices.enumerateDevices` 함수가 `audioinput`만 나열하고 `videoinput`을 나열하지 않는 문제는 주로 HTTPS 환경과 사용자 권한, 브라우저 캐시에 관련이 있습니다. 이 문제를 해결하기 위해서는 이러한 요소들을 체크하고 조정해야 합니다. 이를 통해 웹 페이지에서 카메라와 마이크에 원활하게 접근할 수 있을 것입니다.