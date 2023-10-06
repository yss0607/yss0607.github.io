---
title: Google App Script 파일 열기 에러 해결 방법
date: 2023-08-26 20:00:00 +0900
categories:
  - JavaScript
tags:
  - GoogleAppScript
---

## 문제 상황 및 에러 메시지
"Sorry, unable to open the file at this time. Please check the address and try again"라는 에러 메시지가 Google App Script를 실행할 때 나타났다면, 이 글은 여러분을 위한 것입니다. 이 에러는 파일의 주소나 연결에 문제가 있을 때 발생합니다.

## 원인 파악
이 에러는 주로 Google Drive와 연동된 스크립트 파일이나 Google Sheets, Google Docs 등을 열려고 할 때 발생합니다. 파일 ID나 URL이 올바르지 않거나, 권한 설정에 문제가 있는 경우가 대부분입니다.

## 해결 방안 1: 파일 ID 확인
파일을 열려고 할 때 사용하는 ID가 올바른지 확인하세요. 잘못된 ID를 사용하면 이런 에러가 발생할 수 있습니다.

1. Google Drive에서 원하는 파일로 이동합니다.
2. 주소창의 URL에서 "https://drive.google.com/file/d/" 뒤에 있는 문자열이 파일 ID입니다.

## 해결 방안 2: 권한 설정
파일에 액세스할 수 있는 권한이 있는지 확인하세요. 권한이 없다면, 파일의 소유자에게 요청하여 권한을 얻어야 합니다.

1. 파일을 우클릭 후 '공유'를 선택합니다.
2. 권한 설정에서 자신의 이메일이 있는지 확인합니다.

## 해결 방안 3: 캐시와 쿠키 삭제
브라우저의 캐시나 쿠키가 문제를 일으킬 수 있습니다. 이를 삭제한 후 다시 시도해 보세요.

1. 브라우저 설정으로 이동합니다.
2. '캐시 삭제' 옵션을 선택하여 캐시와 쿠키를 삭제합니다.

## 마무리
"Sorry, unable to open the file at this time. Please check the address and try again"라는 에러는 주로 파일 ID나 권한, 브라우저 캐시 등에 문제가 있을 때 발생합니다. 위의 해결 방안을 차례대로 시도하여 문제를 해결할 수 있습니다.