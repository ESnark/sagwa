# UnsafePointer

> 원문출처  
> [https://developer.apple.com/documentation/swift/unsafepointer](https://developer.apple.com/documentation/swift/unsafepointer)

## 개요

UnsafePointer 타입 인스턴스는 메모리의 특정 타입 데이터에 접근하는데 사용됩니다. 포인터가 접근할 수 있는 데이터의 타입은 해당 포인터의 _Pointee_ 타입입니다. UnsafePointer는 자동 메모리 관리나 정렬을 지원하지 않고 개발자는 UnsafePointer를 통해 작업하는 메모리의 라이프 사이클을 관리함으로써 메모리 누수와 정의되지 않은 동작을 방지해야 합니다. 직접 관리하는 메모리는 타입정의 형태가 될수도 있고 타입이 정해지지 않은 형태가 될 수도 있지만 UnsafePointer 타입은 특정 타입에 바인딩 된 메모리를 엑세스하고 관리하는데 사용됩니다.

## 포인터 메모리 상태의 이해

UnsafePointer 인스턴스에 의해 참조되는 메모리는 몇가지 상태 중 하나에 속하게 됩니다. 많은 종류의 포인터 연산들이 특정 상태의 메모리를 가리키는 포인터에만 적용이 가능합니다. 그러므로 작업중인 메모리들의 상태는 반드시 지속적으로 추적이 되어야 하며 다른 연산수행으로 인해 일어나는 상태변화를 이해해야 합니다. 메모리는 타입이 지정되지 않았으면서 초기화되지 않은 상태, 타입이 지정되었지만 초기화되지 않은 상태, 타입이 지정되고 특정 값으로 초기화 된 상태가 가능하며, 마지막으로 메모리 할당이 해제된 후에도 남아서 기존 메모리를 참조하는 포인터가 남아있을 수도 있습니다.

### 초기화되지 않은 메모리

타입 지정된 포인터에 의해서 방금 할당된 메모리나 초기화 해제\(할당 해제\)된 메모리는 초기화되지 않은\(uninitialized\) 상태입니다. 초기화 되지 않은 메모리는 값을 읽기 위해 접근하기 전에 초기화되어야 합니다.

### 초기화된 메모리

초기화된 메모리는 포인터의 _pointee_ 프로퍼티나 첨자\(인덱스\) 표기법을 통해 접근할 수 있습니다. 다음 예시를 살펴보면 `ptr`는 값이 23으로 초기화된 메모리를 가리키는 포인터라는 것을 알수 있습니다.

```swift
let ptr: UnsafePointer<Int> = ...
// ptr.pointee == 23
// ptr[0] == 23
```

## 포인터의 메모리를 다른 타입으로 접근하기

UnsafePointer 인스턴스로 메모리에 접근할때 pointee 프로퍼티는 반드시 바인딩된 타입과 일치하도록 되어 있습니다. 만약 해당 메모리에 바인딩되지 않은 다른 타입으로 접근해야 할 필요가 있다면 스위프트 포인터 타입이 제공하는 type-safe한 방법을 사용할 수 있습니다. 이 방법을 통해 일시적 또는 영구적으로 메모리의 바인딩 타입을 바꾸거나 raw 메모리를 특정 타입 인스턴스로 로드할 수도 있습니다.

uint8Pointer라는 이름으로 여덟 바이트짜리 메모리에 할당된 UnSafePointer&lt;UInt8&gt; 인스턴스는 다음 예시와 같이 사용될 수 있습니다.

```swift
let uint8Pointer: UnsafePointer<UInt8> = fetchEightBytes()
```

일시적으로 메모리에 다른 타입으로 접근해야 한다면 withMemoryRebound\(to:capacity:\) 메서드를 사용하세요. 예를 들어 포인터의 pointee와 레이아웃이 호환되는 다른 타입의 포인터를 필요로 하는 API를 호출할때 해당 메서드를 사용할 수 있습니다. 다음 코드는 import된 strlen C 함수를 사용하기 위해 일시적으로 uint8Pointer의 참조타입을 UInt8에서 Int8로 재 바인딩합니다.

```swift
// Imported from C
func strlen(_ __s: UnsafePointer<Int8>!) -> UInt

let length = uint8Pointer.withMemoryRebound(to: Int8.self, capacity: 8) {
    return strlen($0)
}
// length == 7
```

메모리를 영구적으로 다른 타입에 재바인딩 시킬때에는 raw 포인터를 얻어낸 다음 bindMemory\(to:capacity:\) 메서드를 사용합니다. 다음 예시는 uint8Pointer를 UInt64 타입 인스턴스로 바인딩시킵니다.

```swift
let uint64Pointer = UnsafeRawPointer(uint8Pointer)
                                .bindMemory(to: UInt64.self, capacity: 1)
```

uint8Pointer에서 참조하는 메모리를 UInt64에 재바인딩시키고 해당 포인터가 참조하는 메모리에 UInt8 인스턴스로 액세스하면 undefined로 나옵니다.

```swift
var fullInteger = uint64Pointer.pointee          // OK
var firstByte = uint8Pointer.pointee             // undefined
```

untyped 메모리 접근을 거쳐서 재바인딩시키는 방법 대신에 같은 메모리를 다른 타입으로 접근하는 방법도 있습니다. 바인드된 타입과 접근하고자 하는 다른 타입이 둘다 trivial하다면 UnsafeRawPointer로 변환한 다음 raw pointer의 load\(fromByteOffset:as:\) 메서드로 읽어낼 수 있습니다.

> 역자 주
>
> trival한 타입이란 저장 공간이 연속적이며 static default initializer만 지원하는 타입을 뜻합니다.  
> 본문에서는 trival한 타입으로써 UInt64와 UInt8 타입을 예시로 하고 있습니다.
>
> 참조 : [http://www.cplusplus.com/reference/type\_traits/is\_trivial/](http://www.cplusplus.com/reference/type_traits/is_trivial/)

```swift
let rawPointer = UnsafeRawPointer(uint64Pointer)
fullInteger = rawPointer.load(as: UInt64.self)   // OK
firstByte = rawPointer.load(as: UInt8.self)      // OK
```

## 타입 지정 포인터의 연산

타입지정된 포인터의 포인터 연산은 pointee 타입의 stride\(해당 타입의 최대 byte 사이즈\)로 계산됩니다. UnsafePointer 인스턴스에 값을 더하거나 뺐을 경우의 결과는 동일한 타입의 새 포인터이며 해당 Pointee 타입의 인스턴스 수만큼 오프셋됩니다.

```swift
// [10, 20, 30, 40]으로 초기화된 메모리를 가리키는 'intPointer'
let intPointer: UnsafePointer<Int> = ...

// 메모리 상의 첫번째 값을 로드
let x = intPointer.pointee
// x == 10

// 메모리 상의 세번째 값을 로드
let offsetPointer = intPointer + 2
let y = offsetPointer.pointee
// y == 30
```

인덱스 표기법으로도 메모리 특정 오프셋의 값에 접근할 수 있습니다.

```swift
let z = intPointer[2]
// z == 30
```

## 암묵적 캐스팅과 브릿징

UnsafePointer 파라미터를 사용하는 함수나 메서드를 호출할 때에는 지정된 포인터 타입의 인스턴스나 그에 호환되는 포인터 타입 인스턴스를 전달할 수도 있고 또는 호환되는 포인터를 넘기기 위해서 스위프트의 암묵적 브릿징\(implicit bridging\)을 사용할 수도 있습니다.

예를 들어 다음 코드 샘플에서 첫번째 파라미터로 UnsafePointer를 받도록 되어있는 printInt\(atAddress:\)함수를 살펴 보겠습니다.

```swift
func printInt(atAddress p: UnsafePointer<Int>) {
    print(p.pointee)
}
```

일반적인 스위프트 문법에 따라서 UnsafePointer 인스턴스를 받는 printInt\(atAddress:\)를 호출할 수 있습니다.  
다음 예시는 Int값을 가리키는 intPointer를 printInt\(atAddress:\)로 넘깁니다.

> 역자 주
>
> 원문에서는 마지막 printInt\(atAddress:\)라는 부분이 print\(address:\)로 되어있지만 예시 어디에도 그런 함수가 정의되있지 않은 바, 오타라고 생각하여 임의로 수정합니다.

```swift
printInt(atAddress: intPointer)
// Prints "42"
```

그러나 타입지정 변수 포인터\(mutable typed pointer\)가 파라미터로 전달될 때 같은 pointee 타입의 타입지정 상수 포인터\(immutable typed pointer\)로 캐스팅되기 때문에 print\(atAddress:\) 함수에 UnsafeMutablePointer 인스턴스를 전달하는 것 또한 가능합니다.

```swift
let mutableIntPointer = UnsafeMutablePointer(mutating: intPointer)
printInt(atAddress: mutableIntPointer)
// Prints "42"
```

또 다른 방법으로는 인스턴스나 배열 요소에 스위프트의 암묵적 브릿징을 사용하여 포인터로 전달하는 방법이 있습니다. 다음 예시에서는 _value_ 변수에 inout 구문을 사용하여 포인터값을 넘기고 있습니다.

```swift
var value: Int = 23
printInt(atAddress: &value)
// Prints "23"
```

배열을 인자로 넘기는 경우 해당 배열의 인자를 가리키는 상수 포인터가 암묵적으로 생성됩니다. 다음 예시에서는 printInt\(atAddress:\)를 호출하면서 암묵적 브릿징을 사용하여 _numbers_의 요소를 가리키는 포인터를 전달하고 있습니다.

```swift
let numbers = [5, 10, 15, 20]
printInt(atAddress: numbers)
// Prints "5"
```

inout 구문을 사용해서 배열 요소의 변수 포인터를 넘기는 것도 가능합니다. printInt\(atAddress:\) 함수가 상수 포인터를 받기 때문에 문법적으로는 유효합니다만 반드시 필요한 것은 아닙니다.

```swift
var mutableNumbers = numbers
printInt(atAddress: &mutableNumbers)
```

어떤 방법으로 printInt\(atAddress:\)를 호출하든지간에 스위프트의 타입 안전성은 함수에서 요구하는 타입의 포인터만 전달될수 있게 보장합니다. \(이번 예시에서는 Int 타입 포인터\)

{% hint style="warning" %}
중요

인스턴스나 배열의 인자의 암묵적 브릿징을 통해서 생성된 포인터는 호출된 함수의 실행 중에만 유효합니다. 포인터를 함수 실행 구간 밖으로 이스케이프시키는 것은 정의되지 않은\(Undefined\) 동작입니다. 특히 UnsafePointer의 이니셜라이저를 호출할때 암묵적 브릿징을 사용하지 마세요.

```swift
var number = 5
let numberPointer = UnsafePointer<Int>(&number)
// 'numberPointer'에 접근하는 것은 정의되지 않은 동작입니다.
```
{% endhint %}

## 주제

### 이니셜라이저

* init\(OpaquePointer\)

  주어진 Opaque 포인터로부터 새로운 타입지정 포인터를 생성합니다.

* init?\(UnsafeMutablePointer?\)

  주어진 mutable 포인터와 동일한 메모리를 가리키는 immutable 타입지정 포인터를 생성합니다.

* init\(UnsafeMutablePointer\)

  주어진 mutable 포인터와 동일한 메모리를 가리키는 immutable 타입지정 포인터를 생성합니다.

* init\(UnsafePointer\) 주어진 타입지정 포인터로부터 새로운 포인터를 생성합니다.
* init?\(UnsafePointer?\) 주어진 타입지정 포인터로부터 새로운 포인터를 생성합니다.
* init?\(OpaquePointer?\) 주어진 Opaque 포인터로부터 새로운 타입지정 포인터를 생성합니다.
* init?\(bitPattern: UInt\) bit pattern 표기법으로 주어진 주소로부터 새로운 타입지정 포인터를 생성합니다.
* init?\(bitPattern: Int\) bit pattern 표기법으로 주어진 주소로부터 새로운 타입지정 포인터를 생성합니다.

### 인스턴스 프로퍼티

* _var_ customMirror: Mirror
* ~~_var_ customPlaygroundQuickLook: PlaygroundQuickLook~~ `Deprecated`
* _var_ debugDescription: String

  디버깅에 적합한 포인터의 텍스트 표현

* _var_ pointee: Pointee

  이 포인터가 참조하는 인스턴스에 접근합니다.

### 인스턴스 메서드

* _func_ advanced\(by: Int\) -&gt; UnsafePointer

  포인터로부터 인스턴스의 `by:` 갯수만큼의 오프셋을 반환합니다.

* _func_ deallocate\(\)

  포인터에 할당되었던 메모리 블럭을 해제합니다.

* _func_ distance\(to: UnsafePointer\) -&gt; Int

  이 포인터와 주어진 포인터 사이의 거리를 반환합니다. 포인터의 Pointee 타입 인스턴스를 단위로 하여 계산됩니다.

* _func_ hash\(into: inout Hasher\)

  이 값의 필수 구성요소를 `into:` 해셔에 제공하여 해시합니다. `Beta`

* _func_ predecessor\(\) -&gt; UnsafePointer

  이전의 연속 인스턴스 포인터를 반환합니다.  
  Returns a pointer to the previous consecutive instance.

* _func_ successor\(\) -&gt; UnsafePointer  
  다음의 연속 인스턴스 포인터를 반환합니다.

  Returns a pointer to the next consecutive instance.

* _func_ withMemoryRebound\(to: T.Type, capacity: Int, \(UnsafePointer\) -&gt; Result\) -&gt; Result `capacity:` 숫자만큼의 인스턴스를 `to:` 타입으로 일시적으로 바인딩하여 클로저를 실행합니다.

### Subscripts

* subscript\(Int\) -&gt; Pointee

  이 포인터로부터 지정된 오프셋에 해당하는 pointee에 접근합니다.

### 연산자 함수

* _static func_ != \(UnsafePointer, UnsafePointer\) -&gt; Bool

  두 값이 같지 않음을 가리키는 Boolean 값을 반환합니다.

* _static func_ + \(Int, UnsafePointer\) -&gt; UnsafePointer `Beta`
* _static func_ + \(UnsafePointer, Int\) -&gt; UnsafePointer `Beta`
* _static func_ += \(inout UnsafePointer, Int\) `Beta`
* _static func_ - \(UnsafePointer, UnsafePointer\) -&gt; Int `Beta`
* _static func_ - \(UnsafePointer, Int\) -&gt; UnsafePointer `Beta`
* _static func_ -= \(inout UnsafePointer, Int\) `Beta`
* _static func_ ... \(UnsafePointer\) -&gt; PartialRangeFrom&gt;

  Returns a partial range extending upward from a lower bound. `Beta`

* _static func_ ... \(UnsafePointer\) -&gt; PartialRangeThrough&gt;

  Returns a partial range up to, and including, its upper bound. `Beta`

* _static func_ ... \(UnsafePointer, UnsafePointer\) -&gt; ClosedRange&gt;

  Returns a closed range that contains both of its bounds. `Beta`

* _static func_ ... \(UnsafePointer, UnsafePointer\) -&gt; ClosedRange&gt;

  Returns a countable closed range that contains both of its bounds. `Beta`

* _static func_ ..&lt; \(UnsafePointer\) -&gt; PartialRangeUpTo&gt;

  Returns a partial range up to, but not including, its upper bound.

* _static func_ ..&lt; \(UnsafePointer, UnsafePointer\) -&gt; Range&gt;

  Returns a half-open range that contains its lower bound but not its upper bound. `Beta`

* _static func_ &lt; \(UnsafePointer, UnsafePointer\) -&gt; Bool

  Returns a Boolean value indicating whether the first pointer references an earlier memory location than the second pointer. `Beta`

* _static func_ &lt; \(UnsafePointer, UnsafePointer\) -&gt; Bool

  Returns a Boolean value indicating whether the value of the first argument is less than that of the second argument. `Beta`

* _static func_ &lt;= \(UnsafePointer, UnsafePointer\) -&gt; Bool

  Returns a Boolean value indicating whether the value of the first argument is less than or equal to that of the second argument.

* _static func_ == \(UnsafePointer, UnsafePointer\) -&gt; Bool

  Returns a Boolean value indicating whether two pointers are equal. `Beta`

* _static func_ == \(UnsafePointer, UnsafePointer\) -&gt; Bool

  Returns a Boolean value indicating whether two values are equal. `Beta`

* _static func_ &gt; \(UnsafePointer, UnsafePointer\) -&gt; Bool

  Returns a Boolean value indicating whether the value of the first argument is greater than that of the second argument.

* _static func_ &gt;= \(UnsafePointer, UnsafePointer\) -&gt; Bool

  Returns a Boolean value indicating whether the value of the first argument is greater than or equal to that of the second argument.

