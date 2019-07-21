---
description: URL 요청에 대해 캐시된 응답
---

# CachedURLResponse

> 원문 출처  
> [https://developer.apple.com/documentation/foundation/cachedurlresponse](https://developer.apple.com/documentation/foundation/cachedurlresponse)

## Declaration

{% tabs %}
{% tab title="Swift" %}
```swift
class CachedURLResponse : NSObject
```
{% endtab %}

{% tab title="Objective-C" %}
```objectivec
@interface NSCachedURLResponse : NSObject
```
{% endtab %}
{% endtabs %}

## Summary

> **SDKs**
>
> * iOS 2.0+
> * macOS 10.2+
> * Mac Catalyst 13.0+ `Beta`
> * tvOS 9.0+
> * watchOS 2.0+
>
> **Framework**
>
> * Foundation

## 개요

CachedURLResponse 객체는 서버의 응답 메타데이터를 URLResponse 객체의 형태로 제공하며 실제 캐시 내용이 포함된 [NSData](../../../etc/not-found.md) 객체를 함께 제공합니다. CachedURLResponse 객체의 스토리지 정책은 응답을 디스크에 저장할 것인지 메모리에 저장할 것인지, 또는 아예 저장하지 않을 것인지를 결정합니다.

캐시된 응답은 앱에 대한 데이터를 저장할 수 있는 user info dictionary도 포함하고 있습니다.

[URLCache](../../../etc/not-found.md) 클래스는 CachedURLResponse 인스턴스를 저장하고 불러옵니다.

## 주제

### 캐시된 URLResponse 생성

* init\(response: URLResponse, data: Data\) 캐시된 URL response 인스턴스를 생성합니다.
* init\(response: URLResponse, data: Data, userInfo: \[AnyHashable : Any\]?, storagePolicy: URLCache.StoragePolicy\) 주어진 서버 응답, 데이터, user-info dictionary와 storage 정책으로 캐시된 URL response 인스턴스를 생성합니다.

### 캐시된 URL 응답 속성

* _var_ data: Data 캐시된 응답의 데이터
* _var_ response :URLResponse 인스턴스와 연관된 URL response 객체
* _var_ storagePolicy: URLCache.StoragePolicy 캐시된 응답의 스토리지 정책
* _var_ userInfo: \[AnyHashable : Any\]? 캐시된 응답의 user info dictionary

### 캐시 스토리지 정책 설정

* _enum_ URLCache.StoragePolicy [CachedURLResponse](cachedurlresponse.md) 객체의 캐싱 전략을 지정하는 상수

## 관련 문서

### 상속받은 대상

* NSObject

### 준수하는 프로토콜

* CVarArg
* Equatable
* Hashable
* NSCopying
* NSSecureCoding

## 같이 보기

### 캐시 동작

* [캐시 데이터에 접근하기](accessing-cached-data.md) URL 요청시 캐시 데이터의 사용방식을 제어합니다.
* _class_ [URLCache](urlcache.md) URL 요청을 캐시된 응답에 매핑시키는 객체

