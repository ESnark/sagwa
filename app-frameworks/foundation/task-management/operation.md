# Operation

> 원본 출처  
> [https://developer.apple.com/documentation/foundation/operation](https://developer.apple.com/documentation/foundation/operation)

> 역자 주
>
> 1. 본 문서에서는 "operation", "task" 및 기타 비슷한 단어들이 많이 사용됩니다. 이 용어들은 모두 "작업"이라고 번역될 수 있지만 이 단어가 사전적 정의대로 "일정한 목적과 계획 아래 하는 일"인지 "Operation 클래스의 인스턴스"인지 파악하기가 쉽지 않습니다. 따라서 이번 문서에서는 가급적 엄격하게 operation이라는 원문의 단어를 보존하여 번역하도록 하겠습니다. 또한 클래스 명명법에 따라서 첫 글자가 대문자면 클래스, 소문자면 인스턴스라는 룰을 암묵적으로 따릅니다.
> 2. 원문에서는 Objective-C의 런타임 객체인 NSOperation이라는 명칭이 종종 등장합니다. 이전 문서에 영향을 받은 오타라고 생각하지만 일단은 그대로 번역합니다.

## 개요

Operation은 추상 클래스이기 때문에 작업 수행을 위해 직접 사용되지는 않고 \(시스템 정의된\) 서브클래스를 사용합니다. 시스템 정의 서브클래스로는 [NSInvocationOperation](../../../etc/not-found.md), [BlockOperation](../../../etc/not-found.md)이 있습니다. Operation의 기본 구현에는 추상적이지만 작업의 안전한 실행을 조정하는 중요한 로직이 포함되어 있습니다. 이 기본 내장된 로직은 개발자가 다른 시스템 객체와 올바르게 동작하도록 하기 위한 글루코드가 아니라 실제 작업 구현에 집중하도록 돕습니다.

operation 객체는 싱글샷 객체입니다. 즉, 작업을 한 번 실행한 후에는 다시 사용할 수 없습니다. 일반적으로 작업 대기열\([OperationQueue](operationqueue.md) 클래스의 인스턴스\)에 추가하여 작업을 실행하는데 operationQueue 보조 쓰레드에서 직접 실행하거나 libdispatch 라이브러리\(Grand Central Dispatch라고도 함\)를 사용하여 간접적으로 operation을 수행합니다. operationQueue가 operation을 실행하는 방법에 대한 자세한 내용은 [OperationQueue](operationqueue.md)를 참조하세요.

operationQeueu를 원하지 않는다면 코드에서 직접 start\(\) 메서드를 호출하여 작업을 직접 실행할 수 있습니다. 준비 상태가 아닌 작업을 시작하면 예외가 발생하기 때문에 operation을 수동적으로 실행하는 것은 코드에 많은 부담이 됩니다. isReady 프로퍼티는 작업 준비 상태를 나타냅니다.

## operation 종속성

종속성은 operation을 순서대로 실행하는 편리한 방법입니다. addDependency\(\_:\)와 removeDependency\(\_:\) 메서드를 사용하여 operation에 대한 종속성을 추가하고 제거할 수 있습니다. 기본적으로 종속성이 있는 operation 객체는 해당 객체가 종속된 모든 operation 객체\(선행하는 operation\)의 실행이 완료되기 전까지 준비되지 않은 것으로 간주됩니다.  그러나 선행 operation이 전부 실행된 후에는 종속된 operation 객체가 준비되고 실행가능해집니다.

NSOperation에서 지원되는 종속성은 선행 operation이 성공적으로 완료되었는지 실패했는지를 구분하지 않습니다. 즉, operation을 취소하면 유사한 방식으로 완료된 것으로 표시됩니다. 선행 operation이 취소되었거나 작업을 성공적으로 완료되지 못한 경우 종속 operation을 계속해서 진행할지 여부는 개발자에게 달려 있습니다. 이를 위해 operation 객체에 몇 가지 추가 오류 추적 기능을 통합해야 할 수 있습니다.

## KVO 준수 프로퍼티

NSOperation 클래스의 몇몇 프로퍼티는 key-value coding \(KVC\)과 key-value observing \(KVO\)를 준수합니다. 필요에 따라 이 프로퍼티들을 관찰하여 앱의 다른 부분을 제어할 수 있습니다. 프로퍼티를 관찰하려면 다음 key path를 사용하세요:

* isCancelled - 읽기 전용
* isAsynchronous - 읽기 전용
* isExecuting - 읽기 전용
* isFinished - 읽기 전용
* isReady - 읽기 전용
* dependencies - 읽기 전용
* queuePriority - 읽기 쓰기 가능
* completionBlock - 읽기 쓰기 가능

이 프로퍼티에 관찰자를 연결할 수는 있지만 코코아 바인딩을 사용해서 유저 인터페이스 요소를 결합시키면 안됩니다. 유저 인터페이스와 연결된 코드는 일반적으로 애플리케이션의 메인 스레드에서만 실행되어야 하는데 operation은 어떤 스레드에서든지 실행될 수 있기 때문입니다. 따라서 유사하게 KVO 노티피케이션도 모든 스레드에서 발생할 수 있습니다.

앞서 소개한 프로퍼티에 커스텀 구현을 제공하는 경우에도 KVC와 KVO 호환을 유지해야 합니다. 또한 NSOperation 객체에 추가적으로 프로퍼티를 정의하는 경우에도 KVC/KVC를 준수하는 것이 좋습니다. key-value coding을 지원하는 방법에 대해서는 [Key-Value Coding 프로그래밍 가이드](../../../etc/not-found.md)를 참조하세요. key-value observing을 지원하는 방법은 [Key-Value Oberving 프로그래밍 가이드](../../../etc/not-found.md) 문서에 나와 있습니다.

## 멀티코어 고려사항

NSOperation은 그 자체로 멀티코어를 지원합니다. 따라서 여러 스레드에서 NSOperation 객체의 메서드를 호출할 때에는 액세스 동기화를 위한 추가적인 lock을 생성하지 않는 편이 안전합니다. 이는 일반적으로 operation이 생성되고 모니터링하는 스레드와 실제 실행되는 스레드가 다르기 때문에 필수적인 동작입니다.

NSOperation을 서브클래싱 할때는 오버라이드한 메서드가 여러 스레드에서 호출하기에 안전한지 확인해야 합니다. 예를 들어 서브클래스에서 데이터에 접근하는 커스텀 메서드를 구현했다면 그 메서드가 thread-safe한지 반드시 확인해야 합니다. 이런 경우 operation에서의 데이터 변수에 대한 모든 접근은 잠재적인 데이터 손상을 방지하기 위해서 반드시 동기화되어야 합니다. 동기화에 대한 자세한 내용은 [스레딩 프로그래밍 가이드](../../../etc/not-found.md)를 참조하세요

## 비동기 Operation vs 동기 Operation

operation 객체를 대기열에 추가하는 대신 수동적으로 실행하기로 했다면 설계에 따라operation이 비동기식 또는 동기식으로 실행되게 할 수도 있습니다. 그렇지만 기본적으로는 동기식으로 동작합니다. 동기식 operation 객체는 작업을 실행할 별도의 스레드를 생성하지 않고 해당 객체의 start\(\) 메서드를 호출하면 현재 스레드에서 operation이 즉시 실행됩니다. start\(\) 메서드가 작업을 완료하면 호출자에게 제어권을 되돌려줍니다.

비동기식 operation 객체의 start\(\) 메서드를 호출하면 이 메서드는 작업이 끝나기 전에 제어권을 반환합니다. 비동기 operation 객체는 별도의 스레드에서 작업을 예약합니다. operation은 새 스레드를 직접 시작하거나, 비동기 메서드를 호출하거나, 디스패치 큐에 블럭을 제출하는 방식으로 수행할 수 있습니다. 비동기식 operation으로 작업시에 제어권이 호출자에게 되돌아오는 시점은 operation 완료 시점과는 관련이 없으며 제어권이 돌아왔다고 하더라도 operation은 계속 진행중일 수 있습니다.

수동으로 비동기 operation을 정의하려면 KVO 노티피케이션을 사용하여 작업의 진행상태를 모니터링하고 진행 상태의 변경사항을 보고해야 하기 때문에 더 많은 작업이 필요합니다. 그렇지만 수동으로 실행된 작업이 호출 스레드를 차단하지 않도록 하려는 경우에는 유용합니다.

operationQueue에 operation을 추가하면 대기열은 [isAsynchronous](../../../etc/not-found.md) 프로퍼티를 무시하고 항상 별도의 스레드에서 start\(\) 메서드를 호출합니다. 따라서 operation을 항상 operationQeueu에 추가하여 실행하면 비동기화 할 필요가 없습니다.

동기식 operation과 비동기식 operation을 정의하는 방법에 대해서는 Subclassing Notes를 참조하세요.

## Subclassing Notes

NSOperation 클래스는 operation의 실행 상태를 추적하기 위한 기본 로직을 제공하지만 실제 작업을 수행하려면 서브클래싱 되어야합니다. 하위 클래스를 생성하는 방법에 따라서 작업이 비동기적\(concurrent\)으로 실행되거나 동기적\(non-concurrent\)으로 실행될 수 있습니다.

### 오버라이드할 메서드

동기 operation을 위해서는 보통 하나의 메서드만 오버라이드 하게 됩니다:

* [main\(\)](../../../etc/not-found.md)

이 메서드를 사용하면 지정된 코드를 수행하도록 할수 있습니다. 물론, 커스텀 클래스의 인스턴스를 더 쉽게 생성할 수 있도록 커스텀 초기화 메서드를 정의해야 합니다. 그리고 operation의 데이터에 접근하는 getter와 setter 메서드를 정의할 수도 있습니다. 그러나 getter와 setter 메서드를 직접 정의하는 경우 여러 스레드에서 안전하게 접근할 수 있는지\(thread-safe\) 확인해야 합니다.

비동기 operation을 생성할 때에는 기본적으로 다음 메서드와 프로퍼티가 오버라이드 되어야 합니다:

* start\(\)
* isAsynchronous
* isExecuting
* isFinished

비동기 operation에서는 start\(\) 메서드가 비동기적으로 작업을 시작할 책임이 있습니다. 스레드를 생성하든 비동기 함수를 호출하든간에 이 메서드에서 수행합니다. operation을 시작하면 start\(\) 메서드는 isExecuting 프로퍼티에게 보고받은대로 실행 상태를 업데이트 해야합니다. 이 작업은 KVO 노티피케이션을 발송하여 isExecuting key path를 주시하고 있는 클라이언트에게 operation이 현재 실행중임을 알립니다. isExecuting 프로퍼티는 thread-safe하게 상태를 제공해야 합니다.

작업 완료 또는 작업 취소 시에 비동기 operation 객체는 반드시 isExecuting과 isFinished key path에 대한 KVO 노티피케이션을 발송하여 operation의 최종 상태 변경을 알려야 합니다. \(작업 취소의 경우 작업이 완전히 완료되지 않았더라도 isFinished는 반드시 업데이트 해야합니다. 대기중인 operation들은 대기열에서 제거되기 전에 완료되었음을 보고해야 합니다.\) In addition to generating KVO notifications, your overrides of the isExecuting and isFinished properties should also continue to report accurate values based on the state of your operation.

비동기 operation을 정의하는 방법에 대한 더 자세한 내용은 [동시성 프로그래밍 가이드](../../../etc/not-found.md)를 참조하세요

{% hint style="warning" %}
중요

start\(\) 메서드에서 super를 호출해서는 안됩니다.  
비동기 operation을 정의할 때에는 작업 시작, KVO 노티피케이션 발송 등 기본 start\(\) 메서드와 동일한 동작을 직접 제공해야 하고 메서드가 실제 작업을 시작하기 전에 operation 자체가 취소되지는 않았는지도 확인해야 합니다.

취소 시멘틱에 대한 자세한 내용은 [Responding to the Cancel Command](../../../etc/not-found.md) 문서를 참조하세요
{% endhint %}

동기 operation도 그렇지만 비동기 operation의 경우에도 위에 설명된 이외의 메서드를 정의해야 할 일은 거의 없습니다. 하지만 operation의 종속성 기능을 커스터마이즈 하는 경우 추가적인 메서드 오버라이드와 KVO 노티피케이션을 제공해야할 수 있습니다. 종속성의 경우 isReady key path에 대한 노티피케이션만 제공하면 됩니다. 종속성 프로퍼티에는 선행 operation 리스트가 포함되어 있기 때문에 기본 NSOperation 클래스에서 변경내용을 알아서 처리합니다.

### Operation 객체상태 유지하기

operation 객체는 상태 정보를 내부적으로 유지하며 안전하게 실행할 시점을 결정하고 operation의 수명주기를 통해서 진행정보를 외부 클라이언트에게 알립니다. 커스텀 서브클래스는 이 상태 정보를 유지하면서 operation 코드의 올바른 실행을 보장합니다. operation 상태와 관련된 주요 key path는 다음과 같습니다:

* **isReady** isReady key path는 operation을 실행할 준비가 되면 client에게 알려줍니다. [isReady](../../../etc/not-found.md) 프로퍼티는 operation이 실행할 준비가 되었을 때에는 true이고 아직 완료되지 않은 선행 operation이 있을 때는 false입니다.  대부분의 경우 이 key path의 상태를 직접 관리할 필요는 없습니다. 그러나 operation의 준비 상태가 선행 operation 이외의 요인에 의해 결정되는 경우 \(예를 들면 프로그램의 외부조건 같은 것들\) 개발자가 직접 [isReady](../../../etc/not-found.md) 프로퍼티를 구현하고 준비상태를 추적할 수 있습니다.It is often simpler though just to create operation objects only when your external state allows it.  macOS 10.6 이상 버전에서는 하나 이상의 선행 operation이 완료될 때까지 기다리는 동안 operation을 취소하면 이 종속성들은 무시되고 isReady 프로퍼티의 값은 true로 바뀝니다. 이 동작을 수행하면 operationQueue에서 취소된 작업을 대기열에서 더 빨리 제거할 수 있습니다. 
* **isExecuting** isExecuting key path는 operation이 현재 할당된 작업을 실행중임을 클라이언트들에게 알립니다. [isExecuting](../../../etc/not-found.md) 프로퍼티는 operation이 작업중이면 true, 아니면 false값입니다.  operation 객체의 [start\(\)](../../../etc/not-found.md) 메서드를 교체할 때에는 [isExecuting](../../../etc/not-found.md) 프로퍼티도 교체되어야 하며 상태 변화에 따라 KVO 노티피케이션을 생성하도록 만들어야 합니다. 
* **isFinished** isFinished key path는 operation 작업이 성공적으로 끝났거나 취소되어 종료중임을 클라이언트들에게 알립니다. operation 객체는 isFinished key path의 값이 true가 되기 전까지 종속성을 지우지 않습니다. 마찬가지로 operationQueue도 operation의 [isFinished](../../../etc/not-found.md) 프로퍼티가 true가 되기 전까지는 대기열에서 operation을 제거하지 않습니다. 따라서 대기열을 진행 중이거나 취소된 작업으로 백업하지 못하도록 하려면 operation의 isFinished를 마킹하는 것이 중요합니다.  operation 객체의 [start\(\)](../../../etc/not-found.md) 메서드를 교체할 때에는 [isFinished](../../../etc/not-found.md) 프로퍼티도 교체되어야 하며 상태 변화에 따라 KVO 노티피케이션을 생성하도록 만들어야 합니다. 
* **isCancelled** isCancelled key path는 operation의 취소가 요청되었음을 클라이언트들에게 알립니다. 취소상태에 대한 지원 여부는 권장되는 사항이지만 개발자 재량에 달려있고 반드시 KVO 노티피케이션을 보내야 하는 것은 아닙니다. operation의 취소 알림 처리에 대한 자세한 내용은 [취소 명령에 대한 대응](operation.md#responding-to-the-cancel-command) 문서를 참조하세요.

### 취소 명령에 대한 대응 <a id="responding-to-the-cancel-command"></a>

한번 operation이 대기열에 들어가게 되면 해당 operation은 개발자의 손에서 떠나가고 대기열이 해당 작업의 스케줄을 대신 처리합니다.하지만 사용자가 진행률 패널에서 취소버튼을 누른다든지 애플리케이션을 종료해서 operation이 실행하지 않기로 결정된 경우 CPU 시간을 불필요하게 사용하지 않도록 operation을 취소할 수 있습니다. 이 작업은 operation 객체의 cancel\(\) 메서드를 호출하거나 OperationQueue 클래스의 [cancelAllOperations\(\)](../../../etc/not-found.md) 메서드를 호출해서 수행합니다.

operation을 취소해도 바로 중지되지는 않습니다. isCancelled 프로퍼티 값을 고려해서 모든 작업을 수행해야 하지만 코드에서는 이 프로퍼티의 값을 명시적으로 점검하고 필요에 따라 취소해야 합니다. NSOperation의 기본 구현에는 취소 점검이 포함되어 있습니다. 예를 들어 start\(\) 메서드를 호출하기 전에 operation을 취소하면 start\(\) 메서드는 작업을 실행하지 않고 종료됩니다.

{% hint style="info" %}
알림

macOS 10.6 이상 버전에서는 operationQueue에 있으면서 선행 operation이 완료되지 않은 operation에 대해서 cancel\(\) 메서드를 호출하면 선행 operation은 무시됩니다. operation이 이미 취소되었기 때문에 main\(\) 메서드를 호출하지 않고도 대기열에서 operation의 start\(\) 메서드를 호출할 수 있습니다.  
또한 대기열에 없는 operation의 cancel\(\) 메서드를 호출하면 그 즉시 operation이 취소된 것으로 표시됩니다.  
각각의 경우 operation을 준비 또는 완료로 표시하면 적절한 KVO 노티피케이션이 발송됩니다.
{% endhint %}

cancellation 시멘틱은 작성하는 모든 커스텀 코드에서 지원되어야 합니다. 특히 메인 작업 코드는 주기적으로 isCancelled 프로퍼티 값을 확인하면서 프로퍼티가 true를 보고하면 operation 객체를 가능한 한 빨리 정리하고 종료해야 합니다. start\(\) 커스텀 메서드를 구현하는 경우 이 메서드는 취소 여부를 조기 확인하고 적절하게 동작해야 합니다.

## 주제

### operation 실행

* _func_ start\(\) operation의 실행을 시작합니다.
* _func_ main\(\) 수신자의 동기성 작업을 수행합니다.
* _var_ completionBlock: \(\(\) -&gt; Void\)? 이 블럭은 메인 태스크가 완료된 후에 실행됩니다.

### operation 취소

* _func_ cancel\(\) operation 객체에 작업 실행을 중지해야 함을 알립니다.

### operation 상태 가져오기

* _var_ isCancelled: Bool

  operation 취소여부를 나타내는 Boolean 값

* _var_ isExecuting: Bool

  operation의 현재 실행 여부를 나타내는 Boolean 값

* _var_ isFinished: Bool

  operation 완료 여부를 나타내는 Boolean 값

* _var_ isConcurrent: Bool

  operation의 비동기 실행 여부를 나타내는 Boolean 값

* _var_ isAsynchronous: Bool

  operation의 비동기 실행 여부를 나타내는 Boolean 값

* _var_ isReady: Bool operation이 지금 실행 가능한지를 나타내는 Boolean값
* _var_ name: String?

  operation의 이름

### 종속성\(의존성\) 관리 <a id="managing-dependencies"></a>

* _func_ addDependency\(Operation\)

  수신자가 주어진 Operation의 완료에 종속성을 갖습니다.

* _func_ removeDependency\(Operation\)

  주어진 Operation에 대한 수신자의 종속성을 제거합니다.

* _var_ dependencies: \[Operation\]

  현재 객체를 실행하기 전에 완료되어야 하는 operation 객체들의 리스트

### 실행 우선순위 설정

* _var_ qualityOfService: QualityOfService

  작업에 시스템 리소스를 부여하기 위한 상대적 중요도

* ~~_var_ threadPriority: Double~~

  The thread priority to use when executing the operation `Deprecated`

* _var_ queuePriority: Operation.QueuePriority

  operationQueue에서 operation의 실행 우선순위

### operation 객체 대기

* _func_ waitUntilFinished\(\) operation 객체가 작업을 완료할 때까지 현재 스레드의 실행을 차단합니다.

### 상수Constants

* _enum_ Operation.QueuePriority

  operation의 작업 순서에 우선순위를 매기는데 사용되는 상수

* _enum_ QualityOfService 시스템에 대한 작업의 성격과 중요성을 나타내는데 사용됩니다. 더 높은 품질의 서비스 클래스를 사용하는 작업은 리소스 경합이 있을때 더 낮은 품질의 서비스 클래스를 사용하는 작업보다 많은 리소스를 받습니다.

## 관련 문서

### 상속받은 대상

* NSObject

### 준수하는 프로토콜

* CVarArg
* Equatable
* Hashable

## 같이 보기

### Operations

* _class_ [OperationQueue](operationqueue.md)

  작업 실행을 제어하는 대기열\(queue\)

* _class_ BlockOperation

  한 개 이상의 블록의 동시 실행을 관리하는 operation

