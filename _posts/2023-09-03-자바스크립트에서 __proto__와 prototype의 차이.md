---
title: 자바스크립트에서 __proto__와 prototype의 차이
date: 2023-09-03 20:00:00 +0900
categories:
  - JavaScript
tags:
  - proto
---

## 개요

자바스크립트는 프로토타입 기반의 언어입니다. 이러한 개념을 이해하는 데 있어서 `__proto__`와 `prototype`은 매우 중요한 역할을 합니다. 하지만 이 두 개념이 종종 혼동되기도 합니다. 이 글에서는 `__proto__`와 `prototype`의 차이점과 각각 어떻게 사용되는지에 대해 자세히 알아보겠습니다.

## `__proto__`의 역할

`__proto__`는 객체가 생성될 때 그 객체의 부모(프로토타입)를 참조하는 내부 속성입니다. 즉, 어떤 객체 A가 있을 때, A의 `__proto__`는 A가 상속받은 부모 객체를 가리킵니다. 이 부모 객체는 A 객체가 사용할 수 있는 메소드와 속성을 제공합니다.

```javascript
const animal = { type: 'Animal' };
const dog = Object.create(animal);
console.log(dog.__proto__ === animal);  // true
```

## `prototype`의 역할

`prototype`은 함수만 가지고 있는 속성입니다. 이 속성은 해당 함수로 생성된 모든 객체가 공유할 수 있는 메소드와 속성을 포함하는 객체를 가리킵니다. 예를 들어, 함수 `Dog`가 있고, 이 함수로 생성된 객체가 `buddy`라면, `Dog.prototype`에 추가한 모든 것은 `buddy` 객체에서도 사용할 수 있습니다.

```javascript
function Dog() {}
Dog.prototype.bark = function() {
  console.log('Woof!');
};
const buddy = new Dog();
buddy.bark();  // Woof!
```

## `__proto__`와 `prototype`의 관계

두 개념의 가장 큰 차이는, `__proto__`는 어떤 객체든 가질 수 있지만, `prototype`은 함수만이 가질 수 있다는 것입니다. 또한, 함수의 `prototype` 객체의 `constructor` 속성은 그 함수 자신을 가리키고, 이 `prototype` 객체는 함수로 생성된 새 객체의 `__proto__`가 됩니다.

## 주의할 점: Error명은 원문과 동일하게

`__proto__`를 직접 조작하는 것은 권장되지 않습니다. 이로 인해 발생하는 에러는 `TypeError`가 일반적입니다.

## 결론

`__proto__`와 `prototype`은 자바스크립트에서 객체와 함수가 어떻게 상호작용하는지 이해하는 데 있어 핵심 요소입니다. `__proto__`는 객체의 부모를, `prototype`은 함수로 생성된 객체가 공유할 메소드와 속성을 가리킵니다. 이 두 개념을 명확히 이해하면, 자바스크립트의 중요한 부분을 더 잘 이해할 수 있습니다.