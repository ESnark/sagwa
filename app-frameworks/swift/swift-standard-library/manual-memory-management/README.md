# 메모리 직접 관리

> \`원문출처  
> [https://developer.apple.com/documentation/swift/swift\_standard\_library/manual\_memory\_management](https://developer.apple.com/documentation/swift/swift_standard_library/manual_memory_management)

## 주제

### 첫 스텝

* [포인터 파라미터를 사용하는 함수 호출](calling-functions-with-pointer-parameters.md) 포인터를 파라미터로 받는 함수를 호출할때 암시적인 포인터 캐스팅이나 브릿징을 사용하세요.

### 타입이 결정된 포인터

타입이 결정된 포인터와 버퍼를 사용해서 메모리의 특정 타입 인스턴스에 접근하세요

* struct [UnsafePointer](unsafepointer.md) 특정 타입의 데이터에 접근하는 포인터
* struct UnsafeMutablePointer 특정 타입의 데이터에 접근하고 조작하는 포인터
* struct UnsafeBufferPointer A nonowning collection interface to a buffer of elements stored contiguously in memory.
* struct UnsafeMutableBufferPointer A nonowning collection interface to a buffer of mutable elements stored contiguously in memory.

### 원시 포인터

raw 바이트를 저장하고 로딩하기 위해서 원시 포인터와 버퍼를 사용하세요.

* struct UnsafeRawPointer 타입이 정해지지 않은 데이터에 접근하는 원시 포인터
* struct UnsafeMutableRawPointer 타입이 정해지지 않은 데이터에 접근하고 조작하는 원시 포인터
* struct UnsafeRawBufferPointer A nonowning collection interface to the bytes in a region of memory.
* [struct UnsafeMutableRawBufferPointer](unsafemutablerawbufferpointer.md) A mutable nonowning collection interface to the bytes in a region of memory.

### 메모리 접근

* func withUnsafePointer&lt;T, Result&gt;\(to: T, \(UnsafePointer&lt;T&gt;\) -&gt; Result\) -&gt; Result 주어진 인자에 대한 포인터를 사용하여 클로저를 실행합니다. `Beta`
* func withUnsafePointer\(to: inout T, \(UnsafePointer\) -&gt; Result\) -&gt; Result

  주어진 인자에 대한 포인터를 사용하여 클로저를 실행합니다.

* func withUnsafeMutablePointer\(to: inout T, \(UnsafeMutablePointer\) -&gt; Result\) -&gt; Result

  주어진 인자의 Mutable 포인터를 사용하여 클로저를 실행합니다.

* func withUnsafeBytes\(of: T, \(UnsafeRawBufferPointer\) -&gt; Result\) -&gt; Result

  주어진 인자의 raw byte를 커버하는 Buffer 포인터를 사용하여 클로저를 실행합니다. `Beta`

* func withUnsafeBytes\(of: inout T, \(UnsafeRawBufferPointer\) -&gt; Result\) -&gt; Result

  주어진 인자의 raw byte를 커버하는 Buffer 포인터를 사용하여 클로저를 실행합니다.

* func withUnsafeMutableBytes\(of: inout T, \(UnsafeMutableRawBufferPointer\) -&gt; Result\) -&gt; Result

  주어진 인자의 raw byte를 커버하는 Mutable buffer 포인터를 사용하여 클로저를 실행합니다.

* func swap\(inout T, inout T\)

  두 인자의 값을 바꿉니다.

### 메모리 레이아웃

* enum MemoryLayout The memory layout of a type, describing its size, stride, and alignment.

### 참조 카운팅

* struct Unmanaged 관리되지 않는 객체 참조를 전파하기 위한 타입
* func withExtendedLifetime\(T, \(T\) -&gt; Result\) -&gt; Result

  클로저가 반환되기 전에 주어진 인스턴스가 destroy 되지 않도록 보장하면서 클로저를 평가합니다.

* func withExtendedLifetime\(T, \(\) -&gt; Result\) -&gt; Result 클로저가 반환되기 전에 주어진 인스턴스가 destroy 되지 않도록 보장하면서 클로저를 평가합니다.

## 같이 보기

### 프로그래밍 작업

* 입출력 값을 콘솔에 출력하고, 텍스트 스트림에 값을 쓰거나 읽고, 커맨드 라인 인자를 사용하세요.
* 디버깅과 반영 런타임 점검을 통해 코드를 강화하고 값의 런타임 표현을 검토합니다.
* Key-Path 표현법 Key-Path를 사용해서 프로퍼티에 동적으로 접근하세요.
* Type Casting and Existential Types 타입간에 캐스팅을 하거나 모든 타입의 값을 나타냅니다.
* C 상호운용성 import된 C 타입이나 C 가변함수를 사용하세요.
* 연산자 선언 접두어, 접미어 및 중위어 연산자로 작업하세요.

