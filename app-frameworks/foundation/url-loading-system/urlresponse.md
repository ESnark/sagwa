---
description: URL 로드 요청에 대한 응답과 관련된 메타데이터로써 프로토콜과 URL 스키마로부터 독립적입니다.
---

# URLResponse

> 원문 출처  
> [https://developer.apple.com/documentation/foundation/urlresponse](https://developer.apple.com/documentation/foundation/urlresponse)

## Declaration

{% tabs %}
{% tab title="Swift" %}
```swift
class URLResponse
```
{% endtab %}

{% tab title="Objective-C" %}
```objectivec
@interface NSURLResponse : NSObject
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

연관 [HTTPURLResponse](httpurlresponse.md) 클래스는 일반적으로 사용되는 URLResponse 클래스의 서브 클래스로써, HTTP URL load 요청에 대한 응답을 표현하고 \(응답 헤더와 같은\) HTTP 프로토콜의 특징적인 정보를 저장합니다. HTTP 요청을 할 때마다 반환되는 URLResponse 객체는 실제로는 [HTTPURLResponse](httpurlresponse.md) 클래스의 인스턴스입니다.

{% hint style="info" %}
Note

URLResponse 객체는 URL의 컨텐츠를 나타내는 실제 데이터를 가지지 않습니다. 그 대신 요청을 초기화할 때 사용 메서드와 클래스에 따라 delegate 호출을 통해 한번에 한 조각씩 반환되거나 요청이 완료된 이후 한번에 반환됩니다.

URL 로딩시 컨텐츠 데이터를 받는 다양한 방법에 대해서 알고 싶으시다면 [웹사이트 데이터를 메모리에 저장하기](fetching-website-data-into-memory.md) 문서를 읽어보세요.
{% endhint %}

## 주제

### Response 생성

* init\(url: URL, mimeType: String?, expectedContentLength: Int, textEncodingName: String?\)

  URL, MIME 타입, 컨텐츠 길이\(크기\)와 텍스트 인코딩으로 URLResponse 객체를 생성하고 초기화하세요.

### Response 속성 읽기

* _var_ expectedContentLength: Int64 응답 컨텐츠의 예상 길이
* _var_ suggestedFilename: String? 응답 데이터에 제안된 파일 이름
* _var_ mimeType: String? 응답 MIME 타입
* _var_ textEncodingName: String? 응답 원본 소스에서 제공하는 텍스트 인코딩명
* _var_ url: URL? 응답 URL

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

### 요청과 응답

* _struct_ [URLRequest](urlrequest.md) 프로토콜이나 URL 스키마로부터 독립적인 URL 로드 요청
* _class_ [HTTPURLResponse](httpurlresponse.md) HTTP 프로토콜을 따르는 URL 로드 요청에 대한 응답과 관련된 메타데이터



