---
description: 연관된 네트워크 데이터 전송 태스크들의 그룹을 조정하는 객체
---

# URLSession

> 원문 출처  
> [https://developer.apple.com/documentation/foundation/urlsession](https://developer.apple.com/documentation/foundation/urlsession)

## Declaration

{% tabs %}
{% tab title="Swift" %}
```swift
class URLSession: NSObject
```
{% endtab %}

{% tab title="Objective-C" %}
```objectivec
@interface NSURLSession : NSObject
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

URLSession 및 관련 클래스들은 URL이 가리키는 엔드포인트로 데이터를 다운로드하거나 업로드하기 위한 API를 제공합니다. 이 API는 앱이 실행중이지 않거나 \(iOS에서는\) 앱이 일시정지 상태일때에도 백그라운드 다운로드를 수행할 수 있도록 해줍니다. 수많은 delegate 메서드들은 인증 절차를 돕고 리다이렉트와 같은 이벤트가 발생했을 때 알려줍니다.

{% hint style="warning" %}
중요

URLSession API는 다른 많은 클래스와 함께 상당히 복잡한 방식으로 동작합니다. 이 문서만 읽을 경우 이해하기가 쉽지 않습니다. 이 API를 사용하기 전에 [URL 로딩 시스템](../)의 주제들을 읽어보세요. [첫 단계](../#undefined-3), [업로드](../#undefined-5)와 [다운로드](../#undefined-6) 섹션의 문서에는 URLSession을 사용한 일반적인 task를 수행하는 예시들이 제공되고 있습니다.
{% endhint %}

앱은 URLSession API를 사용하여 하나 이상의 세션을 만들고 각 세션은 관련 데이터 전송 작업 그룹을 조정합니다. 예를 들어, 웹 브라우저를 하나 만든다고 하면 이 앱은 각 탭이나 윈도우별로 세션을 하나씩 생성할 것입니다. 또는 대화형으로 사용할 하나의 세션과 백그라운드 다운로드를 위 다른 하나의 세션을 만들수도 있습니다. 각 세션 내에 앱은 일련의 task들을 추가하고, 각 task는 특정 URL에 대한 요청을 나타냅니다 \(필요하다면 HTTP 리다이렉트를 따를 것입니다.\)

#### URL Session의 종류

하나의 URL session에 속한 task들은 같은 session configuration 객체를 공유합니다. 이 객체는 호스트당 생성 가능한 동시 접속갯수나 cellular 네트워크를 허용할 것인지와 같은 접속 동작을 정의합니다.

URLSession 중에는 기본적인 요청에 적합한 \(configuration 객체가 없는\) 싱글톤 [shared](../../../../etc/not-found.md) 세션이 존재합니다. 이것은 직접 생성하는 것만큼 자유롭게 커스터마이징할 수는 없지만 아주 제한적인 용도로만 사용한다면 좋은 출발점이 될 것입니다. shared 클래스 메서드를 사용함으로써 이 세션에 접근할 수 있습니다.  
다른 종류의 session들은 다음 세가지 configuration과 함께 URLSession을 초기화 하는 방식으로 사용할 수 있습니다.

* default session은 shared session과 상당히 비슷하게 동작하지만 더 많은 설정이 가능하며 delegate를 통해서 데이터를 점진적으로 받아오는 것이 가능합니다.
* Ephemeral session은 shared session과 비슷하지만 캐시나 쿠키, 자격증명을 디스크에 기록하지 않습니다.
* Background session은 앱이 실행중이지 않을 때도  백그라운드에서 컨텐츠를 업로드하거나 다운로드할 수 있게 해줍니다.

각 타입의 configuration을 생성하는 방법에 대한 자세한 내용은 [URLSession Configuration](urlsessionconfiguration.md) 클래스와 [Session Configuration 객체 생성](urlsessionconfiguration.md#session-configuration-1)을 참고하세요

#### URL Session Task의 종류

세션 내에서 데이터를 선택적으로 업로드하거나 서버로부터 데이터를 불러오는 Task를 생성할 수 있습니다. 데이터는 디스크의 파일 형태가 될 수도 있고 메모리 상의 NSData 객체 형태일 수도 있습니다. URLSession API는 세가지 종류의 task를 제공합니다.

* Data task는 NSData 객체를 사용해서 데이터를 전송하고 받습니다. Data task는 짧고, 잦은 요청을 서버와 주고 받는 경우에 사용하도록 만들어졌습니다.
* Upload task는 data task와 비슷하지만 \(주로 파일의 형태로\) 데이터를 보낼 수 있습니다. 또한 앱이 실행중이지 않을 때에도 백그라운드 업로드를 지원합니다.
* Download task는 파일의 형태로 데이터를 불러옵니다. 또한 앱이 실행중이지 않을 때 백그라운드 다운로드와 업로드를 지원합니다.

#### Session Delegate 사용하기

한 세션 안에 있는 task들은 공통 delegate를 공유합니다. delegate는 다양한 이벤트\(인증 실패, 서버로부터 데이터 도착했을 때, 데이터가 캐시할 준비가 되었을 때 등등\)가 발생했을때 정보를 제공하거나 받을 수 있게 해줍니다. 만약 delegate가 제공하는 기능들이 필요 없다면 세을 생성할 때 nil을 전달하면 됩니다.

{% hint style="warning" %}
중요

session 객체는 앱이 종료되거나 해당 session을 명시적으로 무효화하기 전까지 delegate에 대한 강한 참조를 유지합니다. 만약 session을 무효화하지 않으면 앱이 종료되기 전까지 메모리 누수가 발생할 것입니다.
{% endhint %}

#### 비동기성과 URL session

대부분의 네트워킹 API들과 마찬가지로 URLSession API는 매우 비동기적입니다. 이 API는 호출되는 메서드에 따라 두가지 방식으로 데이터를 반환합니다.

* 전송이 성공적으로 끝났거나 에러가 발생한 경우 completion handler 블록을 호출
* 데이터가 수신되고 전송이 완료된 후에 delegate가 메서드를 호출

URLSession API는 delegate를 통해서 정보들을 전달하는 것 외에도 status와 progress 프로퍼티를 제공함으로써 task의 현재 상태에 기반하여 프로그래밍적인 방식의 결정을 내리는데 도움을 줍니다. \(상태값은 언제든지 바뀔수 있습니다.\)

URL Session은 또한 task의 취소, 재시작, 일시정지 및 재개를 지원하며 취소, 일시정지, 실패한 다운로드는 해당 지점부터 재개하도록 할 수 있습니다.

#### 지원하는 프로토콜

URLSession 클래스는 기본적으로 사용자의 시스템 환경 설정에 구성된 프록시 서버 및 SOCKS 게이트웨이에 대한 투명한 지원을 통해 데이터, 파일, FTP, HTTP 및 HTTPS URL 스키마를 지원합니다.

URLSession은 HTTP/1.1, SPDY, HTTP/2 프로토콜을 지원합니다. HTTP/2 지원은 [RFC 7540](https://tools.ietf.org/html/rfc7540)에 설명되어 있으며 Application-Layer Protocol Negotiation \(ALPN\)이나 Next Protocol Negotiation \(NPN\) 둘 중 하나를 지원하는 서버를 필요로 합니다.

#### App Transport Security \(ATS\)

iOS 9.0, OS X 10.11 버전부터 App Transport Security \(ATS\)라는 새로운 보안 기능이 URLSession을 통해 만들어지는 모든 HTTP 접속에 적용됩니다. ATS는 HTTPS를 사용하는 HTTP 접속을 필요로 합니다. \([RFC 2818](https://tools.ietf.org/html/rfc2818)\)

자세한 내용은 [Information Property List Key Reference](../../../../etc/not-found.md)의 [NSAppTransportSecurity](../../../../etc/not-found.md)를 참고하세요.

#### NSCopying 동작

세션과 task 객체는 다음과 같이 [NSCopying](../../notification/) 프로토콜을 준수합니다.

* 세션이나 task 객체를 복사하면 같은 객체를 받습니다.
* configuration 객체를 복사하면 독립적으로 조작가능한 새로운 복사본을 받습니다.

#### 스레드 안전성

URL session API는 그 자체로 완전히 스레드 안전하며 어느 스레드 컨텍스트에서든지 자유롭게 세션과 task를 생성할 수 있습니다. delegate 메서드가 completion handler를 호출할 때 이 작업은 자동적으로 올바른 delegate queue에 스케줄링 됩니다.

{% hint style="danger" %}
경고

시스템이 [urlSessionDidFinishEvents\(forBackgroundURLSession:\)](../../../../etc/not-found.md)이라는 session delegate 메서드를 보조 스레드에서 호출할 수도 있습니다. 하지만 iOS에서 해당 메서드를 구현하면 [application\(\_:handleEventsForBackgroundURLSession:completionHandler:\)](../../../../etc/not-found.md)라는 App delegate 메서드에서 제공하는 completion handler를 호출해야 할 수 있습니다. **이 completion handler는 반드시 메인 스레드에서 호출되어야 합니다.**
{% endhint %}

## **주제**

### shared 세션 사용하기

* _class_ _var_ shared: URLSession 공유 싱글톤 세션 객체

### 세션 생성하기

* init\(configuration: URLSessionConfiguration\) 특정 session configuration으로 세션을 생성합니다.
* init\(configuration: URLSessionConfiguration, delegate: URLSessionDelegate?, delegateQueue: OperationQeueu?\) 특정 session configuration과 delegate, delegateQueue로 세션을 생성합니다.
* _class_ [URLSessionConfiguration](urlsessionconfiguration.md) URL session의 동작과 정책을 정의하는 configuration 객체
* _var_ [configuration](configuration.md): URLSessionConfiguration session configuration 객체의 복사본

### Delegate로 작업하기

* _var_ delegate: URLSessionDelegate? delegate는 이 객체가 만들어질 때 할당됩니다.
* _protocol_ URLSessionDelegate URL session 인스턴스가 \(세션 수명주기 변경 같은\) 세션 수준의 이벤트를 처리하기 위해서 호출하는 메서드를 정의하는 프로토콜
* _protocol_ URLSessionTaskDelegate URL session 인스턴스가 task 수준의 이벤트를 처리하기 위해서 호출하는 메서드를 정의하는 프로토콜
* _var_ delegateQueue: OperationQueue 이 operation queue는 객체가 생성될 때 제공됩니다.

### Data Task를 세션에 추가하기

* _func_ dataTask\(with: URL\) -&gt; URLSessionDataTask 특정 URL의 컨텐츠를 불러오는 task를 생성합니다.
* _func_ dataTask\(with: URL, completionHandler: \(Data?, URLResponse?, Error?\) -&gt; Void\) -&gt; URLSessionDataTask 특정 URL의 컨텐츠를 불러와서 파일로 저장하고, 완료 후에 handler를 호출하는 download task를 생성합니다.
* _func_ downloadTask\(with: URLRequest\) -&gt; URLSessionDownloadTask 특정 URLRequest 객체를 기반으로 URL의 컨텐츠를 불러와서 파일에 저장하는 download task를 생성합니다.
* _func_ downloadTask\(with: URLRequest, completionHandler: \(URL?, URLResponse?, Error?\) -&gt; Void\) -&gt; URLSessionDownloadTask 특정 URLRequest 객체를 기반으로 컨텐츠를 불러와서 파일로 저장하고, 완료 후에 handler를 호출하는 download task를 생성합니다.
* _func_ downloadTask\(withResumeData: Data\) -&gt; URLSessionDownloadTask 이전에 최소되었거나 실패한 다운로드를 재개하는 download task를 생성합니다.
* _func_ downloadTask\(withResumeData: Data, completionHandler: \(URL?, URLResponse?, Error?\) -&gt; Void\) -&gt; URLSessionDownloadTask 이전에 최소되었거나 실패한 다운로드를 재개하고 완료 후에 handler를 호출하는 download task를 생성합니다.
* _class_ URLSessionDownloadTask 다운로드된 데이터를 파일로 저장하는 URL session task
* _protocol_ URLSessionDownloadDelegate A protocol defining methods that URL session instances call on their delegates to handle task-level events specific to data and upload tasks.

### 세션 관리

* func finishTasksAndInvalidate\(\) 세션을 무효화하고 완료되지 않은 task를 완료시킵니다.
* func flush\(completionHandler: \(\) -&gt; Void\) Flushes cookies and credentials to disk, clears transient caches, and ensures that future requests occur on a new TCP connection.
* func getTasksWithCompletionHandler\(\(\[URLSessionDataTask\], \[URLSessionUploadTask\], \[URLSessionDownloadTask\]\) -&gt; Void\) 세션 내 모든 data, upload, download task들의 completion 콜백을 비동기 호출합니다.
* func getAllTasks\(completionHandler: \(\[URLSessionTask\]\) -&gt; Void\) 세션 내 모든 task들의 completion 콜백을 비동기 호출합니다.
* func invalidateAndCancel\(\) 모든 완료되지 않은 task들을 취소하고 세션을 무효화시킵니다.
* func reset\(completionHandler: \(\) -&gt; Void\) 모든 쿠키와 캐시, 자격증명 저장소를 비우고, 디스크 파일을 지우며, 진행중인 다운로드를 디스크로 옮겨서 향후에 요청이 새 소켓에서 발생할 수 있도록 합니다.
* var sessionDescription: String? 세션에 대해서 앱이 정의한 설명 레이블

### 에러 처리

* NSURLSessioin-Specific NSError userInfo Dictionary Keys NSURLSession API에서 반환한 NSError 객체와 함께 사용되는 키.
* Background Task Cancellation 백그라운드 task가 취소된 이유를 설명하는 상수

## 관련 문서

### 상속받은 대상

* NSObject

### 준수하는 프로토콜

* CVarArg
* Equatable
* Hashable

## 같이 보기

* [웹사이트 데이터를 메모리에 저장하기](../fetching-website-data-into-memory.md) URL 세션으로부터 데이터 task를 생성하고 데이터를 받아 메모리에 바로 저장하세요.
* _class_ [URLSessionTask](../urlsessiontask.md) 리소스 다운로드와 같이 URLSession에서 수행되는 task

