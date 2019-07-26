---
description: >-
  윈도우에 웹 컨텐츠를 표시합니다. 사용자 활성화 링크, 뒤로 가기 목록 관리, 최근 방문한 페이지의 기록 관리 등의 브라우저 기능을
  구현하세요.
---

# WebKit

> 원문 출처  
> [https://developer.apple.com/documentation/webkit](https://developer.apple.com/documentation/webkit)

## Summary

> **SDKs**
>
> * iOS 8.0+
> * macOS 10.2+
> * Mac Catalyst 13.0+ `Beta`

## 개요 <a id="overview"></a>

WebKit는 윈도우에 웹 컨텐츠를 표시할 수 있는 클래스를 제공하며, 사용자가 링크를 클릭했을 때 이동하거나, 뒤로가기 목록, 최근 방문한 페이지 기록을 관리하는 등의 브라우저 기능을 구현합니다. WebKit은 웹페이지를 로딩하는 복잡한 프로세스를 크게 단순화합니다. 이 복잡한 프로세스란 점진적, 비순차적, \(네트워크 오류로 인한\) 부분적 응답을 하는 HTTP 서버에 웹 컨텐츠를 비동기적으로 요청하는 동작을 뜻합니다. 뿐만 아니라 WebKit은 컨텐츠를 표시하는 프로세스를 단순화시키기도 합니다. 표시되는 컨텐츠에는 개별적으로 스크롤 바를 갖는 복합적인 프레임 요소들과 다양한 MIME 타입들이 포함됩니다.

{% hint style="info" %}
Important

WebKit의 함수와 메서드들은 앱의 메인 스레드나 main dispatch queue에서만 호출되어야 합니다.
{% endhint %}

## 주제 <a id="topics"></a>

### Safari

* 사파리 도구와 기능 브라우저 지원 기능과 도구를 사용하여 웹 컨텐츠를 사파리에 최적화하세요.

### 초기화 <a id="initialization"></a>

* _protocol_ WKNavigationDelegate WKNavigationDelegate 프로토콜 메서드는 웹 뷰 네비게이션 요청의 수락, 로딩, 완료 중에 트리거되는 커스텀 동작의 구현을 돕습니다. 
* _class_ WKProcessPool WKProcessPool 객체는 웹 컨텐츠 프로세스 풀을 나타냅니다.
* _class_ WKWindowFeatures WKWindowFeatures 객체는 새 웹 뷰를 요청할때 포함된 창에 대한 옵셔널 속성을 지정합니다.
* _class_ WKWebView 인 앱 브라우저와 같이 인터렉티브 웹 컨텐츠를 표시하는 객체
* _class_ WKWebViewConfiguration 웹 뷰를 초기화하는데 사용되는 프로퍼티 콜렉션
* _class_ WKPreferences WKPreferences 객체는 웹 뷰에 대한 기본 설정을 캡슐화합니다.
* _class_ WKWebpagePreferences `Beta`
* _protocol_ WKUIDelegate WKUIDelegate 클래스는 웹 페이지를 대신하여 네이티브 유저 인터페이스 요소를 표시하는 메서드를 제공합니다.
* 웹 뷰를 사용하여 데스크탑이나 모바일 웹 컨텐츠 보기 웹 사이트의 데스크톱 또는 모바일 버전을 볼 수있는 간단한 iPad 웹 브라우저를 구현하세요.

### Navigation

* _class_ WKNavigation

  WKNavigation 객체는 웹페이지의 로딩 진행상황을 추적하는 정보를 포함합니다.

* _class_ WKNavigationAction WKNavigationAction 객체는 네비게이션을 작동시키는 동작에 대한 정보를 담고 있으며 정책 결정에 사용됩니다.
* _class_ WKNavigationResponse WKNavigationResponse 객체는 네비게이션 응답에 대한 정보를 담고 있으며 정책 결정에 사용됩니다.

### Back-Forward List

* _class_ WKBackForwardList

  WKBackForwardList 객체는 방문한 페이지들의 리스트를 유지하여 최근 페이지에 대해 뒤로 가기/앞으로 가기 하는데 사용됩니다.

* _class_ WKBackForwardListItem WKBackForwardListItem 객체는 웹 뷰의 back-forward 리스트의 웹 페이지를 나타냅니다.

### 엘리먼트와 프레임 정보 <a id="element-and-frame-information"></a>

* _class_ WKFrameInfo WKFrameInfo 객체는 웹페이지의 프레임에 대한 정보를 나타냅니다.

### 웹사이트 데이터 <a id="website-data"></a>

* _class_ WKWebsiteDataRecord

  WKWebsiteDataRecord 객체는 원본 URL의 도메인 이름과 접미사로 그룹화된 웹사이트 데이터를 나타냅니다.

* _class_ WKWebsiteDataStore WKWebsiteDataStore 객체는 선택된 웹사이트에서 사용되는 다양한 타입의 데이터를 나타냅니다. 사용되는 데이터 타입의 종류로는 쿠키, 디스크와 메모리 캐시가 있으며 WebSQL, IndexedDB 데이터베이스나 로컬 스토리지와 같은 영구 데이터도 포함됩니다.

### 파일 로딩 <a id="file-loading"></a>

* _class_ WKOpenPanelParameters WKOpenPanelParameters 객체는 파일 업로드 컨트롤이 지정한 파라미터를 포함합니다.

### 스크립트 <a id="scripts"></a>

* _class_ WKUserContentController

  WKUserContentController 객체는 메세지 포스트와 사용자 스크립트를 웹 뷰에 주입할 수 있는 방법을 제공합니다.

* _class_ WKScriptMessage WKScriptMessage 객체는 웹페이지로부터 온 메세지 정보를 포함합니다.
* _class_ WKUserScript WKUserScript 객체는 웹페이지에 삽입가능한 스크립트를 나타냅니다.
* _protocol_ WKScriptMessageHandler WKScriptMessageHandler 프로토콜을 준수하는 클래스는 웹페이지에서 실행되는 자바스크립트로부터 메세지를 받는 메서드를 제공합니다.

### URL 스키마 처리 <a id="url-scheme-handling"></a>

* _protocol_ WKURLSchemeHandler

  WebKit이 처리하지 못하는 URL 스키마로 리소스를 로딩하는 프로토콜

* _protocol_ WKURLSchemeTask 리소스를 로드하기 위해 생성되는 태스크

### First-party 웹페이지 <a id="first-party-webpages"></a>

* _class_ WKSecurityOrigin WKSecurityOrigin 객체는 호스트명, 프로토콜과 포트 번호롤 구성됩니다. First-party load는 모든 로드 URL이 요청중인 웹사이트와 동일한 security origin을 갖는 것을 의미합니다. First-party 웹페이지들은 스크립트나 데이터베이스와 같은 서로의 리소스에 접근할 수 있습니다.

### Preview

* ~~_class_ WKPreviewElementInfo~~ `Deprecated`

  The WKPreviewElement object contains information for previewing a webpage.

* ~~_protocol_ WKPreviewActionItem~~ `Deprecated`

  The WKPreviewActionItem protocol provides access to the properties of a Preview action item.

### 뷰 스냅샷 <a id="view-snapshots"></a>

* _class_ WKSnapshotConfiguration

### WebKit 레거시 API들 <a id="webkit-lagacy-apis"></a>

* Document Object Models API \(Legacy\)
* 웹 뷰 설정 \(Legacy\)
* 이전 웹페이지 접근 \(Legacy\)
* 웹페이지 보관 \(Legacy\)
* 리소스 로딩 \(Legacy\)
* 프레임 작업 \(Legacy\)
* 정보 다운로드 \(Legacy\)
* 파일 열기 \(Legacy\)
* 정책 설정 \(Legacy\)
* 플러그인 구현 \(Legacy\)
* 스크립트 통합 \(Legacy\)
* Document Web View 작업 \(Legacy\)

###  웹 드라이버 <a id="web-driver"></a>

* 사파리 11.1 이하 버전의 macOS 웹 드라이버 명령어 WebDriver는 브라우저 자동화 API로써 웹 컨텐츠의 자동화된 테스트를 생성하는데 사용됩니다. 웹드라이버의 사파리 구현은 Selenium의 [JSON Wire Protocol](https://github.com/SeleniumHQ/selenium/wiki/JsonWireProtocol)을 지원합니다.
* 사파리 12 이상 버전의 macOS 웹 드라이버 명령어 WebDriver는 브라우저 자동화 API로써 웹 컨텐츠의 자동화된 테스트를 생성하는데 사용됩니다. 웹드라이버의 사파리 구현은 [W3C](https://www.w3.org/TR/webdriver/#list-of-endpoints) 엔드포인트를 지원합니다.
* 사파리 웹드라이버에 대해서 테스트 자동화를 위한 사파리의 향상된 공통 API 구현에 대해 알아보세요.
* Testing with WebDriver in Safari 웹 드라이버를 활성화 하고 테스트를 실행하세요.

### 구조체 <a id="structures"></a>

* ~~_struct_ DOMEventExceptionCode~~ `Deprecated`
* ~~_struct_ DOMExceptionCode~~ `Deprecated`
* ~~_struct_ DOMRangeExceptionCode~~ `Deprecated`
* ~~_struct_ DOMXPathExceptionCode~~ `Deprecated`
* _struct_ WKError WebKit API로부터 반환될 수 있는 에러값

### 클래스 <a id="classes"></a>

* _class_ WKContextMenuElementInfo `Beta`

### 참고 <a id="reference"></a>

* WebKit Enumerations WebKit enumerations affecting multiple classes.
* WebKit Data Types

  WebKit data types affecting multiple classes.



