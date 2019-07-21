---
description: 세션 내에서의 요청에 대해 캐쉬된 응답을 제공하는 URL cache
---

# urlCache

> 원문 출처  
> [https://developer.apple.com/documentation/foundation/urlsessionconfiguration/1410148-urlcache](https://developer.apple.com/documentation/foundation/urlsessionconfiguration/1410148-urlcache)

## Declaration

{% tabs %}
{% tab title="Swift" %}
```swift
var urlCache: urlCache { get set }
```
{% endtab %}

{% tab title="Objective-C" %}
```objectivec
@property(retain) NSURLCache *URLCache;
```
{% endtab %}
{% endtabs %}

## Summary

> **SDKs**
>
> * iOS 7.0+
> * macOS 10.9+
> * Mac Catalyst 13.0+ `Beta`
> * tvOS 9.0+
> * watchOS 2.0+
>
> **Framework**
>
> * Foundation

## Discussion

이 속성은 현재 configuration에 기반한 세션 내의 task에서 사용하는 URL 캐시 객체를 결정합니다.

이 속성을 nil로 설정하면 캐시가 비활성화됩니다.

Default 세션의 기본값은 shared URL cache 객체입니다.

Background 세션의 기본값은 nil입니다.

Ephemeral 세션의 기본값은 메모리에만 데이터를 저장하는 private cache객체이며 세션을 비활성화 할때 삭제됩니다.

## 같이 보기

### 캐시 정책 설정

* var [requestCachePolicy](requestcachepolicy.md): NSURLRequest.CachePolicy 캐시된 응답의 반환 조건을 결정하는 사전 정의 상수

