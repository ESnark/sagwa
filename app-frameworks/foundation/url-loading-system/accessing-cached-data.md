---
description: URL 요청시 캐시 데이터의 사용방식을 제어합니다.
---

# 캐시 데이터에 접근하기

> 원문 출처  
> [https://developer.apple.com/documentation/foundation/url\_loading\_system/accessing\_cached\_data](https://developer.apple.com/documentation/foundation/url_loading_system/accessing_cached_data)

## 개요

URL 로딩 시스템은 성능 향상과 네트워크 트래픽 감소를 위해서 응답 데이터를 메모리와 디스크 양쪽에 저장합니다.

[URLCache](urlcache.md) 클래스는 네트워크 리소스로부터의 응답을 캐싱하는데 사용됩니다. 앱에서 URLCache의 [shared](../../../etc/not-found.md) 속성을 사용하여 공유 캐시 인스턴스에 직접 접근하는 것이 가능합니다. 아니면 다른 목적을 위해  [URLSessionConfiguration](urlsession/urlsessionconfiguration.md)에 고유한 캐시를 생성할 수도 있습니다.

### URL Request에 대한 캐시 정책 설정

각 [URLRequest](../../../etc/not-found.md) 인스턴스에는 [URLRequest.CachePolicy](../../../etc/not-found.md) 객체가 포함되어있어 캐싱을 수행해야 할지,  어떻게 캐싱할 것인지를 알려줍니다.

편의를 위해서 [URLSessionConfiguration](urlsession/urlsessionconfiguration.md)에는 [requestCachePolicy](../../../etc/not-found.md)라는 속성이 있습니다. 이 Configuration을 사용하는 Session으로부터 생성된 모든 Request는 requestCachePolicy를 Configuration으로부터 상속받아 사용합니다.

표 1은 다양한 정책들이 어떻게 동작하는지를 설명합니다. 이 표는 서버 또는 로컬에서 캐시 및 원본 파일을 로딩하기 위한 각 정책의 기본 설정을 보여줍니다. 현재는 HTTP와 HTTPS 응답만 캐시가 가능하며 FTP 및 파일 URL에 대해서는 원본 소스에 응답을 허용할 것인지에 대해서만 정책 적용이 되고 있습니다.

**표 1. 캐시 정책과 각 정책의 동작** 

| 캐시 정책 | 로컬 캐시 | 원본 소스 |
| :--- | :--- | :--- |
| NSURLRequest.CachePolicy.reloadIgnoringLocalCacheData | 무시됨 | 무조건 접근 |
| NSURLRequest.CachePolicy.returnCacheDataDontLoad | 무조건 접 | 무시됨 |
| NSURLRequest.CachePolicy.returnCacheDataElseLoad | 우선 시도 | 필요하다면 접근 |
| NSURLRequest.CachePolicy.useProtocolCachePolicy | 프로토콜에 따라 다름 | 프로토콜에 따라 다름 |

useProtocolCachePolicy가 HTTP와 HTTPS에 어떻게 적용되는지는 [NSURLRequest.CachePolicy](../../../etc/not-found.md)를 참조하세요. useProtocolCachePolicy는 URLRequest 객체의 기본값입니다.

{% hint style="info" %}
Note

useProtocolCachePolicy는 HTTPS 응답을 캐시하면서 원치않게 중요한 사용자 데이터를 디스크에 저장할 수 있습니다.[ 프로그래밍적으로 캐시 처리하면](accessing-cached-data.md#undefined-3) 이런 동작을 바꿀 수 있습니다. 
{% endhint %}

### 캐시에 직접 접근

세션 configuration 객체의 urlCache 속성을 사용하면 URLSession 객체의 캐시를 읽거나 쓸 수 있습니다.

특정 요청에 대해 캐시된 응답을 찾으려면 [cachedResponse\(for:\)](../../../etc/not-found.md)을 호출하면 됩니다. 캐시된 데이터가 있다면 CachedURLResponse 객체를 반환하고 없으면 nil을 반환합니다.

캐시에서 사용되는 리소스를 검사할 수도 있습니다. [currentDiskUsage](../../../etc/not-found.md), [diskCapacity](../../../etc/not-found.md) 속성은 파일시스템 상의 캐시 리소스에 대해서, [currentMemoryUsage](../../../etc/not-found.md)와 [memoryCapacity](../../../etc/not-found.md)는 메모리 상의 캐시 리소스에 대해서 알려줍니다.

[removeCachedResponse\(for:\)](../../../etc/not-found.md)을 사용하면 캐시된 개별 아이템을 삭제할 수도 있습니다. 특정 날짜 이전의 캐시된 아이템을 동시에 삭제하려면 [removeCachedResponses\(since:\)](../../../etc/not-found.md) 메서드를, 전체 캐시를 삭제하려면 [removeAllCachedResponses\(\)](../../../etc/not-found.md) 메서드를 호출하면 됩니다.

### 프로그래밍적으로 캐시 처리하기

캐시 방식을 프로그래밍하려면 storeCachedResponse\(\_:for:\) 메서드에 새로운 CachedURLResponse 객체와 URLRequest 객체를 전달하면 됩니다.

일반적으로 캐시 관리는 URLSessionTask 객체가 응답을 처리하는 도중에 이루어집니다. 응답 단위로 캐시를 관리하기 위해서는 [URLSessionDataDelegate](../../../etc/not-found.md)프로토콜의  [urlSession\(\_:dataTask:willCacheResponse:completionHandler:\)](../../../etc/not-found.md) 메서드를 구현해야 합니다. 이 delegate 메서드는 upload task와 data task에서만 호출된다는 점에 주의하세요. background, ephemeral configuration으로 설정된 세션에서는 호출되지 않습니다.

이 delegate는 CachedURLResponse 객체와 completion handler를 파라미터로 받으며, completion handler에 다음 중의 하나를 전달하면서 호출하도록 되어 있습니다.

* 있는 그대로 캐시하기 위해서 제공된 CachedURLResponse 객체
* nil, 이 경우 캐시를 하지 않습니다.
* 새로 생성된 CachedURLResponse 객체, 일반적으로 제공된 객체를 기반으로 하지만 수정된 storagePolicy와 userInfo Dictionary를 포함합니다.

목록 1은 HTTPS 응답을 가로채서 인메모리 방식으로만 캐시하도록 urlSession\(\_:dataTask:willCacheResponse:completionHandler:\)를 구현하고 있습니다.

**목록 1. urlSession\(\_:dataTask:willCacheResponse:completionHandler:\) 콜백 처리**

```swift
func urlSession(_ session: URLSession, dataTask: URLSessionDataTask,
                willCacheResponse proposedResponse: CachedURLResponse,
                completionHandler: @escaping (CachedURLResponse?) -> Void) {
    if proposedResponse.response.url?.scheme == "https" {
        let updatedResponse = CachedURLResponse(response: proposedResponse.response,
                                                data: proposedResponse.data,
                                                userInfo: proposedResponse.userInfo,
                                                storagePolicy: .allowedInMemoryOnly)
        completionHandler(updatedResponse)
    } else {
        completionHandler(proposedResponse)
    }
}
```

## 같이 보기

### 캐시 동작

* _class_ [CachedURLResponse](cachedurlresponse.md) URL 요청에 대해 캐시된 응답
* _class_ [URLCache](urlcache.md) URL 요청을 캐시된 응답에 매핑시키는 객체



