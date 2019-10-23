---
description: C나 Objective-C의 단일 데이터 항목에 대한 단순한 컨테이너
---

# NSValue

> 원문 출처  
> [https://developer.apple.com/documentation/foundation/nsvalue](https://developer.apple.com/documentation/foundation/nsvalue)

## 개요

NSValue 객체는 int, float 및 char와 같은 스칼라 타입뿐만 아니라 포인터, 구조체 및 객체 ID 참조를 포함할 수 있습니다. 콜렉션\(예: [NSArray](../../../etc/not-found.md) 및 [NSSet](../../../etc/not-found.md)\), [Key-Value Coding](../../../etc/not-found.md) 및 Objective-C 객체가 필요한 기타 API에 이러한 데이터 타입을 사용해야 할 경우 이 클래스를 사용하세요. NSValue 객체는 변경 불가능\(immutable\)합니다.

## Subclassing Notes

추상 NSValue 클래스는 주어진 상황에 적합한 값 객체를 만들고 반환하는 private, concrete 클래스로 구성된 클래스 클러스터의 공용 인터페이스입니다. NSValue를 서브 클래스할 수는 있지만 그렇게 하려면 \(하위 클래스에 상속되지 않는\)값에 대한 저장 기능을 제공하고 두 가지 기본 메서드를 구현해야합니다.

### 오버라이드 할 메서드

NSValue의 서브클래스는 기본 인스턴스 메서드인 getValue\(\_:\)와 objCType을 오버라이드해야 합니다. 이 메서드들은 값을 제공하는 스토리지에서 동작되어야 합니다.

제공할 스토리지에 알맞는 서브클래스 이니셜라이저를 구현하고 싶을 수도 있습니다. NSValue 클래스는 지정된 이니셜라이저가 없기 때문에 구현할 이니셜라이저가 호출해야 할 것은 슈퍼 클래스의 init\(\) 메서드 뿐입니다. NSValue 클래스는 NSCopying과 NSSecuerCoding 프로토콜을 준수합니다. copying이나 coding을 통해서 커스텀 서브클래스의 인스턴스를 생성하고자 한다면 이들 프로토콜의 메서드를 오버라이드하세요.

서브클래스가 collection에서 잘 동작하도록 하려면 hash 메소드를 구현하는 것이 좋습니다.

### 서브클래싱의 대안

커스텀 데이터 타입이나 구조체를 감싸는 목적으로만 NSValue를 사용하는 것이라면 NSValue의 서브클래스를 꼭 생성할 필요는 없습니다. 대신에 기존의 NSValue 메서드를 사용해서 커스텀 타입 데이터를 저장하고 불러올 수 있습니다. 예를 들어 아래의 코드는 Polyhedron 커스텀 구조체를 정의하고, NSValue convenience 메소드를 만들어서 저장 및 불러오기를 수행하고 있습니다:

```objectivec
typedef struct {
    int numFaces;
    float radius;
} Polyhedron;
 
@interface NSValue (Polyhedron)
+ (instancetype)valuewithPolyhedron:(Polyhedron)value;
@property (readonly) Polyhedron polyhedronValue;
@end
 
@implementation NSValue (Polyhedron)
+ (instancetype)valuewithPolyhedron:(Polyhedron)value
{
    return [self valueWithBytes:&value objCType:@encode(Polyhedron)];
}
- (Polyhedron) polyhedronValue
{
    Polyhedron value;
    [self getValue:&value];
    return value;
}
@end
```

## 주제

### Working with Raw Values

* init\(bytes: UnsafeRawPointer, objCType: UnsafePointer\) 주어진 값이 지정된 Objective-C 타입으로 변환된 값을 포함하는 객체를 초기화 합니다.
* init\(UnsafeRawPointer, withObjCType: UnsafePointer\) 주어진 값이 지정된 Objective-C 타입으로 변환된 값 객체\(value object\)를 생성합니다.
* func getValue\(UnsafeMutableRawPointer\)

  ~~Copies the value into the specified buffer.~~ `Deprecated`

* var objCType: UnsafePointer 값 객체에 포함된 데이터의 Objective-C 타입을 보유하는 C 문자열

### Working with Pointer and Object Values

* init\(pointer: UnsafeRawPointer?\) 포인터를 포함하는 값 객체를 생성합니다.
* init\(nonretainedObject: Any?\) non-retained 객체를 포함하는 값 객체를 생성합니다.
* var pointerValue: UnsafeMutableRawPointer? 타입지정되지 않은 포인터를 값으로 반환합니다.
* var nonretainedObjectValue: Any?

  The value as a non-retained pointer to an object.

### Working with Range Values

* init\(range: NSRange\) Foundation range 구조체를 포함하는 새 값 객체를 생성합니다.
* var rangeValue: NSRange Foundation range 구조체 표현값

### Working with Foundation Geometry Values

* init\(point: NSPoint\) Foundation point 구조체를 포함하는 값 객체를 생성합니다. Creates a new value object containing the specified Foundation point structure.
* init\(size: NSSize\) Foundation size

  구조체를 포함하는 값 객체를 생성합니다.

* init\(rect: NSRect\) Foundation rectangle

  구조체를 포함하는 값 객체를 생성합니다.

* var pointValue: NSPoint

  Foundation point 구조체 표현 The Foundation point structure representation of the value.

* var sizeValue: NSSize

  Foundation size 구조체 표현

* var rectValue: NSRect

  Foundation rectangle 구조체 표현

### Working with CoreGraphics Geometry Values

* init\(cgPoint: CGPoint\)

  CoreGrapics point 구조체를 포함하는 값 객체를 생성합니다.

* init\(cgVector: CGVector\)

  CoreGrapics vector 구조체를 포함하는 값 객체를 생성합니다.

* init\(cgSize: CGSize\)

  CoreGrapics size 구조체를 포함하는 값 객체를 생성합니다.

* init\(cgRect: CGRect\)

  CoreGrapics rectangle 구조체를 포함하는 값 객체를 생성합니다.

* init\(cgAffineTransform: CGAffineTransform\)

  CoreGrapics affine transform 구조체를 포함하는 값 객체를 생성합니다.

* var cgPointValue: CGPoint

  Returns the CoreGraphics point structure representation of the value.

* var cgVectorValue: CGVector

  Returns the CoreGraphics vector structure representation of the value.

* var cgSizeValue: CGSize

  Returns the CoreGraphics size structure representation of the value.

* var cgRectValue: CGRect

  Returns the CoreGraphics rectangle structure representation of the value.

* var cgAffineTransformValue: CGAffineTransform

  Returns the CoreGraphics affine transform representation of the value.



### Working with UIKit Geometry Values

* init\(uiEdgeInsets: UIEdgeInsets\)

  UIkit edge inset 구조체를 포함하는 값 객체를 생성합니다.

* init\(uiOffset: UIOffset\)

  UIkit offset 구조체를 포함하는 값 객체를 생성합니다.

* var uiEdgeInsetsValue: UIEdgeInsets

  Returns the UIKit edge insets structure representation of the value.

* var uiOffsetValue: UIOffset

  Returns the UIKit offset structure representation of the value.

### Working with CoreAnimation Transform Values

* init\(caTransform3D: CATransform3D\)

  CoreAnimation transform 구조체를 포함하는 값 객체를 생성합니다.

* var caTransform3DValue: CATransform3D

  The CoreAnimation transform structure representation of the value.

### Working with Media Time Values

* init\(time: CMTime\)

  CoreMedia time 구조체를 포함하는 값 객체를 생성합니다.

* init\(timeRange: CMTimeRange\)

  CoreMedia time range 구조체를 포함하는 값 객체를 생성합니다.

* init\(timeMapping: CMTimeMapping\)

  CoreMedia time mapping 구조체를 포함하는 값 객체를 생성합니다.

* var timeValue: CMTime

  The CoreMedia time structure representation of the value.

* var timeRangeValue: CMTimeRange

  The CoreMedia time range structure representation of the value.

* var timeMappingValue: CMTimeMapping

  The CoreMedia time mapping structure representation of the value.

### Working with Geographic Coordinate Values

* init\(mkCoordinate: CLLocationCoordinate2D\)

  CoreLocation geographic coordinate 구조체를 포함하는 값 객체를 생성합니다.

* init\(mkCoordinateSpan: MKCoordinateSpan\)

  MapKit coordinate span 구조체를 포함하는 값 객체를 생성합니다.

* var mkCoordinateValue: CLLocationCoordinate2D

  The CoreLocation geographic coordinate structure representation of the value.

* var mkCoordinateSpanValue: MKCoordinateSpan

  The MapKit coordinate span structure representation of the value.

### Working with SceneKit Vector and Matrix Values

* init\(scnVector3: SCNVector3\)

  Three-element SceneKit vector를 포함하는 값 객체를 생성합니다.

* init\(scnVector4: SCNVector4\)

  Four-element SceneKit vector를 포함하는 값 객체를 생성합니다.

* init\(scnMatrix4: SCNMatrix4\)

  SceneKit 4 x 4 matrix를 포함하는 값 객체를 생성합니다.

* var scnVector3Value: SCNVector3

  The three-element Scene Kit vector representation of the value.

* var scnVector4Value: SCNVector4

  The four-element Scene Kit vector representation of the value.

* var scnMatrix4Value: SCNMatrix4

  The Scene Kit 4 x 4 matrix representation of the value.

### Comparing Value Objects

* func isEqual\(to: NSValue\) -&gt; Bool

  값 객체와 다른 값 객체가 동일한지를 알려주는 Boolean 값을 반환합니다.

### Initializers

* init?\(coder: NSCoder\)
* init\(directionalEdgeInsets: NSDirectionalEdgeInsets\)
* init\(edgeInsets: NSEdgeInsets\)

### Instance Properties

* var directionalEdgeInsetsValue: NSDirectionalEdgeInsets
* var edgeInsetsValue: NSEdgeInsets

### Instance Methods

* func getValue\(UnsafeMutableRawPointer, size: Int\)
* func value\(of: StoredType.Type\) -&gt; StoredType?

## 관련 문서

### 상속받은 대상

* NSObject

### 준수하는 프로토콜

* CVarArg
* Equatable
* Hashable
* NSCopying
* NSSecureCoding

## 같이 보기

### Value 래퍼와 변형

* _class_ NSNumber

  원시 스칼라 숫자값에 대한 객체 래퍼

* _class_ ValueTransformer 하나의 표현형에서 다른 표현형으로 값을 변환하는데 사용되는 추상 클래스



