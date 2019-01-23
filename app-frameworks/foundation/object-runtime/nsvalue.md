---
description: C나 Objective-C의 단일 데이터 항목에 대한 간단한 컨테이너
---

# NSValue

> 원문 출처  
> [https://developer.apple.com/documentation/foundation/nsvalue](https://developer.apple.com/documentation/foundation/nsvalue)

## 개요

NSValue 객체는 int, float 및 char와 같은 스칼라 타입뿐만 아니라 포인터, 구조체 및 객체 ID 참조를 포함할 수 있습니다. 콜렉션\(예: [NSArray](../../../etc/not-found.md) 및 [NSSet](../../../etc/not-found.md)\), [Key-Value Coding](../../../etc/not-found.md) 및 Objective-C 객체가 필요한 기타 API에 이러한 데이터 타입을 사용해야 할 경우 이 클래스를 사용하세요. NSValue 객체는 변경 불가능\(immutable\)합니다.

## 서브클래싱 시에

추상 NSValue 클래스는 주어진 상황에 적합한 값 객체를 만들고 반환하는 private, concrete 클래스로 구성된 클래스 클러스터의 공용 인터페이스입니다. NSValue를 서브 클래스할 수는 있지만 그렇게 하려면 \(하위 클래스에 상속되지 않는\)값에 대한 저장 기능을 제공하고 두 가지 기본 메서드를 구현해야합니다.

### 오버라이드 할 메서드

NSValue의 서브클래스는 기본 인스턴스 메서드인 getValue\(\_:\)와 objCType을 오버라이드해야 합니다. 이 메서드들은 값을 제공하는 스토리지에서 동작되어야 합니다.

You might want to implement an initializer for your subclass that is suited to the storage you provide. The NSValue class does not have a designated initializer, so your initializer need only invoke the init\(\) method of super. The NSValue class adopts the NSCopying and NSSecureCoding protocols; if you want instances of your own custom subclass created from copying or coding, override the methods in these protocols.

You may also wish to implement the hash method to make your subclass work well in collections.

