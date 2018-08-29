---
description: 하나의 열과 커스텀 가능한 행에 데이터를 표시하세요.
---

# Table Views

> 원본 출처[https://developer.apple.com/documentation/uikit/views\_and\_controls/table\_views](https://developer.apple.com/documentation/uikit/views_and_controls/table_views)

## 주제

### View

* class [UITableView](uitableview.md)

  단일 열에 정렬된 행을 사용하여 데이터를 표시하는 뷰

* class UITableViewController

  테이블 뷰 관리를 전문으로 하는 뷰 컨트롤러

* class UITableViewFocusUpdateContext

  컨텍스트 객체로써 한 뷰에서 다른 뷰로 업데이트 되는 특정 포커스 갱신에 대한 정보를 제공합니다.

* class UILocalizedIndexedCollation 섹션 인덱스를 갖는 테이블 뷰에 대해서 해당 데이터의 구성, 정렬, 지역화 하는 방법을 제공하는 객체입니다.

### Rows

* class UITableViewCell

  테이블 뷰에 있는 셀

* class UISwipeActionsConfiguration

  테이블 행을 스와이프할 때 실행되는 action의 집합입니다.

* class UIContextualAction

  사용자가 테이블 행을 스와이프할 때 표시할 action입니다.

* class UITableViewRowAction

  사용자가 테이블 행을 수평으로 스와이프할 때 표시할 action입니다.

* enum UIContextualAction.Style

  action 버튼에 적용되는 스타일 정보를 나타내는 상수

* 자체 크기 조정 테이블 뷰 셀 만들기

  동적 유형을 지원하는 테이블 뷰 셀을 작성하고 시스템 간격 제약 조건을 사용하여 텍스트 레이블 주변의 간격을 조정합니다.

### Headers and Footers

* class UITableViewHeaderFooterView

  테이블 섹션의 상단 또는 하단에 배치하여 해당 섹션에 대한 추가 정보를 표시할 수 있는 재사용 가능한 뷰입니다.

### Adornments

* class UIRefreshControl

  스크롤 뷰 컨텐츠를 새로고침 할 수 있는 표준 컨트롤

### Drag and Drop

* 테이블 뷰에서 Drag and Drop 지원하기

  테이블 뷰에서 드래그 앤 드롭을 시작합니다.

* protocol UITableViewDragDelegate

  테이블 뷰에서 드래그를 시작하기 위한 인터페이스입니다.

* protocol UITableViewDropDelegate

  테이블 뷰에서 놓기 동작을 처리하기 위한 인터페이스입니다.  
  The interface for handling drops in a table view.

* protocol UITableViewDropCoordinator

  테이블 뷰에서 커스텀 드롭 동작을 조정하기 위한 인터페이스입니다.

* class UITableViewDropPlaceholder
* class UITableViewDropProposal

  테이블 뷰에서 드롭을 처리하기 위해 제안된 솔루션

* protocol UITableViewDropItem 테이블 뷰로 놓여지는 항목과 관련된 데이터
* protocol UITableViewDropPlaceholderContext

  표시할 데이터가 실제로 들어오기 전에 임시적으로 테이블 뷰에 삽입되는 객체

* protocol UIDataSourceTranslating DataSource 객체를 관리하기 위한 고급 인터페이스
* class UITableViewPlaceholder

## 같이 보기

### 컨테이너 뷰

* Collection Views 설정 및 커스텀이 가능한 레이아웃을 사용하여 중첩된 뷰를 표시하세요.
* Table Views 하나의 열과 커스텀 가능한 행에 데이터를 표시하세요.
* _class_ UIStackView 열또는 행으로 뷰 집합을 배치하기 위한 효율적인 인터페이스입니다.
* _class_ UIScrollView 포함된 뷰를 스크롤하고 확대/축소할 수 있는 뷰입니다.

