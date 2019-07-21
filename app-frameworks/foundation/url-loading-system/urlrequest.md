---
description: 프로토콜이나 URL 스키마로부터 독립적인 URL 로드 요청
---

# URLRequest

> 원문 출처  
> [https://developer.apple.com/documentation/foundation/urlrequest](https://developer.apple.com/documentation/foundation/urlrequest)

## Declaration

{% tabs %}
{% tab title="Swift" %}
```swift
struct URLRequest
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
> * Xcode 8.0+
>
> **Framework**
>
> * Foundation

## 개요

URLRequest는 요청을 로딩하기 위해서 필수 속성 두 가지를 캡슐화하고 있습니다. 하나는 로딩할 URL이고 다른 하나는 로딩하는데 사용되는 정책입니다. 또한 HTTP와 HTTPS 요청을 위해서 URLRequest는 HTTP 메서드 \(GET, POST 등등\) 및 HTTP 헤더를 내장하고 있습니다.

URLRequest는 오로지 요청에 대한 정보를 표현할 뿐이며 서버로 요청을 보내기 위해서는 URLSession과 같은 다른 클래스를 사용해야 합니다. 이러한 테크닉은 [웹사이트 데이터를 메모리에 저장하기,](fetching-website-data-into-memory.md) [웹사이트에 데이터 업로드하기](../../../etc/not-found.md) 문서에서 소개하고 있습니다.

스위프트 코드를 작성할 때에는 [NSURLRequest](../../../etc/not-found.md)나 [NSMutableURLRequest](../../../etc/not-found.md) 클래스보다는 이 구조체를 사용하세요.

몇몇 헤더 필드는 예약되어 있습니다. [예약된 헤더](../../../etc/not-found.md) 문서를 참조하세요.

## 주제

### Request 생성

* init\(url: URL, cachePolicy: URLRequest.CachePolicy, timeoutInterval: TimeInterval\) 주어진 URL, 캐시 정책과 timeout 간격으로 URL 요청을 생성하고 초기화합니다.

### 캐시 정책 작업

* _var_ cachePolicy: URLRequest.CachePolicy Request의 캐시 정책
* _typealias_ URLRequest.CachePolicy 캐시 정책의 별칭
* _enum_ NSURLRequest.CachePolicy 캐시된 응답과의 상호작용을 지정하는 상수

### 요청 컴포넌트 접근

* _var_ httpMethod: String?

  HTTP 요청 메서드

* _var_ url: URL?

  요청 URL

* _var_ httpBody: Data? POST와 같은 요청의 메세지 본문으로 전달되는 데이터
* _var_ httpBodyStream: InputStream? HTTP 본문을 전달하는 스트림
* _var_ mainDocumentURL: URL? 이 요청과 관련된 메인 문서 URL

### 헤더 필드 접근

* _var_ allHTTPHeaderFields: \[String : String\]? 요청에 포함된 모든 HTTP 헤더 필드를 담고 있는 dictionary
* _func_ addValue\(String, forHTTPHeaderField: String\)

  헤더 필드와 값을 새로 추가합니다.

* _func_ setValue\(String?, forHTTPHeaderField: String\) 헤더 필드 값을 설정합니다.
* _func_ value\(forHTTPHeaderField: String\) -&gt; String?

  헤더값을 불러옵니다.

### 요청 동작 컨트롤

* _var_ timeoutInterval: TimeInterval Request 타임아웃 간격
* _var_ httpShouldHandleCookies: Bool 해당 요청에 쿠키를 포함할 것인지를 가리키는 Boolean 값
* _var_ httpShouldUsePipelining: Bool 이전 응답이 완료된 후에 요청을 보내도록 하는 Boolean 값
* _var_ allowsCellularAccess: Bool 해당 요청이 내장 셀룰러 통신\(Wifi가 아닌 모바일 네트워크\)을 사용할 수 있도록 허용할 것인지를 나타내는 Boolean 값

### 서비스 타입 접근

* _var_ networkServiceType: URLRequest.NetworkServiceType

  해당 요청과 관련된 서비스 타입

* _typealias_ URLRequest.NetworkServiceType 네트워크 서비스 타입의 별칭
* _enum_ NSURLRequest.NetworkServiceType

  요청의 서비스 타입을 지정하는데 사용되는 상수

### 요청 비교

* _static_ func != \(URLRequest, URLRequest\) -&gt; Bool 두 값이 같지 않음을 나타내는 Boolean 값
* _static_ func == \(URLRequest, URLRequest\) -&gt; Bool 두 URL request가 같음을 나타냅니다.

### 요청 설명

* _var_ description: String

  요청에 대한 텍스트 설명

* _var_ debugDescription: String

  디버깅에 적합한 텍스트 설명

* _var_ customMirror: Mirror 요청을 반영하는 미러

### 참조 타입 사용

* _class_ NSURLRequest 참조 시멘틱이나 파운데이션 고유 동작이 필요할 때 사용할 수 있는 URL load request 표현
* _class_ NSMutableURLRequest

  A mutable URL load request that bridges to NSURLRequest and you use when you need reference semantics or other Foundation-specific behavior.

* ~~_typealias_ MutableURLRequest~~ `Deprecated`
* _typealias_ URLRequest.ReferenceType

  An alias for this value type's equivalent reference type.

### 인스턴스 메서드

* _func_ hash\(into: inout Hasher\)

## 관련 문서

### 준수하는 프로토콜

* CustomDebugStringConvertible
* CustomReflectable
* CustomStringConvertible
* Equatable
* Hashable
* ReferenceConvertible

## 같이 보기

### 요청과 응답

* _class_ [URLResponse](urlresponse.md) URL 로드 요청에 대한 응답과 관련된 메타데이터로써 프로토콜과 URL 스키마로부터 독립적입니다.
* _class_ [HTTPURLResponse](httpurlresponse.md) HTTP 프로토콜을 따르는 URL 로드 요청에 대한 응답과 관련된 메타데이터

