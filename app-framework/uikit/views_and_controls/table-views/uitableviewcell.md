---
description: 테이블 뷰에 있는 셀
---

# UITableViewCell

> 원본출처  
> [https://developer.apple.com/documentation/uikit/uitableviewcell](https://developer.apple.com/documentation/uikit/uitableviewcell)

## 개요

이 클래스에 포함된 프로퍼티와 메서드는 셀 컨텐츠와 백그라운드\(텍스트, 이미지, 커스텀 뷰\), 셀 선택과 하이라이팅 상태, 액서세리 뷰를 설정 및 관리하고 셀 컨텐츠의 편집 시작을 지원합니다.

셀을 작성할 때에는 미리 정의된 스타일 중에서 골라서 사용할 수 있습니다. 직접 커스텀하여 사용할 수도 있지만 미리 정의된 셀 스타일을 사용하는것이 가장 간단합니다. 미리 정의된 스타일을 사용하면 셀은 위치와 스타일이 고정된 라벨 및 이미지 하위 뷰를 제공합니다. 개발자가 해야 할 일은 고정된 뷰에 들어갈 텍스트와 이미지 컨텐츠를 제공하는 것 뿐입니다. 미리 정의된 스타일의 셀을 사용하려면 [init\(style:reuseIdentifier:\)](../../../../etc/not-found.md) 메서드를 사용하여 셀을 초기화하거나 Xcode에서 해당 스타일로 셀을 구성하는 것입니다. 셀의 텍스트 및 이미지를 설정하려면 [textLabel](../../../../etc/not-found.md), [detailTextLabel](../../../../etc/not-found.md) 및 [imageView](../../../../etc/not-found.md) 속성을 사용하세요.

미리 정의된 스타일 이상을 만들고자 한다면 셀의 contentView 프로퍼티에 하위 뷰를 추가할 수 있습니다. 하위 뷰를 추가할때에는 뷰의 위치를 지정하고 해당 내용을 직접 설정해야 합니다.

[backgroundView](../../../../etc/not-found.md) 프로퍼티나 상속받은 [backgroundColor](../../../../etc/not-found.md) 프로퍼티를 변경하여 셀의 배경을 바꾸는 것은 미리 정의된 셀이든 커스텀 셀이든 상관없이 가능합니다. iOS 7부터는 셀의 기본 배경 색상이 흰색이 되었습니다. 그 이전 버전에서는 셀을 포함한 테이블 뷰의 배경 색상을 상속합니다. 셀의 배경색을 변경하려면 [tableView\(\_:willDisplay:forRowAt:\)](../../../../etc/not-found.md) 메서드를 호출해야 합니다.

## 주제

### UITableViewCell 초기화하기

* init\(style: UITableViewCell.CellStyle, reuseIdentifier: String?\)

  `style:` 스타일과 `reuseIdentifier:` 재사용 식별자를 사용하여 테이블 셀을 초기화하고 호출자에게 반환합니다.

* init?\(coder: NSCoder\)

### 셀 재사용

* _var_ reuseIdentifier: String?

  재사용 가능한 셀을 식별하는데 사용되는 문자열

* _func_ prepareForReuse\(\)

  테이블 뷰의 delegate가 사용할 수 있도록 재사용 가능한 셀을 준비합니다.

### 미리 정의된 컨텐츠 관리

* _var_ textLabel: UILabel?

  테이블 셀의 메인 텍스트 내용을 표시하는 레이블

* _var_ detailTextLabel: UILabel?

  테이블 셀의 보조 레이블

* _var_ imageView: UIImageView?

  테이블 셀의 이미지 뷰

### 셀 객체 뷰에 액세스

* _var_ contentView: UIView

  셀 객체의 컨텐츠 뷰

* _var_ backgroundView: UIView?

  셀의 배경으로 사용되는 뷰

* _var_ selectedBackgroundView: UIView?

  선택된 셀의 배경으로 사용되는 뷰

* _var_ multipleSelectionBackgroundView: UIView?

  여러 행을 선택할 수 있는 테이블 뷰에서 선택된 셀의 background 뷰

### 액세서리 뷰 관리

* _var_ accessoryType: UITableViewCell.AccessoryType

  셀이 사용할 표준 액서세리 타입 \(일반 상태\)

* _var_ accessoryView: UIView?

  일반적으로 컨트롤로 사용되는 셀 오른쪽의 뷰 \(일반 상태\)

* _var_ editingAccessoryType: UITableViewCell.AccessoryType 셀이 사용할 표준 액서세리 타입 \(편집 상태\)
* _var_ editingAccessoryView: UIView? 일반적으로 컨트롤로 사용되는 셀 오른쪽의 뷰 \(편집 상태\)

### 셀 선택과 하이라이팅

* _var_ isSelected: Bool

  셀 선택 여부를 나타내는 Boolean 값

* _var_ selectionStyle: UITableViewCell.SelectionStyle

  선택된 셀의 스타일

* _func_ setSelected\(Bool, animated: Bool\)

  셀의 선택 상태를 설정합니다. `animated:` 옵션으로 상태간 전환 애니메이션을 줄 수 있습니다..

* _var_ isHighlighted: Bool

  하이라이팅 상태를 나타내는 Boolean 값

* _func_ setHighlighted\(Bool, animated: Bool\)

  셀의 하이라이팅 상태를 설정합니다. `animated:` 옵션으로 상태간 전환 애니메이션을 줄 수 있습니다.

### 셀 편집

* _var_ isEditing: Bool

  셀의 편집 가능 상태를 나타내는 Boolean 값

* _func_ setEditing\(Bool, animated: Bool\)

  수신자의 편집 모드를 설정합니다.

* _var_ editingStyle: UITableViewCell.EditingStyle

  셀의 편집 스타일

* _var_ showingDeleteConfirmation: Bool

  셀이 삭제 확인 버튼을 표시할지 결정하는 Boolean 값

* _var_ showsReorderControl: Bool 셀이 순서 조정 컨트롤을 표시할 지 결정하는 Boolean 값

### 행 드래그

* _var_ userInteractionEnabledWhileDragging: Bool

  드래그하는 동안 사용자와 셀이 상호작용할 수 있는지를 나타내는 Boolean 값

* _func_ dragStateDidChange\(UITableViewCell.DragState\)

  셀에 드래그 상태가 변경되었음을 알립니다.

* _enum_ UITableViewCell.DragState

  드래그 작업과 관련된 행의 현재 상태를 나타내는 상수

### 상태 전환 조정

* _func_ willTransition\(to: UITableViewCell.StateMask\)

  셀 상태가 전환되기 직전에 셀에서 호출됩니다.

* _func_ didTransition\(to: UITableViewCell.StateMask\)

  셀 상태가 전환된 직후 셀에서 호출됩니다.

### 컨텐츠 들여쓰기 관리

* _var_ indentationLevel: Int

  셀 컨텐츠의 들여쓰기 수준.

* _var_ indentationWidth: CGFloat

  셀 콘텐츠의 각 들여쓰기 수준에 대한 너비.

* _var_ shouldIndentWhileEditing: Bool

  테이블 뷰가 편집 모드일때 셀 배경의 들여쓰기 여부를 제어하는 Boolean 값

* _var_ separatorInset: UIEdgeInsets

  셀 컨텐츠에 대한 inset 값

### 포커스 관리

* _var_ focusStyle: UITableViewCell.FocusStyle

  포커스 된 셀의 스타일

### 상수Constants

* _enum_ UITableViewCell.CellStyle

  다양한 셀 스타일의 enum 타입

* _enum_ UITableViewCell.SelectionStyle

  선택된 셀 스타일

* _enum_ UITableViewCell.EditingStyle

  셀에서 사용되는 편집 컨트롤

* _enum_ UITableViewCell.AccessoryType

  셀에서 사용되는 표준 액서세리 컨트롤 타입

* _struct_ UITableViewCell.StateMask

  상태 전환시에 셀의 새 상태를 결정하는데 사용되는 상수

* _enum_ UITableViewCell.SeparatorStyle

  셀 separator 스타일

* _enum_ UITableViewCell.FocusStyle

  포커스 된 셀의 스타일

## 관련 문서

### 상속받은 대상

* [UIView](../uiview.md)

### 준수하는 프로토콜

* CVarArg
* Equatable
* Hashable
* NSCoding
* UIAccessibilityIdentification
* UIGestureRecognizerDelegate
* UIPasteConfigurationSupporting
* UIUserActivityRestoring

## 같이 보기

### 행

* _class_ UISwipeActionsConfiguration

  테이블 행을 스와이프할 때 실행되는 action의 집합입니다.

* _class_ UIContextualAction

  사용자가 테이블 행을 스와이프할 때 표시할 action입니다.

* _class_ UITableViewRowAction

  사용자가 테이블 행을 수평으로 스와이프할 때 표시할 action입니다.

* _enum_ UIContextualAction.Style

  action 버튼에 적용되는 스타일 정보를 나타내는 상수

* 자체 크기 조정 테이블 뷰 셀 만들기

  동적 유형을 지원하는 테이블 뷰 셀을 작성하고 시스템 간격 제약 조건을 사용하여 텍스트 레이블 주변의 간격을 조정합니다.

