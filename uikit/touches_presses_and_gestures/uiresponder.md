# UIResponder

> 원본출처  
> [https://developer.apple.com/documentation/uikit/uiresponder](https://developer.apple.com/documentation/uikit/uiresponder)

## 개요

응답자\(Responder\) 객체 \(즉, [UIResponder](uiresponder.md)의 인스턴스\)는 UIKit 응용 프로그램의 이벤트 처리 백본을 구성합니다. [UIApplication](../core-app/uiapplication.md), [UIViewController](../view-controllers/uiviewcontroller.md) 및 모든 [UIView](../views_and_controls/uiview.md) 객체 \([UIWindow](../../not-found.md) 포함\)를 포함한 중요 객체들도 응답자입니다. 이벤트가 발생하면 UIKit은 이를 처리 할 수 ​​있도록 앱의 응답 객체에 전달합니다.

터치 이벤트, 모션 이벤트, 원격 제어 이벤트 및 프레스 이벤트를 비롯한 여러 종류의 이벤트가 있습니다. 특정 유형의 이벤트를 처리하려면 응답자가 해당 메서드를 오버라이드해야 합니다.  
예를 들어, 터치 이벤트를 처리하기 위해 응답자는 [touchesBegan \( : with :\)](../../not-found.md), [touchesMoved \( : with :\)](../../not-found.md), [touchesEnded \( : with :\)](../../not-found.md) 및 [touchesCancelled \( : with :\)](../../not-found.md) 메서드를 구현합니다. 터치가 일어났을때 응답자는 UIKit에서 제공한 이벤트 정보를 사용하여 해당 터치의 변경 사항을 추적하고 앱의 인터페이스를 적절하게 업데이트합니다.

이벤트 처리 외에도 UIKit 응답자는 처리되지 않은 이벤트를 앱의 다른 부분으로 전달하는 작업을 관리합니다. 주어진 응답자가 이벤트를 처리하지 않으면 응답자 체인의 다음 이벤트로 해당 이벤트를 전달합니다. UIKit은 미리 정의된 규칙으로 이벤트를 수신하려면 다음에 어떤 개체가 있어야 하는지 확인하여 응답자 체인을 동적으로 관리합니다. 예를 들어 뷰는 이벤트를 수퍼 뷰로 전달하고 계층 구조의 루트 뷰는 해당 뷰 컨트롤러로 이벤트를 전달합니다.

응답자는 [UIEvent](../../not-found.md) 개체를 처리하기도 하지만 input view를 통해 custom input을 허용할 수도 있습니다. 시스템의 키보드는 input view의 가장 명확한 예입니다. 사용자가 화면에서 [UITextField](../../not-found.md) 및 [UITextView](../../not-found.md) 개체를 탭하면 해당 view가 첫 번째 응답자가 되어 시스템 키보드인 input view를 표시합니다. 마찬가지로 custom input view를 생성하고 다른 응답자가 활성화될 때 이를 표시할 수 있습니다. custom input view를 응답자와 연결하려면 해당 view를 응답자의 inputView 속성에 할당합니다.

응답자 및 응답자 체인에 대한 자세한 내용은 [UIKit 앱에 대한 이벤트 처리 가이드](../../not-found.md)를 참조하십시오.

## 주제

### 응답자 체인 관리

* var next: UIResponder? 응답자 체인의 다음 응답자를 반환합니다. 다음 응답자가 없으면 nil을 반환합니다.
* var isFirstResponder: Bool 첫 번째 응답자임을 알리는 값
* var canBecomeFirstResponder: Bool 해당 객체가 첫번째 응답자가 될 수 있는지를 나타내는 값
* func becomeFirstResponder\(\) 이 객체를 해당 window 상의 첫번째 응답자로 만들도록 UIKit에 요청합니다.
* var canResignFirstResponder: Bool 수신자가 첫번째 응답자 지위를 포기할 의사가 있는지를 나타내는 값
* func resignFirstResponder\(\) window 상의 첫번째 응답자 지위를 포기하라는 요청을 이 객체에 알립니다.

### 터치 이벤트에 응답하기

* _func_ touchesBegan\(Set, with: UIEvent?\) view나 window에서  하나 이상의 새 터치가 발생했음을 이 객체에 알립니다.
* _func_ touchesMoved\(Set, with: UIEvent?\) 이벤트와 관련된 하나 이상의 터치가 변경된 경우 응답자에게 알립니다.
* _func_ touchesEnded\(Set, with: UIEvent?\) view 또는 window에서 하나 이상의 터치가 끝났을때 응답자에게 알려줍니다.
* _func_ touchesCancelled\(Set, with: UIEvent?\) 시스템 이벤트\(예: 시스템 경고\)가 터치 시퀀스를 취소할 때 응답자에게 알립니다.
* _func_ touchesEstimatedPropertiesUpdated\(Set\) 예측중인 프로퍼티에 대해 업데이트된 값이 응답자에게 수신되었거나 업데이트가 더 이상 필요하지 않음을 알립니다.

### 모션 이벤트에 응답하기

* _func_ motionBegan\(UIEventSubtype, with: UIEvent?\) 수신자에게 모션 이벤트가 시작되었음을 알립니다.
* _func_ motionEnded\(UIEventSubtype, with: UIEvent?\) 수신자에게 모션 이벤트가 끝났음을 알립니다.
* _func_ motionCancelled\(UIEventSubtype, with: UIEvent?\) 수신자에게 모션 이벤트가 취소되었음을 알립니다.

### Press 이벤트에 응답하기

일반적으로 press 이벤트를 처리하는 응답자는 다음 네 가지 메서드를 모두 오버라이합니다.

* _func_ pressesBegan\(Set, with: UIPressesEvent?\) 물리 버튼이 눌렸을때 이 객체에 알립니다.
* _func_ pressesChanged\(Set, with: UIPressesEvent?\) press에 관련된 값에 변동이 있음을 알립니다.
* _func_ pressesEnded\(Set, with: UIPressesEvent?\) 눌렸던 버튼을 놓았을때 이 객체에 알립니다.
* _func_ pressesCancelled\(Set, with: UIPressesEvent?\) 메모리 경고와 같은 시스템 이벤트로 인해서 press 이벤트가 취소되었음을 객체에 알립니다.

### 원격제어 이벤트에 응답하기

* _func_ remoteControlReceived\(with: UIEvent?\) 원격 제어 이벤트가 수신되었을 때 객체에 알립니다.

### Input view 관리

* _var_ inputView: UIView? 수신자가 첫번째 응답자가 될 때 표시되는 custom input view
* _var_ inputViewController: UIInputViewController? 수신자가 첫번째 응답자가 될 때 사용할 custom input view controller
* _var_ inputAccessoryView: UIView? 수신자가 첫번째 응답자가 될 때 표시되는 custom input accessory view
* _var_ inputAccessoryViewController: UIInputViewController? 수신자가 첫번째 응답자가 될 때 사용할 custom input accessory view controller
* _func_ reloadInputViews\(\) 객체가 첫번째 응답자일 경우 custom input 및 accessory view를 업데이트 합니다.

### Undo Manager 얻기

* _var_ undoManager: UndoManager? 응답자 체인의 가장 가까운 공유 undo manager

### 커맨드 유효성 검사

* _func_ canPerformAction\(Selector, withSender: Any?\) 사용자 인터페이스에서 지정된 명령을 활성화하거나 비활성화하도록 수신 응답자를 요청합니다.
* _func_ target\(forAction: Selector, withSender: Any?\) 작업에 응답하는 대상 객체를 반환합니다.

### 사용 가능한 키 커맨드 접근

* _var_ keyCommands: \[UIKeyCommand\]? 이 응답자에 대한 작업을 트리거하는 키 커맨드

### 텍스트 입력모드 관리

* _var_ textInputMode: UITextInputMode? 이 응답자 객체의 텍스트 입력 모드
* _var_ textInputContextIdentifier: String?

  응답자가 텍스트 입력 모드 정보를 보존해야함을 나타내는 식별자.

* _class func_ clearTextInputContextIdentifier\(String\)

  텍스트 입력 모드 정보를 앱의 User default값에서 지웁니다.

* _var_ inputAssistantItem: UITextInputAssistantItem 키보드 단축 표시줄을 구성할 때 사용할 입력 어시스턴트

### 유저 활동 지원

* _var_ userActivity: NSUserActivity?

  이 응답자가 지원하는 사용자 활동을 캡슐화하는 객체

* _func_ restoreUserActivityState\(NSUserActivity\)

  지정된 사용자 활동을 계속하는 데 필요한 상태를 복원합니다.

* _func_ updateUserActivityState\(NSUserActivity\)

  지정된 사용자 활동의 상태를 업데이트합니다.

## 관련 문서

### 상속받은 대상

* NSObject

### 준수하는 프로토콜

* CVarArg
* Equatable
* Hashable
* UIPasteConfigurationSupporting
* UIResponderStandardEditActions

