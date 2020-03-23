---
description: 객체가 CALayer 변경에 의해 트리거 된 액션에 응답할 수 있게 해주는 인터페이스
---

# CAAction

> 원문 출처  
> [https://developer.apple.com/documentation/quartzcore/caaction](https://developer.apple.com/documentation/quartzcore/caaction)

## Summary

> **SDKs**
>
> * iOS 2.0+
> * macOS 10.5+
> * tvOS 9.0+
> * Mac Catalyst 13.0+
>
> **Framework**
>
> * Core Animation

## Declaration

{% tabs %}
{% tab title="Swift" %}
```swift
protocol CAAction
```
{% endtab %}

{% tab title="Objective-C" %}
```objectivec
@protocol CAAction
```
{% endtab %}
{% endtabs %}

## 개요 <a id="overview"></a>

Action 식별자\(key path, 외부 action 이름 또는 미리 정의된 작업 식별자\)로 쿼리할 때 레이어는 적절한 action 객체\([CAAction](caaction.md) 프로토콜이 구현되어있어야 함\)를 반환하고 [run\(forKey:object:arguments:\)](../../etc/not-found.md) 메시지를 전송합니다.

## 주제 <a id="topics"></a>

### 액션에 응답하기 <a id="responding-to-an-action"></a>

* func run\(forKey: String, object: Any, arguments: \[AnyHashable : Any\]?\)

  `forKey:` 식별자로 지정된 action을 호출합니다. `Required`

## 관련 문서

### 준수하는 프로토콜

* CAAnimation
* NSNull

## 같이 보기

### 레이어 기초

* _class_ [CALayer](calayer.md)

  이미지 기반 컨텐츠를 관리하고 해당 컨텐츠에 대해 애니메이션을 수행할 수 있는 객체

* _protocol_ CALayerDelegate 레이어 관련 이벤트에 응답하기 위해 앱이 구현할 수 있는 메서드
* _class_ CAConstraint 두 레이어 사이의 단일 레이아웃 제약 조건
* _protocol_ CALayoutManager 객체가 레이어와 그 하위 레이어의 레이아웃을 관리할 수 있게 해주는 메서드
* _class_ CAConstraintLayoutManager

  제약 기반 레이아웃 관리자를 제공하는 객체



