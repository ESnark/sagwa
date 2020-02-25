---
description: 컨텐츠를 화면에 표시하고 사용자 상호 작용을 처리하세요.
---

# 뷰와 컨트롤

> 원문 출처  
> [https://developer.apple.com/documentation/swiftui/views\_and\_controls](https://developer.apple.com/documentation/swiftui/views_and_controls)

## Summary

> **Framework**
>
> * SwiftUI

## Overview

뷰와 컨트롤은 앱 UI의 시각적인 블록으로써, 앱 컨텐츠를 화면에 표시하는데 사용됩니다. 뷰는 텍스트, 이미지, 모양, Custom drawing과 이것들이 조합된 구성요소들을 나타낼 수 있습니다. 컨트롤은 플랫폼 및 맥락과 일치하는 일관된 API로 사용자가 상호작용할 수 있게 해줍니다.

컴바인 뷰는 시각적 관계와 계층을 지정하기 위해서 컨테이너를 사용합니다. modifers라고 불리는 메서드를 사용하면 화면, 동작, 내장된 뷰와 앱을 위해 생성된 뷰의 상호작용성을 커스텀할 수 있습니다.

modifier는 뷰와 컨트롤에 다음과 같은 용도로 적용될 수 있습니다:

* 뷰의 크기, 위치와 모양 속성 조정하기
* 탭, 제스처 등의 사용자 상호작용에 응답하기
* 드래그 앤 드롭 지원
* 애니메이션과 transition 커스터마이징
* 스타일 설정 및 다른 환경변수 지정

뷰와 컨트롤의 사용방법에 대한 더 자세한 정보는 Human Interface Guidelines를 참조하세요

## 주제

### Essentials

* _protocol_ View SwiftUI View를 나타내는 타입
* [뷰의 생성과 조합\(컴바인\)](https://developer.apple.com/tutorials/swiftui/creating-and-combining-views) 이 튜토리얼은 여러분이 좋아하는 장소를 발견하고 공유하는 _Landmarks_라는 iOS 앱을 만들면서 진행됩니다. 여러분은 랜드마크의 상세정보를 보여주는 화면을 구성하는 것부터 시작하게 될 것입니다.
* [UI 컨트롤로 작업하기](https://developer.apple.com/tutorials/swiftui/working-with-ui-controls) Landmarks 앱에서는 사용자가 프로필을 작성함으로써 개성을 표현할 수 있습니다. 사용자들에게 자기 자신의 프로필을 수정할 수 있는 기능을 제공하기 위해서 여러분들은 편집모드를 추가하고 설정 화면을 디자인하게 될 것입니다.

### Text

* _struct_ Text 한 줄 이상의 읽기전용 텍스트를 보여주는 뷰
* _struct_ TextField 편집 가능한 텍스트 인터페이스를 보여주는 컨트롤
* _struct_ SecureField 사용자가 노출되지 않는 텍스트를 입력할 수 있는 컨트롤
* _struct_ Font 실행환경에 의존적인 폰트

### Images

* _struct_ Image 실행환경에 의존적인 이미지를 표시하는 뷰

### Buttons

* _struct_ Button 트리거 되었을 때 동작하는 컨트롤
* _struct_ NavigationLink A button that triggers a navigation presentation when pressed.
* _struct_ MenuButton 누르면 선택지 리스트를 포함한 메뉴를 나타내는 버튼
* _struct_ EditButton 현재 편집 스코프의 편집모드를 토글하는 버튼
* _struct_ PasteButton 트리거되면 클립보드로부터 데이터를 읽어오는 시스템 버튼

### Value Selectors

* _struct_ Toggle on/off 상태를 토글하는 컨트롤
* _struct_ Picker 상호배제적인 선택을 수행하는 컨트롤
* _struct_ DatePicker 날짜를 선택하는 컨트롤
* _struct_ Slider 선형적으로 경계가 정해진 범위 내에서 값을 선택하는 컨트롤
* _struct_ Stepper 증가, 감소 동작을 수행하는데 사용되는 컨트롤

### Supporting Types

* _struct_ ViewBuilder 클로저로부터 뷰를 구성해내는 커스텀 파라미터 속성
* _protocol_ ViewModifier 뷰나 다른 ViewModifier에 적용되는 수정자\(modifier\)로써, 원본 값과 다른 버전을 생성해냅니다.

## 같이 보기

### 사용자 인터페이스

* [뷰 레이아웃과 표현](view-layout-and-presentation.md) 뷰를 스택에 결합하고 뷰 그룹과 리스트를 동적으로 생성하며 뷰 표현과 계층을 정의하세요
* 그리기와 애니메이션 색상, 모양, 그림자와 상태에 따른 커스텀 전환 애니메이션으로 뷰를 강화하세요
* 프레임워크 통합 기존의 앱에 SwiftUI 뷰를 통합시키고 AppKit, UIKit, WatchKit 뷰와 컨트롤러를 SwiftUI 뷰 계층에 내장시키세요

