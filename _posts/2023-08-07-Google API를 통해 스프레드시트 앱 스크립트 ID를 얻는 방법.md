---
title: Google API를 통해 스프레드시트 앱 스크립트 ID를 얻는 방법
date: 2023-08-07 20:00:00 +0900
categories:
  - JavaScript
tags:
  - GoogleAPI
---

## 개요

Google Apps Script는 Google Workspace에서 사용할 수 있는 자동화 및 확장 도구입니다. 이 글에서는 Google API를 사용하여 Google Apps Script의 스크립트 ID를 얻는 방법에 대해 상세히 설명하겠습니다.

## Google Apps Script API 활성화

먼저 Google Cloud Console에 접속해서 Google Apps Script API를 활성화해야 합니다. 활성화란 해당 서비스를 사용할 수 있게 하는 것을 의미합니다.

## OAuth 인증

다음으로 OAuth 인증을 설정해야 합니다. OAuth는 사용자 인증을 위한 표준 프로토콜입니다. 이 인증은 사용자가 스크립트 ID에 접근할 수 있는 권한을 부여합니다.

## API 호출하기

API를 호출할 때는 다음과 같은 정보가 필요합니다.

- `projectId`: Google Cloud Console에서 생성한 프로젝트의 ID
- `scriptId`: 스크립트의 고유한 ID

이러한 정보를 바탕으로 Google Apps Script API를 호출할 수 있습니다.

## 코드 예시

다음은 스크립트 ID를 얻기 위한 코드 예시입니다. 이 코드는 JavaScript를 사용하며, `google-auth-library` 및 `googleapis` 패키지가 필요합니다.

```javascript
const { google } = require('googleapis');
const { auth } = require('google-auth-library');

const client = await auth.getClient({
  keyFile: '/path/to/keyfile.json',
  scopes: 'https://www.googleapis.com/auth/script.projects',
});

const scriptId = 'YOUR_SCRIPT_ID';

const script = google.script('v1');

const projectInfo = await script.projects.get({
  auth: client,
  scriptId: scriptId,
});

console.log(`The project info is ${JSON.stringify(projectInfo.data)}`);
```

`keyFile`은 키 파일의 경로이고, `YOUR_SCRIPT_ID`는 얻고자 하는 스크립트의 ID입니다.

## 마무리

Google API를 사용하여 Google Apps Script의 스크립트 ID를 얻는 것은 상당히 직관적입니다. 위에서 설명한 방법을 따라하면 쉽게 스크립트 ID를 얻을 수 있습니다. 이렇게 얻은 스크립트 ID는 다양한 작업에 활용할 수 있습니다.