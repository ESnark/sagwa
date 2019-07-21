---
description: '변경 가능/변경 불가능 타입의 그래픽 경로: 그래픽 컨텍스트에 그려질 모양이나 선의 수학적 설명'
---

# CGPath

> 원문 출처  
> [https://developer.apple.com/documentation/coregraphics/cgpath](https://developer.apple.com/documentation/coregraphics/cgpath)

## Summary

> **SDKs**
>
> * iOS 2.2+
> * macOS 10.7+
> * Mac Catalyst 13.0+ `Beta`
> * tvOS 9.0+
> * watchOS 3.0+
>
> **Framework**
>
> * Core Graphics

## 주제

### 그래픽 경로 생성

* init\(rect: CGRect, transform: UnsafePointer?\)

  변경불가능한 사각형 경로를 생성합니다.

* init\(ellipseIn: CGRect, transform: UnsafePointer?\) 변경불가능한 타원경로를 생성합니다.
* init\(roundedRect: CGRect, cornerWidth: CGFloat, cornerHeight: CGFloat, transform: UnsafePointer?\) 변경불가능한 둥근 사각형 경로를 생성합니다.

### 그래픽 경로 복사

* _func_ copy\(\) -&gt; CGPath? 그래픽 경로의 변경 불가능한 사본을 생성합니다.
* _func_ copy\(using: UnsafePointer?\) -&gt; CGPath? 변환 매트릭스에 의해 변형된 그래픽 경로의 변경 불가능한 사본을 생성합니다.
* _func_ copy\(dashingWithPhase: CGFloat, lengths: \[CGFloat\], transform: CGAffineTransform\) -&gt; CGPath 점선 스트로크 경로를 그린 결과물에 해당하는 새로운 경로를 반환합니다.
* _func_ copy\(strokingWithWidth: CGFloat, lineCap: CGLineCap, lineJoin: CGLineJoin, miterLimit: CGFloat, transform: CGAffineTransform\) -&gt; CGPath 실선 경로를 그린 결과물에 해당하는 새로운 경로를 반환합니다.
* _func_ mutableCopy\(\) -&gt; CGMutablePath? 존재하는 그래픽 경로의 변경 가능한 사본을 생성합니다.
* _func_ mutableCopy\(using: UnsafePointer?\) -&gt; CGMutablePath? 변환 매트릭스에 의해 변형된 그래픽 경로듸 변경 가능한 사본을 생성합니다.

### 그래픽 경로 검사

* _var_ boundingBox: CGRect 그래픽 경로의 모든 지점을 포함하는 경계 박스를 반환합니다.
* _var_ boundingBoxOfPath: CGRect 그래픽 경로의 경계 박스를 반환합니다.
* _var_ currentPoint: CGPoint 그래픽 경로의 현재 지점을 반환합니다.
* _func_ contains\(CGPoint, using: CGPathFillRule, transform: CGAffineTransform\) -&gt; Bool 지정된 지점이 경로 내부에 있는지를 Boolean 값으로 반환합니다.
* _var_ isEmpty: Bool 그래픽 경로가 비어있는지를 Boolean 값으로 반환합니다.
* _func_ isRect\(UnsafeMutablePointer?\) -&gt; Bool 그래픽 경로가 사각형인지를 가리키는 값을 반환합니다.

### 경로 요소에 함수 적용

* _func_ apply\(info: UnsafeMutableRawPointer?, function: CGPathApplierFunction\)

  그래픽 경로의 각 요소마다 커스텀 적용 함수를 호출합니다.

* _typealias_ CGPathApplierFunction 그래픽 경로에서 요소를 볼 수 있는 콜백함수를 정의합니다.
* _struct_ CGPathElement 경로 요소에 대한 정보를 제공하는 데이터 구조체
* _enum_ CGPathElementType 경로상의 요소 타입

### Core Foundation 타입으로 작업하기

* _class var_ typeID: CFTypeID

  Core Graphics 경로에 대한 Core Foundation 타입 식별자를 반환합니다.

### 인스턴스 메서드

* _func_ applyWithBlock\(\(UnsafePointer\) -&gt; Void\)

## 같이 보기

* _class_ CGContext

  Quartz 2D 드로잉 환경

* _class_ CGImage

  비트맵 이미지 또는 이미지 마스크

* _class_ CGMutablePath

  변경 가능한 그래픽 경로: 그래픽 컨텍스트에 그려질 모양이나 선의 수학적 설명

* _class_ CGLayer

  Core Graphics로 그려진 컨텐츠를 재사용하기 위한 오프스크린 컨텍스트

