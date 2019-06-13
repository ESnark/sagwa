---
description: Table View 관리에 특화된 view controller
---

# UITableViewController

> 원문 출처  
> [https://developer.apple.com/documentation/uikit/uitableviewcontroller](https://developer.apple.com/documentation/uikit/uitableviewcontroller)

## Declaration

{% tabs %}
{% tab title="Swift" %}
```swift
class UITableViewController : UIViewController
```
{% endtab %}

{% tab title="Objective-C" %}
```objectivec
@interface UITableViewController : UIViewController
```
{% endtab %}
{% endtabs %}

## Summary

> **SDKs**
>
> * iOS 2.0+
> * tvOS 9.0+
>
> **Framework**
>
> * UIKit

## 개요

인터페이스가 테이블 뷰 외의 다른 컨텐츠가 거의 없는 경우에는 UITalbeViewController를 서브클래싱하세요. 테이블 뷰 컨트롤러는 테이블 뷰의 컨텐츠를 관리하거나 변화에 대응하는 프로토콜을 처음부터 채택하고 있습니다. UITableViewController는 다음 동작을 구현합니다:

* 스토리보드나 nib 파일에 저장되어 있는 테이블 뷰를 자동으로 로딩해옵니다. 이 테이블 뷰는 [tableView](../../../etc/not-found.md) 프로퍼티를 통해 접근할 수 있습니다.
* 테이블 뷰의 dataSource와 delegate를 자기 자신\(_self_\)으로 설정합니다.
* [viewWillAppear\(\_:\)](../../../etc/not-found.md) 메서드를 구현해서 테이블 뷰가 처음 나타날때 자동으로 데이터를 다시 불러옵니다. 테이블 뷰가 보일 때마다 항목이 선택해제되는데 \(요청에 따라서 애니메이션을 비활성화 할 수 있습니다\) [clearsSelectonOnViewWillAppear](../../../etc/not-found.md) 프로퍼티값을 바꿈으로써 이 동작을 바꿀 수 있습니다.
* [viewDidApear\(\_:\)](../../../etc/not-found.md) 메서드를 구현해서 테이블 뷰가 처음으로 나타날때 스크롤 인디케이터를 깜박입니다.
* [setEditing\(\_:animated\)](../../../etc/not-found.md) 메서드를 구현하여 사용자가 네비게이션 바의 Edit/Done 버튼을 탭하면 자동으로 편집 모드를 토글할 수 있습니다.
* 스크린에 키보드가 나타나고 사라짐에 따라 테이블 뷰의 크기를 자동으로 조정합니다.

관리할 테이블 뷰마다 UITableViewController의 커스텀 서브클래스를 만드세요. 테이블 뷰 컨트롤러를 초기화 할 때에는 만드시 테이블 뷰의 스타일\(일반 또는 그룹 테이블\)을 지정해야 합니다. 또한 테이블을 데이터로 채우기 위해서 data source와 delegate 메서드도 반드시 오버라이드해야 합니다. [loadView\(\)](../../../etc/not-found.md) 또는 다른 상위 클래스 메서드를 오버라이드 할 수 있지만 그럴 경우 상위 클래스의 구현을 우선적으로 호출하도록 해야 합니다.

> 역자 주  
> 설명이 어려운 듯 하여 추가 설명을 간략히 덧붙입니다. 즉 오버라이드를 할 경우 다음과 같이 구현해야 한다는 뜻입니다.

```swift
ovrride func loadView() {
    super.loadView()    // 상위 클래스 loadView 호출
    // ...이하 오버라이드할 구현 코드
}
```

## 주제

### 테이블 뷰 컨트롤러 생성

* init\(style: UITableView.Style\)

  주어진 style대로 테이블 뷰 컨트롤러를 초기화합니다.

* init?\(coder: NSCoder\)
* init\(nibName: String?, bundle: Bundle?\)

### 테이블 뷰 가져오기

* _var_ tableView: UITableView! 컨트롤러 객체로 관뢰되는 테이블 뷰를 반환합니다.

### 테이블 뷰 동작 설정

* _var_ clearsSelectionOnViewWillAppear: Bool 테이블이 나타날 때 컨트롤러가 선택된 항목을 선택 해제하도록 할 것인지를 나타내는 Boolean 값

### 테이블 뷰 새로고침

* _var_ refreshControl: UIRefreshControl? 테이블 컨텐츠를 업데이트하는데 사용되는 refresh 컨트롤

## 관련 문서

### 상속받은 대상

* UIViewController

### 준수하는 프로토콜

* CVarArg
* Equatable
* Hashable
* NSExtensionRequestHandling
* UIPasteConfigurationSupporting
* UIStateRestoring
* UITableViewDataSource
* UITableViewDelegate
* UIUserActivityRestoring

## 같이 보기

### 커스텀 뷰 컨트롤러

* _class_ [UIViewController](uiviewcontroller.md) UIKit 앱의 View 계층구조를 관리하는 객체
* _class_ UICollectionViewController Collection View 관리에 특화된 view controller
* _protocol_ UIContentContainer view controller의 컨텐츠를 뷰 사이즈와 제약사항에 맞게 조정하는 메서드들

