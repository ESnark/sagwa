---
description: 뷰를 스택에 결합하고 뷰 그룹과 리스트를 동적으로 생성하며 뷰 표현과 계층을 정의하세요
---

# 뷰 레이아웃과 표현

> 원문 출처  
> [https://developer.apple.com/documentation/swiftui/view\_layout\_and\_presentation](https://developer.apple.com/documentation/swiftui/view_layout_and_presentation)

## Summary

> **Framework**
>
> * SwiftUI

## Overview

스택과 리스트를 사용하여 UI View를 배치하세요. 정적 View와 데이터 콜렉션으로부터 동적으로 생성되는 View를 조합할 수 있습니다. 모든 컨테이너 View는 컨텐츠나 인터페이스 크기의 변화에 따라 자식 View의 위치를 조정하게 됩니다.

## 주제 <a id="topics"></a>

### Essentials

* [리스트와 네비게이션 구성](https://developer.apple.com/tutorials/swiftui/building-lists-and-navigation) 기본 랜드마크 디테일 View를 만들기 위해서 랜드마크 전체 리스트를 사용자에게 보여주고,  각 지역의 상세 정보를 사용자가 볼 수 있는 방법을 제공해야 합니다.
* [복잡한 인터페이스 구성하기](https://developer.apple.com/tutorials/swiftui/composing-complex-interfaces) 랜드마크 앱의 홈 화면은 \(세로로\) 스크롤 가능한 카테고리 리스트와 각 가로로 스크롤 되는 카테고리별 랜드마크 리스트로 이루어져 있습니다. 이 기본 네비게이션을 만들면서 구성된 View가 다양한 장치 크기 및 방향에 어떻게 적용될 수 있는지 살펴보게 됩니다.

### Stacks

* struct HStack 자식 View를 수평선에 배치하는 View
* struct VStack 자식 View를 수직선에 배치하는 View
* struct ZStack 자식 View를 같은 축에 겹쳐서 배치하는 View

### 리스트와 스크롤 View <a id="lists-and-scroll-views"></a>

* struct List 하나의 열에 대이터 행을 배치하는 컨테이너
* struct ForEach SwiftUI가 View를 동적으로 생성하는 데 사용하는 식별된 데이터 콜렉션
* struct ScrollView 스크롤 가능한 View
* protocol DynamicViewContent 데이터 콜렉션으로부터 View를 생성해내는 View 타입
* protocol Identifiable A class of types whose instances hold the value of an entity with stable identity.
* enum Axis 2차원 좌표계의 수평 또는 수직 위치값

### 컨테이너 View <a id="container-views"></a>

* struct Form 설정 또는 인스펙터와 같이 데이터 입력에 사용되는 컨트롤을 그룹화 하기 위한 컨테이너입니다.
* struct Group View 컨텐츠를 그룹화 할 수 있는 공간
* struct GroupBox 컨텐츠의 논리적 그룹과 연관된 선택적 레이블이 있는 스타일 View
* struct Section 계층적 View 컨텐츠를 생성할 수 있는 공간

### Spacers and Dividers

* struct Spacer 스택 레이아웃에 포함된 경우 스택의 주축을 따라서 확장되고, 스택에 포함되지 않은 경우 양 축에 모두 확장되는 가변적인 공간
* struct Divider 컨텐츠간 분리를 하는데 사용되는 시각적 요소

### Architectural Views

* struct NavigationView 네비게이션 계층 상에서 가시적인 경로를 보여주는 View 스택을 표현하는 View
* struct TabView 인터렉티브 UI 요소를 사용하여 다수의 자식 View를 스위치할 수 있는 View
* struct HSplitView 자식 View를 수평선 상에 배치하고 자식 View 간에 디바이더를 사용하여 사이즈를 조절할 수 있는 레이아웃 컨테이너
* struct VSplitView 자식 View를 수직선 상에 배치하고 자식 View 간에 디바이더를 사용하여 사이즈를 조절할 수 있는 레이아웃 컨테이너

### Presentations

* struct Alert 경고 표시를 위한 컨테이너
* struct ActionSheet Action sheet 표시를 위한 저장 타입

### 조건부로 보이는 항목 <a id="conditionally-visible-items"></a>

* struct EmptyView
* struct EquatableView 이전 값과 자기 자신을 비교하여 새 값이 이전 값과 동일한 경우 자식 업데이트를 방지하는 View 타입

### 자주 사용되지 않는 View <a id="infrequently-used-views"></a>

* struct AnyView 타입이 삭제된 View
* struct TupleView View 값의 스위프트 튜플로부터 생성된 View



## 같이 보기 <a id="see-also"></a>

### 사용자 인터페이스 <a id="user-interface"></a>

* [뷰와 컨트롤](views-and-controls.md) 컨텐츠를 화면에 표시하고 사용자 상호 작용을 처리하세요.
* [그리기와 애니메이션](drawing-and-animation.md) 색상, 모양, 그림자와 상태에 따른 커스텀 전환 애니메이션으로 뷰를 강화하세요
* [프레임워크 통합](framework-intergration.md) 기존의 앱에 SwiftUI 뷰를 통합시키고 AppKit, UIKit, WatchKit 뷰와 컨트롤러를 SwiftUI 뷰 계층에 내장시키세요

