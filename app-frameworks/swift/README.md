# Swift

> 원문출처  
> [https://developer.apple.com/documentation/swift](https://developer.apple.com/documentation/swift)

## 개요

스위프트는 타입추론, 옵셔널, 클로저와 같은 현대적 프로그래밍 언어의 기능을 갖추고 있어 구문을 간결하고도 표현력있게 만듭니다. 스위프트는 여러분의 코드가 빠르고 효율적으로 구동될 것을 보장하며 메모리 안전성과 기본 에러 처리를 통해 안전한 언어로 설계되었습니다. Swift Playgrounds 앱과 Xcode Playgrounds 그리고 REPL에서 스위프트 코드를 작성하는 일은 대화형의 재미있는 경험을 제공할 것입니다.

```swift
var interestingNumbers = ["primes": [2, 3, 5, 7, 11, 13, 17],
    "triangular": [1, 3, 6, 10, 15, 21, 28],
    "hexagonal": [1, 6, 15, 28, 45, 66, 91]
]

for key in interestingNumbers.keys {
    interestingNumbers[key]?.sort(by: >)
}

print(interestingNumbers["primes"]!)
// Prints "[17, 13, 11, 7, 5, 3, 2]"
```

## 스위프트 배우기

만약 스위프트가 처음이라면, [The Swift Programming Language](https://docs.swift.org/swift-book/)의 quick tour, 언어 가이드, 전체 레퍼런스 메뉴얼을 읽어보세요. 그리고 프로그래밍이 처음이라면 아이패드에서 [Swift Playgrounds](https://www.apple.com/swift/playgrounds/) 앱을 확인하세요.

스위프트는 오픈소스로 개발되고 있습니다. 스위프트 프로젝트와 커뮤니티에 대해 더 알고 싶다면 [Swift.org](https://swift.org/)를 방문하세요.

## 주제

### 표준 라이브러리 <a id="standard-library"></a>

* struct Int 부호가 있는 정수형 타입
* struct Double 배정밀도 부동소수점 타입
* struct String 문자의 컬렉션으로 이루어진 유니코드 문자열
* struct Array 순서가 있는 랜덤 액세스 컬렉션
* struct Dictionary key-value 쌍의 요소로 이루어진 컬렉션
* [스위프트 표준 라이브러리](swift-standard-library/) 복잡한 문제를 해결하고 높은 성능의 가독성이 좋은 코드를 작성하세요.

### 데이터 모델링 <a id="data-modeling"></a>

* 구조체와 클래스 중에서 선택하기 데이터를 저장하는 방법과 모델 동작을 결정하세요.
* 일반 프로토콜 채택하기 커스텀 타입이 스위프트 프로토콜을 준수하는지 확인함으로써 더 쉽게 사용할 수 있습니다.

### 데이터 흐름과 제어 흐름 <a id="data-flow-and-control-flow"></a>

* 애플리케이션 상태 유지하기
* 클로저를 사용할때 타이밍 문제를 막는 법

### 언어 상호운용성 <a id="language-interoperability"></a>

* Objective-C와 C 코드 커스텀하기
* Objective-C를 스위프트로 마이그레이션 하는 법
* 코코아 디자인 패턴
* 스위프트에서 동적타입 메서드와 객체 처리하기
* 스위프트에서 Objective-C 런타임 기능 사용하기
* Import된 C와 Objective-C API

### Reference

* Type Aliases

