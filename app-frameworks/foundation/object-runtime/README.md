---
description: '기본 Objective-C 기능, 코코아 디자인 패턴, 스위프트 통합에 대한 저수준 지원을 받을 수 있습니다.'
---

# Object Runtime

> 원문 출처  
> [https://developer.apple.com/documentation/foundation/object\_runtime](https://developer.apple.com/documentation/foundation/object_runtime)

## 주제

### Object 기초

* _class_ NSObject 거의 모든 Objective-C 클래스들의 루트 클래스로써, 서브클래스들은 런타임 시스템의 기초 인터페이스와 Objective-C 객체로서 행동하기 위한 기능들을 NSObject로부터 상속받습니다.
* _protocol_ NSObjectProtocol 모든 Objective-C 객체의 기본을 이루는 메서드 그룹
* NSKeyValueCoding 이름이나 키로 객체의 속성에 간접적으로 액세스할 수 있는 메커니즘

### Copying

* _protocol_ NSCopying 자기 자신의 함수적인 복사본을 제공하기 위해서 객체들이 채택하는 프로토콜
* _protocol_ NSMutableCopying 자기 자신의 함수적인 복사본을 제공하기 위해서 mutable 객체들이 채택하는 프로토콜

### Value 래퍼와 변형

* _class_ NSNumber

  원시 스칼라 숫자값에 대한 객체 래퍼

* _class_ [NSValue](nsvalue.md) C나 Objective-C의 단일 데이터 항목에 대한 간단한 컨테이너
* _class_ ValueTransformer 하나의 표현형에서 다른 표현형으로 값을 변환하는데 사용되는 추상 클래스

### 스위프트 지원

* _protocol_ ReferenceConvertible 파운데이션 참조타입으로 뒷받침되는 타입에 적용되는 데코레이션
* Classes Bridged to Swift Standard Library Value Types

  Use bridged reference types when you need reference semantics or Foundation-specific behavior.

### Remote Object

* _class_ NSProxy 다른 객체나 아직 존재하지 않는 객체의 stand-in 역할을 하는 객체의 API를 정의하는 추상 수퍼클래스

### 메모리 관리

* 메모리 관리 함수들 저수준 메모리 작업을 수행합니다.

### Objective-C 런타임

* Objective-C 런타임 유틸리티

  Objective-C 런타임과 상호작용하세요.

### 버전과 API 가용성

* 파운데이션 프레임워크 버전 번호

  현재 실행 중인 Foundation 버전을 알려진 OS 버전과 비교하기 위한 상수에 대해서 알아보세요.

### 레거시

* Distributed Objects Support 로컬 및 원격 시스템에서 서로 다른 프로세스의 객체간 통신을 가능하게 합니다.
* Objective-C 가비지 콜렉션

  레거시 가비지 콜렉션 시스템과의 인터페이스

## 같이 보기

### 저레벨 유틸리티 <a id="low_level_utilities"></a>

* XPC

  보안 인터프로세스 통신을 관리합니다.

* 프로세스와 스레드

  호스트 운영 체제 및 기타 프로세스와의 상호 작용을 관리하고 저수준의 동시성 기능을 구현합니다.

* 스트림, 소켓과 포트

  저수준 Unix 기능을 사용하여 파일, 프로세스 및 네트워크 간의 입력 및 출력을 관리합니다.

