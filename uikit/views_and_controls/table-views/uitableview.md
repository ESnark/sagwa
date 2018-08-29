---
description: 단일 열에 정렬된 행을 사용하여 데이터를 표시하는 뷰
---

# UITableView

> 원본 출처  
> [https://developer.apple.com/documentation/uikit/uitableview](https://developer.apple.com/documentation/uikit/uitableview)

## 개요

테이블 뷰는 항목 리스트를 단일 열에 표시합니다. UITableView는 UIScrollView을 서브 클래싱 함으로써 사용자가 테이블을 스크롤 할 수 있게 만들었지만 수직 스크롤만 허용됩니다. 테이블의 개별 항목을 구성하는 셀은 UITableViewCell 객체이며, UITableView는 이러한 객체를 사용하여 테이블에 행을 그립니다. 셀에는 제목과 이미지가 있으며 오른쪽 가장자리 부근에 액서세리 뷰가 있을 수 있습니다. 표준 액서세리 뷰에는 disclosure indicator와 detail disclosure indicator가 있으며 전자는 데이터 계층의 다음 단계로, 후자는 선택된 항목의 상세 보기로 이어집니다. 액세서리 뷰는 스위치, 슬라이더와 같은 프레임워크 컨트롤이나 커스텀 뷰일 수도 있습니다. 테이블 뷰는 사용자가 테이블의 행을 삽입, 삭제하고 순서를 변경할 수 있는 편집 모드로 전환될 수도 있습니다.

테이블 뷰는 각각 자체 행이 있는 0개 이상의 섹션으로 구성됩니다. 섹션은 테이블 뷰 내에서 인덱스 번호로 식별되고, 행은 섹션 내에서 인덱스 번호로 식별됩니다. 원하는 섹션 앞에 섹션 Header를 붙일 수 있으며, 선택적으로 섹션 Footer를 선택할 수 있습니다.

테이블 뷰는 [UITableView.Style.plain](../../../not-found.md)과 [UITableView.Style.grouped](../../../not-found.md)의 두 가지 스타일 중 하나를 가질 수 있습니다. UITableView 인스턴스를 만들 때 테이블 스타일을 지정해야하며 이 스타일은 변경할 수 없습니다. plain 스타일에서는 전체 섹션의 일부가 보이는 경우 섹션 머리글과 바닥 글이 내용 위에 떠있게됩니다. 테이블 뷰에는 테이블 오른쪽에 막대 모양으로 나타나는 색인이 있고\(예 : "A"에서 "Z"까지\) 특정 라벨을 터치하여 대상 섹션으로 이동할 수 있습니다.  
grouped 스타일은 모든 셀에 기본 배경색과 기본 백그라운드 뷰를 제공합니다. 백그라운드 뷰는 특정 섹션의 모든 셀에 대한 시각적 그룹화를 제공합니다. 예를 들어, 한 그룹은 개인의 이름을 나타내고 다른 그룹은 그 사람이 사용하는 전화번호를 표시하며, 또 다른 그룹은 이메일 계정을 표시하는 그룹이 될 수도 있습니다. 그룹화 된 테이블의 예는 설정 응용 프로그램을 참조하십시오. grouped 스타일의 테이블 뷰는 인덱스를 가질 수 없습니다.

UITableView declares a category on NSIndexPath that enables you to get the represented row index \(row property\) and section index \(section property\), and to construct an index path from a given row index and section index \(init\(row:section:\) method\). Especially in table views with multiple sections, you must evaluate the section index before identifying a row by its index number.

UITableView 객체는 반드시 데이터 소스 역할을 하는 객체와 delegate 역할을 하는 객체가 있어야 합니다. 일반적으로 App delegate 객체가 그 역할을 하지만 더 자주 쓰이는 것은 커스텀 UITableViewController 객체입니다. UITableView는 테이블을 만들고 테이블에 행이 추가, 제거, 순서 변경될 때 데이터 모델을 관리해야 합니다. delegate는 테이블 행 구성 및 선택, 행 순서 변경, 강조 표시, 액서세리 뷰 조작을 관리합니다.

\(첫 번째 파라미터가 true인\) [setEditing\(\_:animated:\)](../../../not-found.md) 메세지가 보내지면 해당 테이블 뷰는 편집 모드로 진입해서 편집과 순서 변경을 위한 컨트롤을 표시합니다. 이 컨트롤들은 각 UITableViewCell의 [editingStyle](../../../not-found.md)에 따라서 다릅니다.  
삽입이나 삭제 컨트롤을 클릭하면 데이터 원본이 [tableView\(\_:commit:forRowAt:\)](../../../not-found.md) 메시지를 받게 됩니다. 필요한 경우 [deleteRows\(:at:with\)](../../../not-found.md) 또는 [insertRows\(:at:with\)](../../../not-found.md)를 호출하여 삭제 또는 삽입을 커밋합니다. 또한 테이블 뷰 셀에 [showsReorderControl](../../../not-found.md) 프로퍼티가 true로 설정된 경우 데이터 원본은 편집 모드에서 [tableView\(\_:moveRowAt:to:\)](../../../not-found.md) 메시지를 수신합니다. 데이터 소스는 [tableView\(\_:canMoveRowAt:\)](../../../not-found.md)를 구현하여 셀에 대한 재정렬 컨트롤을 선택적으로 제거할 수 있습니다.

UITableView는 보이는 행의 테이블 뷰 셀을 캐시합니다. 기본 셀과는 다른 내용이나 동작 특성을 갖는 커스텀 [UITableViewCell](../../../not-found.md)을 만들 수가 있습니다. [A Closer Look at Table View Cells](../../../not-found.md) 문서가 방법을 설명합니다.

UITableView는 UITableView의 새 인스턴스를 생성하거나 새 데이터 소스를 할당할 때만 [reloadData\(\)](../../../not-found.md)를 호출하도록 UIView의 [layoutSubviews\(\)](../../../not-found.md) 메서드를 오버라이드합니다. 테이블 뷰를 다시 로드하면 선택된 테이블 항목을 포함한 테이블의 현재 상태가 지워집니다. 그러나 reloadData\(\)를 직접 명시적으로 호출하면 테이블 상태가 삭제된 후에는 layoutSubviews\(\)이 직/간접적으로 호출되어도 [reloadData\(\)](../../../not-found.md)가 트리거되지 않습니다.

## 상태 보존

테이블 뷰의 [restorationIdentifier](../../../not-found.md) 속성에 값을 지정하면 선택된 행과 현재 화면상에 보이는 첫번째 행이 보존됩니다. 테이블의 데이터 소스는 [UIDataSourceModelAssociation](../../../not-found.md) 프로토콜을 준수함으로써 테이블의 행 위치와 관계없이 행의 내용을 식별할 수 있습니다. 테이블의 데이터 원본이 UIDataSourceModelAssociation 프로토콜을 사용하는 경우, 상태를 저장할 때 데이터 소스를 참조하여 화면상의 첫번째 행과 선택한 셀의 indexPath를 식별자로 변환합니다.  
복원 중에는 데이터 소스를 참조하여 식별자를 다시 indexPath로 변환하며 맨 위에 보이는 행을 재설정하고 셀을 다시 선택합니다. 테이블의 데이터 소스가 UIDataSourceModelAssociation 프로토콜을 구현하지 않으면 선택된 셀의 indexPath와 마찬가지로 스크롤 위치가 직접 저장 및 복원됩니다.

상태 보존 및 복원에 대한 자세한 내용은 [iOS용 앱 프로그래밍 가이드](../../../not-found.md)를 참조하세요.

## 주제

### UITableView 객체 초기화

* init\(frame: CGRect, style: UITableView.Style\)

  `frame:` 과 `style:` 을 갖는 테이블 뷰 객체를 초기화하고 반환합니다.

* init?\(coder: NSCoder\)

### 테이블 뷰 데이터 제공

* var dataSource: UITableViewDataSource?

  테이블 뷰의 데이터 소스 역할을 하는 객체

* protocol UITableViewDataSource

  UITableViewDataSource 프로토콜은 UITableView 객체에 대한 앱 데이터 모델을 조정하는 객체에서 사용됩니다.

* protocol UITableViewDataSourcePrefetching

  테이블 뷰의 데이터 요구 사항에 대한 사전 경고를 제공하여 비동기 데이터 로드 작업의 트리거를 허용하는 프로토콜입니다.

### 테이블 뷰 동작 커스터마이징

* var delegate: UITableViewDelegate?

  테이블 뷰의 delegate 역할을 하는 객체입니다.

* protocol UITableViewDelegate

  UITableView 객체의 delegate는 UITableViewDelegate 프로토콜을 준수해야 합니다. 프로토콜의 선택적 메서드들을 통해서 섹션 Header와 Footer 설정과 셀 선택, 삭제, 위치 조정 등의 작업을 수행할 수 있습니다.

### 테이블 뷰 설정하기

* var style: UITableView.Style

  테이블 뷰의 스타일

* func numberOfRows\(inSection: Int\) -&gt; Int

  `inSection:` 에 해당하는 섹션의 행 \(테이블 셀\) 갯수를 반환합니다.

* var numberOfSections: Int

  테이블 뷰의 섹션 갯수

* var rowHeight: CGFloat

  테이블 뷰의 각 행 \(즉, 테이블 셀\)의 높이

* var separatorStyle: UITableViewCell.SeparatorStyle

  셀을 구분하는 Separator의 스타일

* var separatorColor: UIColor? Separator의 색깔
* var separatorEffect: UIVisualEffect? Separator에 적용되는 효과
* var backgroundView: UIView?

  테이블 뷰의 백그라운드 뷰

* var separatorInset: UIEdgeInsets

  셀 Separator의 기본 inset을 지정합니다.

* var separatorInsetReference: UITableView.SeparatorInsetReference

  Separator Inset 값을 해석하는 방법

* enum UITableView.SeparatorInsetReference

  Separator Inset 값의 해석방법을 나타내는 상수

* var cellLayoutMarginsFollowReadableWidth: Bool 셀 margin이 읽을 수 있는 컨텐츠 가이드 너비에서 유래한 것인지를 나타내는 Boolean 값

### 테이블 뷰 셀 생성하기

* func register\(UINib?, forCellReuseIdentifier: String\)

  테이블 셀의 nib 객체를 `forCellReuseIdentifier:` 로 등록합니다.

* func register\(AnyClass?, forCellReuseIdentifier: String\)

  새 테이블 셀 생성에 사용할 클래스를 등록합니다.

* func dequeueReusableCell\(withIdentifier: String, for: IndexPath\) -&gt; UITableViewCell

  `withIdentifier:` 식별자를 갖는 재사용 가능한 테이블 뷰 셀을 반환하고 테이블에 추가합니다.

* func dequeueReusableCell\(withIdentifier: String\) -&gt; UITableViewCell?

  `withIdentifier:` 식별자로 지정된 재사용 가능한 테이블 뷰 셀 객체를 반환합니다.

### Header 뷰와 Footer 뷰에 액세스

* func register\(UINib?, forHeaderFooterViewReuseIdentifier: String\)

  nib 파일을 통해서 `forHeaderFooterViewReuseIdentifier:` 를 갖는 Header 셀이나 Footer 셀을 등록합니다.

* func register\(AnyClass?, forHeaderFooterViewReuseIdentifier: String\)

  새 Header 셀이나 Footer 셀을 만드는데 사용할 클래스를 등록합니다.

* func dequeueReusableHeaderFooterView\(withIdentifier: String\) -&gt; UITableViewHeaderFooterView?

  `withIdentifier:` 식별자로 지정된 재사용 가능한 Header 셀이나 Footer 셀을 반환합니다.

* var tableHeaderView: UIView?

  테이블 위에 표시되는 액서세리 뷰

* var tableFooterView: UIView?

  테이블 아래에 표시되는 액서세리 뷰

* var sectionHeaderHeight: CGFloat

  섹션 Header의 높이

* var sectionFooterHeight: CGFloat

  섹션 Footer의 높이

* func headerView\(forSection: Int\) -&gt; UITableViewHeaderFooterView?

  `forSection:` 순서에 해당하는 섹션의 Header 뷰를 반환합니다.

* func footerView\(forSection: Int\) -&gt; UITableViewHeaderFooterView?

  `forSection:` 순서에 해당하는 섹션의 Footer 뷰를 반환합니다.

### 셀과 섹션에 액세스

* func cellForRow\(at: IndexPath\) -&gt; UITableViewCell? `at:` IndexPath에 있는 테이블 셀을 반환합니다.
* func indexPath\(for: UITableViewCell\) -&gt; IndexPath?

  `for:` 테이블 셀의 IndexPath를 반환합니다.

* func indexPathForRow\(at: CGPoint\) -&gt; IndexPath?

  `at:` 위치에 해당하는 행과 섹션에 해당하는 IndexPath를 반환합니다.

* func indexPathsForRows\(in: CGRect\) -&gt; \[IndexPath\]? `in:` CGRect로 둘러싸인 행을 나타내는 IndexPath 배열을 반환합니다.
* var visibleCells: \[UITableViewCell\] 현재 테이블에 보여지고 있는 테이블 셀 배열
* var indexPathsForVisibleRows: \[IndexPath\]? 현재 테이블에 보여지고 있는 테이블 셀의 IndexPath 배열

### 엘리먼트 높이 추정

* var estimatedRowHeight: CGFloat

  테이블 행의 추정 높이

* var estimatedSectionHeaderHeight: CGFloat

  테이블 섹션 Header의 높이

* var estimatedSectionFooterHeight: CGFloat

  테이블 섹션 Footer의 높이

### 테이블 뷰 스크롤

* func scrollToRow\(at: IndexPath, at: UITableView.ScrollPosition, animated: Bool\)

  `at:IndexPath`에 있는 행이 `at: UITableView.ScrollPosition`위치에 올때까지 테이블 뷰를 스크롤합니다.

* func scrollToNearestSelectedRow\(at: UITableView.ScrollPosition, animated: Bool\)

  테이블 뷰를 스크롤 했을때 `at:` 위치에 가장 가까운 행이 위치하도록 합니다.

### 섹션 관리

* var indexPathForSelectedRow: IndexPath?

  선택한 행의 행과 섹션을 가리키는 IndexPath

* var indexPathsForSelectedRows: \[IndexPath\]? 선택한 행들을 가리키는 IndexPath
* func selectRow\(at: IndexPath?, animated: Bool, scrollPosition: UITableView.ScrollPosition\)

  `at:` IndexPath의 행을 선택하고 `scrollPosition:` 위치로 자동 스크롤 시킬지 선택할 수 있습니다.

* func deselectRow\(at: IndexPath, animated: Bool\)

  `at:` IndexPath의 선택을 취소하고 `animated:` 옵션으로 취소 애니메이션을 줄 것인지 선택할 수 있습니다.

* var allowsSelection: Bool

  사용자가 행을 선택할 수 있는지를 결정하는 Boolean 값

* var allowsMultipleSelection: Bool

  편집모드가 아닌 상황에서 사용자가 두개 이상의 행을 선택할수 있을지를 결정하는 Boolean 값

* var allowsSelectionDuringEditing: Bool 편집모드 상태에서 사용자가 셀을 선택할 수 있는지를 선택할 수 있을지를 선택하는 Boolean 값
* var allowsMultipleSelectionDuringEditing: Bool

  편집모드 상태에서 사용자가 두개 이상의 cell을 선택할 수 있게 할지를 결정하는 Boolean 

### 행과 섹션을 삽입, 삭제, 이동하기

* func insertRows\(at: \[IndexPath\], with: UITableView.RowAnimation\)

  `with:` 삽입 애니메이션 옵션을 사용하여 `at:` IndexPath 위치에 행을 삽입합니다.

* func deleteRows\(at: \[IndexPath\], with: UITableView.RowAnimation\)

  `with:` 삭제 애니메이션 옵션을 사용하여 `at:` IndexPath 위치의 행을 삭제합니다.

* func moveRow\(at: IndexPath, to: IndexPath\)

  `at:` 위치의 행을 `to:` 위치로 이동시킵니다.

* func insertSections\(IndexSet, with: UITableView.RowAnimation\)

  하나 이상의 섹션을 테이블 뷰에 삽입한니다. `with:` 옵션을 통해 삽입 애니메이션을 설정할 수 있습니다.

* func deleteSections\(IndexSet, with: UITableView.RowAnimation\)

  하나 이상의 섹션을 테이블 뷰에서 삭제합니다. `with:` 옵션을 통해 삭제 애니메이션을 설정할 수 있습니다.

* func moveSection\(Int, toSection: Int\)

  섹션을 새로운 위치로 이동시킵니다.

* func performBatchUpdates\(\(\(\) -&gt; Void\)?, completion: \(\(Bool\) -&gt; Void\)? = nil\)

  삽입, 삭제, 재로딩, 이동을 하는 여러개의 작업을 그룹화해서 애니메이션합니다.

* func beginUpdates\(\)

  테이블 뷰의 행과 섹션을 삽입, 삭제 또는 선택하는 일련의 메서드 호출을 시작합니다.

* func endUpdates\(\)

  테이블 뷰의 행 섹션을 삽입, 삭제, 선택 또는 다시 로드하는 일련의 메서드 호출을 완료합니다.

### 드래그 상호작용 관리

* var dragDelegate: UITableViewDragDelegate?

  테이블 뷰에서 드래그 앤 드롭을 관리하는 delegate 객체

* protocol UITableViewDragDelegate

  테이블 뷰에서 드래그를 시작하기 위한 인터페이스

* var hasActiveDrag: Bool

  행이 테이블 뷰에서 들어올려져 있으며 아직 내려놓지 않았음을 나타내는 Boolean 값

* var dragInteractionEnabled: Bool

  테이블 뷰가 앱 간의 드래그앤 드롭을 지원하는지를 나타내는 Boolean 값

### 드롭 상호작용 관리

* var dropDelegate: UITableViewDropDelegate?

  테이블 뷰에 컨텐츠를 내려놓는 동작을 관리하는 delegate

* protocol UITableViewDropDelegate

  테이블 뷰로 내려놓는 동작을 관리하는 인터페이스

* var hasActiveDrop: Bool

### 테이블 셀 수정모드 관리

* var isEditing: Bool

  테이블 뷰의 편집모드 상태를 결정짓는 Boolean 값

* func setEditing\(Bool, animated: Bool\)

  테이블 뷰의 편집모드 상태를 토글합니다.

### 테이블 뷰 다시 로드하기

* var hasUncommittedUpdates: Bool

  테이블 뷰에서 새로운 행이 놓일 자리에 drop placeholder를 표시할지, 행의 순서를 변경할지 결정하는 Boolean 값

* func reloadData\(\)

  테이블 뷰의 섹션과 행을 다시 로드합니다.

* func reloadRows\(at: \[IndexPath\], with: UITableView.RowAnimation\)

  `with:` 애니메이션 효과를 사용하여 `at:` 위치의 행을 다시 로드합니다.

* func reloadSections\(IndexSet, with: UITableView.RowAnimation\)

  `with:` 애니메이션 효과를 사용하여 지정된 섹션을 다시 로드합니다.

* func reloadSectionIndexTitles\(\)

  테이블 뷰 오른쪽의 인덱스 바를 다시 로드합니다.

### 테이블 뷰의 그리기 영역 액세스

* func rect\(forSection: Int\) -&gt; CGRect

  `forSection:` 위치에 있는 섹션의 drawing 영역을 반환합니다.

* func rectForRow\(at: IndexPath\) -&gt; CGRect

  `at:` 위치에 있는 행의 drawing 영역을 반환합니다.

* func rectForFooter\(inSection: Int\) -&gt; CGRect

   `forSection:` 섹션의 Footer drawing 영역을 반환합니다.

* func rectForHeader\(inSection: Int\) -&gt; CGRect

   `forSection:` 섹션의 Header drawing 영역을 반환합니다.

### Prefetching Data

테이블 뷰가 시간이 오래 걸리는 데이터 로딩 프로세스에 의존하고 있다면 뷰를 표시하기 이전에 데이터를 프리페치해서 사용자 경험을 개선할 수 있습니다. [UITableViewDataSourcePrefetching](../../../not-found.md) 프로토콜을 준수하는 객체를 [prefetchDataSource](../../../not-found.md) 객체에 할당함으로써 셀의 데이터를 프리페치할 시기를 전달받을 수 있습니다.

* var prefetchDataSource: UITableViewDataSourcePrefetching? 테이블 뷰에 대한 프리페치 데이터 소스 역할을 하는 객체로써 곧 있을 셀 데이터 요구사항에 대한 알림을 받습니다.

### 테이블 인덱스 설정하기

* var sectionIndexMinimumDisplayRowCount: Int

  테이블 행의 갯수가 해당 값 이상으로 늘어나면 테이블 오른쪽에 인덱스 리스트가 나타나기 시작합니다.

* var sectionIndexColor: UIColor?

  인덱스 텍스트의 색깔

* var sectionIndexBackgroundColor: UIColor?

  터치하지 않은 상태에서의 섹션 인덱스 배경 색상

* var sectionIndexTrackingBackgroundColor: UIColor?

  터치한 상태에서의 섹션 인덱스 배경 색상

### 포커스 관리

* var remembersLastFocusedIndexPath: Bool

  테이블 뷰가 마지막으로 포커스되었던 IndexPath의 포커스를 자동으로 반환해야 할지를 나타내는 Boolean 값

### 상수Constants

* enum UITableView.Style

  테이블 뷰 스타일

* enum UITableView.ScrollPosition

  주어진 행이 스크롤될 테이블 뷰 상의 위치 \(상단, 중간, 하단\)

* enum UITableView.RowAnimation

  행을 삽입하거나 삭제하는 애니메이션

* Section Index Icons

  섹션 인덱스에 아이콘 표시를 요청합니다.

* Default Dimension

  지정된 항목의 기본값

### 노티피케이션Notification

* class let selectionDidChangeNotification: NSNotification.Name

  테이블 뷰 상의 선택된 셀이 바뀌었을때 발송됩니다.

### Instance Properties

* var insetsContentViewsToSafeArea: Bool

## 관련 문서

### 상속받은 대상

* UIScrollView

### 준수하는 프로토콜

* CVarArg
* Equatable
* Hashable
* NSCoding
* UIAccessibilityIdentification
* UIDataSourceTranslating
* UIPasteConfigurationSupporting
* UISpringLoadedInteractionSupporting
* UIUserActivityRestoring

## 같이 보기

### View

* class UITableViewController

  테이블 뷰 관리를 전문으로 하는 뷰 컨트롤러

* class UITableViewFocusUpdateContext

  컨텍스트 객체로써 한 뷰에서 다른 뷰로 업데이트 되는 특정 포커스 갱신에 대한 정보를 제공합니다.

* class UILocalizedIndexedCollation 섹션 인덱스를 갖는 테이블 뷰에 대해서 해당 데이터의 구성, 정렬, 지역화 하는 방법을 제공하는 객체입니다.

