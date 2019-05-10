# Core Graphics

> 원문 출처  
> [https://developer.apple.com/documentation/coregraphics](https://developer.apple.com/documentation/coregraphics)

## 개요

Core Graphics 프레임워크는 Quartz 고급 드로잉 엔진을 기반으로 합니다. 이 프레임워크는 저수준의 경량 2D 렌더링을 탁월한 해상도로 출력합니다. 이 프레임워크를 사용하면 경로 기반 그리기, 변환, 색상 관리, 오프스크린 렌더링, 패턴, 그라데이션 및 쉐이딩, 이미지 데이터 관리, 이미지 생성 및 마스킹, PDF 문서의 작성, 표시, 파싱을 처리할 수 있습니다.

또한 MacOS에서 코어 그래픽은 디스플레이 하드웨어, 저수준 사용자 입력 이벤트 및 윈도우 설정 시스템 관련 서비스를 포함하고 있습니다.

## 주제

### 기하 데이터 유형

* _struct_ CGFloat

  Core Graphics 및 연관 프레임워크에서 사용되는 기본 부동소수점 스칼라 타입

* _struct_ CGPoint 2차원 좌표계상의 지점을 나타내는 구조체
* _struct_ CGSize 너비와 높이 값을 갖는 구조체
* _struct_ CGRect 사각형의 위치와 크기값을 갖는 구조체
* _struct_ CGVector 2차원 벡터값을 갖는 구조체
* _struct_ CGAffineTransform 2D 그래픽을 그릴때 사용되는 affine 변환 매트릭스

### 2D 드로잉

* _class_ CGContext

  Quartz 2D 드로잉 환경

* _class_ CGImage

  비트맵 이미지 또는 이미지 마스크

* _class_ [CGPath](cgpath.md)

  변경 가능/변경 불가능 타입의 그래픽 경로: 그래픽 컨텍스트에 그려질 모양이나 선의 수학적 설명

* _class_ CGMutablePath

  변경 가능한 그래픽 경로: 그래픽 컨텍스트에 그려질 모양이나 선의 수학적 설명

* _class_ CGLayer

  Core Graphics로 그려진 컨텐츠를 재사용하기 위한 오프스크린 컨텍스트

### 색상과 폰트

* _class_ CGColor

  A set of components that define a color, with a color space specifying how to interpret them.

* _class_ CGColorConversionInfo

  다른 시스템 서비스에서 사용하기 위해서 색 영역 간 변환방법을 설명하는 객체

* _class_ CGColorSpace

  색상값을 표시하기 위해 해석 방법을 지정하는 프로파일

* _class_ CGFont

  텍스트 드로잉을 위한 문자 글리프와 레이아웃 정보 집합

### PDF 문서로 작업하기

* _class_ CGPDFDocument

  PDF 드로잉 정보를 포함한 문서

### Utility and Support Classes

* _class_ CGDataConsumer

  An abstraction for data-writing tasks that eliminates the need to manage a raw memory buffer.

* _class_ CGDataProvider

  An abstraction for data-reading tasks that eliminates the need to manage a raw memory buffer.

* _class_ CGShading

  색상 간의 자연스러운 전환을 위한 정의로서, 개발자가 제공하는 커스텀 함수로 제어됩니다. 이 함수는 방사상 또는 축 그라데이션을 채우는 기능을 합니다.

* _class_ CGGradient 방사상 그라데이션과 축 그라데이션에서 색상간에 부드러운 전환을 위한 정의
* _class_ CGFunction

  콜백함수를 정의하고 사용하는 일반 기능

* _class_ CGPattern 그래픽 경로를 그리는데 사용되는 2D 패턴

### 서비스

* Quartz Display Services

  디스플레이 하드웨어를 구성하고 제어하는 macOS 윈도우 서버 기능에 대한 직접 액세스를 제공합니다.

* Quartz Event Services 이벤트 탭\(tap\) 관리 기능을 제공합니다. \(이벤트 탭은 macOS 상에서 저수준 유저 input 이벤트를 관찰하고 스트림을 바꾸는 필터 역할을 합니다.\)
* Quartz Window Services macOS 윈도우 서버가 관리하는 윈도우에 대한 정보를 제공합니다.

### 참고

* Core Graphics Structures
* Core Graphics Enumerations
* Core Graphics Constants
* Core Graphics Functions
* Core Graphics Data Types
* Core Graphics Data Types

### Enumerations

* enum CGPathFillRule 어느 영역이 경로\(Path\)의 내부인지를 결정하는 규칙. [fillPath\(using:\)](../../etc/not-found.md)과 [clip\(using:\)](../../etc/not-found.md) 메서드에서 사용됩니다.

### 구조체

* _struct_ CGPDFAccessPermissions
* _struct_ CGPSConverterCallbacks PostScript 컨버터 객체를 생성할 때 제공되는 콜백을 유지하기 위한 구조체

### 클래스

* _class_ CGPSConverter

  PostScript 데이터를 PDF 데이터로 변환하는데 사용되는 불투명 데이터 타입

## 같이 보기

### 관련 문서

* [Quartz 2D 프로그래밍 가이드](https://developer.apple.com/library/archive/documentation/GraphicsImaging/Conceptual/drawingwithquartz2d/Introduction/Introduction.html#//apple_ref/doc/uid/TP30001066)



