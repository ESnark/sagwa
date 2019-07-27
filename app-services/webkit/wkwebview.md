---
description: 인 앱 브라우저와 같이 인터렉티브 웹 컨텐츠를 표시하는 객체
---

# WKWebView

> 원문 출처  
> [https://developer.apple.com/documentation/webkit/wkwebview](https://developer.apple.com/documentation/webkit/wkwebview)

## Summary

> **SDKs**
>
> * iOS 8.0+
> * macOS 10.10+
>
> **Framework**
>
> * WebKit

## Declaration

{% tabs %}
{% tab title="Swift" %}
{% code-tabs %}
{% code-tabs-item title="iOS, Mac Catalyst" %}
```swift
class WKWebView : UIView
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="macOS" %}
```swift
class WKWebView : NSView
```
{% endcode-tabs-item %}
{% endcode-tabs %}
{% endtab %}

{% tab title="Objective-C" %}
{% code-tabs %}
{% code-tabs-item title="iOS" %}
```objectivec
@interface WKWebView : UIView
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="macOS" %}
```objectivec
@interface WKWebView : NSView
```
{% endcode-tabs-item %}
{% endcode-tabs %}
{% endtab %}
{% endtabs %}

## 개요 <a id="overview"></a>

{% hint style="info" %}
Important

iOS 8.0과 OS X 10.10부터는 웹 컨텐츠를 앱에 추가할 때 WKWebView를 사용해야 합니다. UIWebView나 WebView를 사용하지 마세요.
{% endhint %}

WKWebView 클래스를 사용하면 웹 컨텐츠를 앱에 내장시킬 수 있습니다. WKWebView 클래스를 사용하기 위해서는 WKWebView 객체를 생성하고 뷰로써 설정한 다음 웹 컨텐츠를 불러오기 위해서 요청을 보내야 합니다.

{% hint style="warning" %}
Note

WKWebView 안에서 [httpBody](../../etc/not-found.md) 컨텐츠로 POST 요청을 할 수 있습니다.
{% endhint %}

[init\(frame:configuration:\)](../../etc/not-found.md) 메서드로 새 WKWebView 객체를 생성한 후에는 웹 컨텐츠를 로딩해야 합니다. [loadHTMLString\(\_:baseURL:\)](../../etc/not-found.md) 메서드는 로컬 HTML파일을, [load\(\_:\)](../../etc/not-found.md) 메서드로는 웹 컨텐츠의 로드를 시작할 수 있습니다. [stopLoading\(\)](../../etc/not-found.md) 메서드는 로딩을 멈추게 할 수 있으며 [isLoading](../../etc/not-found.md) 프로퍼티는 웹 뷰가 로딩중인지를 알 수 있습니다. [WKUIDelegate](../../etc/not-found.md) 프로토콜을 준수하는 객체를 delegate 프로퍼티로 지정하여 웹 컨텐츠의 로딩을 추적할 수 있습니다. Listing 1에서 WKWebView를 프로그래밍적으로 생성하는 예시를 확인하세요.

{% code-tabs %}
{% code-tabs-item title="Listing 1. 프로그래밍적으로 WKWebView 생성" %}
```swift
import UIKit
import WebKit
class ViewController: UIViewController, WKUIDelegate {
    
    var webView: WKWebView!
    
    override func loadView() {
        let webConfiguration = WKWebViewConfiguration()
        webView = WKWebView(frame: .zero, configuration: webConfiguration)
        webView.uiDelegate = self
        view = webView
    }
    override func viewDidLoad() {
        super.viewDidLoad()
        
        let myURL = URL(string:"https://www.apple.com")
        let myRequest = URLRequest(url: myURL!)
        webView.load(myRequest)
    }}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

사용자가 웹페이지 기록의 앞이나 뒤로 이동할 수 있게 하려면 [goBack\(\)](../../etc/not-found.md)과 [goForward\(\)](../../etc/not-found.md) 메서드를 버튼의 액션으로 지정하세요. [canGoBack](../../etc/not-found.md)과 [canGoForward](../../etc/not-found.md) 프로퍼티는 사용자가 해당 방향으로 이동하지 못하게 할 수 있습니다.

기본적으로 웹 뷰는 웹 컨텐츠 상의 전화번호를 전화 링크로 자동변환합니다. 전화 링크를 터치하면 전화 앱이 실행되고 전화번호가 입력됩니다. 이 기본동작을 끄려면 [WKDataDetectorTypePhoneNumber](../../etc/not-found.md) 플래그가 없는 [WKDataDetectorTypes](../../etc/not-found.md) 비트필드를 사용해서 [dataDetectorTypes](../../etc/not-found.md) 프로퍼티를 설정하세요.

[setMagnification\(\_:centeredAt:\)](../../etc/not-found.md)을 사용해서 웹 뷰가 처음 웹 컨텐츠를 표시할 때 표시 스케일을 설정할 수 있습니다. 따라서 사용자는 제스처를 통해 스케일을 조절할 수 있습니다.

## 주제 <a id="topics"></a>

###  Determining Whether WebKit can Load Content

* _class_ _func_ handlesURLScheme\(String\) -&gt; Bool 리소스를 로딩하는 특정 URL 스키마에 대한 WebKit의 네이티브 지원 여부를 반환합니다.

### 웹 뷰 초기화 <a id="initializing-a-web-view"></a>

* _var_ configuration: WKWebViewConfiguration

  웹 뷰를 초기화하기 위한 설정의 복사본

* init\(frame: CGRect, configuration: WKWebViewConfiguration\) 지정된 프레임과 설정으로 초기화된 웹 뷰를 반환합니다.
* init?\(coder: NSCoder\)

### 뷰 정보 검사 <a id="inspecting-the-view-information"></a>

* _var_ scrollView: UIScrollView 웹 뷰에 연결된 스크롤 뷰
* _var_ title: String? 페이지 제목
* _var_ url: URL?

  활성 URL

* _var_ customUserAgent: String?

  커스텀 User agent 문자열

* _var_ serverTrust: SecTrust? 현재 커밋된 탐색에 대한 SecTrustRef 객체
* ~~_var_ certificateChain: \[Any\]~~ `Deprecated`

  An array of objects forming the certificate chain for the currently committed navigation.

### Delegate 설정 <a id="setting-delegates"></a>

* _var_ navigationDelegate: WKNavigationDelegate?

  웹 뷰의 네비게이션 delegate

* _var_ uiDelegate: WKUIDelegate? 웹 뷰의 유저 인터페이스 delegate

### 컨텐츠 로딩 <a id="loading-content"></a>

* _var_ estimatedProgress: Double

  현재 네비게이션의 로드량을 추정합니다.

* _var_ hasOnlySecureContent: Bool 페이지의 모든 리소스가 안전하게 암호화된 연결을 통해서 로드된 것인지를 나타냅니다.
* _func_ loadHTMLString\(String, baseURL: URL?\) -&gt; WKNavigation? 웹페이지 내용과 base URL을 설정합니다.
* _var_ isLoading: Bool 뷰가 현재 컨텐츠를 로딩 중인지를 나타냅니다.
* _func_ reload\(\) -&gt; WKNavigation? 현재 페이지를 새로고침합니다.
* _func_ reload\(Any?\) 현재 페이지를 새로고침합니다.
* _func_ reloadFromOrigin\(\) -&gt; WKNavigation? \(가능하다면\) 캐시 유효성 검사 조건을 사용하여 종단간 재검증을 수행하고 현재 페이지를 새로 고침합니다.
* _func_ reloadFromOrigin\(Any?\)

  \(가능하다면\) 캐시 유효성 검사 조건을 사용하여 종단간 재검증을 수행하고 현재 페이지를 새로 고침합니다.

* _func_ stopLoading\(\)

  현재 페이지의 모든 리소스 로딩을 중단합니다.

* _func_ stopLoading\(Any?\) 현재 페이지의 모든 리소스 로딩을 중단합니다.
* _func_ load\(Data, mimeType: String, characterEncodingName: String, baseURL: URL\) -&gt; WKNavigation? 웹페이지 컨텐츠와 base URL을 설정합니다.
* _func_ loadFileURL\(URL, allowingReadAccessTo: URL\) -&gt; WKNavigation? 파일 시스템 상의 요청된 파일 URL로 이동합니다.

### 컨텐츠 스케일링 <a id="scaling-content"></a>

* _var_ allowsMagnification: Bool

  확대 제스처를 통한 웹 뷰 확대 여부를 나타냅니다.

* _var_ magnification: CGFloat

  The factor by which the page content is currently scaled.

* _func_ setMagnification\(CGFloat, centeredAt: CGPoint\)

  지정된 값에 따라서 페이지 컨텐츠를 확대하고 중심점을 맞춥니다.

### Navigating

* _var_ allowsBackForwardNavigationGestures: Bool

  수평 스와이프를 통한 전후 페이지 이동가능 여부를 나타냅니다.

* _var_ backForwardList: WKBackForwardList 웹 뷰의 전후 리스트
* _var_ canGoBack: Bool back-forward 리스트 상에 이전 항목이 존재하는 경우 해당 항목으로 이동이 가능한지에 대한 여부를 나타냅니다.
* _var_ canGoForward: Bool back-forward 리스트 상에 다음 항목이 존재하는 경우 해당 항목으로 이동이 가능한지에 대한 여부를 나타냅니다.
* _var_ allowsLinkPreview: Bool 링크를 눌렀을때 미리보기의 표시 여부를 나타냅니다.
* _func_ goBack\(\) -&gt; WKNavigation? back-forward 리스트상의 이전 항목으로 이동합니다.
* _func_ goBack\(Any?\) back-forward 리스트상의 이전 항목으로 이동합니다.
* _func_ goForward\(\) -&gt; WKNavigation? back-forward 리스트상의 다음 항목으로 이동합니다.
* _func_ goForward\(Any?\) back-forward 리스트상의 다음 항목으로 이동합니다.
* _func_ go\(to: WKBackForwardListItem\) -&gt; WKNavigation? back-forward 리스트 상의 항목으로 이동하고 현재 항목으로 설정합니다.
* _func_ load\(URLRequest\) -&gt; WKNavigation? 요청 URL로 이동합니다.

### 자바스크립트 실행 <a id="executing-javascript"></a>

* _func_ evaluateJavaScript\(String, completionHandler: \(\(Any?, Error?\) -&gt; Void\)?\) 자바스크립트 문자열을 평가합니다.

### 스크린샷 캡처 <a id="taking-snapshots"></a>

* _func_ takeSnapshot\(with: WKSnapshotConfiguration?, completionHandler: \(UIImage?, Error?\) -&gt; Void\) 뷰에서 보여지고 있는 뷰포트의 스크린샷을 찍습니다.

## 관련 문서 <a id="relationships"></a>

### 상속 <a id="inherits-from"></a>

* NSView
* UIView

### 준수하는 프로토콜 <a id="conforms-to"></a>

* CVarArg
* Equatable Hashable
* NSStandardKeyBindingResponding
* NSTouchBarProvider
* NSUserActivityRestoring
* NSUserInterfaceValidations
* UIAccessibilityIdentification
* UILargeContentViewerItem
* UIPasteConfigurationSupporting
* UIUserActivityRestoring

## 같이 보기 <a id="see-also"></a>

### 초기화 <a id="initialization"></a>

* _protocol_ WKNavigationDelegate WKNavigationDelegate 프로토콜 메서드는 웹 뷰 네비게이션 요청의 수락, 로딩, 완료 중에 트리거되는 커스텀 동작의 구현을 돕습니다. 
* _class_ WKProcessPool WKProcessPool 객체는 웹 컨텐츠 프로세스 풀을 나타냅니다.
* _class_ WKWindowFeatures WKWindowFeatures 객체는 새 웹 뷰를 요청할때 포함된 창에 대한 옵셔널 속성을 지정합니다.
* _class_ WKWebViewConfiguration 웹 뷰를 초기화하는데 사용되는 프로퍼티 콜렉션
* _class_ WKPreferences WKPreferences 객체는 웹 뷰에 대한 기본 설정을 캡슐화합니다.
* _class_ WKWebpagePreferences `Beta`
* _protocol_ WKUIDelegate WKUIDelegate 클래스는 웹 페이지를 대신하여 네이티브 유저 인터페이스 요소를 표시하는 메서드를 제공합니다.
* 웹 뷰를 사용하여 데스크탑이나 모바일 웹 컨텐츠 보기 웹 사이트의 데스크톱 또는 모바일 버전을 볼 수있는 간단한 iPad 웹 브라우저를 구현하세요.



