---
description: 좌표공간에 cubic Bezier spline을 그리는 레이어
---

# CAShapeLayer

> 원문 출처  
> [https://developer.apple.com/documentation/quartzcore/cashapelayer](https://developer.apple.com/documentation/quartzcore/cashapelayer)

## Summary

> **SDKs**
>
> * iOS 3.0+
> * macOS 10.6+
> * tvOS 9.0+
> * Mac Catalyst 13.0+
>
> **Framework**
>
> * Core Animation

## Declaration

{% tabs %}
{% tab title="Swift" %}
```swift
class CAShapeLayer : CALayer
```
{% endtab %}

{% tab title="Objective-C" %}
```objectivec
@interface CAShapeLayer : CALayer
```
{% endtab %}
{% endtabs %}

## 개요

이 Shape는 레이어의 컨텐츠와 첫 번째 하위 레이어 사이에 합성됩니다.

Shape는 안티앨리어싱 되어 그려지며, 해상도 독립성을 유지하기 위해서 가능하다면 언제든지 래스터링 전에 화면 공간에 매핑됩니다. 그러나 레이어 또는 그 상위 항목에 적용되는 CoreImage 필터와 같은 특정 유형의 이미지 처리 작업은 로컬 좌표 공간에서 래스터화를 강제 적용할 수 있습니다.

목록 1은 shape 레이어를 사용하여 복잡한 복합 경로를 작성하고 표시하는 방법을 보여줍니다. 이 예시에서, 점차적으로 변형된 일련의 타원들은 간단한 꽃 모양을 형성합니다. 경로를 표시하는 이 shape 레이어는 [fillRule](../../etc/not-found.md)을 가지고 있으며 fillRule은 꽃잎이 겹쳐지는 부분이 노란색으로 채워지는 것을 막는 [evenOdd](../../etc/not-found.md)를 설정합니다.

_목록 1 Shape 레이어를 사용하여 스타일링된 꽃 만들기_

```swift
let width: CGFloat = 640
let height: CGFloat = 640
     
let shapeLayer = CAShapeLayer()
shapeLayer.frame = CGRect(x: 0, y: 0,
                          width: width, height: height)
     
let path = CGMutablePath()
     
stride(from: 0, to: CGFloat.pi * 2, by: CGFloat.pi / 6).forEach {
    angle in 
    var transform  = CGAffineTransform(rotationAngle: angle)
        .concatenating(CGAffineTransform(translationX: width / 2, y: height / 2))
    
    let petal = CGPath(ellipseIn: CGRect(x: -20, y: 0, width: 40, height: 100),
                       transform: &transform)
    
    path.addPath(petal)
}
    
shapeLayer.path = path
shapeLayer.strokeColor = UIColor.red.cgColor
shapeLayer.fillColor = UIColor.yellow.cgColor
shapeLayer.fillRule = kCAFillRuleEvenOdd
```



![&#xADF8;&#xB9BC; 1 Shape &#xB808;&#xC774;&#xC5B4;&#xC5D0; &#xD45C;&#xC2DC;&#xB418;&#xB294; &#xBCF5;&#xD569; &#xACBD;&#xB85C;](../../.gitbook/assets/image%20%281%29.png)

{% hint style="info" %}
알림

Shape 래스터화는 정확성보다 속도를 선호할 수 있습니다. 예를 들어 교차 경로가 여러 개인 픽셀은 정확한 결과를 제공하지 않을 수 있습니다.
{% endhint %}

## 주제 <a id="topics"></a>

### Shape 경로 지정 <a id="specifying-the-shape-path"></a>

* _var_ path: CGPath?

  렌더링될 shape를 정의하는 경로. 애니메이션 가능합니다.

### Shape 스타일 프로퍼티 액세스 <a id="accessing-shape-style-properties"></a>

* _var_ fillColor: CGColor?

  Shape 경로를 채우는 데 사용되는 색상. 애니메이션 가능합니다.

* _var_ fillRule: CAShapeLayerFillRule

  Shape의 경로를 채울 때 사용되는 규칙

* _var_ lineCap: CAShapeLayerLineCap

  Shape 경로의 line cap 스타일

* _var_ lineDashPattern: \[NSNumber\]? 스트로크 시 Shape의 경로에 적용되는 대시 패턴.
* _var_ lineDashPhase: CGFloat

  스트로크 시 Shape 경로에 적용되는 대시 단계. 애니메이션 가능합니다.

* _var_ lineJoin: CAShapeLayerLineJoin Shape 경로에 대한 line join 스타일
* _var_ lineWidth: CGFloat

  Shape 경로의 line 너비. 애니메이션 가능합니다.

* _var_ miterLimit: CGFloat

  Shape 경로를 스트로킹할때 사용되는 miter 한계. 애니메이션 가능합니다.

* _var_ strokeColor: CGColor?

  Shape 경로를 스트로크할때 사용되는 색상. 애니메이션 가능합니다.

* _var_ strokeStart: CGFloat

  경로 스트로크를 시작할 상대 위치. 애니메이션 가능합니다.  
  The relative location at which to begin stroking the path. Animatable.

* _var_ strokeEnd: CGFloat

  경로 스트로크를 끝낼 상대 위치. 애니메이션 가능합니다.

### 상수 <a id="constants"></a>

* Shape Fill Mode Values

  이 상수들은 [fillRule](../../etc/not-found.md)에 적용가능한 채우기 모드를 지정하는데 사용됩니다.

* Line Join Values

  이 상수들은 스트로크된 경로의 연결된 세그먼트 사이의 결합 모양을 지정합니다. [lineJoin](../../etc/not-found.md)의 [그림 1](../../etc/not-found.md)은 line join 스타일 모양을 보여줍니다.

* Line Cap Values

  이 상수들은 스트로킹시 열린 경로에 대한 끝점의 모양을 지정합니다. [lineCap](../../etc/not-found.md)의 [그림 1](../../etc/not-found.md)은 line cap 스타일의 모양을 보여줍니다.

## 관련 문서

### 상속받은 대상 <a id="inherits-from"></a>

* CALayer

### 준수하는 프로토콜 <a id="conforms-to"></a>

* CVarArg
* Equatable
* Hashable

## 같이 보기 <a id="see-also"></a>

### 텍스트, 모양, 그라디언트 <a id="text-shapes-and-gradients"></a>

* _class_ CATextLayer

  일반 문자열이나 속성 문자열의 간단한 텍스트 레이아웃과 렌더링을 제공하는 레이어

* _class_ CAGradientLayer

  배경색 위에 색상 그라디언트를 그리고 레이어의 모양을 채우는 레이어 \(둥근 모서리 포함\)

