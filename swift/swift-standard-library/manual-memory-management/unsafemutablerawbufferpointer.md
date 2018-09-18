---
description: 특정 타입의 데이터에 접근하고 조작하는 포인터
---

# UnsafeMutableRawBufferPointer

> 원문출처  
> [https://developer.apple.com/documentation/swift/unsafemutablerawbufferpointer](https://developer.apple.com/documentation/swift/unsafemutablerawbufferpointer)

## 개요

저수준 작업에서의 UnsafeMutableRawBufferPointer는 고유성 검사와 릴리즈 모드에서의 경계 검사를 해제할 수 있습니다. \(디버그 모드에서는 경계검사가 무조건 동작합니다.\)

UnsafeMutableRawBufferPointer 인스턴스는 메모리 영역 내의 raw 바이트를 살필수 있는 하나의 관점을 제공합니다. 메모리상의 각 바이트는 실제로 메모리상에 잡혀있는 값의 타입과는 별개로 UInt8 값으로 보여지며 raw 버퍼를 통해 메모리로부터 읽고 쓰는 작업은 타입이 정해지지 않은 작업\(Untyped operations\)을 통해 이루어집니다. 이 컬렉션의 바이트에 접근한다고 해서 메모리가 UInt8로 바인딩되지는 않습니다.

또한 UnsafeMutableRawBufferPointer 인스턴스는 컬렉션 인터페이스 외에도 디버그모드에서의 경계 검사를 포함, UnsafeMutableRawPointer가 제공하는 다음 메서드들을 지원합니다.

* load\(fromByteOffset:as:\)
* storeBytes\(of:toByteOffset:as:\)
* copyMemory\(from:\)



