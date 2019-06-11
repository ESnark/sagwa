---
description: session configuration 객체의 복사본
---

# configuration

> 원문 출처  
> [https://developer.apple.com/documentation/foundation/urlsession/1411477-configuration](https://developer.apple.com/documentation/foundation/urlsession/1411477-configuration)

## Declaration

{% tabs %}
{% tab title="Swift" %}
```swift
@NSCopying var configuration: URLSessionConfiguration { get }
```
{% endtab %}

{% tab title="Objective-C" %}
```objectivec
@property(readonly, copy) NSURLSessionConfiguration *configuration;
```
{% endtab %}
{% endtabs %}

## Summary

> **SDKs**
>
> * iOS 7.0+
> * macOS 10.9+
> * tvOS 9.0+
> * watchOS 2.0+
>
> **Framework**
>
> * Foundation

## Discussion

iOS 9, OS X 10.11 버전부터 URLSession 객체는 초기화될 때 넘겨받은 URLSessionConfiguration 객체를 내부에 저장하기 때문에 초기화 이후에는 configuration을 변경할 수 없습니다. 세션 초기화 메서드에 전달된 configuration 객체 또는 세션에서 반환된 configuration의 속성을 변경하더라도 세션의 동작에는 영향을 주지 않습니다. 하지만 수정된 configuration 객체로 새로운 세션을 만들 수는 있습니다.

{% hint style="info" %}
이전 버전의 iOS나 macOS에서는 URLSession객체가 구현 시의 버그로 인해 초기화 메서드에 전달된 configuration 객체의 복사본이 아닌 참조를 저장했습니다. URLSession 초기화 메서드에 전달되었거나 configuration 속성에서 반환된 객체에 대해 명시적으로 copy\(\)를 호출함으로써 플랫폼간의 일관적인 동작을 보장할 수 있습니다.
{% endhint %}

## 같이 보기

### 세션 생성하기

* init\(configuration: URLSessionConfiguration\) 특정 session configuration으로 세션을 생성합니다.
* init\(configuration: URLSessionConfiguration, delegate: URLSessionDelegate?, delegateQueue: OperationQeueu?\) 특정 session configuration과 delegate, delegateQueue로 세션을 생성합니다.
* _class_ [URLSessionConfiguration](urlsessionconfiguration/) URL session의 동작과 정책을 정의하는 configuration 객체

