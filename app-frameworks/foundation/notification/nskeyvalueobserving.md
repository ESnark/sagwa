# NSKeyValueObserving

> 원문 출처  
> [https://developer.apple.com/documentation/foundation/notifications/nskeyvalueobserving](https://developer.apple.com/documentation/foundation/notifications/nskeyvalueobserving)

## 개요

옵저버는 객체의 단순 속성과, 일대일 관계, 일대 다 관계를 포함한 객체의 모든 프로퍼티를 관찰할 수 있게 해줍니다. 일대 다 관계의 Observer는 변경 유형뿐만 아니라 변경과 관련된 객체에 대해서도 통지를 받습니다.

[NSObject](../../../etc/not-found.md)는 KeyValueObserving 프로토콜의 구현을 제공함으로써 모든 객체에 자동 관찰 기능을 추가합니다. 자동 관찰 기능을 비활성화시킨 다음 이 프로토콜의 메서드를 사용하여 더 개선된 notification을 수동으로 구현할 수 있습니다.

## 주제

### 변경 노티피케이션

* _func_ observeValue\(forKeyPath: String?, of: Any?, change: \[NSKeyValueChangeKey : Any\]?, context: UnsafeMutableRawPointer?\) 관찰 대상 객체에 대한 특정 key path의 값이 변경된 경우 Observer 객체에게 통보합니다.

### Observer 등록

* _func_ addObserver\(NSObject, forKeyPath: String, options: NSKeyValueObservingOptions = \[\], context: UnsafeMutableRawPointer?\) Observer 객체로 등록해서 이 메세지를 수신하는 객체와 관련된 key path에 대한 KVO notification을 받도록 합니다.
* _func_ removeObserver\(NSObject, forKeyPath: String\)

  Observer 객체가 특정 key path와 관련된 변경 메세지를 더 이상 받지 않도록 합니다.

* _func_ removeObserver\(NSObject, forKeyPath: String, context: UnsafeMutableRawPointer?\)

  주어진 context 하에서 Observer 객체가 특정 key path와 관련된 변경 메세지를 더 이상 받지 않도록 합니다.  
  \(역자 주: context의 역할에 대한 [stackoverflow의 설명](https://stackoverflow.com/questions/11916502/what-is-the-context-parameter-used-for-in-key-value-observing)\)

### Notifying Observers of Changes

* _func_ willChangeValue\(forKey: String\) Observer 객체에게 `forKey:` 에 해당하는 프로퍼티가 곧 변경될 것임을 알립니다.
* _func_ didChangeValue\(forKey: String\)

  Observer 객체에게 `forKey:` 에 해당하는 프로퍼티가 방금 변경되었음을 알립니다.

* _func_ willChange\(NSKeyValueChange, valuesAt: IndexSet, forKey: String\)

  Informs the observed object that the specified change is about to be executed at given indexes for a specified ordered to-many relationship.

* _func_ didChange\(NSKeyValueChange, valuesAt: IndexSet, forKey: String\) Informs the observed object that the specified change has occurred on the indexes for a specified ordered to-many relationship.
* _func_ willChangeValue\(forKey: String, withSetMutation: NSKeyValueSetMutationKind, using: Set\)

  Informs the observed object that the specified change is about to be made to a specified unordered to-many relationship.

* _func_ didChangeValue\(forKey: String, withSetMutation: NSKeyValueSetMutationKind, using: Set\)

  Informs the observed object that the specified change was made to a specified unordered to-many relationship.

### Observing Customization

* _class_ _func_ automaticallyNotifiesObservers\(forKey: String\) -&gt; Bool

  Observer 객체가 `forKey:` 를 자동 key-value observing\(KVO\) 하고 있다면 true를 반환합니다.

* _class_ _func_ keyPathsForValuesAffectingValue\(forKey: String\) -&gt; Set

  Returns a set of key paths for properties whose values affect the value of the specified key.

* _protocol_ NSKeyValueObservingCustomization
* _var_ observationInfo: UnsafeMutableRawPointer?

  Returns a pointer that identifies information about all of the observers that are registered with the observed object.

### 상수

* _class_ NSKeyValueObservation
* _struct_ NSKeyValueObservedChange
* _enum_ NSKeyValueChange 관찰 가능한 변경 유형들
* _struct_ NSKeyValueObservingOptions The values that can be returned in a change dictionary.
* _struct_ NSKeyValueChangeKey

  The keys that can appear in the change dictionary.

* _enum_ NSKeyValueSetMutationKind

  The kinds of mutation that you can make to an unordered collection.

## 같이 보기

### 관련 문서

* [Key - Value Observing 프로그래밍 가이드](https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/KeyValueObserving/KeyValueObserving.html#//apple_ref/doc/uid/10000177i)

