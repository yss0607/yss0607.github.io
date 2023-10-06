---
title: Rails 컨트롤러에서 update_attributes 실패 시 처리 방법
date: 2023-08-19 20:00:00 +0900
categories:
  - JavaScript
tags:
  - Rails컨트롤러
---

## 오류 상황 소개

여러분이 Ruby on Rails 프레임워크를 사용하다가 컨트롤러의 `update` 액션에서 `update_attributes` 메서드가 실패하는 상황을 겪을 수 있습니다. 이 문제는 주로 모델의 유효성 검사(validation)에 실패할 때 발생합니다.

## 원인: 유효성 검사 실패

Rails 모델에서는 데이터의 유효성을 검사하기 위해 다양한 검사 기능을 제공합니다. 예를 들어, `validates_presence_of`나 `validates_numericality_of` 같은 유효성 검사 메서드가 있습니다. `update_attributes` 메서드를 호출할 때, 이러한 유효성 검사가 실패하면 메서드는 `false`를 반환합니다.

## 해결 방법 1: `if-else` 구문 사용

```ruby
def update
  @user = User.find(params[:id])
  if @user.update_attributes(user_params)
    # 성공 시 로직
  else
    # 실패 시 로직
  end
end
```

위 코드에서 `if-else` 구문을 사용하여 `update_attributes`가 `true` 또는 `false`를 반환하는지 확인합니다. 이를 통해 성공 또는 실패에 따른 다른 로직을 실행할 수 있습니다.

## 해결 방법 2: `update!` 메서드 사용

다른 방법으로는 `update!` 메서드를 사용하는 것입니다. 이 메서드는 유효성 검사에 실패하면 예외(Exception)를 발생시킵니다. 따라서 `begin-rescue` 블록을 사용하여 예외를 처리할 수 있습니다.

```ruby
def update
  @user = User.find(params[:id])
  begin
    @user.update!(user_params)
    # 성공 시 로직
  rescue ActiveRecord::RecordInvalid
    # 실패 시 로직
  end
end
```

여기서 `ActiveRecord::RecordInvalid`는 유효성 검사에 실패할 때 발생하는 예외입니다.

## 정리

Rails에서 `update_attributes` 메서드가 실패하는 경우, 이는 대부분 모델의 유효성 검사에 실패했기 때문입니다. 이 문제를 해결하기 위해 `if-else` 구문이나 `begin-rescue` 블록을 사용할 수 있습니다. 어떤 방법을 선택할지는 여러분의 프로젝트 요구 사항과 개인적인 취향에 달려 있습니다.