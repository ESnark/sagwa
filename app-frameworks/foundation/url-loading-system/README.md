---
description: URL과 상호 작용하고 표준 인터넷 프로토콜을 사용하여 서버와 통신합니다.
---

# URL 로딩 시스템

> 원문 출처  
> [https://developer.apple.com/documentation/foundation/url\_loading\_system](https://developer.apple.com/documentation/foundation/url_loading_system)

## 개요

URL 로딩 시스템은 https같은 표준 프로토콜이나 직접 만든 커스텀 프로토콜을 통해서 URL로 구별되는 리소스에 대한 접근을 제공합니다. 로딩은 비동기적으로 이루어지기 때문에 앱의 응답속도를 저하시키거나 정지시키지 않으며, 데이터나 오류가 도착하는대로 처리할 수 있습니다.

[URLSessionTask](urlsessiontask.md) 인스턴스는 데이터를 가져와서 앱에 반환하거나 파일을 다운로드하고, 데이터 및 파일을 업로드할 수 있습니다. [URLSessionTask](urlsessiontask.md) 인스턴스는 [URLSession](urlsession/) 인스턴스를 통해서 몇개든지 생성할 수 있습니다. Session을 설정할 때에는 [URLSessionConfiguration](../../../etc/not-found.md) 객체를 사용합니다. 이 객체는 캐시나 쿠키를 어떻게 사용할 것인지, 또는 셀룰러 네트워크에서 연결을 허용할 것인지와 같은 옵션을 구성할 수 있습니다.

task를 생성하기 위해서 하나의 세션을 계속해서 사용하는 것도 가능합니다. 예를 들어, 웹 브라우저에는 일반 브라우징과 프라이빗 브라우징을 위한 별도의 세션이 존재하며 프라이빗 브라우징을 위한 세션에서는 데이터를 캐시하지 않습니다. 그림 1은 다르게 설정된 두 세션이 어떻게 여러개의 태스크를 생성할 수 있는지를 보여줍니다.

![&#xADF8;&#xB9BC; 1. URL &#xC138;&#xC158;&#xC73C;&#xB85C; &#xD0DC;&#xC2A4;&#xD06C; &#xC0DD;&#xC131;&#xD558;&#xAE30;](../../../.gitbook/assets/url_loading_system.png)

각 세션은 주기적인 업데이트 \(또는 오류\)를 수신하는 delegate와 연결되어 있습니다. 기본 delegate는 개발자가 제공하는 completion handler 블록을 호출하며, 커스텀 delegate를 사용하는 경우 이 블록은 호출되지 않습니다.

세션은 백그라운드에서 돌아갈 수 있도록 설정할 수 있으며 이 경우 앱이 suspend 상태에 들어가더라도 시스템이 대신 데이터를 다운로드하고 앱이 깨어난 이후에 결과를 제공받을 수 있습니다.

## 주제

### 첫 단계

세션을 설정하고 생성하세요. 그리고 URL과 상호작용하는 task를 생성하세요.

* [웹사이트 데이터를 메모리에 저장하기](fetching-website-data-into-memory.md) URL 세션으로부터 데이터 task를 생성하고 데이터를 받아 메모리에 바로 저장하세요.
* _class_ [URLSession](urlsession/) 연관된 네트워크 데이터 전송 태스크들의 그룹을 조정하는 객체
* _class_ [URLSessionTask](urlsessiontask.md) 리소스 다운로드와 같이 URLSession에서 수행되는 task

### 요청과 응답

* _struct_ [URLRequest](urlrequest.md) 프로토콜이나 URL 스키마로부터 독립적인 URL 로드 요청
* _class_ [URLResponse](urlresponse.md) URL 로드 요청에 대한 응답과 관련된 메타데이터로써 프로토콜과 URL 스키마로부터 독립적입니다.
* _class_ HTTPURLResponse HTTP 프로토콜을 따르는 URL 로드 요청에 대한 응답과 관련된 메타데이터

### 업로드

* 웹사이트에 데이터 업로드하기 앱에서 서버로 데이터를 POST하세요
* 데이터 스트림 업로드하기 서버로 데이터 스트림을 전송합니다.

### 다운로드

* 웹사이트에서 파일 다운로드하기 파일 시스템에 파일을 다운로드하세요
* 다운로드 일시정지와 재개 처음부터 다시 받지 않고 파일을 계속해서 다운로드 할 수 있습니다.
* 백그라운드 파일 다운로드 앱이 inactive 상태일때 파일을 다운로드 할 수 있는 task를 생성하세요.

### 캐시 동작

* [캐시 데이터에 접근하기](accessing-cached-data.md) URL 요청시 캐시 데이터의 사용방식을 제어합니다.
* _class_ [CachedURLResponse](cachedurlresponse.md) URL 요청에 대해 캐시된 응답
* _class_ [URLCache](urlcache.md) URL 요청을 캐시된 응답에 매핑시키는 객체

### 인증 및 자격증

* Authentication Challenge 처리하기 서버가 인증을 위한 URL 요청을 요구할때 적절하게 응답합니다.
* _class_ URLAuthenticationChallenge A challenge from a server requiring authentication from the client.
* _class_ URLCredential An authentication credential consisting of information specific to the type of credential and the type of persistent storage to use, if any.
* _class_ URLCredentialStorage 공유 자격증명 캐시의 관리자
* _class_ URLProtectionSpace 인증이 필요한 서버, 또는 서버의 영역

### 쿠키

* _class_ HTTPCookie HTTP 쿠키 구현
* _class_ HTTPCookieStorage 쿠키 저장소를 관리하는 컨테이너

### 에러

* _struct_ URLError URL 로딩 API로부터 반환되는 에러코드
* URL Loading System Error Info Keys Recognize these keys from the user info dictionary of error objects produced by URL Loading APIs.

### Legacy

* 레거시 URL 로딩 시스템 레거시 객체로부터 코드를 마이그레이션하세요.

## 같이보기

### 네트워킹

* Bonjour 로컬 네트워크 상에서 쉽게 발견할 수 있도록 서비스를 알리거나 다른 서비스를 찾습니다.



