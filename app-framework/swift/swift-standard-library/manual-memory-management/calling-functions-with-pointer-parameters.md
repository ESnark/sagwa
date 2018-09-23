---
description: 포인터를 파라미터로 받는 함수를 호출할때 암시적인 포인터 캐스팅이나 브릿징을 사용하세요.
---

# 포인터 파라미터를 사용하는 함수 호출

> 원문출처  
> [https://developer.apple.com/documentation/swift/swift\_standard\_library/manual\_memory\_management/calling\_functions\_with\_pointer\_parameters](https://developer.apple.com/documentation/swift/swift_standard_library/manual_memory_management/calling_functions_with_pointer_parameters)

## 개요

포인터를 파라미터로 받는 함수를 호출할때 암묵적 캐스팅을 사용하여 호환되는 포인터 타입이나 암묵적 브릿징을 넘겨서 포인터를 변수나 배열 요소로 전달할 수 있습니다.

## 파라미터에 상수 포인터를 전달하기

UnsafePointer&lt;Type&gt; 인자를 받는 함수를 호출할 때에는 다음과 같은 인자를 넘길 수 있습니다.

* 암묵적으로 UnsafePointer&lt;Type&gt;으로 캐스팅되는 타입들.

  UnsafePointer&lt;Type&gt;, UnsafeMutablePointer&lt;Type&gt;, AutoreleasingUnsafeMutablePointer&lt;Type&gt;

* \(Type이 Int8이나 UInt8인 경우\) String. 이 경우 문자열은 `\0`으로 끝나는 UTF8 형식의 버퍼로 자동변환되고 버퍼를 가리키는 포인터가 함수에 전달됩니다.
* inout 표현식이 사용된 mutable 변수, 프로퍼티 또는 인덱스로 참조 가능한 타입. 이 경우 왼쪽 식별자 주소\(address of th left-hand side identifier\)를 가리키는 포인터가 전달됩니다.
* Type 배열 이 경우 배열의 시작부분을 가리키는 포인터가 전달됩니다.

아래 예시는 상수 포인터를 받는 함수가 호출되는 여러가지 방법을 보여줍니다:

```swift
func takesAPointer(_ p: UnsafePointer<Float>) {
    // ...
}

var x: Float = 0.0
takesAPointer(&x)
takesAPointer([1.0, 2.0, 3.0])
```

UnsafeRawPointer 인자를 받는 함수를 호출할때는 어떤 Type이라도 받는 UnsafePointer&lt;Type&gt;을 넘길 수 있습니다.

다음 예시는 raw 상수 포인터를 받는 함수가 호출되는 여러가지 방법을 보여줍니다:

```swift
func takesARawPointer(_ p: UnsafeRawPointer?)  {
    // ...
}

var x: Float = 0.0, y: Int = 0
takesARawPointer(&x)
takesARawPointer(&y)
takesARawPointer([1.0, 2.0, 3.0] as [Float])
let intArray = [1, 2, 3]
takesARawPointer(intArray)
takesARawPointer("How are you today?")
```

## 파라미터에 변수 포인터를 전달하기

UnsafeMutablePointer를 받는 함수를 호출할 때에는 다음과 같은 인자를 넘길 수 있습니다.

* UnsafeMutablePointer&lt;Type&gt;
* inout 표현식이 사용된 mutable 변수, 프로퍼티 또는 인덱스로 참조 가능한 타입 이 경우 mutable 값의 주소를 가리키는 포인터가 전달됩니다.
* inout 표현식이 사용된 mutable 변수, 프로퍼티 또는 인덱스로 참조가능한 타입값으로 구성된 배열 이 경우 배열의 시작부분을 가리키는 포인터가 전달되며 호출이 끝나기 전까지 참조는 유효하게 유지됩니다.

다음 예시는 변수 포인터를 받는 함수가 호출되는 여러가지 방법을 보여줍니다.

```swift
func takesAMutablePointer(_ p: UnsafeMutablePointer<Float>) {
    // ...
}

var x: Float = 0.0
var a: [Float] = [1.0, 2.0, 3.0]
takesAMutablePointer(&x)
takesAMutablePointer(&a)
```

UnsafeMutableRawPointer 인자를 받는 함수를 호출할때는 어떤 Type이라도 받는 UnsafeMutablePointer&lt;Type&gt;을 넘길 수 있습니다.

다음 예시는 raw 변수 포인터를 받는 함수가 호출되는 여러가지 방법을 보여줍니다.

```swift
func takesAMutableRawPointer(_ p: UnsafeMutableRawPointer?)  {
    // ...
}

var x: Float = 0.0, y: Int = 0
var a: [Float] = [1.0, 2.0, 3.0], b: [Int] = [1, 2, 3]
takesAMutableRawPointer(&x)
takesAMutableRawPointer(&y)
takesAMutableRawPointer(&a)
takesAMutableRawPointer(&b)
```

## 파라미터에 Autoreleasing 포인터를 전달하기

AutoreleasingUnsafeMutablePinter&lt;Type&gt;을 받는 함수를 호출할때 다음과 같은 인자를 넘길 수 있습니다.

* AutoreleasingUnsafeMutablePointer&lt;Type&gt;
* inout 표현식이 사용된 mutable 변수, 프로퍼티 또는 인덱스로 참조가능한 타입값으로 구성된 배열 이 피연산자의 값은 비트연산을 통해 임시 nonowning buffer로 복사됩니다. 복사된 버퍼의 주소는 피호출자에게 전달되며 리턴되는 시점에 피연산자에게 load, retain, 재할당됩니다.

다른 포인터 타입과는 다르게 배열을 암묵적으로 브릿지된 파라미터로 사용할 수 없습니다.

## 파라미터에 함수 포인터를 전달하기

C 함수 포인터를 인자로 받는 함수를 호출할때에는 top-level 스위프트 함수, 클로저 리터럴, @convention\(c\) 속성으로 선언된 클로저 또는 nil을 전달할 수 있습니다. 또한 클로저의 인자 목록이나 본문에서 제네릭 타입 파라미터가 참조되지 않는 한 제네릭 타입이나 제네릭 메서드의 클로저 프로퍼티를 전달할 수 있습니다.

예를 들어 Core Foundation의 CFArrayCreateMutable\(\_:\_:\_:\) 함수가 함수 포인터 콜백으로 초기화된 CFArrayCallBacks 구조체를 받는다고 가정해봅시다.

```swift
func customCopyDescription(_ p: UnsafeRawPointer?) -> Unmanaged<CFString>? {
    // return an Unmanaged<CFString>? value
}
 
var callbacks = CFArrayCallBacks(
    version: 0,
    retain: nil,
    release: nil,
    copyDescription: customCopyDescription,
    equal: { (p1, p2) -> DarwinBoolean in
        // return Bool value
    }
)
var mutableArray = CFArrayCreateMutable(nil, 0, &callbacks)
```

이 예시에서 CFArrayCallBacks의 이니셜라이저는 retain과 release 파라미터의 인자로 nil을 사용했고 customCopyDescription\(\_:\) 함수를 copyDescription 파라미터\(원문에서는customCopyDescription parameter라고 쓰여있었음\)의 인자로 사용했습니다. 그리고 클로저 리터럴을 equal 파라미터의 인자로 사용했습니다.

{% hint style="info" %}
알림

C 함수 호출 컨벤션을 사용하는 Swift 함수만이 함수 포인터 인자로 사용될 수 있습니다. C 함수 포인터와 마찬가지로 @convention\(c\) 속성으로 쓰인 Swift 함수타입은 그것을 감싸고 있는 스코프의 컨텍스트를 캡쳐하지 않습니다.
{% endhint %}

