---
title: React Native에서 하이퍼링크 표시 방법
date: 2023-08-20 20:00:00 +0900
categories:
  - JavaScript
tags:
  - ReactNative
---

## 문제 상황

React Native 앱에서 하이퍼링크를 어떻게 표시할 수 있는지는 많은 개발자들이 궁금해하는 문제 중 하나입니다. 대부분의 웹 기반 언어에서는 이를 매우 쉽게 할 수 있지만, React Native에서는 약간의 추가 작업이 필요합니다.

## 기본 솔루션: `Linking` 모듈 사용하기

React Native에서는 `Linking`이라는 모듈을 사용하여 하이퍼링크를 실행할 수 있습니다. 이 모듈은 웹 브라우저나 다른 앱을 열 수 있게 해줍니다. 예를 들어, 다음과 같이 코드를 작성할 수 있습니다.

```javascript
import { Linking } from 'react-native';

Linking.openURL('https://www.example.com');
```

## 고급 솔루션: `Touchable` 컴포넌트와 결합하기

`Touchable` 컴포넌트 (예: `TouchableOpacity`, `TouchableHighlight` 등)를 사용하면 더 사용자 친화적인 경험을 제공할 수 있습니다.

```javascript
import { Linking, TouchableOpacity, Text } from 'react-native';

const OpenURLButton = ({ url, label }) => {
  const handlePress = () => Linking.openURL(url);

  return (
    <TouchableOpacity onPress={handlePress}>
      <Text>{label}</Text>
    </TouchableOpacity>
  );
};
```

## 예외 처리하기: `canOpenURL` 메소드

하이퍼링크를 열기 전에 해당 URL을 열 수 있는지 확인하려면 `canOpenURL` 메소드를 사용할 수 있습니다.

```javascript
Linking.canOpenURL('https://www.example.com')
  .then((supported) => {
    if (supported) {
      return Linking.openURL('https://www.example.com');
    }
  })
  .catch((err) => console.error('An error occurred', err));
```

## 정리

React Native에서 하이퍼링크를 표시하는 방법은 다양하지만, 가장 기본적인 방법은 `Linking` 모듈을 사용하는 것입니다. 더 나아가 사용자 친화적인 방법을 원한다면 `Touchable` 컴포넌트와 함께 사용할 수 있습니다. 예외 처리를 위해 `canOpenURL` 메소드를 사용할 수도 있습니다. 이러한 방법들을 활용하면 React Native 앱에서 효과적으로 하이퍼링크를 관리할 수 있습니다.