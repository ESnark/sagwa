---
description: Core Graphics 및 연관 프레임워크에서 사용되는 기본 부동소수점 스칼라 타입
---

# CGFloat

> 원문 출처  
> [https://developer.apple.com/documentation/coregraphics/cgfloat](https://developer.apple.com/documentation/coregraphics/cgfloat)

## Declaration

{% tabs %}
{% tab title="Swift" %}
```swift
@frozen struct CGFloat
```
{% endtab %}
{% endtabs %}

## Summary

> **SDKs**
>
> * iOS 7.0+
> * macOS 10.9+
> * Mac Catalyst 13.0+
> * tvOS 9.0+
> * watchOS 2.0+
> * Xcode 6.0.1+
>
> **Framework**
>
> * Core Graphics

## Overview

이 타입의 크기와 정밀도는 CPU 아키텍처에 따라서 다릅니다. 64-bit CPU 용도로 빌드하면 CGFloat은 [Double](../../etc/not-found.md)에 해당하는 IEEE 배정밀도 부동소수점 타입의 64비트가 됩니다. 만약 32-bit CPU 용으로 빌드한다면 CGFloat은 32비트로써 IEEE 단정밀도 부동소수점 타입으로써 [Float](../../etc/not-found.md)에 해당하는 타입이 됩니다.

## 주제

### Type Aliases

* _typealias_ CGFloat.FloatLiteralType
* _typealias_ CGFloat.IntegerLiteralType
* _typealias_ CGFloat.Magnitude
* _typealias_ CGFloat.RawExponent
* _typealias_ CGFloat.Stride
* _typealias_ CGFloat.Exponent 쓰여진 지수를 표현할 수 있는 정수 타입
* _typealias_ CGFloat.NativeType CGFloat을 저장하는데 사용되는 네이티브 타입으로써 32비트 아키텍쳐에서는 [Float](../../etc/not-found.md), 64비트 아키텍처에서는 [Double](../../etc/not-found.md)입니다.
* _typealias_ CGFloat.RawSignificand

  An unsigned integer type that can represent the significand of any value.

### Initializers

* init\(\) 0으로 초기화된 인스턴스를 생성합니다.
* init\(Float\) Float을 표현 가능한 범위 내에서 가장 가까운 값으로 반올림합니다.
* init\(Double\) Double을 표현 가능한 범위 내에서 가장 가까운 값으로 반올림합니다.
* init\(CGFloat\) 주어진 값으로 초기화된 인스턴스를 생성합니다.
* init\(Float80\) Float80을 표현가능한 범위 내에서 가장 가까운 값으로 반올림합니다.
* init&lt;Source&gt;\(Source\) 주어진 값으로 새로운 인스턴스를 생성하되, 가능한 표현범위 내에서 가장 가까운 값으로 반올림합니다.
* init&lt;Source&gt;\(Source\) 주어진 값으로 새 값을 생성하되, 가능한 표현범위 내에서 가장 가까운 값으로 반올림합니다.
* ~~init\(NSNumber\)~~ `Deprecated`
* init\(bitPattern: UInt\)
* init?&lt;T&gt;\(exactly: T\)
* init?&lt;Source&gt;\(exactly: Source\) 정확히 표현될 수 있다면, 주어진 값으로부터 새 인스턴스를 생성합니다.
* init?&lt;Source&gt;\(exactly: Source\) 주어진 정수가 정확히 표현될 수 있다면, 새 값을 생성합니다.
* init?\(exactly: NSNumber\)
* init\(floatLiteral: CGFloat.NativeType\) 주어진 값으로 초기화된 인스턴스를 생성합니다.
* init\(floatLiteral: CGFloat.NativeType\) 주어진 값으로 초기화된 인스턴스를 생성합니다.
* init\(from: Decoder\)
* init\(integerLiteral: Int\) 주어진 값으로 초기화된 인스턴스를 생성합니다.
* init\(nan: CGFloat.RawSignificand, signaling: Bool\)

  NaN with specified payload.

* init\(sign: FloatingPointSign, exponent: Int, significand: CGFloat\) 부호, 지수와 가수로 초기화합니다.
* init\(sign: FloatingPointSign, exponentBitPattern: UInt, significandBitPattern: UInt\) 부호, 지수와 가수 비트 패턴을 조합하여 부동 소수점 값을 만들어냅니다.
* init\(signOf: CGFloat, magnitudeOf: CGFloat\) 하나의 값에서 부호를 취하고, 다른 값에 적용시켜서 새로운 부동소수점 값을 생성합니다.
* init\(truncating: NSNumber\)

### 인스턴스 속성

* _var_ binade: CGFloat

  The least-magnitude member of the binade of self.

* _var_ bitPattern: UInt
* _var_ customMirror: Mirror

  CGFloat 인스턴스를 반영하는 Mirror.

* _var_ description: String

  self의 텍스트 표현

* _var_ exponent: Int self를 기수\(밑수\)가 r인 로그로 표현했을 때의 지수를 가리킵니다. \(r은 이진법 타입인 경우에는 2, 십진법 타입인 경우에는 10입니다.\) IEEE 754 logB 연산의 구현입니다.
* _var_ exponentBitPattern: UInt raw encoding으로 나타낸 부동 소수점 값의 지수부
* _var_ floatingPointClass: FloatingPointClassification
* _var_ hashValue: Int

  해시 값

* _var_ isCanonical: Bool

  self가 표준 형식이면 true를 반환합니다.

* _var_ isFinite: Bool self가 0이거나, 준정규 값이거나, 정규값이라면 \(infinity나 NaN이 아님\) true를 반환합니다. \(역자 주: 준정규 값, 정규값에 관한 [설명](https://ko.wikipedia.org/wiki/%EB%B9%84%EC%A0%95%EA%B7%9C_%EA%B0%92)\)
* _var_ isInfinite: Bool self가 infinity라면 true를 반환합니다.
* _var_ isNaN: Bool self가 NaN\(Not A Number\)라면 true를 반환합니다.
* _var_ isNormal: Bool self가 정규값이라면 \(0, 준정규 값, infinity, NaN이 아님\) true를 반환합니다.
* _var_ isSignalingNaN: Bool self가 signaling NaN인 경우에만 true를 반환합니다.
* _var_ isSubnormal: Bool self가 준 정규값이라면 true를 반환합니다.
* _var_ isZero: Bool self가 +0.0이나 -0.0이라면 true를 반환합니다.
* _var_ magnitude: CGFloat
* _var_ magnitudeSquared: Double
* _var_ native: CGFloat.NativeType

  The native value.

* _var_ native: CGFloat.NativeType

  The native value.

* _var_ nextDown: CGFloat 이 값보다 작은 범위 내에서 표현 가능한 가장 큰 값
* _var_ nextUp: CGFloat 이 값보다 큰 범위 내에서 표현 가능한 가장 작은 값
* _var_ sign: FloatingPointSign self의 sign bit가 \(1로\) 설정되어 있으면 음수, 그렇지 않으면 양수입니다. IEEE 754 signbit 동작의 구현입니다.
* _var_ significand: CGFloat 부동 소수점 숫자의 가수
* _var_ significandBitPattern: UInt raw encoding으로 표현된 부동 소수점 값의 가수부
* _var_ significandWidth: Int 가수를 표현하는데 요구되는 비트 갯수
* _var_ ulp: CGFloat self의 마지막 자리의 단위

### 타입 속성

* _static_ _var_ exponentBitCount: Int 지수를 표현하는데 사용되는 비트 갯수
* _static_ _var_ greatestFiniteMagnitude: CGFloat 가장 큰 유한수
* _static_ _var_ infinity: CGFloat

  양의 무한수

* _static_ _var_ leastNonzeroMagnitude: CGFloat 가장 작은 양수
* _static_ _var_ leastNormalMagnitude: CGFloat 가장 작은 양의 정규값
* _static_ _var_ nan: CGFloat

  A quiet NaN.

* _static_ _var_ pi: CGFloat

  상수 π \(3.14159...\)

* _static_ _var_ radix: Int 이 부동소수점 타입의 기수, 또는 지수의 밑수입니다.
* _static_ _var_ signalingNaN: CGFloat

  A signaling NaN \(not-a-number\).

* _static_ _var_ significandBitCount: Int 고정 길이 부동소수점 타입에서 이 속성은 가수부 비트의 갯수를 나타냅니다.
* _static_ _var_ ulpOfOne: CGFloat

  The unit in the last place of 1.0.

* _static_ _var_ zero: CGFloat

  0의 값

### 인스턴스 메소드

* _func_ addProduct\(CGFloat, CGFloat\)
* _func_ addingProduct\(CGFloat, CGFloat\) -&gt; CGFloat 중간 반올림없이 주어진 두 값을 곱하고, self에 더한 값을 반환합니다.
* _func_ advanced\(by: CGFloat\) -&gt; CGFloat

  Returns a Self x such that self.distance\(to: x\) approximates n.

* _func_ distance\(to: CGFloat\) -&gt; CGFloat

  Returns a stride x such that self.advanced\(by: x\) approximates other.

* _func_ encode\(to: Encoder\)
* _func_ formRemainder\(dividingBy: CGFloat\)
* _func_ formSquareRoot\(\)
* _func_ formTruncatingRemainder\(dividingBy: CGFloat\) 나머지 연산의 결과값으로 self를 대체합니다. C 표준 라이브러리 함수 fmod와 유사합니다.
* _func_ hash\(into: inout Hasher\)
* _func_ isEqual\(to: CGFloat\) -&gt; Bool

  IEEE 754 equality predicate.

* _func_ isLess\(than: CGFloat\) -&gt; Bool

  IEEE 754 less-than predicate.

* _func_ isLessThanOrEqualTo\(CGFloat\) -&gt; Bool

  IEEE 754 less-than-or-equal predicate.

* _func_ isTotallyOrdered\(belowOrEqualTo: CGFloat\) -&gt; Bool

  Returns a Boolean value indicating whether this instance should precede or tie positions with the given value in an ascending sort.

* _func_ negate\(\)

  Replace self with its additive inverse.

* _func_ remainder\(dividingBy: CGFloat\) -&gt; CGFloat

  Returns the remainder of this value divided by the given value.

* _func_ round\(\) "schoolbook rounding"을 사용하여 이 값을 정수값으로 반올림합니다.
* _func_ round\(FloatingPointRoundingRule\)
* _func_ rounded\(\) -&gt; CGFloat

  "schoolbook rounding"을 사용하여 self를 정수값으로 반올림해서 반환합니다.

* _func_ rounded\(FloatingPointRoundingRule\) -&gt; CGFloat 지정된 반올림 규칙을 사용하여 정수로 반올림된 self값을 반환합니다.
* _func_ scale\(by: Double\) func squareRoot\(\) -&gt; CGFloat 이 값의 제곱근을 표현 가능한 값으로 반올림하여 반환합니다.
* _func_ truncatingRemainder\(dividingBy: CGFloat\) -&gt; CGFloat 주어진 값으로 나머지 연산하여 나오는 나머지 값을 반환합니다.

### 타입 메소드

* _static_ _func_ maximum\(CGFloat, CGFloat\) -&gt; CGFloat

  주어진 두 개의 값 중 더 큰 값을 반환합니다.

* _static_ _func_ maximumMagnitude\(CGFloat, CGFloat\) -&gt; CGFloat \(절대값 기준으로\) 크기가 더 큰 값을 반환합니다.
* _static_ _func_ minimum\(CGFloat, CGFloat\) -&gt; CGFloat 주어진 두 개의 값 중 더 작은 값을 반환합니다.
* _static_ _func_ minimumMagnitude\(CGFloat, CGFloat\) -&gt; CGFloat \(절대값 기준으로\) 크기가 더 작은 값을 반환합니다.
* _static_ _func_ random\(in: ClosedRange\) -&gt; CGFloat 지정된 범위 내에서 랜덤한 값을 반환합니다.
* _static_ _func_ random\(in: Range\) -&gt; CGFloat 지정된 범위 내에서 랜덤한 값을 반환합니다.
* _static_ _func_ random\(in: ClosedRange, using: inout T\) -&gt; CGFloat `in` 범위 내에서 `using` 을 랜덤 제너레이터로 사용하여 무작위 값을 반환합니다.
* _static_ _func_ random\(in: Range, using: inout T\) -&gt; CGFloat `in` 범위 내에서 `using` 을 랜덤 제너레이터로 사용하요 무작위 값을 반환합니다.

### 연산자 함수

* _static_ _func_ != \(CGFloat, CGFloat\) -&gt; Bool 두 값이 다른지를 비교해서 다르면 true를 반환합니다.
* _static_ _func_ \*  __\(CGFloat, CGFloat\) -&gt; CGFloat
* _static_ _func_ \*= \(inout CGFloat, CGFloat\)
* _static_ _func_ + \(CGFloat\) -&gt; CGFloat

  Returns the given number unchanged.

* _static_ _func_ + \(CGFloat, CGFloat\) -&gt; CGFloat
* _static_ _func_ += \(inout CGFloat, CGFloat\)
* _static_ _func_ - \(CGFloat\) -&gt; CGFloat 지정된 값의 역수를 더합니다.
* _static_ _func_ - \(CGFloat, CGFloat\) -&gt; CGFloat
* _static_ _func_ -= \(inout CGFloat, CGFloat\)
* _static_ _func_ ... \(CGFloat\) -&gt; PartialRangeFrom 하한선을 기준으로 위로 확장되는 부분 구간을 반환합니다.
* _static_ _func_ ... \(CGFloat\) -&gt; PartialRangeThrough 상한선까지 포함되는 부분 구간을 반환합니다.
* _static_ _func_ ... \(CGFloat, CGFloat\) -&gt; ClosedRange 경계를 포함하는 닫힌 구간을 반환합니다.
* _static_ _func_ ..&lt; \(CGFloat\) -&gt; PartialRangeUpTo 상한을 포함하지 않는 부분 구간을 반환합니다.
* _static_ _func_ ..&lt; \(CGFloat, CGFloat\) -&gt; Range 하한선을 포함하고 상한선을 포함하지 않는 반 열린 구간을 반환합니다.
* _static_ _func_ / \(CGFloat, CGFloat\) -&gt; CGFloat
* _static_ _func_ /= \(inout CGFloat, CGFloat\)
* _static_ _func_ &lt; \(CGFloat, CGFloat\) -&gt; Bool 첫번째 인자가 두번째 인자보다 작은지를 나타내는 Boolean 값을 반환합니다.
* _static_ _func_ &lt; \(CGFloat, CGFloat\) -&gt; Bool

  첫번째 인자가 두번째 인자보다 작은지를 나타내는 Boolean 값을 반환합니다.

* _static_ _func_ &lt;= \(CGFloat, CGFloat\) -&gt; Bool 첫번째 인자가 두번째 인자보다 작거나 같은지를 나타내는 Boolean 값을 반환합니다.
* _static_ _func_ &lt;= \(CGFloat, CGFloat\) -&gt; Bool 첫번째 인자가 두번째 인자보다 작거나 같은지를 나타내는 Boolean 값을 반환합니다.
* _static_ _func_ == \(CGFloat, CGFloat\) -&gt; Bool 두 값이 같은지를 나타내는 Boolean 값을 반환합니다.
* _static_ _func_ == \(CGFloat, CGFloat\) -&gt; Bool 두 값이 같은지를 나타내는 Boolean 값을 반환합니다.
* _static_ _func_ &gt; \(CGFloat, CGFloat\) -&gt; Bool 첫번째 인자가 두번째 인자보다 더 큰지를 나타내는 Boolean 값을 반환합니다.
* _static_ _func_ &gt; \(CGFloat, CGFloat\) -&gt; Bool 첫번째 인자가 두번째 인자보다 더 큰지를 나타내는 Boolean 값을 반환합니다.
* _static_ _func_ &gt;= \(CGFloat, CGFloat\) -&gt; Bool 첫번째 인자가 두번째 인자보다 더 크거나 같은지를 나타내는 Boolean 값을 반환합니다.
* _static_ _func_ &gt;= \(CGFloat, CGFloat\) -&gt; Bool 첫번째 인자가 두번째 인자보다 더 크거나 같은지를 나타내는 Boolean 값을 반환합니다.

## 관련 문서

### 준수하는 프로토콜

* BinaryFloatingPoint
* CustomReflectable
* CustomStringConvertible
* Decodable
* Encodable
* Hashable
* SignedNumeric
* Strideable
* VectorArithmetic

## 같이 보기

### 기하 데이터 유형

* _struct_ CGPoint 2차원 좌표계상의 지점을 나타내는 구조체
* _struct_ CGSize 너비와 높이 값을 갖는 구조체
* _struct_ CGRect 사각형의 위치와 크기값을 갖는 구조체
* _struct_ CGVector 2차원 벡터값을 갖는 구조체
* _struct_ CGAffineTransform 2D 그래픽을 그릴때 사용되는 affine 변환 매트릭스

