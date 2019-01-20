# 스위프트 표준 라이브러리

> 원문 출처  
> [https://developer.apple.com/documentation/swift/swift\_standard\_library](https://developer.apple.com/documentation/swift/swift_standard_library)

## 개요

Swift 표준 라이브러리는 Swift 프로그램을 작성하기 위한 기능성의 기초 레이어를 정의합니다.

* [Int](../../../etc/not-found.md), [Double](../../../etc/not-found.md) 그리고 [String](../../../etc/not-found.md)과 같은 기초 데이터 타입
* [Array](../../../etc/not-found.md), [Dictionary](../../../etc/not-found.md) 그리고 [Set](../../../etc/not-found.md)과 같은 공용 데이터 구조체
* [print\(\_:separator:terminator:\)](../../../etc/not-found.md)와 abs\(\_:\) 같은 전역 함수
* [Collection](../../../etc/not-found.md)과 [Equatable](../../../etc/not-found.md) 같은 공통 추상화를 설명하는 프로토콜
* Protocols, such as [CustomDebugStringConvertible](../../../etc/not-found.md) and [CustomReflectable](../../../etc/not-found.md), that you use to customize operations that are available to all types.
* Protocols, such as [OptionSet](../../../etc/not-found.md), that you use to provide implementations that would otherwise require boilerplate code.

{% hint style="info" %}
표준 라이브러리 탐색

Swift 표준 라이브러리 타입을 실험하고 시각화와 실용적인 예제를 사용해서 고수준의 개념을 배우세요. Swift 표준 라이브러리로 프로토콜과 제네릭을 사용해서 강력한 제약조건을 표현하는 방법을 공부하세요. 아래에서 playground 파일을 다운받아 시작해볼 수 있습니다.

[Swift Standard Library.playground](https://developer.apple.com/sample-code/swift/downloads/standard-library.zip)
{% endhint %}

## 주제

### 값과 콜렉션

* 숫자와 기본 값 숫자, Boolean값, 다른 기본 타입을 사용해서 데이터를 모델링합니다.
* 문자열과 텍스트   유니코드와 안전하게 호환되는 문자열을 사용한 텍스트로 작업하세요.
* 콜렉션 배열, 딕셔너리, set과 다른 데이터 구조체를 사용해서 데이터를 저장하고 조직화하세요.

### 타입을 위한 도구

* 기본 동작 Use your custom types in operations that depend on testing for equality or order and as members of sets and dictionaries.
* 인코딩, 디코딩, 시리얼화 암시적인 인코딩이나 커스텀된 인코딩으로 타입 인스턴스를 시리얼화하거나 되돌리세요.
* 리터럴 방식으로 초기화 다른 종류의 리터럴을 사용해서 타입값이 표현될수 있도록 만드세요.

### 프로그래밍 작업

* 입출력 값을 콘솔에 출력하고, 텍스트 스트림에 값을 쓰거나 읽고, 커맨드 라인 인자를 사용하세요.
* 디버깅과 반영 런타임 점검을 통해 코드를 강화하고 값의 런타임 표현을 검토합니다.
* Key-Path 표현법 Key-Path를 사용해서 프로퍼티에 동적으로 접근하세요.
* [메모리 직접 관리](manual-memory-management/) 메모리를 직접 할당하고 관리하세요.
* Type Casting and Existential Types 타입간에 캐스팅을 하거나 모든 타입의 값을 나타냅니다.
* C 상호운용성 import된 C 타입이나 C 가변함수를 사용하세요.
* 연산자 선언 접두어, 접미어 및 중위어 연산자로 작업하세요.

## 같이 보기

### 표준 라이브러리

* struct Int 부호가 있는 정수형 타입
* struct Double 배정밀도 부동소수점 타입
* struct String 문자의 컬렉션으로 이루어진 유니코드 문자열
* struct Array 순서가 있는 랜덤 액세스 컬렉션
* struct Dictionary key-value 쌍의 요소로 이루어진 컬렉션

