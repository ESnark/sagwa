---
description: URL 요청을 캐시된 응답에 매핑시키는 객체
---

# URLCache

> 원문 출처  
> [https://developer.apple.com/documentation/foundation/urlcache](https://developer.apple.com/documentation/foundation/urlcache)

## Declaration

{% tabs %}
{% tab title="Swift" %}
```swift
class URLCache : NSObject
```
{% endtab %}

{% tab title="Objective-C" %}
```objectivec
@interface NSURLCache : NSObject
```
{% endtab %}
{% endtabs %}

## Summary

> **SDKs**
>
> * iOS 2.0+
> * macOS 10.2+
> * UIKit for Mac 13.0+ `Beta`
> * tvOS 9.0+
> * watchOS 2.0+
>
> **Framework**
>
> * Foundation

## 개요

URLCache 클래스는 [NSURLRequest](../../../etc/not-found.md) 객체를 [CachedURLResponse](cachedurlresponse.md) 객체에 매핑함으로써 URL load 요청에 대한 응답의 캐싱을 구현합니다. 또한 인메모리 및 디스크에 저장된 캐시를 제공하며 각 캐시의 크기를 모두 조절할 수 있고 캐시 데이터가 영구적으로 저장될 경로를 제어할 수 있습니다.

{% hint style="info" %}
Note

iOS에서는 시스템 디스크 공간이 부족할 경우 앱이 실행중이지 않을 때 디스크에 저장된 캐시를 삭제할 수 있습니다.
{% endhint %}

### 스레드 안전성

iOS 8, macOS 10.10 이상에서 URLCache는 스레드 안전합니다.

URLCache 인스턴스 메서드들이 여러 실행 컨텍스트에서 호출되더라도 스레드 안전하기는 하지만, cachedResponse\(for:\)와 storeCachedResponse\(\_:for:\)와 같은 메서드가 같은 요청에 대한 응답을 동시에 읽고 쓰려고 한다면 경쟁상태\(race condition\)를 피할 수 없으므로 조심해야 합니다.

URLCache의 서브 클래스들은 반드시 이러한 상황에서 스레드 안전하게 동작할 수 있도록 메서드를 오버라이드하여 구현해야 합니다.

### Subclassing Notes

URLCache 클래스는 있는 그대로 사용되도록 만들어졌지만 캐시가 필요한 응답을 가려내려 하거나, 보안상의 이유로 저장 메커니즘을 재구현 하려는 등 특정한 경우에는 서브클래싱 할 필요가 생길수도 있습니다.

이 클래스의 메서드를 오버라이드 할 경우, 시스템이 task 파라미터를 사용하는 메서드를 그렇지 않은 메서드보다 우선시 한다는 것을 유의해야 합니다. 그러므로 서브클래싱을 할때에는 다음과 같이 task 기반의 메서드를 오버라이드 해야합니다:

* 응답을 캐시로 저장할 때 — request 기반의 [storeCachedResponse\(\_:for:\)](../../../etc/not-found.md) 대신에 task 기반의 [storeCachedResponse\(\_:for:\)](../../../etc/not-found.md)를 오버라이드하세요.
* 캐시에서 응답을 읽어올 때 — [cachedResponse\(for:\)](../../../etc/not-found.md) 대신에 [getCachedResponse\(for:completionHandler:\)](../../../etc/not-found.md)를 오버라이드하세요.
* 캐시된 응답을 삭제할 때 — request 기반의 [removeCachedResponse\(for:\)](../../../etc/not-found.md) 대신에 task기반의 [removeCachedResponse\(for:\)](../../../etc/not-found.md)를 오버라이드하세요.

## 주제

### 공유 캐시 읽고 쓰기

* _class_ _var_ shared: URLCache 공유 URL 캐시 인스턴스

### 새 캐시 객체 생성

* ~~init\(memoryCapacity: Int, diskCapacity: Int, diskPath: String?\)~~ `Deprecated`

  ~~Creates an URL cache object with the specified values.~~

### 캐시 객체 읽고 저장하기

* _func_ cachedResponse\(for: URLRequest\) -&gt; CachedURLResponse? 지정된 URL 요청에 대한 캐시된 URL 응답을 반환합니다.
* _func_ storeCachedResponse\(CachedURLResponse, for: URLRequest\) 지정된 URL 요청에 대한 캐시된 URL 응답을 저장합니다.
* _func_ getCachedResponse\(for: URLSessionDataTask, completionHandler: \(CachedURLResponse?\) -&gt; Void\) data task에 대한 캐시된 URL 응답을 읽어서 completion handler로 전달합니다.
* _func_ storeCachedResponse\(CachedURLResponse, for: URLSessionDataTask\) 지정된 data task에 대한 캐시된 URL 응답을 저장합니다.

### 캐시 객체 삭제

* _func_ removeCachedResponse\(for: URLRequest\) 지정된 URL 요청에 대한 캐시된 URL 응답을 삭제합니다.
* _func_ removeCachedResponse\(for: URLSessionDataTask\) 지정된 data task에 대한 캐시된 URL 응답을 삭제합니다.
* _func_ removeCachedResponses\(since: Date\) 지정된 날짜 이전의 모든 캐시된 응답을 삭제합니다.
* _func_ removeAllCachedResponses\(\) 수신자의 저장된 모든 캐시된 URL 응답을 삭제합니다.

### 온 디스크 캐시 속성 읽고 쓰기

* _var_ currentDiskUsage: Int 온 디스크 캐시의 현재 크기를 바이트 단위로 나타냅니다.
* _var_ diskCapacity: Int 온 디스크 캐시의 가용 용량을 바이트 단위로 나타냅니다.

### 캐시 스토리지 정책

* _enum_ URLCache.StoragePolicy 캐싱 전략을 지정하는 상수로써 [CachedURLResponse](cachedurlresponse.md) 객체가 사용합니다.

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
* _class_ [CachedURLResponse](cachedurlresponse.md) URL 요청에 대해 캐시된 응답

