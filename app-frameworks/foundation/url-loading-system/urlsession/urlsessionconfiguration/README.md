---
description: URL session의 동작과 정책을 정의하는 configuration 객체
---

# URLSessionConfiguration

> 원문 출처  
> [https://developer.apple.com/documentation/foundation/urlsessionconfiguration](https://developer.apple.com/documentation/foundation/urlsessionconfiguration)

## Declaration

{% tabs %}
{% tab title="Swift" %}
```swift
class URLSessionConfiguration: NSObject
```
{% endtab %}

{% tab title="Objective-C" %}
```objectivec
@interface NSURLSessionConfiguration : NSObject
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

## 개요

URLSessionConfiguration 객체는 URLSession 객체가 데이터를 업로드하고 다운로드 할때의 동작과 정책을 정의합니다. 데이터를 업로드하거나 다운로드 할 때 configuratioin 객체를 만드는 것은 반드시 해야할 첫 단계입니다. 이 객체를 사용해서 timeout 값, 캐시 정책, 접속 요구사항 및 URLSession 객체와 함께 사용할 기타 유형의 정보를 설정합니다.

세션 객체를 초기화하기 전에 URLSessionConfiguration 객체를 적절하게 설정하는 것은 아주 중요한 일입니다. 세션 객체는 configuration 설정을 복사하여 자기 자신의 설정으로 삼고 한번 설정된 이후에는 URLSessionConfiguration이 어떤 변경이 발생하든지 무시합니다. 전송 정책을 변경하고 싶다면 session configuration 객체를 수정한다음 그것으로 새로운 URLSession 객체를 만들어야 합니다.

{% hint style="info" %}
Note

몇몇 경우, task에 제공되는 NSURLRequest에 의해서 이미 정의된 configuration이 오버라이드될 수 있습니다. Request 객체의 정책에 비해 세션의 정책이 더 엄격한 경우가 아니라면 Request 객체에 지정된 모든 정책은 받아들여집니다. 예를 들어 session configuration이 cellular 네트워크를 제한하고 있다면 NSURLRequest는 cellular 네트워크를 통해서 요청할 수 없습니다.
{% endhint %}

configuration 객체를 사용하여 세션을 생성하는 방법에 대해서 더 자세한 내용이 알고 싶다면 [URLSession](../)을 참고하세요.

### Session Configuration의 타입

URL session의 기능과 동작은 상당수가 세션을 생성할때 사용된 configuration의 종류에 따라서 결정됩니다.

\(configuration 객체를 갖지 않는\) 싱글톤 shared 세션은 기초적인 요청에 사용되며 직접 생성한 것만큼 커스터마이징할 수 없습니다. 그렇지만 제한된 요구사항 내에서는 좋은 출발점이 됩니다. shared 클래스 메서드를 사용함으로써 이 세션에 접근할 수 있으며 이 세션의 제한사항에 대해서 알고 싶다면 해당 메서드 문서를 읽어보십시오.

Default 세션은 \(커스터마이징을 하지 않는다면\) shared 세션과 상당히 비슷하지만 delegate를 통해서 데이터를 점진적으로 얻어올 수 있습니다. URLSessionConfiguration 클래스의 default 메서드를 호출함으로써 생성할 수 있습니다.

Ephemeral session은 shared session과 비슷하지만 캐시나 쿠키, 자격증명을 디스크에 기록하지 않습니다. URLSessionConfiguration 클래스의 ephemeral 메서드를 호출함으로써 생성할 수 있습니다.

Background session은 앱이 실행중이지 않을 때도  백그라운드에서 컨텐츠를 업로드하거나 다운로드할 수 있게 해줍니다. URLSessionConfiguration 클래스의 backgroundSessionConfiguration\(\_:\) 메서드를 호출하여 생성할 수 있습니다.

## 주제

### Session Configuration 객체 생성

* _class_ _var_ \`default\`: URLSessionConfiguration default session configuration 객체
* _class_ _var_ ephemeral: URLSessionConfiguration 캐시, 쿠키나 자격증명을 디스크에 기록하지 않는 session configuration
* _class_ _func_ background\(withIdentifier: String\) -&gt; URLSessionConfiguration HTTP 또는 HTTPS 업로드/다운로드를 백그라운드에서 수행할 수 있는 session configuration

### 일반 프로퍼티 설정

* _var_ identifier: String? configuration 객체의 background 세션 식별자
* _var_ httpAdditionalHeaders: \[AnyHashable: Any\]? 요청을 보낼때 보내지는 추가적인 헤더 딕셔너리
* _var_ networkServiceType: NSURLRequest.NetworkServiceType 이 configuration을 기반으로 한 세션 내 모든 task들의 네트워크 서비스 타입
* _var_ allowsCellularAccess: Bool cellular 네트워크 연결을 하용할 것인지를 결정하는 Boolean 값
* _var_ timeoutIntervalForRequest: TimeInterval 추가적인 데이터를 기다릴 때 사용할 timeout 시간 간격
* _var_ timeoutIntervalForResource: TimeInterval 리소스 요청에 허용되는 최대 시간
* _var_ sharedContainerIdentifier: String? 백그라운드 URL session이 파일을 다운로드 할 공유 컨테이너의 식별자
* _var_ waitsForConnectivity: Bool 연결이 사용가능할때까지 세션을 대기시킬지, 즉시 실패처리 할것인지를 나타내는 Boolean 값

### 쿠키 정책 설정

* _var_ httpCookieAcceptPolicy: HTTPCookie.AcceptPolicy 쿠키 수락 조건을 결정하는 정책 상수
* _var_ httpShouldSetCookies: Bool 요청에 쿠키저장소의 쿠키가 포함되어야 하는지를 결정하는 Boolean 값
* _var_ httpCookieStorage: HTTPCookieStorage? 세션 내의 쿠키를 저장하는 쿠키 저장소
* _class_ HTTPCookieStorage 쿠키 저장소를 관리하는 컨테이너
* _class_ HTTPCookie HTTP 쿠키 구현

### 보안 정책 설정

* var tlsMaximumSupportedProtocol: SSLProtocol 현재 세션에서 접속 시 클라이언트가 요청해야 하는 TLS 프로토콜의 최고 버전
* var tlsMinimumSupportedProtocol: SSLProtocol

  프로토콜 협상 중에 클라이언트가 받아들일 수 있는 TLS 프로토콜의 최소 버전

* urlCredentialStorage: URLCredentialStorage? 인증을 위한 자격증명\(Credential\)을 제공하는 저장소

### 캐시 정책 설정

* var [urlCache](urlcache.md): URLCache? 세션 내에서의 요청에 대해 캐쉬된 응답을 제공하는 URL cache
* var [requestCachePolicy](requestcachepolicy.md): NSURLRequest.CachePolicy 캐시된 응답의 반환 조건을 결정하는 사전 정의 상수

### 백그라운드 전송 지원

* _var_ sessionSendsLaunchEvents: Bool 전송이 완료되었을때 앱이 재개 또는 다시 시작되어야 할지를 나타내는 Boolean 값
* _var_ isDiscretionary: Bool 최적의 성능을 위해 백그라운드 작업을 시스템의 재량에 따라 스케줄링시킬 것인지를 결정하는 Boolean 값
* _var_ shouldUseExtendedBackgroundIdleMode: Bool

  앱이 백으라운드로 이동했을 때에도 TCP 커넥션을 유지할 것인지를 나타내는 Boolean 값

### 커스텀 프로토콜 지원

* _var_ protocolClasses: \[AnyClass\]? 세션의 요청을 처리하는 추가적인 프로토콜 하위클래스의 배열
* _class_ URLProtocol 프로토콜 고유의 URL 데이터 로딩을 처리하는 추상 클래스

### Multipath TCP 지원

* Multipath TCP를 사용한 네트워크 신뢰성 향상 iOS 디바이스의 사용가능한 무선장치를 이용하여 앱의 네트워크 신뢰성과 성능을 향상시키세요.
* _var_ multipathServiceType: URLSessionConfiguration.MultipathServiceType

  Wi-Fi 및 셀룰러 인터페이스를 통해 데이터를 전송하기위한 Multipath TCP 연결 정책을 나타내는 서비스 타입

* _enum_ URLSessionConfiguration.MultipathServiceType Multipath TCP가 사용하는 서비스 타입을 나타내는 상수
* Multipath Entitlement Wi-Fi와 cellular 네트워크 간의 원활한 전환을 위해 앱에 Multipath 프로토콜을 사용할 것인지를 지정하는 Boolean 값 **Key:** com.apple.developer.networking.multipath

### HTTP 정책과 프록시 속성 설정

* _var_ httpMaximumConnectionsPerHost: Int 해당 호스트에 대한 최대 동시 접속 수
* _var_ httpShouldUsePipelining: Bool 세션에서 HTTP 파이프라이닝을 사용할 것인지를 나타내는 Boolean 값
* _var_ connectionProxyDictionary: \[AnyHashable : Any\]? 세션에서 사용할 프록시에 대한 정보를 갖는 딕셔너리

### 연결성 변경 지원

* _var_ waitsForConnectivity: Bool 연결이 사용가능할때까지 세션을 대기시킬지, 즉시 실패처리 할것인지를 나타내는 Boolean 값

### Deprecated Methods

* ~~_class_ _func_ backgroundSessionConfiguration\(String\) -&gt; URLSessionConfiguration~~ `deprecated`

  Returns a session configuration object that allows HTTP and HTTPS uploads or downloads to be performed in the background.

## 관련 문서

### 상속받은 대상

* NSObject

### 준수하는 프로토콜

* CVarArg
* Equatable
* Hashable
* NSCopying

## 같이 보기

### 세션 생성하기

* init\(configuration: URLSessionConfiguration\) 특정 session configuration으로 세션을 생성합니다.
* init\(configuration: URLSessionConfiguration, delegate: URLSessionDelegate?, delegateQueue: OperationQeueu?\) 특정 session configuration과 delegate, delegateQueue로 세션을 생성합니다.
* _var_ [configuration](../configuration.md): URLSessionConfiguration session configuration 객체의 복사본

