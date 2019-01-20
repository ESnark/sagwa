# OperationQueue

> 원문 출처  
> [https://developer.apple.com/documentation/foundation/operationqueue](https://developer.apple.com/documentation/foundation/operationqueue)

## 개요

operation queue는 대기열의 [Operation](operation.md) 객체를 각 우선순위와 준비 상태에 따라 실행합니다. operation은 operation queue에 추가된 후에 해당 operation의 작업이 끝났음을 보고받기 전까지 대기열에 남아있습니다. 대기열에 한번 추가된 이후에는 직접적으로 제거하는 것이 불가능합니다.

{% hint style="info" %}
알림

operation queue는 operation이 완료될 때까지 작업을 유지하며 대기열 자체는 모든 작업이 완료될 때까지 유지됩니다. operation이 완료되지 않은 operation queue를 중단시키면 메모리 누수가 발생할 수 있습니다.
{% endhint %}

operation queue 사용방법에 대한 더 자세한 정보는 [동시성 프로그래밍 가이드](../../../etc/not-found.md)를 참조하세요.

## 실행 순서 결정

대기열 내의 operation은 준비 상태, 우선 순위 수준, operation간 의존성에 의해 순서가 정해지고 실행됩니다. [queuePriority](../../../etc/not-found.md)가 동일한 operation들이 준비가 된 상태로 \(즉, [isReady](../../../etc/not-found.md) 프로퍼티가 true라는 것을 말합니다.\) 대기열에 들어간다면 대기열에 제출된 순서대로 실행됩니다. 그렇지 않다면 operation queue는 항상 준비된 operation중에서 우선순위가 높은 작업을 실행합니다.

그러나 operation의 준비 상태가 변경될 경우 실행 순서가 변경될 수 있으므로 대기열 시멘틱에 의존해서는 안 됩니다. operation 상호 의존성은 operation이 서로 다른 대기열에 있더라도 operation에 대한 절대적인 실행 순서를 제공합니다. 모든 선행 operation이 완료될 때까지 operation 객체는 실행 준비 상태로 간주되지 않습니다.

우선순위와 의존성을 설정하는 방법에 대한 자세한 내용은 [종속성 관리](operation.md#managing-dependencies)를 참조하세요.

## operation 취소

작업을 끝낸다는 것이 operation이 반드시 작업을 완료해야 한다는 뜻은 아닙니다. operation은 취소될 수도 있습니다. operation 객체를 취소하면 해당 객체는 대기열에 남아있지만 가능한 빨리 작업을 중지해야 한다는 것을 객체에 알립니다.  
현재 실행중인 operation에게 취소라는 것은 operation 객체의 취소 상태를 확인하고 하던것을 중단한 다음 스스로를 완료 상태로 표시한다는 것을 의미합니다.  
대기열에 있지만 아직 실행되지 않은 operation의 경우, 취소되어도 여전히 [start\(\)](../../../etc/not-found.md) 메서드는 호출되어서 취소 이벤트를 처리하고 스스로를 완료 상태로 표시해야 합니다.

{% hint style="info" %}
알림

operation을 취소하면 해당 객체와 연관된 모든 종속성이 무시됩니다. 이 동작은 취소된 operation의 start\(\) 메서드를 가능한한 빨리 실행하도록 만들고 start\(\) 메서드는 operation을 finished 상태로 변경시켜서 대기열로부터 제거될 수 있기 만듭니다.
{% endhint %}

operation 취소에 대한 정보는 [취소 명령에 대한 대응](operation.md#responding-to-the-cancel-command) 문서를 참조하세요.

## KVO 준수 프로퍼티

OperationQueue 클래스는 key-value coding \(KVC\)과 key-value observing \(KVO\)를 따릅니다. 개발자는 다음 프로퍼티를 관찰함으로써 애플리케이션의 다른 부분을 제어할 수 있습니다. 프로퍼티를 관찰하려면 다음 key path를 사용하세요:

* operations - 읽기 전용
* operationCount - 읽기 전용
* maxConcurrentOperationCount - 읽기 쓰기 가능
* isSuspended - 읽기 쓰기 가능
* name - 읽기 쓰기 가능

이 프로퍼티에 관찰자를 연결할 수는 있지만 코코아 바인딩을 사용해서 유저 인터페이스 요소를 결합시키면 안됩니다. 유저 인터페이스와 연결된 코드는 일반적으로 애플리케이션의 메인 스레드에서만 실행되어야 하는데 operation와 연관된 KVO 노티피케이션은 모든 스레드에서 발생할 수 있기 때문입니다.

key-value observing과 객체에 observer를 붙이는 방법에 대한 더 자세한 내용은 [Key-Value Oberving 프로그래밍 가이드](../../../etc/not-found.md) 문서를 참조하세요

## 스레드 안전성Thread Safety

여러 스레드에서 하나의 OperationQueue 객체를 사용할때 객체에 대한 접근을 동기화하기 위해서 추가적인 lock을 만드는 것은 안전하지 않습니다.

Operation queue는 operation 실행을 초기화하기 위해서 [Dispatch](../../../etc/not-found.md) 프레임워크를 사용합니다. 그 결과 operation들은 동기적이든 비동기적이든 관계없이 항상 별도의 스레드에서 실행됩니다.

## 주제

### 특정 operation queue에 접근하기

* _class var_ main: OperationQueue 메인 스레드와 연관된 operationQueue
* _class var_ current: OperationQueue?

  현재 operation을 시작한 operationQueue

### 대기열에서 operation 관리

* _func_ addOperation\(Operation\)

  지정된 operation을 수신자에 추가합니다.

* _func_ addOperations\(\[Operation\], waitUntilFinished: Bool\)

  지정된 operation을 대기열에 추가합니다.

* _func_ addOperation\(\(\) -&gt; Void\)

  지정된 블럭을 래핑하여 수신자에 추가합니다.

* _var_ operations: \[Operation\]

  현재 대기열에 있는 operation들

* _var_ operationCount: Int 현재 대기열에 있는 operation의 갯수
* _func_ cancelAllOperations\(\) 대기 중인 operation과 실행중인 operation들을 모두 취소합니다.
* _func_ waitUntilAllOperationsAreFinished\(\) 모든 수신자의 대기 중인 operation과 실행중인 operation이 완료될 때까지 현재 스레드를 차단합니다.

### operation 실행 관리

* _var_ qualityOfService: QualityOfService

  대기열을 사용하여 실행될 operation에 적용되는 기본 서비스 수준

* _var_ maxConcurrentOperationCount: Int

  동시에 실행할 수 있는 operation의 최대 수

* _class let_ defaultMaxConcurrentOperationCount: Int

  동시에 실행할 수 있는 operation의 기본 최대 수

### 실행 정지

* _var_ isSuspended: Bool 대기열이 operation을 스케줄링하고 있는지를 나타내는 Boolean 값

### 대기열 설정

* _var_ name: String?

  operation queue의 이름

* _var_ underlyingQueue: DispatchQueue?

  operation을 실행하는데 사용되는 dispatch queue

## 관련 문서

### 상속받은 대상

* NSObject

### 준수하는 프로토콜

* CVarArg
* Equatable
* Hashable

## 같이 보기

* _class_ [Operation](operation.md)

  단일 태스크와 관련된 코드 및 데이터를 나타내는 추상 클래스

* _class_ BlockOperation

  한 개 이상의 블록의 동시 실행을 관리하는 operation

