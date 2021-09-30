---
description: 이벤트 처리 연산자를 결합하여 비동기 이벤트 처리를 커스터마이즈 하세요
---

# Combine

> 원문 출처  
> [https://developer.apple.com/documentation/Combine](https://developer.apple.com/documentation/Combine)

## Summary

> SDKs
>
> * iOS 13.0+
> * macOS 10.15+
> * Mac Catalyst 13.0+
> * tvOS 13.0+
> * watchOS 6.0+

## 개요 <a id="overview"></a>

Combine 프레임워크는 시간 경과에 따른 처리를 위한 선언적 Swift API를 제공합니다. 처리되는 값들은 여러 종류의 비동기 이벤트로 표현됩니다. Combine은 값을 노출시키기 위해 Publisher를 선언하며 이 값은 시간에 따라 바뀝니다. 그리고 Subscriber는 Publisher로부터 값을 받습니다.

* Publisher 프로토콜은 시간에 따라 일련의 값을 전달할 수 있는 타입을 선언합니다. Publisher에는 업스트림 Publisher로부터 받은 값에 대해 동작하고 이를 다시 게시하는 연산자가 있습니다.
* Publisher 체인 끝에는 Subscriber가 존재하여 받은 값에 따라서 요소에 동작을 수행합니다. Publisher는 Subscriber로부터 명시적인 요청을 받을 때에만 값을 전달하며 이는 코드를 통해 Subscriber가 연결된 Publisher로부터 이벤트를 받는 속도를 조절할 수 있게 해줍니다.

[Timer](../app-frameworks/foundation/task-management/timer.md), NotificationCenter, [URLSession](../app-frameworks/foundation/url-loading-system/urlsession/)과 같은 몇몇 Foundation 타입들은 Publisher를 통해 그 기능을 노출합니다. 또한 Combine은 프로퍼티에 내장 publisher를 제공하며 Key-Value Observing과 호환됩니다.

여러 publisher들의 출력값을 조합하고 상호작용을 조절하는 것도 가능합니다. 예를 들어, 텍스트 필드의 publisher 업데이트를 추적하는 subscriber를 사용하면 해당 텍스트를 사용하여 URL 요청을 수행할 수 있고, 그 응답값을 처리하여 앱을 업데이트하는데 다른 publisher를 활용할 수 있습니다.

Combine을 사용하면 이벤트 처리 코드를 집중화 시키고 중첩 클로저와 컨벤션 기반 콜백과 같은 복잡한 기술들을 제거할 수 있습니다. 이렇게 함으로써 읽거나 유지보수하기에 더 좋은 코드가 만들어집니다.

## 주제 <a id="topics"></a>

### Essentials

* Combine으로 이벤트 받고 처리하기 비동기 소스로부터 이벤트를 받고 커스터마이징하세요

### Publishers

* _protocol_ Publisher 시간에 따라 일련의 값을 전송하는 타입을 선언합니다
* _enum_ Publishers publisher 기능을 하는 타입들의 네임스페이스
* _struct_ AnyPublisher 다른 publisher로 감싸서 타입 삭제를 수행하는 publisher
* _struct_ Published attribute로 지정된 property를 퍼블리싱하는 타입
* _protocol_ Cancellable 활동이나 동작의 취소가 가능함을 가리키는 프로토콜
* _class_ AnyCancellable 타입을 삭제하는 cacellable 객체로써 취소될 때 제공된 클로저를 실행합니다

### Convenience Publishers

* _class_ Future 단일값을 생성한 후 완료되거나 실패하는 publisher
* _struct_ Just 각 subscriber마다 단 한번 결과값을 주고 완료되는 publisher
* _struct_ Deferred 대기 중에 subscription이 발생하면 제공된 클로저를 실행해서 새 subscriber를 위한 publisher를 생성합니다.
* _struct_ Empty 어떤 값도 내놓지 않고 경우에 따라 즉시 완료됩니다
* _struct_ Fail 지정된 에러와 함께 즉시 중단됩니다
* _struct_ Record 각 subscriber가 추후 다시 볼 수 있도록 일련의 입력값과 완료 상태를 기록하는 것이 가능합니다

### Connectable Publishers

* 연결 가능한 Publisher로 퍼블리싱 조작하기 Publisher가 Subscriber에게 요소를 보내기 시작할 때 조정합니다.
* _protocol_ ConnectablePublisher Publication의 연결과 취소라는 명시적인 의미를 제공하는 publisher

### Subscribers

* 퍼블리싱 된 요소를 Subscriber로 처리하기 Publisher가 요소를 생성하는 시점을 정확하게 제어하기 위해 반대 방향의 압력을 적용합니다.
* _protocol_ Subscriber Publisher로부터 입력값을 받을 수 있는 타입을 선언하는 프로토콜
* _enum_ Subscribers Subscriber 역할을 하는 타입들의 네임스페이스
* _struct_ AnySubscriber 타입을 삭제하는 subscriber
* _protocol_ Subscription Subscriber에서 Publisher로 향하는 연결을 표현하는 프로토콜
* _enum_ Subscriptions Subscription과 연관된 symbol들의 네임스페이스

### Subjects

* _protocol_ Subject 외부 호출자가 요소를 퍼블리싱할 수 있도록 Publisher가 노출시키는 메소드
* _class_ CurrentValueSubject 단일 값을 감싸서 값의 변화가 일어날 때마다 새 요소를 퍼블리싱하는 객체
* _class_ PassthroughSubject 요소를 다운스트림 subscriber들에게 전파하는 객체

### Schedulers

* _protocol_ Scheduler 클로저를 언제, 어떻게 실행할 것인지 정의하는 프로토콜
* _struct_ ImmediateScheduler 동기적인 동작을 위한 스케줄러
* _protocol_ SchedulerTimeIntervalConvertible 스케줄러에 상대 시간에 대한 표현식을 제공하는 프로토콜

### Combine Migration

* 노티피케이션을 Combine Subscriber로 라우트하기 노티피케이션 센터의 Publisher를 사용해서 노티피케이션을 Subscriber로 전달하세요
* Timer Publisher로 Foundation Timer 대체하기 Timer를 사용해서 주기적으로 요소를 퍼블리싱합니다
* Combine으로 Key-Value Observing 수행하기 Combine publisher를 사용해서 KVO 변화를 노출시킵니다
* 비동기 코드를 위한 Combine 사용법 클로저 기반의 이벤트 처리 코드를 마이그레이션하는 일반적인 패턴

### Observable Objects

* _protocol_ ObservableObject 변화가 일어나기 전에 값을 내보내는 Publisher가 포함된 객체 타입
* _class_ ObservableObjectPublisher Observable object의 변화를 퍼블리싱하는 Publisher

### Encoders and Decoders

* _protocol_ TopLevelEncoder 인코딩 메소드를 정의하는 타입
* _protocol_ TopLevelDecoder 디코딩 메소드를 정의하는 타입

### Debugging Identifiers

* _protocol_ CustomCombineIdentifierConvertible 유니크하게 식별되는 Publisher 스트림을 위한 프로토콜
* _struct_ CombineIdentifier Publisher 스트림을 식별하기 위한 유니크 식별자

### Structures

* _struct_ AsyncPublisher
* _struct_ AsyncThrowingPublisher

