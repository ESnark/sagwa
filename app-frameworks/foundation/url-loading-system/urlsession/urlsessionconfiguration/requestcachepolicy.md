---
description: Instance Property
---

# requestCachePolicy

> 원문 출처  
> [https://developer.apple.com/documentation/foundation/urlsessionconfiguration/1411655-requestcachepolicy](https://developer.apple.com/documentation/foundation/urlsessionconfiguration/1411655-requestcachepolicy)

## Declaration

{% tabs %}
{% tab title="Swift" %}
```swift
var requestCachePolicy: NSURLRequest.CachePolicy { get set }
```
{% endtab %}

{% tab title="Objective-C" %}
```objectivec
@property NSURLRequestCachePolicy requestCachePolicy;
```
{% endtab %}
{% endtabs %}

## Summary

> **SDKs**
>
> * iOS 7.0+
> * macOS 10.9+
> * UIKit for Mac 13.0+ `Beta`
> * tvOS 9.0+
> * watchOS 2.0+
>
> **Framework**
>
> * Foundation

## Discussion

이 속성은 현재 configuration에 기반한 task의 캐시 정책을 결정합니다.

이 속성을 NSURLRequest.CachePolicy에 정의된 상수 중의 하나로 설정하세요. 만료 날짜 또는 기간에 따라 캐시를 사용하거나, 아예 사용하지 않도록 할 수도 있고 마지막 요청 이후 컨텐츠가 변경되었는지 서버에 접속하도록 정책을 설정할 수 있습니다.

## 같이 보기

### 캐시 정책 설정

* var [urlCache](urlcache.md): URLCache? 세션 내에서의 요청에 대해 캐쉬된 응답을 제공하는 URL cache

