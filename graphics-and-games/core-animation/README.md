---
description: '시각적 요소들을 렌더링하고, 구성하고 애니메이션화하세요'
---

# Core Animation

> 원본 출처  
> [https://developer.apple.com/documentation/quartzcore](https://developer.apple.com/documentation/quartzcore)

## 개요

Core Animation은 CPU에 부담을 주지 않고 앱 속도를 저하시키지 않으면서 높은 프레임 속도와 부드러운 애니메이션을 제공합니다. 애니메이션의 각 프레임을 그리는데 필요한 대부분의 작업이 알아서 수행됩니다. 시작 지점이나 끝 지점과 같은 애니메이션 매개 변수를 구성하면 Core Animation이 나머지 작업을 수행하고 대부분의 작업을 그래픽 전 하드웨어로 전달하여 렌더링 속도를 높입니다. 자세한 내용은 [Core Animation 프로그래밍 가이드](../../etc/not-found.md)를 참조하십시오.

## 주제

### 레이어 기초

* _class_ [CALayer](calayer.md)

  이미지 기반 컨텐츠를 관리하고 해당 컨텐츠에 대해 애니메이션을 수행할 수 있는 객체

* _protocol_ CALayerDelegate 레이어 관련 이벤트에 응답하기 위해 앱이 구현할 수 있는 메서드
* _class_ CAConstraint 두 레이어 사이의 단일 레이아웃 제약 조건
* _protocol_ CALayoutManager 객체가 레이어와 그 하위 레이어의 레이아웃을 관리할 수 있게 해주는 메서드
* _class_ CAConstraintLayoutManager

  제약 기반 레이아웃 관리자를 제공하는 객체

* _protocol_ [CAAction](caaction.md)

  객체가 [CALayer](calayer.md) 변경에 의해 트리거 된 액션에 응답할 수 있게 해주는 인터페이스

### 텍스트, 모양, 그라디언트

* _class_ CATextLayer

  일반 문자열이나 속성 문자열의 간단한 텍스트 레이아웃과 렌더링을 제공하는 레이어

* _class_ CAShapeLayer

  좌표공간에 cubic Bezier spline을 그리는 레이어

* _class_ CAGradientLayer

  배경색 위에 색상 그라디언트를 그리고 레이어의 모양을 채우는 레이어 \(둥근 모서리 포함\)

### 애니메이션

* _class_ CAAnimation

  코어 애니메이션의 애니메이션에 대한 추상 슈퍼 클래스

* _protocol_ CAAnimationDelegate

  애니메이션의 시작 또는 중지 시 앱의 응답을 구현할 수 있는 메서드

* _class_ CAPropertyAnimation

  레이어 프로퍼티를 조작하는 애니메이션을 생성하기 위한 CAAnimation의 추상 슈퍼 클래스

* _class_ CABasicAnimation

  레이어 프로퍼티에 기본 단일 키 프레임 애니메이션 기능을 제공하는 객체

* _class_ CAKeyframeAnimation

  레이어 객체에 키 프레임 애니메이션 기능을 제공하는 객체

* _class_ CASpringAnimation

  레이어 프로퍼티에 스프링과 같은 힘을 적용하는 애니메이션

* _class_ CATransition

  레이어의 상태 간 전환에 애니메이션을 제공하는 객체

* _class_ CAValueFunction 애니메이션 변형을 정의하는 유연한 메서드를 제공하는 객체

### 애니메이션 그룹

* _class_ CAAnimationGroup

  여러 애니메이션을 그룹화하고 동시에 실행할 수 있게 해주는 객체

* _class_ CATransaction

  A mechanism for grouping multiple layer-tree operations into atomic updates to the render tree.

### 애니메이션 타이밍

* _func_ CACurrentMediaTime

  현재 절대 시간을 초 단위로 반환합니다.

* _class_ CAMediaTimingFunction

  애니메이션의 페이싱을 타이밍 커브로 정의하는 함수

* _protocol_ CAMediaTiming 계층적 타이밍 시스템을 모델링하는 메서드로서, 객체가 부모 객체와 로컬 시간 사이의 시간을 매핑할 수 있도록 합니다.
* _class_ CADisplayLink

  애플리케이션에서 드로잉을 디스플레이의 주사율와 동기화 할 수 있게 해주는 타이머 객체

### 파티클 시스템

* _class_ CAEmitterLayer

  파티클 시스템을 방출, 애니메이션 및 렌더링하는 레이어

* _class_ CAEmitterCell

  CAEmitterLayer에서 방출되는 입자의 정의

### 고급 레이어 옵션

* _class_ CAScrollLayer

  자체 bound보다 크고 스크롤 가능한 컨텐츠를 표시하는 레이어

* _class_ CATiledLayer 레이어의 컨텐츠 타일을 비동기식으로 제공하는 메서드를 제공하는 레이어. 여러 세부 수준에서 캐시될 수 있습니다.
* _class_ CATransformLayer

  Objects used to create true 3D layer hierarchies, rather than the flattened hierarchy rendering model used by other CALayer classes.

* _class_ CAReplicatorLayer

  다양한 기하학적, 시간적 및 색상 변환을 사용하여 지정된 수의 하위 레이어 복사본을 만드는 레이어

### Metal과 OpenGL

* _class_ CAMetalLayer

  Metal로 그릴수 있는 풀을 관리하는 레이어

* _protocol_ CAMetalDrawable

  Metal로 렌더링되거나 작성될 수 있는 표시 가능한 리소스

* ~~_class_ CAEAGLLayer~~

  A layer that supports drawing OpenGL content in iOS and tvOS applications. `Deprecated`

* ~~_class_ CAOpenGLLayer~~

  A layer that provides a layer suitable for rendering OpenGL content. `Deprecated`

* _class_ CARenderer 애플리케이션이 레이어 트리를 Core OpenGL 컨텍스트로 렌더링할 수 있게 해주는 레이어

### 레이어 컨텐츠의 원격 디스플레이

* _class_ CARemoteLayerClient
* _class_ CARemoteLayerServer

### 변형

* Transforms

  코어 애니메이션의 레이어에 affine 변환을 적용하기 위해 변환 매트릭스를 정의하세요.

### Quartz Composer

* ~~_class_ QCCompositionLayer~~

  A layer that loads, plays, and controls Quartz Composer compositions in a Core Animation layer hierarchy. `Deprecated`

### 참조

* Core Animation Constants
* Core Animation Data Types

## 같이 보기

### 관련 문서

* Core Animation 프로그래밍 가이드

