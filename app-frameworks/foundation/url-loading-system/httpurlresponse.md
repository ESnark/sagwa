---
description: HTTP 프로토콜을 따르는 URL 로드 요청에 대한 응답과 관련된 메타데이터
---

# HTTPURLResponse

> 원문 출처  
> [https://developer.apple.com/documentation/foundation/httpurlresponse](https://developer.apple.com/documentation/foundation/httpurlresponse)

## Declaration

{% tabs %}
{% tab title="Swift" %}
```swift
class HTTPURLResponse : URLResponse
```
{% endtab %}

{% tab title="Objective-C" %}
```objectivec
@interface NSURLResponse : NSURLResponse
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

HTTPURLResponse 클래스는 [URLResponse](urlresponse.md)의 서브클래스로써 HTTP 프로토콜 응답의 특징적인 정보에 접근할 수 있는 메서드들을 제공합니다. HTTP URL load 요청을 할때 [URLSession](urlsession/), [NSURLConnection](../../../etc/not-found.md), [NSURLDownload](../../../etc/not-found.md) 클래스로부터 받는 모든 응답 객체는 HTTPURLResponse 클래스의 인스턴스입니다.

## 주제

### Response 객체 초기화

* init?\(url: URL, statusCode: Int, httpVersion: String?, headerFields: \[String : String\]?\)

  상태코드, 프로토콜 버전과 응답헤더로 HTTP URL 응답 객체를 초기화합니다.

### HTTP 응답 헤더 읽기

* _var_ allHeaderFields: \[AnyHashable : Any\]

  Response의 모든 HTTP 헤더 필드

### Response 상태코드 읽기

* _class_ _func_ localizedString\(forStatusCode: Int\) -&gt; String

  주어진 HTTP 상태코드에 해당하는 문자열을 지역화하여 반환합니다.

* _var_ statusCode: Int Response의 HTTP 상태코드

### 인스턴스 메서드

* _func_ value\(forHTTPHeaderField: String\) -&gt; String? `Beta`

## 관련 문서

### 상속받은 대상

* [URLResponse](urlresponse.md)

### 준수하는 프로토콜

* CVarArg
* Equatable
* Hashable

## 같이 보기

### 요청과 응답

* _struct_ [URLRequest](urlrequest.md) 프로토콜이나 URL 스키마로부터 독립적인 URL 로드 요청
* _class_ [URLResponse](urlresponse.md) URL 로드 요청에 대한 응답과 관련된 메타데이터로써 프로토콜과 URL 스키마로부터 독립적입니다.





