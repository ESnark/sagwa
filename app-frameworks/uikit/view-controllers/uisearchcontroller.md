---
description: 검색창과의 상호작용을 기반으로 검색결과 표시를 관리하는 view controller
---

# UISearchController

> 원문 출처  
> [https://developer.apple.com/documentation/uikit/uisearchcontroller](https://developer.apple.com/documentation/uikit/uisearchcontroller)

## Declaration

{% tabs %}
{% tab title="Swift" %}
```swift
class UISearchController : UIViewController
```
{% endtab %}

{% tab title="Objective-C" %}
```objectivec
@interface UISearchController : UIViewController
```
{% endtab %}
{% endtabs %}

## Summary

> **SDKs**
>
> * iOS 8.0+
> * tvOS 9.0+
>
> **Framework**
>
> * UIKit

## 개요 <a id="overview"></a>

Search controller\(검색 컨트롤러\)는 view controller와 함께 사용됩니다. 검색 가능한 컨텐츠가 있는 뷰 컨트롤러가 있다면 UISearchController 객체의 search bar를 뷰 컨트롤러의 인터페이스에 통합시키세요. 사용자가 search bar와 상호작용할때 검색 컨트롤러는 검색결과와 함께 새 뷰 컨트롤러를 보여줍니다.

검색 컨트롤러는 제공받은 두 개의 커스텀 뷰 컨트롤러와 함께 동작합니다. 첫번째 뷰 컨트롤러는 검색가능한 컨텐츠를 보여주고 두번째는 검색 결과를 보여줍니다. 첫번째 뷰 컨트롤러는 앱의 메인 인터페이스의 일부로 존재하며 앱에 적합한 모든 방식으로 표시할 수 있습니다. 두번째 뷰 컨트롤러는 검색 컨트롤러를 초기화할 때 [init\(searchResultsController:\)](../../../etc/not-found.md) 메서드를 통해 전달되며 검색 컨트롤러는 적절한 시점에 해당 뷰 컨트롤러를 보여줍니다.

각 검색 컨트롤러는 Initial View Controller의 UI에 통합되어야 하는 UISearchBar 객체를 제공합니다. 이 객체를 검색가능한 컨텐츠가 포함된 뷰에 추가하세요. 사용자가 검색어를 입력하기 위해 search bar를 터치하면 search controller는 자동적으로 검색결과 뷰 컨트롤러를 표시하고 검색 프로세스가 시작되었다는 것을 앱에 알립니다.

사용자가 search bar와 상호작용하면 검색 컨트롤러는 해당 컨트롤러의 [searchResultsUpdater](../../../etc/not-found.md) 프로퍼티에 알리게 되어 있고 searchResultsUpdater에는 [UISearchResultsUpdating](../../../etc/not-found.md) 프로토콜을 준수하는 객체를 제공해야 합니다. 이 프로토콜의 메서드를 사용하면 컨텐츠를 검색하고 검색결과 뷰 컨트롤러에 결과값을 전달할 수 있습니다. 일반적으로는 검색가능한 컨텐츠가 포함된 뷰 컨트롤러를 검색결과 업데이터 객체로도 사용하지만 원한다면 다른 객체를 업데이터 객체로 사용해도 됩니다.

검색 결과 컨트롤러가 나타나고 사라지는 동작을 커스터마이즈하고 싶다면 검색 컨트롤러의 [delegate](../../../etc/not-found.md) 프로퍼티에 [UIControllerDelegate](../../../etc/not-found.md) 프로토콜을 준수하는 객체를 할당하세요. 해당 프로토콜의 메서드는 검색 컨트롤러가 활성화되었을 때, 검색결과 컨트롤러가 나타나거나 사라질때 알림을 받습니다.

{% hint style="warning" %}
Note

UISearchController 객체는 뷰 컨트롤러기는 하지만 인터페이스에 직접적으로 표현할 수는 없습니다. 명시적으로 검색결과 뷰 컨트롤러를 표현하고 싶다면 검색 컨트롤러를 [UISearchContainerViewController](../../../etc/not-found.md) 객체에 감싸서 나타내세요.
{% endhint %}

iOS에 검색 컨트롤러를 구현하는 방법을 알고 싶으시다면 [검색 컨트롤러로 검색 가능한 컨텐츠 표시하기](../../../etc/not-found.md) 문서를 읽어보세요.

tvOS에서 UISearchContainerViewController에 내장된 검색 컨트롤러를 구현하고 싶으시다면 [UIKit Catalog \(tvOS\): UIKit Control 생성과 커스터마이징](../../../etc/not-found.md) 문서를 읽어보세요.

## 주제 <a id="topics"></a>

### 검색 컨트롤러 초기화 <a id="initializing-a-search-controller"></a>

* init\(searchResultsController: UIViewController?\) 지정된 뷰 컨트롤러에 결과를 보여주는 검색 컨트롤러를 초기화하여 반환합니다.

### Responding to Presentation and Dismissal

* _var_ delegate: UISearchControllerDelegate? 검색 컨트롤러의 delegate
* _protocol_ UISearchControllerDelegate 검색 결과 객체의 delegate 메서드 집합

###  검색 결과 관리 <a id="managing-the-search-results"></a>

* _var_ searchBar: UISearchBar 인터페이스에 설치되는 search bar
* _var_ searchResultsUpdater: UISearchResultsUpdating?

  검색 결과 컨트롤러의 컨텐츠 업데이트를 책임지는 객체

* _var_ searchResultsController: UIViewController? 검색 결과를 보여주는 뷰 컨트롤러
* _var_ isActive: Bool 검색 인터페이스의 표시 상태

### 검색 인터페이스 설정 <a id="configuring-the-search-interface"></a>

* _var_ obscuresBackgroundDuringPresentation: Bool 검색 중에 표시되어 있는 컨텐츠를 흐릿하게 나타냅니다.
* ~~_var_ dimsBackgroundDuringPresentation: Bool~~ `Deprecated` 검색 중에 표시되어있는 컨텐츠를 어둡게 나타냅니다.
* _var_ hidesNavigationBarDuringPresentation: Bool 검색 중에 네비게이션 바를 숨깁니다.

### Initializers

* init?\(coder: NSCoder\)
* init\(nibName: String?, bundle: Bundle?\)

### Instance Properties

* _var_ automaticallyShowsCancelButton: Bool `Beta`
* _var_ automaticallyShowsScopeBar: Bool `Beta`
* _var_ automaticallyShowsSearchResultsController: Bool `Beta`
* _var_ showsSearchResultsController: Bool `Beta`

## 관련 문서  <a id="relationships"></a>

### 상속 <a id="inherits-from"></a>

* [UIViewController](uiviewcontroller.md)

### 준수하는 프로토콜 <a id="conforms-to"></a>

* CVarArg
* Equatable
* Hashable
* NSExtensionRequestHandling
* UIPasteConfigurationSupporting
* UIStateRestoring
* UIUserActivityRestoring
* UIViewControllerAnimatedTransitioning
* UIViewControllerTransitioningDelegate

## 같이 보기 <a id="see-also"></a>

### 검색 인터페이스 <a id="search-interface"></a>

* _class_ UISearchContainerViewController 인터페이스상의 검색결과 표시를 관리하는 view controller
* _class_ UISearchBar 사용자로부터 검색 관련 정보를 받기위한 특수 뷰.
* _protocol_ UISearchResultsUpdating 사용자가 검색창에 입력한 정보를 기반으로 검색결과를 업데이트 할 수 있는 메서드들
* 검색 컨트롤러를 사용하여 검색가능한 컨텐츠 표시하기 검색가능한 컨텐츠와 테이블 뷰를 사용하여 사용자 인터페이스를 생성하세요



