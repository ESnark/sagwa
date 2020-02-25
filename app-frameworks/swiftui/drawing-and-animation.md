---
description: '색상, 모양, 그림자와 상태에 따른 커스텀 전환 애니메이션으로 뷰를 강화하세요'
---

# 그리기와 애니메이션

> 원문 출처  
> [https://developer.apple.com/documentation/swiftui/drawing\_and\_animation](https://developer.apple.com/documentation/swiftui/drawing_and_animation)

## Summary

> **Framework**
>
> * SwiftUI

## Overview

그리기 도구를 사용해서 Shape을 조합하거나 고유 디자인의 Shape을 위해서 커스텀 경로를 정의하세요. Apply styles from environment-aware colors to rich gradients to the foreground, background, and outline of your shapes.

## 주제 <a id="topics"></a>

### Essentials

* 경로와 shape 그리기 Landmark 앱 사용자들은 리스트 상의 랜드마크를 방문할 때마다 배지를 획득합니다. 물론, 사용자마다 매지를 주기 위해서는여러분들이 만들어주어야 할 것입니다. 이 튜토리얼에서 여러분들은 경로와 Shape을 조합하여 배지를 만드는 방법을 안내받을 것이며, 그리고 나서 위치를 나타내는 shape을 오버레이하게 될 것입니다.
* SwiftUI로 커스텀 뷰 빌드하기 데이터 주도 트랜지션과 애니메이션으로 커스텀 뷰를 생성하세요
* protocol Shape 뷰를 그릴 때 사용할 수 있는 2차원 Shape입니다.

### Animation

* 뷰 애니메이션과 트랜지션 SwiftUI를 사용하면 효과의 위치에 관계없이 View 또는 View state에 대한 변경 사항을 개별적으로 애니메이션 할 수 있습니다. SwiftUI는 이러한 결합, 오버랩 및 인터럽트 가능한 애니메이션의 모든 복잡성을 처리합니다.
* struct Animation
* protocol Animatable View 애니메이션을 위한 타입
* protocol AnimatableModifier 애니메이션으로 다른 수정자를 만들 수 있는 수정자
* func withAnimation&lt;Result&gt;\(Animation?, \(\) -&gt; Result\) -&gt; Result 제공된 애니메이션에 따라 View의 body를 다시 계산한 결과를 반환합니다.
* struct AnimatablePair 스스로 애니메이션 가능한 animatable 값의 쌍
* struct EmptyAnimatableData 애니메이션 가능한 데이터의 빈 타입
* struct AnyTransition 타입이 삭제된 트랜지션

### Shapes

* struct Rectangle View 프레임 안에 정렬되는 직사각형 Shape
* enum Edge 사각형의 한 가장자리를 가리키는 열거값
* struct RoundedRectangle View 프레임 안에 정렬되는 모서리가 둥근 직사각형 Shape
* struct Circle View 프레임 중앙에 정렬되는 원
* struct Ellipse View 프레임 안에 정렬되는 타원
* struct Capsule View 프레임 안에 정렬되는 Capsule Shape
* struct Path 2차원 Shape의 외곽선

### Transformed Shapes

* protocol InsettableShape 다른 Shape을 삽입하기 위해서 자체 inset을 설정할 수 있는 Shape 타입
* struct ScaledShape Scale 변이 적용된 Shape
* struct RotatedShape 회전 변환이 적용된 Shape
* struct OffsetShape Offset 변환이 적용된 Shape
* struct TransformedShape Affine 변환이 적용된 Shape

### 페인트, 스타일, 그라디언트 <a id="paints-styles-and-gradients"></a>

* struct Color 환경 의존적인 색상
* struct ImagePaint 무한 평면에서 이미지를 반복하는 페인트 타입
* struct Gradient 각각 위치 값을 갖는 색상 배열로 표시되는 색상 그라디언트
* struct LinearGradient 선형 그라디언트
* struct AngularGradient 각도 그라디언트
* struct RadialGradiant 방사형 그라디언
* struct ForegroundStyle
* struct FillStyle 벡터 Shape의 래스터라이징 스타일
* protocol ShapeStyle Shape을 View로 바꾸는 방법
* enum RoundedCornerStyle 둥근 직사각형의 모서리 Shape을 정의합니다.
* struct SelectionShapeStyle
* struct SeparatorShapeStyle
* struct StrokeStyle

### Geometry

* struct GeometryProxy 컨테이너 뷰의 \(앵커 해상도 기준\) 사이즈와 좌표 공간에 접근할 수 있는 프록시
* struct GeometryReader 컨텐츠를 자기 자신의 사이즈와 좌표공간의 함수로 정의하는 컨테이너 뷰
* protocol GeometryEffect 조상이나 자손 View를 크게 바꾸지 않고 View의 시각적 모양을 변경하는 이펙트
* struct Angle 라디안 또는 각도 단위로 액세스 할 수 있는 기하학적 각도
* struct Anchor 특정한 View와 앵커 소스로부터 파생되는 불투명 값
* struct UnitPoint
* enum CoordinateSpace
* struct ProjectionTransform
* protocol VectorArithmetic 애니메이션 가능한 타입의 애니메이션 가능한 값으로 제공될 수 있는 타입



## 같이 보기 <a id="see-also"></a>

### 사용자 인터페이스 <a id="user-interface"></a>

* [뷰와 컨트롤](views-and-controls.md) 컨텐츠를 화면에 표시하고 사용자 상호 작용을 처리하세요.
* [뷰 레이아웃과 표현](view-layout-and-presentation.md) 뷰를 스택에 결합하고 뷰 그룹과 리스트를 동적으로 생성하며 뷰 표현과 계층을 정의하세요
* 프레임워크 통합 기존의 앱에 SwiftUI 뷰를 통합시키고 AppKit, UIKit, WatchKit 뷰와 컨트롤러를 SwiftUI 뷰 계층에 내장시키세요



