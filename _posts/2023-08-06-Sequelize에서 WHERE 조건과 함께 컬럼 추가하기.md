---
title: Sequelize에서 WHERE 조건과 함께 컬럼 추가하기
date: 2023-08-06 20:00:00 +0900
categories:
  - JavaScript
tags:
  - Sequelize
---

## 문제 상황

Sequelize를 사용할 때, 특정 조건(WHERE)과 함께 쿼리를 할 때 추가적인 컬럼을 포함하고 싶다면 어떻게 해야 할까요? 이 문제는 Sequelize의 고급 쿼리 기능을 이해하고 활용하는 데 있어 중요한 부분입니다.

## 해결 방법: `attributes` 옵션 사용하기

Sequelize에서는 `attributes` 옵션을 사용하여 특정 컬럼만 선택할 수 있습니다. 이 옵션을 활용하면 원하는 컬럼을 쉽게 추가할 수 있습니다. 예를 들어, User 테이블에서 `username`과 `email`만 선택하고 싶다면 다음과 같이 쿼리를 작성할 수 있습니다.

```javascript
const users = await User.findAll({
  attributes: ['username', 'email'],
  where: {
    active: true
  }
});
```

## 고급 활용: 계산된 컬럼 추가하기

또한, `Sequelize.literal`을 사용하여 계산된 컬럼을 추가할 수 있습니다. 예를 들어, 두 컬럼의 값을 더한 결과를 새로운 컬럼으로 추가하고 싶다면 다음과 같이 할 수 있습니다.

```javascript
const users = await User.findAll({
  attributes: [
    'username', 
    'email',
    [Sequelize.literal('column1 + column2'), 'newColumn']
  ],
  where: {
    active: true
  }
});
```

이렇게 하면 `newColumn`이라는 이름의 새로운 컬럼이 생성되고, `column1`과 `column2`의 값을 더한 결과가 저장됩니다.

## 주의 사항: Error `column "newColumn" does not exist`

계산된 컬럼을 추가할 때 주의해야 할 점은 새로운 컬럼 이름이 데이터베이스에 실제로 존재하지 않아야 한다는 것입니다. 그렇지 않으면 `column "newColumn" does not exist`와 같은 오류가 발생할 수 있습니다. 따라서 새로운 컬럼 이름을 정할 때는 기존에 존재하지 않는 이름을 사용해야 합니다.

## 요약

Sequelize에서는 `attributes` 옵션과 `Sequelize.literal`을 활용하여 원하는 컬럼을 쉽게 추가하거나 계산된 컬럼을 생성할 수 있습니다. 이 기능들을 적절히 활용하면 더욱 효율적인 데이터베이스 쿼리를 작성할 수 있습니다.