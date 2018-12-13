# CALayer

> 원본 출처  
> [https://developer.apple.com/documentation/quartzcore/calayer](https://developer.apple.com/documentation/quartzcore/calayer)

## 개요 <a id="overview"></a>

레이어는 종종 뷰에 대한 백업 저장소를 제공하는데 사용되기도 하지만 컨텐츠를 표시할 뷰 없이도 사용될 수 있습니다. 레이어의의 기본 작업은 개발자가 제공하는 시각적 컨텐츠를 관리하는 것이지만 레이어 자체에는 배경색, 테두리 및 그림자 같은 시각적 속성이 설정되어 있습니다. 시각적 컨텐츠 관리 외에도, 레이어는 해당 컨텐츠를 화면에 표시하는데 사용되는 컨텐츠의 형태\(위치, 크기 및 변환 등\)에 대한 정보도 보유합니다. 레이어 프로퍼티를 수정함으로써 레이어의 컨텐츠나 지오메트리 상의 에니메이션을 시작할 수 있습니다. 레이어 객체는 레이어의 타이밍 정보를 정의하는 [CAMediaTiming](../../etc/not-found.md) 프로토콜을 채택하여 레이어와 애니메이션의 지속 시간과 페이싱을 캡슐화합니다.

레이어 객체가 뷰에 의해 생성된 경우 일반적으로 뷰는 자신을 레이어의 delegate로 자동 할당하는데 해당 관계는 변경되어선 안됩니다. 직접 작성하는 레이어의 경우 delegate 객체를 할당하고 해당 객체를 사용하여 레이어의 컨텐츠를 동적으로 제공하며 다른 작업도 수행할 수 있습니다. 또한 레이어에는 하위 뷰의 레이아웃을 별도로 관리하기 위한 레이아웃 관리자 객체가 있을 수 있습니다\(LayoutManager 프로퍼티에 할당됨\)

## 주제 <a id="topics"></a>

### 레이어 생성 <a id="creating-a-layer"></a>

* init\(\)

  초기화된 CALayer 객체를 반환합니다.

* init\(layer: Any\)

  지정된 레이어의 커스텀 필드를 복사하거나 초기화하기 위해 오버라이드합니다.

*  init\(remoteClientId: UInt32\)

  remote client ID로 레이어를 초기화합니다.

### 연관 레이어 객체에 접근하기 <a id="accessing-related-layer-objects"></a>

* _func_ presentation\(\) -&gt; Self? 현재 화면에 표시되는 레이어 상태를 나타내는 프레젠테이션 레이어 객체의 복사본을 반환합니다.
* _func_ model\(\) -&gt; Self

  수신자와 연결된 모델 레이어 객체가 있는 경우 반환합니다.

### Delegate에 접근하기 <a id="accessing-the-delegate"></a>

* _var_ delegate: CALayerDelegate?

  레이어의 delegate 객체

### 레이어 컨텐츠 제공 <a id="providing-the-layers-content"></a>

* _var_ contents: Any?

  레이어의 컨텐츠를 제공하는 객체입니다. 애니메이션 가능합니다.

* _var_ contentsRect: CGRect

  단위 좌표 공간에서 사용되어야하는 레이어의 컨텐츠 부분을 정의하는 사각형. 애니메이션 가능합니다.

* _var_ contentsCenter: CGRect 레이어 컨텐츠의 크기가 조절되었을때 레이어 컨텐츠의 크기가 조정되는 방법을 정의하는 사각형. 애니메이션 가능합니다.
* _func_ display\(\)

  이 레이어의 컨텐츠를 다시 로드합니다.

* _func_ draw\(in: CGContext\)

  지정된 그래픽 컨텍스트를 사용하여 레이어의 컨텐츠를 그립니다.

### 레이어 모양 수정 <a id="modifying-the-layers-appearance"></a>

* _var_ contentsGravity: CALayerContentsGravity

  레이어 컨텐츠가 bound\(경계\) 내에서 배치되거나 스케일되는 방법을 지정하는 상수

* Contents Gravity Values Contents Gravity 상수는 레이어의 bound가 컨텐츠 객체의 bound보다 클 때 컨텐츠 객체의 위치를 지정합니다. [contentsGravity](../../etc/not-found.md) 프로퍼티에서 사용됩니다.
* _var_ opacity: Float

  수신자의 불투명도. 애니메이션 가능합니다.

* _var_ isHidden: Bool

  레이어 표시 여부를 나타내는 Boolean 값. 애니메이션 가능합니다.

* _var_ masksToBounds: Bool

  레이어의 bound를 벗어나는 하위 레이어 부분을 잘라내고 표시할 것인지를 나타내는 Boolean 값. 애니메이션 가능합니다.

* _var_ mask: CALayer? 알파 채널이 레이어 컨텐츠를 마스크하는데 사용되는 선택적 레이어.
* _var_ isDoubleSided: Bool

  A Boolean indicating whether the layer displays its content when facing away from the viewer. Animatable.

* _var_ cornerRadius: CGFloat 둥근 모서리의 레이어를 그릴때 배경에 적용될 반지름. 애니메이션 가능합니다.
* _var_ maskedCorners: CACornerMask
* _struct_ CACornerMask
* _var_ borderWidth: CGFloat

  레이어 테두리의 너비. 애니메이션 가능합니다.

* _var_ borderColor: CGColor? 레이어 테두리의 색상. 애니메이션 가능합니다.
* _var_ backgroundColor: CGColor? 수신자의 배경색. 애니메이션 가능합니다.
* _var_ shadowOpacity: Float 레이어 그림자의 투명도. 애니메이션 가능합니다.
* _var_ shadowRadius: CGFloat 레이어의 그림자를 렌더링하는 데 사용되는 흐림 반경\(point 단위\)입니다. 애니메이션 가능합니다.
* _var_ shadowOffset: CGSize 레이어 그림자의 오프셋\(point 단위\). 애니메이션 가능합니다.
* _var_ shadowColor: CGColor?

  레이어 그림자의 색상. 애니메이션 가능합니다.

* _var_ shadowPath: CGPath? 레이어 그림자의 모양. 애니메이션 가능합니다.
* _var_ style: \[AnyHashable : Any\]? 레이어에 의해 명시적으로 정의되지 않은 프로퍼티 값을 저장하는 데 사용되는 선택적 딕셔너리.
* _var_ allowsEdgeAntialiasing: Bool

  레이어가 가장자리 안티앨리어싱을 허용할 것인지를 나타내는 Boolean 값

* _var_ allowsGroupOpacity: Bool

  레이어를 부모로부터 분리된 그룹으로 합성할 수 있는지를 나타내는 Boolean 값

### 레이어 필터 <a id="layer-filters"></a>

* _var_ filters: \[Any\]?

  레이어와 하위 레이어에 적용되는 CoreImage 필터 배열. 애니메이션 가능합니다.

* _var_ compositingFilter: Any?

  레이어와 그 뒤의 컨텐츠를 구성하는데 사용되는 CoreImage 필터. 애니메이션 가능합니다.

* _var_ backgroundFilters: \[Any\]? 레이어 바로 뒤에 있는 컨텐츠에 적용할 CoreImage 필터 배열. 애니메이션 가능합니다.
* _var_ minificationFilter: CALayerContentsFilter

  컨텐츠의 크기를 줄이는데 사용되는 필터.

* _var_ minificationFilterBias: Float 최소화 필터에서 디테일 수준을 결정하는 데 사용되는 치우침 계수.
* _var_ magnificationFilter: CALayerContentsFilter 컨텐츠의 크기를 늘리는데 사용되는 필터.

### 레이어 렌더링 동작 설정 <a id="configuring-the-layers-rendering-behavior"></a>

* _var_ isOpaque: Bool

  레이어에 완전한 불투명 객체가 포함되어있는지를 알리는 Boolean 값.

* _var_ edgeAntialiasingMask: CAEdgeAntialiasingMask 수신자의 가장자리가 래스터되는 방법을 정의하는 비트마스크입니다.
* _func_ contentsAreFlipped\(\) -&gt; Bool

  렌더링 시 레이어 컨텐츠가 암시적으로 플립되는지를 나타내는 Boolean값을 반환합니다.

* _var_ isGeometryFlipped: Bool 레이어와 하위 레이어의 지오메트리가 수직으로 플립되는지를 나타내는 Boolean 값
* _var_ drawsAsynchronously: Bool 그리기 명령이 백그라운드 스레드에서 처리되고 지연되는 방식이 비동기식인지를 나타내는 Boolean 값
* _var_ shouldRasterize: Bool 레이어가 합성되기 전에 비트맵으로 렌더링되는지를 나타내는 Boolean 값. 애니메이션 가능합니다.
* _var_ rasterizationScale: CGFloat

  레이어의 좌표 공간을 기준으로 컨텐츠를 래스터화할 기준 크기. 애니메이션 가능합니다.

* _var_ contentsFormat: CALayerContentsFormat 레이어 컨텐츠의 원하는 저장 형식에 대한 힌트.
* _func_ render\(in: CGContext\) 레이어와 해당 하위 레이어를 지정된 컨텍스트로 렌더링합니다.

### 레이어 지오메트리 수정 <a id="modifying-the-layer-geometry"></a>

* _var_ frame: CGRect

  레이어의 프레임 사각형

* _var_ bounds: CGRect

  레이어의 bound 사각형. 애니메이션 가능합니다.

* _var_ position: CGPoint

  상위 레이어의 좌표공간상에서 이 레이어가 차지하고 있는 위치. 애니메이션 가능합니다.

* _var_ zPosition: CGFloat 레이어의 z축상 위치. 애니메이션 가능합니다.
* _var_ anchorPointZ: CGFloat z축을 따르는 레이어 위치의 고정점. 애니메이션 가능합니다.
* _var_ anchorPoint: CGPoint

  레이어 bound 사각형의 기준점을 정의합니다. 애니메이션 가능합니다.

* _var_ contentsScale: CGFloat

  레이어에 적용되는 스케일 인자

### 레이어 변형관리 <a id="managing-the-layers-transform"></a>

* _var_ transform: CATransform3D

  레이어 컨텐츠에 적용될 변. 애니메이션 가능합니다.

* _var_ sublayerTransform: CATransform3D

  렌더링 시 하위 레이어에 적용할 변환을 지정합니다. 애니메이션 가능합니다.

* _func_ affineTransform\(\) -&gt; CGAffineTransform 레이어 변환의 affine 버전을 반환합니다.
* _func_ setAffineTransform\(CGAffineTransform\) 레이어의 변환을 지정된 affine 변환으로 설정합니다.

### 레이어 계층관리 <a id="managing-the-layer-hierarchy"></a>

* _var_ sublayers: \[CALayer\]?

  레이어의 하위 레이어를 포함하는 배열

* _var_ superlayer: CALayer? 레이어의 상위 레이어
* _func_ addSublayer\(CALayer\) 하위 레이어 리스트에 새로운 레이어를 추가합니다.
* _func_ removeFromSuperlayer\(\) 상위 레이어로부터 이 레이어를 분리합니다.
* _func_ insertSublayer\(CALayer, at: UInt32\) 지정된 레이어를 하위 레이어 리스트중 `at:` 인덱스에 삽입합니다.
* _func_ insertSublayer\(CALayer, below: CALayer?\) 지정된 레이어를 이미 수신자에 속해있는 다른 `below:` 서브레이어 아래에 삽입합니다.
* _func_ insertSublayer\(CALayer, above: CALayer?\) 지정된 레이어를 이미 수신자에 속해있는 다른 `above:` 서브레이어 위에 삽입합니다.
* _func_ replaceSublayer\(CALayer, with: CALayer\) 지정된 레이어로 다른 `with:` 레이어 객체를 대체합니다.

### 레이어 디스플레이 업데이트 <a id="updating-layer-display"></a>

* _var_ layoutManager: CALayoutManager?

  하위 레이어의 배치를 담당하는 객체

* _func_ setNeedsDisplay\(\)

  레이어를 업데이트되어야 할 것으로 표시합니다.

* _func_ setNeedsDisplay\(CGRect\)

  지정된 사각형 영역을 업데이트되어야 할 것으로 표시합니다.

* _var_ needsDisplayOnBoundsChange: Bool bound 사각형이 변경될 때 레이어 컨텐츠를 업데이트해야 할지 나타내는 Boolean 값
* _func_ displayIfNeeded\(\) 레이어가 업데이트가 필요한 것으로 표시된 경우 업데이트 프로세스를 시작합니다.
* _func_ needsDisplay\(\) -&gt; Bool 레이어가 업데이트가 필요한 것으로 표시되었는지 나타내는 Boolean 값을 반환합니다.
* _class func_ needsDisplay\(forKey: String\) -&gt; Bool `forKey:` 의 변경사항이 레이어의 재디스플레이를 요구하는지 나타내는 Boolean 값을 반환합니다.

### 레이어 애니메이션 <a id="layer-animations"></a>

* _func_ add\(CAAnimation, forKey: String?\)

  지정된 애니메이션 객체를 레이어의 렌더 트리에 추가합니다.

* _func_ animation\(forKey: String\) -&gt; CAAnimation? `forKey:` 식별자의 애니메이션 객체를 반환합니다.
* _func_ removeAllAnimations\(\)

  이 레이어에 연결된 모든 애니메이션을 제거합니다.

* _func_ removeAnimation\(forKey: String\)

  `forKey:` 로 식별된 애니메이션 객체를 제거합니다.

* _func_ animationKeys\(\) -&gt; \[String\]?

  레이어에 현재 연결된 애니메이션을 식별하는 문자열 배열을 반환합니다.

### 레이어 리사이징과 레이아웃 관리 <a id="managing-layer-resizing-and-layout"></a>

* _var_ layoutManager: CALayoutManager?

  하위 레이아웃의 배치를 담당하는 객체

* _func_ setNeedsLayout\(\)

  레이어의 레이아웃을 무효화하고 업데이트가 필요한 것으로 표시합니다.

* _func_ layoutSublayers\(\) 레이어에게 레이아웃을 업데이트하도록 지시합니다.
* _func_ layoutIfNeeded\(\) 필요한 경우 수신자의 레이아웃을 다시 계산합니다.
* _func_ needsLayout\(\) -&gt; Bool 레이어가 레이아웃 업데이트가 필요한 것으로 표시되었는지를 나타내는 Boolean 값을 반환합니다.
* _var_ autoresizingMask: CAAutoresizingMask 슈퍼레이어 bound가 변경될 때 레이어의 크기가 어떻게 조정되어야 할지 정의하는 비트마스크입니다.
* _func_ resize\(withOldSuperlayerSize: CGSize\)

  수신자에게 슈퍼 레이어의 크기가 변경되었음을 알립니다.

* _func_ resizeSublayers\(withOldSize: CGSize\)

  수신자의 서브레이어에 수신자 크기가 변경되었음을 알립니다.

* _func_ preferredFrameSize\(\) -&gt; CGSize 슈퍼 레이어 좌표 공간상에서의 레이어의 기본 크기를 반환합니다.

### 레이어 제약조건 관리 <a id="managing-layer-constraints"></a>

* _var_ constraints: \[CAConstraint\]?

  현재 레이어의 하위 레이어를 배치하는데 사용되는 제약조건

* _func_ addConstraint\(CAConstraint\)

  지정된 제약조건을 레이어에 추가합니다.

### 레이어 액션 가져오기 <a id="getting-the-layers-actions"></a>

* _func_ action\(forKey: String\) -&gt; CAAction?

  `forKey:` 에 할당된 action 객체를 반환합니다.

* _var_ actions: \[String : CAAction\]?

  레이어 action을 포함한 딕셔너리.

* _class func_ defaultAction\(forKey: String\) -&gt; CAAction?

  현재 클래스의 기본 action을 반환합니다.

### 좌표와 시공간 매핑 <a id="mapping-between-coordinate-and-time-spaces"></a>

* _func_ convert\(CGPoint, from: CALayer?\) -&gt; CGPoint

  `from:` 레이어의 좌표계에서 수신자의 좌표계로 CGPoint를 변환합니다.

* _func_ convert\(CGPoint, to: CALayer?\) -&gt; CGPoint 수신자의 좌표계에서 `to:` 레이어의 좌표계로 CGPoint를 변환합니다.
* _func_ convert\(CGRect, from: CALayer?\) -&gt; CGRect `from:` 레이어의 좌표계에서 수신자의 좌표계로 CGRect를 변환합니다.
* _func_ convert\(CGRect, to: CALayer?\) -&gt; CGRect 수신자의 좌표계에서 `to:` 레이어의 좌표계로 CGRect를 변환합니다
* _func_ convertTime\(CFTimeInterval, from: CALayer?\) -&gt; CFTimeInterval `from:` 레이어의 시공간에서 수신자의 시공간으로 시간 간격을 변환합니다.
* _func_ convertTime\(CFTimeInterval, to: CALayer?\) -&gt; CFTimeInterval 수신자의 시공간에서 `to:` 레이어의 시공간으로 시간 간격을 변환합니다.

### Hit Testing

* _func_ hitTest\(CGPoint\) -&gt; CALayer?

  지정된 포인트를 갖는 \(수신자 자신을 포함한\) 레이어 계층구조에서 수신자의 가장 먼 자손 객체를 반환합니다.

* _func_ contains\(CGPoint\) -&gt; Bool

  수신자가 지정된 포인트를 포함하는지 나타내는 Boolean 값을 반환합니다.

### 스크롤링 <a id="scrolling"></a>

* _var_ visibleRect: CGRect

  자체 좌표 공간상 레이어의 가시적 영역.

* _func_ scroll\(CGPoint\)

  레이어의 가장 가까운 상위 스크롤 레이어에서 스크롤을 시작하여 지정된 점이 스크롤 레이어의 원점에 오도록 합니다.

* _func_ scrollRectToVisible\(CGRect\)

  지정된 사각형이 보일때까지 레이어의의 가장 가까운 조상 스크롤 레이어에서 스크롤을 시작합니다.

### 레이어 식별 <a id="identifying-the-layer"></a>

* _var_ name: String?

  수신자의 이름

### Key-Value Coding Extensions

* _func_ shouldArchiveValue\(forKey: String\) -&gt; Bool `forKey:` 의 값이 아카이브되어야 할지를 나타내는 Boolean값을 반환합니다.
* _class func_ defaultValue\(forKey: String\) -&gt; Any? `forKey:` 와 연결된 기본값을 지정합니다.

### 상수 <a id="constants"></a>

* _struct_ CAAutoresizingMask

  이 상수들은 [autoresizingMask](../../etc/not-found.md) 프로퍼티로 사용됩니다.

* Action Identifiers

  이 상수들은 미리 정의된 action 식별자로서 [action\(forKey:\)](../../etc/not-found.md), [add\(\_:forKey:\)](../../etc/not-found.md), [defaultAction\(forKey:\)](../../etc/not-found.md), [removeAnimation\(forKey:\)](../../etc/not-found.md), [레이어 필터](calayer.md#layer-filters)와 [CAAction](caaction.md) 프로토콜 메서드인 [run\(forKey:object:arguments:\)](../../etc/not-found.md)에서 사용됩니다.

* _struct_ CAEdgeAntialiasingMask

  이 마스크는 [edgeAntialiasingMask](../../etc/not-found.md) 프로퍼티로 사용됩니다.

* Identity Transform

  Core Animationd에서 사용되는 identity transform matrix를 정의합니다.

* Scaling Filters

  이 상수들은 [magnificationFilter](../../etc/not-found.md)와 [minificationFilter](../../etc/not-found.md)에서 스케일링 필터로 사용됩니다.

* _struct_ CATransform3D

  Core Animation 전체에서 사용되는 표준 변환 매트릭스입니다.

## 관련 문서 <a id="relationships"></a>

### 상속받은 대상 <a id="inherits-from"></a>

* NSObject

### 준수하는 프로토콜 <a id="conforms-to"></a>

* CAMediaTiming
* CVarArg
* Equatable
* Hashable
* NSSecureCoding

## 같이 보기 <a id="see-also"></a>

### 레이어 기초 <a id="layer-basics"></a>

* _protocol_ CALayerDelegate 레이어 관련 이벤트에 응답하기 위해 앱이 구현할 수 있는 메서드
* _class_ CAConstraint 두 레이어 사이의 단일 레이아웃 제약 조건
* _protocol_ CALayoutManager 객체가 레이어와 그 하위 레이어의 레이아웃을 관리할 수 있게 해주는 메서드
* _class_ CAConstraintLayoutManager

  제약 기반 레이아웃 관리자를 제공하는 객체

* _protocol_ [CAAction](caaction.md)

  객체가 CALayer 변경에 의해 트리거 된 액션에 응답할 수 있게 해주는 인터페이스

