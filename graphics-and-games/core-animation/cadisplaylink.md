# CADisplayLink

> 원본 출처  
> [https://developer.apple.com/documentation/quartzcore/cadisplaylink](https://developer.apple.com/documentation/quartzcore/cadisplaylink)

## 개요

애플리케이션은 새로운 디스플레이 링크를 초기화해서 내놓는데, 디스플레이 링크는 화면이 업데이트 될때 타겟 객체와 호출될 Selector를 제공합니다. 디스플레이 루프를 디스플레이와 동기화하기 위해서는 애플리케이션이 [add\(to:forMode:\)](../../etc/not-found.md) 메서드를 사용하여 런 루프에 디스플레이 루프를 추가해야 합니다.

디스플레이 링크가 런 루프와 연결되면 화면의 내용을 업데이트해야 할 때 타겟의 Selector가 호출됩니다. 타겟은 디스플레이 링크의 [timestamp](../../etc/not-found.md) 프로퍼티를 읽어 이전 프레임이 표시된 시간을 검색할 수 있습니다. 예를 들어 동영상을 표시하는 애플리케이션은 timestamp를 사용하여 다음에 표시할 비디오 프레임을 계산할 수 있습니다. 자체 애니메이션을 수행하는 애플리케이션은 timestamp를 사용하여 표시중인 객체가 다음 프레임의 어디에, 그리고 어떻게 표시되어야 할지를 결정할 수 있습니다.

[duration](../../etc/not-found.md) 프로퍼티는 [maximumFramesPerSecond](../../etc/not-found.md)의 프레임 간 시간을 제공합니다. 실제 프레임 시간을 계산하려면 [targetTimestamp](../../etc/not-found.md) - [timestamp](../../etc/not-found.md)를 사용하세요. 애플리케이션에서 이 값을 사용하여 디스플레이의 주사율을 계산하거나 다음 프레임이 표시될 대략적인 시간을 추측해내고 다음 프레임이 표시될 시간에 준비되도록 그리기 동작을 조정할 수 있습니다.

[isPauseed](../../etc/not-found.md) 속성을 true로 설정하여 노티피케이션을 중지할 수 있습니다. 또한 애플리케이션이 제공된 시간 내에 프레임을 제공할 수 없는 경우 프레임률을 더 느리게 선택할 수 있습니다. 프레임률이 더 느리지만 일관된 애플리케이션은 프레임을 건너뛴 애플리케이션보다 사용자에게 더 부드럽게 보입니다. [preferredFramesPerSecond](../../etc/not-found.md) 프로퍼티를 설정하여 초당 프레임 수를 정의할 수 있습니다.

디스플레이 링크가 함께 완료되면 [invalidate\(\)](../../etc/not-found.md)를 호출하여 모든 런 루프에서 제거하고 타겟과 연결을 끊어야 합니다.

목록 1은 디스플레이 링크를 만들고 현재 런 루프에 추가하는 방법을 보여줍니다. 디스플레이 링크는 각 화면 업데이트마다 현재 타임스탬프를 표시하는 step 함수를 호출합니다.

{% code-tabs %}
{% code-tabs-item title="목록1 디스플레이 링크 생성하기" %}
```swift
func createDisplayLink() {
    let displaylink = CADisplayLink(target: self,
                                    selector: #selector(step))
    
    displaylink.add(to: .current,
                    forMode: .defaultRunLoopMode)
}
     
func step(displaylink: CADisplayLink) {
    print(displaylink.timestamp)
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

CADisplayLink는 서브클래싱되어서는 안됩니다.

## Preferred and Actual Frame Rates

[preferredFramesPerSecond](../../etc/not-found.md)를 설정하여 디스플레이 링크의 프레임률을 제어할 수 있습니다. 그러나 실제 초당 프레임 수는 사용자가 설정한 기본값과 다를 수 있습니다. 실제 프레임률은 항상 기기의 최대 주사율에 영향을 받습니다.

예를 들어 기기의 주사율이 초당 60 프레임\(maximumFramesPerSecond로 정의됨\)인 경우 실제 가능한 프레임률은 초당 15, 20, 30 및 60 프레임입니다. 디스플레이 링크의 기본 프레임률을 최대값보다 높은 값으로 설정해도 실제 프레임률은 최대값에 고정됩니다.

최대 프레임 속도값을 나누었을때 정수가 되지 않는 기본 프레임 속도는 가장 가까운 값으로 반올림됩니다. 예를 들어 최대 재생률이 초당 60 프레임인 기기에서 기본 프레임 속도를 26 또는 35 프레임으로 설정하면 실제 프레임 속도는 초당 30 회가 됩니다.

목록 2는 targetTimestamp에서 디스플레이 링크의 timestamp를 뺀 값으로 1을 나눠서 실제 프레임률을 계산하는 방법을 보여줍니다.

{% code-tabs %}
{% code-tabs-item title="목록2 실제 프레임율 계산하기" %}
```swift
// displaylink is a `CADisplayLink`

let actualFramesPerSecond = 1 / (displaylink.targetTimestamp - displaylink.timestamp)
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## 주제

### 인스턴스 생성하기

* init\(target: Any, selector: Selector\) 새로운 디스플레이 링크를 반환합니다.

### 디스플레이 링크가 노티피케이션을 보내도록 스케줄링하기

* func add\(to: RunLoop, forMode: RunLoop.Mode\) 런 루프에 디스플레이 링크를 등록합니다.
* func remove\(from: RunLoop, forMode: RunLoop.Mode\) `forMode:` 모드의 런 루프에서 디스플레이 링크를 제거합니다.
* func invalidate\(\)

  모든 런 루프 모드에서 디스플레이 링크를 제거합니다.

### 디스플레이 링크 설정하기

* var duration: CFTimeInterval 화면 업데이트 사이의 시간 간격
* var preferredFramesPerSecond: Int

  디스플레이 링크 콜백의 기본 프레임률

* ~~var frameInterval: Int~~

  The number of frames that must pass before the display link notifies the target again. `Deprecated`

* var isPaused: Bool 디스플레이 링크로부터 타겟으로 향하는 노티피케이션의 중지 상태를 나타내는 Boolean 값
* var timestamp: CFTimeInterval 마지막으로 표시된 프레임과 관련된 시간값
* var targetTimestamp: CFTimeInterval 표시된 다음 프레임과 연관된 시간값

## 관련 문서

### 상속받은 대상

* NSObject

### 준수하는 프로토콜

* CVarArg
* Equatable
* Hashable

## 같이 보기

### 애니메이션 타이밍

* _func_ CACurrentMediaTime

  현재 절대 시간을 초 단위로 반환합니다.

* _class_ CAMediaTimingFunction

  애니메이션의 페이싱을 타이밍 커브로 정의하는 함수

* _protocol_ CAMediaTiming 계층적 타이밍 시스템을 모델링하는 메서드로서, 객체가 부모 객체와 로컬 시간 사이의 시간을 매핑할 수 있도록 합니다.

