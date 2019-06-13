---
description: 포함된 뷰를 스크롤하고 확대/축소할 수 있는 뷰입니다.
---

# UIScrollView

> 원문 출처  
> [https://developer.apple.com/documentation/uikit/uiscrollview](https://developer.apple.com/documentation/uikit/uiscrollview)

## Declaration

{% tabs %}
{% tab title="Swift" %}
```swift
class UIScrollView : UIView
```
{% endtab %}

{% tab title="Objective-C" %}
```objectivec
@interface UIScrollView : UIView
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

UIScrollView는 UITableView와 UITextView를 포함한 몇몇 UIKit 클래스들의 상위 클래스입니다.

UIScrollView 객체\(또는 그냥 스크롤 뷰\)의 중심 개념은 컨텐츠 뷰에서 origin\(이하 원점\)을 조정할 수 있는 뷰라는 것입니다. 스크롤 뷰는 컨텐츠를 자체 프레임에 clip 시키고 이 프레임은 \(반드시 그렇지는 않지만\) 일반적으로 애플리케이션의 메인 윈도우와 일치합니다. 스크롤 뷰는 손가락의 움직임을 추적하고 그에 따라 원점을 조정합니다. 스크롤 뷰를 통해서 자신의 컨텐츠를 보여주는 뷰는 컨텐츠 뷰의 오프셋에 고정되어 있는 새로운 원점을 기준으로 해당 부분을 그립니다. 스크롤 뷰는 수직, 수평 스크롤 인디케이터를 보여줄 때를 제외하고는 자체적으로 그리는 것이 없습니다. 스크롤 뷰는 스크롤이 언제 멈출지 알아야 하기 때문에 반드시 컨텐츠 뷰의 크기를 알고 있어야 합니다. 기본적으로 컨텐츠의 범위를 넘는 스크롤이 일어났을 때에는 바운스해서 되돌아가게 되어 있습니다.

스크롤 뷰 내에 컨텐츠를 그리기를 처리하는 객체는 스크린의 크기를 넘지 않도록 컨텐츠의 서브뷰를 채워 넣어야 합니다. 사용자가 스크롤 뷰를 스크롤할때 이 객체는 반드시 서브뷰를 추가하고 제거해야 합니다.

스크롤 뷰에는 스크롤 바가 없기 때문에 터치 신호가 스크롤하려는 의도인지, 컨텐츠의 서브뷰를 추적하려는 것인지를 알아야 합니다. 이것을 알아내기 위해서 스크롤 뷰는 타이머를 시작하면서 터치다운 이벤트를 일시적으로 차단하고 타이머가 끝나기 전까지 터치중인 손가락의 움직임을 관찰합니다. 큰 움직임이 없이 타이머가 끝나면 스크롤 뷰는 컨텐츠의 터치된 서브뷰에 추적 이벤트를 전달하고 타이머가 경과하기 전에 손가락이 충분한 드래그 움직임을 보인다면 서브뷰로 가는 모든 추적을 취소하고 스크롤링을 수행합니다. 서브클래스는 \(스크롤 뷰에 의해 호출되는\) [touchesShouldBegin\(\_:with:in:\)](../../../etc/not-found.md), [isPagingEnabled](../../../etc/not-found.md), [touchesShouldCancle\(in:\)](../../../etc/not-found.md) 메서드를 오버라이드 할 수 있으며 이 메서드들은 스크롤 뷰가 스크롤링 제스처를 컨트롤하는 방법에 영향을 미칩니다.

스크롤 뷰는 컨텐츠의 확대 및 panning도 처리합니다. 사용자가 pinch-in, pinch-out 제스처를 취하면 스크롤 뷰는 컨텐츠의 오프셋과 스케일을 조절합니다. 제스처가 끝났을 때 컨텐츠 뷰를 관리하는 객체는 반드시 컨텐츠의 서브뷰를 업데이트해야 합니다. \(손가락이 여전히 닿아있더라도 제스처는 끝날 수 있습니다.\) 제스처가 진행 중인 동안 스크롤 뷰는 서브뷰에 어떤 추적 호출도 보내지 않습니다.

UIScrollView 클래스는 반드시 UIScrollViewDelegate 프로토콜을 채택해야 하는 delegate를 가질 수 있습니다. 확대와 panning을 동작시키기 위해서는 delegate가 반드시 [viewForZooming\(in:\)](../../../etc/not-found.md)과 [scrollViewDidEndZooming\(\_:with:atScale:\)](../../../etc/not-found.md) 메서드를 구현해야 합니다. 또한 최대\([maximumZoomScale](../../../etc/not-found.md)\)와 최소\([minimumZoomScale](../../../etc/not-found.md)\) 확대 스케일은 반드시 달라야 합니다.

### 상태 보존

뷰의 [restorationIdentifier](../../../etc/not-found.md) 프로퍼티에 값을 할당했다면 해당 뷰는 앱 실행 간에 스크롤 관련 정보를 보존하려 할 것입니다. 구체적으로는 [zoomScale](../../../etc/not-found.md), [contentInset](../../../etc/not-found.md), [contentOffset](../../../etc/not-found.md) 프로퍼티가 보존됩니다. 복원 중에 스크롤 뷰는 이 값들을 불러와서 이전과 똑같은 지점으로 스크롤하여 해당 부분의 컨텐츠를 보여줄 것입니다. 상태 보존과 복구 작업 방법에 대한 더 자세한 정보는 [iOS 앱 프로그래밍 가이드](../../../etc/not-found.md)를 읽어보세요.

## 주제

### Responding to Scroll View Interactions

* _var_ delegate: UIScrollViewDelegate? 스크롤 뷰 객체의 delegate
* _protocol_ UIScrollViewDelegate

  UIScrollViewDelegate 프로토콜에 의해 선언된 메서드는 프로토콜을 채택한 delegate가 UIScrollView 클래스로부터의 메세지를 받을 수 있도록 하여 스크롤링, 확대, 스크롤되는 컨텐츠의 감속 및 스크롤링 애니메이션과 같은 작업에 반응할 수 있게 됩니다.

### 컨텐츠의 사이즈와 오프셋 관리

* _var_ contentSize: CGSize

  컨텐츠 뷰의 크기

* _var_ contentOffset: CGPoint 컨텐츠 뷰의 원점\(origin\)은 스크롤 뷰 원점으로부터의 오프셋 지점입니다.
* _func_ setContentOffset\(CGPoint, animated: Bool\) 수신자의 원점에 해당하는 컨텐츠 뷰 원점에서 오프셋을 설정합니다.

### 컨텐츠 Inset 동작 처리

* _var_ adjustedContentInset: UIEdgeInsets

  컨텐츠 inset과 스크롤 뷰의 safe area에서 유래한 inset

* _var_ contentInset: UIEdgeInsets 컨텐츠 뷰와 safe area 또는 스크롤 뷰 가장자리 사이의 inset 거리
* _var_ contentInsetAdjustmentBehavior: UIScrollView.ContentInsetAdjustmentBehavior

  컨텐츠 오프셋의 조정을 결정하는 동작

* _enum_ UIScrollView.ContentInsetAdjustmentBehavior 조정된 컨텐츠 inset에 safe area inset을 추가하는 방식을 나타내는 상수
* _func_ adjustedContentInsetDidChange\(\) 스크롤 뷰의 조정된 컨텐츠 inset이 변경되었을 때 호출됩니다.

### 레이아웃 가이드 가져오기

* _var_ frameLayoutGuide: UILayoutGuide 스크롤 뷰의 변형되지 않은 frame 직사각형을 기준으로 한 레이아웃 가이드
* _var_ contentLayoutGuide: UILayoutGuide 스크롤 뷰의 이동되지 않은 컨텐츠 직사각형을 기준으로 한 레이아웃 가이드

### 스크롤 뷰 설정

* _var_ isScrollEnabled: Bool

  스크롤 가능 여부를 결정하는 Boolean 값

* _var_ isDirectionalLockEnabled: Bool 특정 방향의 스크롤 비활성화를 가리키는 Boolean 값
* _var_ isPagingEnabled: Bool 스크롤 뷰의 페이지 가능 여부를 결정하는 Boolean 값
* _var_ scrollsToTop: Bool 최상단 스크롤 제스쳐 가능 여부를 결정하는 Boolean 값
* _var_ bounces: Bool 스크롤 뷰가 컨텐츠 가장자리를 벗어났을때 튕겨 돌아오는 효과를 적용할 것인지를 가리키는 Boolean 값
* _var_ alwaysBounceVertical: Bool 수직 스크롤 중 컨텐츠 끝에 도달했을때 항상 바운싱 효과를 적용할 것인지를 결정하는 Boolean 값
* _var_ alwaysBounceHorizontal: Bool 수평 스크롤 중 컨텐츠 끝에 도달했을때 항상 바운싱 효과를 적용할 것인지를 결정하는 Boolean 값

### 스크롤 상태 가져오기

* _var_ isTracking: Bool

  사용자가 스크롤을 하기 위해서 터치했는지를 알려주는 Boolean 값

* _var_ isDragging: Bool 사용자가 컨텐츠 스크롤을 시작했는지를 알려주는 Boolean 값
* _var_ isDecelerating: Bool 사용자가 손을 뗀 후 컨텐츠가 스크롤 뷰에서 움직이고 있음을 알려주는 Boolean 값
* _var_ decelerationRate: UIScrollView.DecelerationRate 사용자가 손을 뗀 후 감속률을 나타내는 부동 소수점 값
* _struct_ UIScrollView.DecelerationRate 스크롤 뷰의 감속률

### 스크롤 인디케이터와 새로고침 컨트롤 관리

* _var_ indicatorStyle: UIScrollView.IndicatorStyle 스크롤 인디케이터 스타일
* _enum_ UIScrollView.IndicatorStyle 스크롤 인디케이터의 스타일. 인디케이터 스타일 값을 설정할 때 사용하는 상수입니다.
* ~~_var_ scrollIndicatorInsets: UIEdgeInsets~~ `Deprecated`

  스크롤 인디케이터와 스크롤 뷰의 가장자리 사이의 inset 거리

* _var_ showsHorizontalScrollIndicator: Bool 수평 스크롤 인디케이터가 보이게 할 것인지를 결정하는 Boolean 값
* _var_ showsVerticalScrollIndicator: Bool 수직 스크롤 인디케이터가 보이게 할 것인지를 결정하는 Boolean 값
* _func_ flashScrollIndicators\(\) 스크롤 인디케이터를 잠시 표시합니다.
* _var_ refreshControl: UIRefreshControl? 스크롤 뷰와 관련된 새로고침 컨트롤

### 특정 위치로 스크롤

* _func_ scrollRectToVisible\(CGRect, animated: Bool\) 특정 위치로 이동하여 수신자에서 해당 위치가 보이도록 합니다.

### 터치 처리하기

* _func_ touchesShouldBegin\(Set, with: UIEvent?, in: UIView\) -&gt; Bool 보여지는 컨텐츠에 손가락이 닿았을 때의 동작을 커스터마이징 하기 위해 서브클래스 상에서 오버라이드 되는 메서드입니다.
* _func_ touchesShouldCancel\(in: UIView\) -&gt; Bool 컨텐츠 서브 뷰와 관련된 터치를 취소하고 드래그를 시작할 것인지를 결정하는 값을 반환합니다.
* _var_ canCancelContentTouches: Bool 컨텐츠에 대한 터치가 추적으로 이어질지를 결정하는 Boolean 값
* _var_ delaysContentTouches: Bool 스크롤 뷰가 터치 다운 제스처의 처리를 지연시킬 지를 결정하는 Boolean 값
* _var_ directionalPressGestureRecognizer: UIGestureRecognizer 방향 버튼 터치를 위한 기본 제스처 인식기

### Zooming and Panning

* _var_ panGestureRecognizer: UIPanGestureRecognizer

  팬 제스처의 기본 제스처 인식기

* _var_ pinchGestureRecognizer: UIPinchGestureRecognizer? 핀치 제스처의 기본 제스처 인식기
* _func_ zoom\(to: CGRect, animated: Bool\) 컨텐츠의 특정 영역으로 확대해서 수신자 상에서 보이도록 합니다.
* _var_ zoomScale: CGFloat 스크롤 뷰의 컨텐츠에 적용된 현재 배율을 나타내는 부동 소수점 값
* _func_ setZoomScale\(CGFloat, animated: Bool\) 현재 확대 배율을 지정합니다.
* _var_ maximumZoomScale: CGFloat 스크롤 뷰 컨텐츠에 적용될 수 있는 최대 배율을 지정하는 부동 소수점 값
* _var_ minimumZoomScale: CGFloat 스크롤 뷰 컨텐츠에 적용될 수 있는 최소 배율을 지정하는 부동 소수점 값
* _var_ isZoomBouncing: Bool 수신자에게 지정된 배율 한계를 초과해서 확대/축소가 일어났음을 알려주는 Boolean 값
* _var_ isZooming: Bool 현재 확대/축소가 일어나고 있음을 알려주는 Boolean 값
* _var_ bouncesZoom: Bool 확대/축소 배율이 최대/최소 한계를 넘었을 때 되돌아가는 컨텐츠 스케일 애니메이션을 사용할 것인지를 나타내는 Boolean 값

### 키보드 관리

* _var_ keyboardDismissMode: UIScrollView.KeyboardDismissMode

  스크롤 뷰에서 드래그가 시작되었을 때 키보드를 사라지게 하는 방법

* _enum_ UIScrollView.KeyboardDismissMode 스크롤 뷰에서 드래그가 시작되었을 때 키보드를 사라지게 하는 방법

### 인덱스 관리

* _var_ indexDisplayMode: UIScrollView.IndexDisplayMode 유저가 스크롤을 하는 동안 인덱스를 표시하는 방법
* _enum_ UIScrollView.IndexDisplayMode

  유저가 스크롤을 하는 동안 인덱스를 표시하는 방법

### 인스턴스 프로퍼티

* _var_ automaticallyAdjustsScrollIndicatorInsets: Bool `Beta`
* _var_ horizontalScrollIndicatorInsets: UIEdgeInsets
* _var_ verticalScrollIndicatorInsets: UIEdgeInsets

## 관련 문서

### 상속받은 대상

* [UIView](uiview.md)

### 준수하는 프로토콜

* CVarArg
* Equatable
* Hashable
* NSCoding
* UIAccessibilityIdentification
* UIFocusItemScrollableContainer
* UILargeContentViewerItem
* UIPasteConfigurationSupporting
* UIUserActivityRestoring

## 같이 보기

### 컨테이너 뷰

* Collection Views 설정 및 커스텀이 가능한 레이아웃을 사용하여 중첩된 뷰를 표시하세요.
* [Table Views](table-views/) 하나의 열과 커스텀 가능한 행에 데이터를 표시하세요.
* _class_ UIStackView 열 또는 행으로 뷰 집합을 배치하기 위한 효율적인 인터페이스입니다.

