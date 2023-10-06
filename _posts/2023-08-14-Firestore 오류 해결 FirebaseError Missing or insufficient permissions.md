---
title: Firestore 오류 해결 FirebaseError Missing or insufficient permissions
date: 2023-08-14 20:00:00 +0900
categories:
  - JavaScript
tags:
  - Firestore
---

## 오류 상황 설명

Firestore를 사용하면서 "FirebaseError: Missing or insufficient permissions"라는 오류 메시지가 나타날 수 있습니다. 이 문제는 대게 Firestore 데이터베이스에 액세스하려 할 때 권한 설정이 올바르지 않기 때문에 발생합니다. 이 오류는 코드의 문제뿐만 아니라 Firestore의 보안 규칙과 관련이 있을 수 있습니다.

## 권한 설정 확인

Firestore의 보안 규칙을 체크하세요. Firestore 콘솔에 접속해서 'Rules' 탭을 선택해 규칙을 확인할 수 있습니다. 보안 규칙은 데이터베이스에 누가 액세스할 수 있는지를 제어합니다. 여기서는 'read'와 'write' 권한을 설정할 수 있습니다. 

## 코드 수정

클라이언트나 서버 코드에서 Firestore 데이터에 액세스하기 전에 권한을 체크하도록 코드를 수정할 수 있습니다. 이렇게 하면 권한 문제를 미리 방지할 수 있습니다.

## Firestore 보안 규칙 업데이트

보안 규칙을 업데이트해 문제를 해결할 수 있습니다. 예를 들어, 모든 사용자에게 읽기 권한을 부여하려면 다음과 같은 규칙을 설정할 수 있습니다.

```plaintext
service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      allow read, write: if true;
    }
  }
}
```

하지만 이 설정은 보안에 취약하므로 실제 서비스에는 적합하지 않습니다. 꼭 필요한 권한만 부여하는 것이 중요합니다.

## 마무리

"FirebaseError: Missing or insufficient permissions" 오류는 권한 설정이 잘못되었을 때 주로 발생합니다. 코드 수정과 Firestore 보안 규칙 업데이트를 통해 이 문제를 해결할 수 있습니다. 올바른 규칙 설정은 앱의 보안을 강화하고 이러한 오류를 미리 방지하는 데 중요한 역할을 합니다.