---
description: 리소스 다운로드와 같이 URLSession에서 수행되는 task
---

# URLSessionTask

> 원문 출처  
> [https://developer.apple.com/documentation/foundation/urlsessiontask](https://developer.apple.com/documentation/foundation/urlsessiontask)

## Declaration

{% tabs %}
{% tab title="Swift" %}
```swift
class URLSessionTask: NSObject
```
{% endtab %}

{% tab title="Objective-C" %}
```objectivec
@interface NSURLSessionTask : NSObject
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

URLSessionTask 클래스는 URL session task의 기본 클래스입니다. task는 언제나 세션의 일부이며 [URLSession](urlsession/) 인스턴스의 task 생성 메서드를 호출함으로써 만들어낼 수 있습니다. 호출되는 메서드에 따라서 생성될 task의 종류가 결정됩니다. 다음은 URLSession 인스턴스의 메서드입니다.

* [dataTask\(with:\)](../../../etc/not-found.md) 및 관련 메서드는 [URLSessionDataTask](../../../etc/not-found.md) 인스턴스를 생성합니다. Data task는 서버에 리소스를 요청하고 응답값을 하나 이상의 NSData 객체로써 메모리에 저장합니다. 이 task는 default, ephemeral, shared 세션에서 사용가능하지만 background 세션에서는 사용할 수 없습니다.
* [uploadTask\(with:from:\)](../notification/) 및 관련 메서드는 [URLSessionUploadTask](../../../etc/not-found.md) 인스턴스를 생성합니다. Upload task는 data task와 비슷하지만 request body를 제공하기가 더 쉽고 서버의 응답을 받기 전에 데이터를 업로드 하는 것이 더 편해집니다. 뿐만 아니라 upload task는 background 세션을 지원합니다.
* [downloadTask\(with:\)](../../../etc/not-found.md) 및 관련 메서드는 [URLSessionDownloadTask](../../../etc/not-found.md) 인스턴스를 생성합니다. Download task는 리소스를 다운로드하여 바로 디스크의 파일로 저장합니다. download task는 어떤 종류의 세션에서든지 사용할 수 있습니다.
* [streamTask\(withHostName:port:\)](../../../etc/not-found.md) 또는 [streamTask\(with:\)](../../../etc/not-found.md)는 [URLSessionStreamTask](../../../etc/not-found.md) 인스턴스를 생성합니다. stream task는 호스트명과 포트, 또는 net service 객체를 통해서 TCP/IP 커넥션을 생성합니다.

task를 생성한 이후에는 resume\(\) 메서드를 호출함으로써 task를 시작할 수 있습니다. 세션은 요청이 끝나거나 실패할 때까지 task에 대해 강한 참조를 유지합니다. 앱 내부 bookkeeping에 유리하지 않다면 task에 대한 참조를 유지할 필요가 없습니다.

{% hint style="info" %}
Note

모든 task 프로퍼티는 key-value observing을 지원합니다.
{% endhint %}

## 주제

### Task 상태 컨트롤

* _func_ cancel\(\) task를 취소합니다.
* _func_ resume\(\) 일시정지된 task를 재개합니다.
* _func_ suspend\(\) task를 일시적으로 정지시킵니다.
* _var_ state: URLSessionTask.State task의 현재 상태를 활성, 일시정지, 취소 중, 완료의 형식으로 나타냅니다.
* _enum_ URLSessionTask.State task의 현재 상태를 나타내는 상수
* _var_ priority: Float 호스트에서 작업을 처리할 상대적인 우선순위. 부동 소수점 0.0\(가장 낮은 우선순위\)에서 1.0\(가장 높은 우선순위\)까지의 값으로 표시됩니다.
* URL Session Task Priority 호스트에 task 우선순위에 대한 힌트로써 제공되는 상수입니다. priority 프로퍼티와 함께 사용됩니다.

### Task 진행정도

* _var_ progress: Progress 전체적인 task 진행상황을 보여줍니다.
* _var_ countOfBytesExpectedToReceive: Int64 task가 수신할 것으로 예상하는 response body의 바이트 수
* _var_ countOfBytesReceived: Int64 task가 서버로부터 수신한 response body의 바이트 수
* _var_ countOfBytesExpectedToSend: Int64 task가 전송할 것으로 예상하는 request body의 바이트 수
* _var_ countOfBytesSent: Int64 task가 전송한 request body의 바이트 수
* _let_ NSURLSessionTransferSizeUnknown: Int64 결정되지 않은 총 전송량

### Task 일반 정보

* _var_ currentRequest: URLRequest? 현재 task가 처리중인 URL request 객체
* _var_ originalRequest: URLRequest? task가 생성될때 전달받은 원본 request 객체
* _var_ responsse: URLResponse? 현재 활성화된 request에 대한 서버 response
* _var_ taskDescription: String? 앱이 제공하는 현재 task에 대한 설명
* _var_ taskIdentifier: Int 해당 세션 내에서 task를 고유하게 식별하는 ID
* _var_ error: Error? task 실패 원인을 알려주는 에러 객체

### Task 스케줄링

* _var_ countOfBytesClientExpectsToReceive: Int64 클라이언트가 수신할 것으로 예상하는 바이트 수에 대한 최고 추정치
* _var_ countOfBytesClientExpectsToSend: Int64 클라이언트가 송신할 것으로 예상하는 바이트 수에 대한 최고 추정치
* _var_ NSURLSessionTransferSizeUnknown: Int64 결정되지 않은 총 전송량
* _var_ earliestBeginDate: Date? 네트워크 로드가 시작되는 가장 빠른 날짜

## 관련 문서

### 상속받은 대상

* NSObject

### 준수하는 프로토콜

* CVarArg
* Equatable
* Hashable
* NSCopying
* ProgressReporting

## 같이 보기

* [웹사이트 데이터를 메모리에 저장하기](fetching-website-data-into-memory.md) URL 세션으로부터 데이터 task를 생성하고 데이터를 받아 메모리에 바로 저장하세요.
* _class_ [URLSession](urlsession/) 연관된 네트워크 데이터 전송 태스크들의 그룹을 조정하는 객체

