---
description: UIKit 앱의 View 계층구조를 관리하는 객체
---

# UIViewController

> 원본출처  
> [https://developer.apple.com/documentation/uikit/uiviewcontroller](https://developer.apple.com/documentation/uikit/uiviewcontroller)

## 개요

UIViewController 클래스는 모든 view controller에 공통적인 동작을 정의합니다.  
UIViewController 클래스의 인스턴스를 직접 만드는 경우는 거의 없습니다. 대신 UIViewController를 하위 클래스로 만들고 view controller의 뷰 계층 구조를 관리하는 데 필요한 메서드와 프로퍼티를 추가하세요.

view controller의 주요 임무는 다음과 같습니다.

* 데이터 변화에 따라서 view 컨텐츠를 업데이트
* view와의 사용자 상호작용에 응답
* view를 리사이징하고 전체적인 인터페이스의 레이아웃 관리
* 앱 내에서 \(다른 view controller를 포함한\) 다른 객체와의 조정

view controller는 자신이 관리하는 view에 단단히 바인딩되어 있고 view 계층에서 이벤트를 처리하는 데 참여합니다. 특히 view controller는 UIResponder 객체로써 view controller의 루트 뷰와 해당 뷰의 상위 뷰 사이에 있는 responder chain에 삽입되며 일반적으로 다른 view controller에 속합니다. view controller상의 어떤 view도 이벤트를 처리하지 않는다면 view controller는 직접 이벤트를 처리하거나 상위 뷰로 전달할 수 있는 옵션을 제공합니다.

view controller가 단독적으로 사용되는 일은 거의 없습니다. 대부분의 경우 유저 인터페이스의 일부를 담당하는 여러개의 view controller가 같이 사용됩니다. 예를 들어, 하나의 view controller에 항목 테이블이 표시되는 동안 다른 view controller에 해당 테이블에서 선택한 항목이 표시됩니다.  
일반적으로 하나의 view controller에는 하나의 뷰만 표시됩니다. view controller는 새로운 뷰 세트를 표시하기 위해 다른 view controller를 표시하거나, 다른 view controller의 컨텐츠에 대한 컨테이너 역할을 하고 원하는 대로 뷰를 애니메이션할 수 있습니다.

## SubClassing Notes

대부분의 앱에는 UIViewController의 커스텀 하위 클래스가 적어도 하나 이상 포함되어 있습니다. 커스텀 view controller는 앱의 생김새와 사용자 상호작용에 응답하는 방법을 포함하여 앱의 전반적인 동작을 정의합니다. 다음 섹션에서는 사용자 정의 하위 클래스에서 수행하는 몇 가지 작업에 대한 간략한 개요를 제공합니다. view controller의 사용 및 구현에 대한 자세한 내용은 [iOS용 뷰 컨트롤러 프로그래밍 가이드](https://melodyarchive.gitbook.io/sagwa/not-found)를 참조하십시오.

### 뷰 관리

각 view controller는 view 계층 구조를 관리하며 루트 뷰는 이 클래스의 view 프로퍼티에 저장됩니다. 루트 뷰는 주로 나머지 view 계층 구조의 컨테이너 역할을 합니다. 루트 뷰의 크기와 위치는 해당 view를 소유한 객체\(상위 view controller 또는 앱의 window\)에 의해 결정됩니다. window가 소유하고있는 view controller는 앱의 루트 뷰 컨트롤러이며 view의 크기는 window를 채울 수 있는 정도로 조정됩니다.

view controller는 소유한 view를 곧바로 로드하지 않습니다. view는 해당 프로퍼에 처음 액세스할때 로드 또는 생성됩니다. view controller의 view를 지정하는 방법에는 여러가지가 있습니다.

* [스토리보드](https://melodyarchive.gitbook.io/sagwa/not-found)에 view controller와 view를 지정하세요. 스토리보드는 view를 지정하는 기본 방법입니다. 스토리보드를 사용해서 view와 view controller에 대한 해당 관계를 설정할 수 있습니다. 또한 view controller 사이의 관계와 하위 뷰를 지정하면 앱 동작을 보고 수정하는 것이 더 쉬워집니다.  스토리보드에서 view controller를 로드하려면 [UIStoryboard](https://melodyarchive.gitbook.io/sagwa/not-found) 객체의 [instantiateViewController \(withIdentifier :\)](https://melodyarchive.gitbook.io/sagwa/not-found) 메서드를 호출하십시오. UIStoryboard 객체는 view controller를 생성하여 코드에 반환합니다.
* [Nib 파일](https://melodyarchive.gitbook.io/sagwa/not-found)을 사용하여 view controller에 대한 view를 지정하세요. nib 파일을 사용하면 단일 view controller의 view를 지정할 수 있지만 view controller 사이의 segue 또는 관계를 정의할 수는 없습니다. nib 파일은 view controller 자체에 대한 최소한의 정보만 저장합니다.  nib 파일을 사용하여 view controller 객체를 초기화하려면 view controller 클래스를 프로그래밍 방식으로 만들고 [init \(nibName : bundle :\)](https://melodyarchive.gitbook.io/sagwa/not-found) 메서드를 사용하여 초기화하세요. view가 요청되면 view controller는 nib 파일에서 view를 로드합니다.
* [loadView\(\)](https://melodyarchive.gitbook.io/sagwa/not-found) 메서드를 사용하여 view controller의 view를 지정하세요. 이 방법에서는 뷰 계층 구조를 프로그래밍 방식으로 만들고 해당 계층 구조의 루트 뷰를 view controller의 view 프로퍼티에 할당합니다.

이러한 모든 방법은 적절한 view의 집합을 만들어 view 프로퍼티를 통해 노출한다는 점에서 같은 결과를 만들어냅니다.

{% hint style="warning" %}
중요

view controller는 view와 view가 생성하는 모든 하위 뷰의 유일한 소유자입니다. 또한 view controller는 view를 생성하거나 \(view controller 자체가 릴리즈 될 때와 같이\) 소유권을 반환하는 일에 있어서 책임이 있습니다. view 객체를 스토리보드나 nib 파일에 저장하는 경우 각 view controller 객체는 view 객체를 요청받을때 자동적으로 해당 뷰의 사본을 가져옵니다.  
하지만 view를 수동적으로 생성한다면 각 view controller는 반드시 고유한 view 집합을 소유하고 있어야 합니다. view controller간에는 view를 공유할 수 없습니다.
{% endhint %}

view controller의 루트 뷰는 항상 할당된 공간에 딱 맞게 크기가 조정됩니다. 인터페이스 빌더를 통해 자동 레이아웃 제약 조건을 지정하면 계층 구조상의 각 view가 상위 뷰의 범위 내에서 배치되고 크기가 조정되는 방식을 제어할 수 있습니다. 또한 제약 조건을 프로그래밍적으로 생성하고 적절한 때에 추가하는 것도 가능합니다. 제약 조건을 만드는 방법에 대한 자세한 내용은 [자동 레이아웃 가이드](https://melodyarchive.gitbook.io/sagwa/not-found)를 참조하십시오.

## 뷰 관련 Notification 처리

View가 나타나거나 사라지면 컨트롤러는 자동적으로 자체 메서드를 호출하여 하위 클래스가 변동사항에 응답할 수 있도록 합니다. [viewWillAppear \( :\)](https://melodyarchive.gitbook.io/sagwa/not-found)와 같은 메서드를 사용하여 화면에 표시 할 뷰를 준비하고 [viewWillDisappear \( :\)](https://melodyarchive.gitbook.io/sagwa/not-found)를 사용하여 변경 내용이나 다른 상태 정보를 저장합니다. 상황에 따라 적절한 메서드를 사용하세요.  
  
그림 1은 view에서 가능한 visibility 상태와 상태 전환을 보여줍니다.  
모든 'will' 콜백 메서드가 'done' 콜백 메서드와 쌍을 이루는 것은 아닙니다. 'will'콜백 메서드로 프로세스를 시작하면 해당 'did'와 반대 'will'콜백 메서드 모두에서 프로세스를 종료해야합니다.

![&#xADF8;&#xB9BC; 1. &#xC0C1;&#xD0DC; &#xC804;&#xD658; &#xB2E4;&#xC774;&#xC5B4;&#xADF8;&#xB7A8;](../../.gitbook/assets/image.png)

## 뷰 회전 처리

iOS 8부터 모든 회전 관련 메서드는 더 이상 사용되지 않습니다. 대신에 회전은 view controller의 view 크기가 변경되는 이벤트로 간주되므로 [viewWillTransition\(to:with:\)](https://melodyarchive.gitbook.io/sagwa/not-found) 메서드를 통해 보고됩니다. 인터페이스 방향이 변경되면 UIKit은 윈도우의 루트 view controller에서 이 메서드를 호출합니다. 그런 다음 해당보기 컨트롤러는 하위 view controller에 알리고 view controller 계층 전체에 메시지를 전파합니다.

iOS 6 및 iOS 7에서 앱은 Info.plist 파일에 정의된 인터페이스 방향을 지원합니다. view controller는 [supportedInterfaceOrientations](https://melodyarchive.gitbook.io/sagwa/not-found) 메서드를 오버라이드하여 지원하는 방향 리스트를 제한할 수 있습니다. 일반적으로 시스템은 이 메서드를 윈도우의 루트 view controller 또는 전체 화면을 채우기 위해 제공된 view controller에서만 호출합니다. 하위 view controller는 상위 view controller가 화면상에서 제공하는 부분을 사용할 뿐 회전모드의 지원 여부에는 영향을 줄 수 없습니다. 앱의 오리엔테이션 마스크와 view controller의 오리엔테이션 마스크의 교차점은 view controller를 어느 방향으로 회전시킬지 결정하는데 사용됩니다.

특정 방향으로 화면을 표시하고 싶은 경우 해당 view controller의 [preferredInterfaceOrientationForPresentation](https://melodyarchive.gitbook.io/sagwa/not-found)를 오버라이드하면 됩니다.

표시중인 view controller에 대해 회전이 발생하면 [willRotate\(to:datation:\)](https://melodyarchive.gitbook.io/sagwa/not-found), [willAnimateRotation\(to:duration:\)](https://melodyarchive.gitbook.io/sagwa/not-found) 및 [doneRotate\(from:\)](https://melodyarchive.gitbook.io/sagwa/not-found) 메서드가 회전 중에 호출됩니다. [viewWillLayoutSubviews\(\)](https://melodyarchive.gitbook.io/sagwa/not-found) 메서드는 view의 크기가 조정되고 상위 항목에 의해 배치된 후에 호출됩니다. 회전시 view controller가 표시되지 않으면 회전 메서드가 호출되지 않습니다. 그러나 view가 표시되는 중이라면 [viewWillLayoutSubviews\(\)](https://melodyarchive.gitbook.io/sagwa/not-found) 메서드가 호출됩니다. 이 메서드를 구현하면 [statusBarOrientation](https://melodyarchive.gitbook.io/sagwa/not-found) 메서드를 호출하여 기기 방향을 결정할 수 있습니다.

{% hint style="info" %}
알림

앱이 시작될 때 앱은 반드시 세로 방향으로 인터페이스를 설정해야 합니다. 앱이 상술된 메커니즘에 따라 화면을 회전시키는 것은 [application\(\_:didFinishLaunchingWithOptions:\)](https://melodyarchive.gitbook.io/sagwa/not-found)가 값을 리턴한 이후부터 적용됩니다.
{% endhint %}

### 컨테이너 뷰 컨트롤러 구현

UIViewController의 하위 커스텀 클래스는 컨테이너 뷰 컨트롤러로도 동작할 수 있습니다. 컨테이너 뷰 컨트롤러는 소유한 하위 view controller에 대한 컨텐츠 표시를 관리합니다. 하위 view는 그대로 표시되거나 컨테이너 뷰 컨트롤러가 소유한 다른 view와 함께 표시될 수 있습니다.

컨테이너 뷰 컨트롤러 하위 클래스는 해당 하위 클래스를 연결할 공개 인터페이스를 선언해야 합니다. 이러한 메서드의 특성은 개발자에게 달려 있으며, 생성하는 컨테이너의 시멘틱에 따라 달라집니다. 이에 따라 컨테이너에 하위 항목이 몇개나 표시되어야 할지, 언제 표시되어야 할지, 뷰 계층의 어느 위치에서 보여질지를 결정해야 합니다. view controller 클래스는 하위 view가 공유하는 관계를 정의합니다. 컨테이너에 대한 공개 인터페이스를 깔끔하게 설정하면 컨테이너의 동작 방법에 대한 비공개 구현 정보에 액세스하지 않고도 하위 컨트롤러가 논리적으로 기능을 사용할 수 있습니다.

하위 루트 뷰를 뷰 계층에 추가하기 전에 컨테이너 뷰 컨트롤러가 하위 뷰 컨트롤러를 연결해야 합니다. 이렇게 하면 iOS에서 이벤트를 하위 뷰 컨트롤러로 올바르게 라우팅하고 해당 컨트롤러가 관리하는 뷰를 볼 수 있습니다. 마찬가지로 하위 루트 뷰를 뷰 계층에서 제거한 후에는 해당 하위 뷰 컨트롤러의 연결을 끊어야 합니다. 이 연결을 만들거나 끊으려면 컨테이너가 기본 클래스에서 정의한 특정 메서드를 호출해야 합니다. 이러한 메서드는 컨테이너 클래스의 클라이언트가 호출하는 것이 아니라, 예상되는 containment 동작을 제공하기 위해 컨테이너의 구현에서만 사용됩니다.

자주 사용되는 필수 메서드들:

* [addChildViewController\(\_:\)](https://melodyarchive.gitbook.io/sagwa/not-found)
* [removeFromParentViewController\(\)](https://melodyarchive.gitbook.io/sagwa/not-found)
* [willMove\(toParentViewController:\)](https://melodyarchive.gitbook.io/sagwa/not-found)
* [didMove\(toParentViewController:\)](https://melodyarchive.gitbook.io/sagwa/not-found)

{% hint style="info" %}
알림

컨테이너 뷰 컨트롤러를 만들때 필수적으로 오버라이드 해야 할 메서드가 있는 것은 아닙니다.

기본적으로 회전 및 appearance 콜백은 자동적으로 하위 항목에 전달됩니다.  
선택적으로 [whichAutomaticallyForwardRotationMethods\(\)](https://melodyarchive.gitbook.io/sagwa/not-found) 및 [automaticallyForwardAppearanceMethods](https://melodyarchive.gitbook.io/sagwa/not-found) 메서드를 오버라이드하여 이 동작을 직접 제어할 수 있습니다.
{% endhint %}

### 메모리 관리

메모리는 iOS에서 중요한 리소스이며, view controller는 중요한 시간에 메모리 공간을 줄일 수 있는 built-in 기능을 지원합니다. UIViewController 클래스는 불필요한 메모리를 해제하는 [didReceeMemoryWarning\(\)](https://melodyarchive.gitbook.io/sagwa/not-found) 메서드를 통해 낮은 메모리 상태를 자동으로 처리합니다.

### 상태 보존과 복구

view controller의 [restorationIdentifier](https://melodyarchive.gitbook.io/sagwa/not-found)\(복원 식별자\) 속성에 값을 할당하면, 앱이 백그라운드로 전환될 때 시스템이 view controller에 인코딩을 요청할 수 있습니다. 요청에 따라 보존이 일어나는 경우 view controller는 restorationIdentifier가 있는 뷰 계층의 뷰를 보존합니다. view controller는 다른 상태를 자동으로 저장하지 않습니다. 커스텀 컨테이너 뷰 컨트롤러를 구현한다면 모든 하위 뷰 컨트롤러를 직접 인코딩해야 하고 인코딩될 각 하위 항목은 고유한 restorationIdentifier가 있어야 합니다.

시스템이 보존 또는 복원할 view controller를 결정하는 방법에 대한 자세한 내용은 [iOS용 앱 프로그래밍 가이드](https://melodyarchive.gitbook.io/sagwa/not-found)를 참조하십시오.

## 주제

### 프로그래밍적으로 View Controller 생성하기

* init\(nibName: String?, bundle: Bundle?\) 지정된 번들에 nib 파일이 포함된 새로 초기화한 뷰 컨트롤러를 반환합니다.
* init?\(coder: NSCoder\)

### 스토리보드와 Segue로 상호작용

* _var_ storyboard: UIStoryboard? view controller가 시작된 스토리보드
* _func_ shouldPerformSegue\(withIdentifier: String, sender: Any?\) 지정된 식별자의 segue를 수행할지 결정합니다.
* _func_ prepare\(for: UIStoryboardSegue, sender: Any?\) Segue가 수행되고 있음을 View Controller에 알립니다.
* _func_ performSegue\(withIdentifier: String, sender: Any?\) 지정된 식별자의 segue를 수행합니다.
* _func_ allowedChildViewControllersForUnwinding\(from: UIStoryboardUnwindSegueSource\) unwind segue 목적지가 될 수 있는 하위 view controller들의 배열을 반환합니다.
* _func_ childViewControllerContaining\(UIStoryboardUnwindSegueSource\) unwind segue의 소스를 포함한 하위 view controller를 반환합니다. 
* _func_ canPerformUnwindSegueAction\(Selector, from: UIViewController, withSender: Any\) view controller에서 호출되어 unwind action에 응답하길 원하는지 확인합니다.
* _func_ unwind\(for: UIStoryboardSegue, towardsViewController: UIViewController\) unwind segue를 통해 새 view controller로 전환하고자 할때 호출됩니다.

### View 관리

* _var_ view: UIView! 컨트롤러가 관리하는 뷰
* _var_ isViewLoaded: Bool 뷰가 현재 메모리에 로드 되었는지를 나타내는 값
* _func_ loadView\(\) 컨트롤러가 관리하는 뷰를 생합니다.
* _func_ viewDidLoad\(\) 컨트롤러의 뷰가 메모리에 로드 된 후에 호출됩니다.
* _func_ loadViewIfNeeded\(\) 아직 로드되지 않은 view controller의 view를 로드합니다.
* _var_ viewIfLoaded: UIView? 뷰가 로드된 상태에서는 view를, 아니라면 nil을 나타냅니다.
* _var_ title: String? 해당 컨트롤러가 관리하는 뷰를 나타내는 지역화 문자열
* _var_ preferredContentSize: CGSize 뷰 컨트롤러 뷰에 대한 기본 크기

### View Controller 표시하기

* _var_ modalPresentationStyle: UIModalPresentationStyle 모달 view controller의 presentation 스타일
* _var_ modalTransitionStyle: UIModalTransitionStyle view controller가 나타날때 사용되는 전환 스타일
* _var_ isModalInPopover: Bool view controller가 팝 오버 모달로 표시되어야 하는지 여부를 나타내는 Boolean 값
* _func_ show\(UIViewController, sender: Any?\) 주 컨텍스트에서 view controller를 표시합니다.
* _func_ showDetailViewController\(UIViewController, sender: Any?\) 보조\(디테일\) 컨텍스트에서 view controller를 표시합니다.
* _func_ present\(UIViewController, animated: Bool, completion: \(\(\) -&gt; Void\)? = nil\) view controller를 모달 방식으로 표시합니다.
* _func_ dismiss\(animated: Bool, completion: \(\(\) -&gt; Void\)? = nil\) 모달 방식으로 표시된 view controller를 닫습니다.
* _var_ definesPresentationContext: Bool 해당 프로퍼티를 소유한 view controller 또는 하위 view controller가 나타날때 새로 나타나는 뷰가 이 view controller의 view를 가리도록 만들것인지를 나타내는 값
* _var_ providesPresentationContextTransitionStyle: Bool 새로 나타나는 view controller에 context view controller의 전환 스타일을 제공할 것인지 나타내는 값
* _var_ disablesAutomaticKeyboardDismissal: Bool 컨트롤을 변경할 때 현재 input view가 자동으로 사라지게 할것인지를 나타내는 값

### 커스텀 화면 전환과 표시

* _var_ transitioningDelegate: UIViewControllerTransitioningDelegate? 전환 애니메이터, 상호작용 컨트롤러, custom presentation 컨트롤러 객체를 제공하는 delegate 객체
* _var_ transitionCoordinator: UIViewControllerTransitionCoordinator? 활성화된 transition coordinator 객체
* _func_ targetViewController\(forAction: Selector, sender: Any?\) 동작에 응답하는 view controller를 반환한다.
* _var_ presentationController: UIPresentationController? 현재 view controller를 관리하는 가장 가까운 presentation 컨트롤러
* _var_ popoverPresentationController: UIPopoverPresentationController? 현재 view controller를 관리하는 가장 가까운 popover presentation 컨트롤러
* _var_ restoresFocusAfterTransition: Bool 이전에 focus 상태였었던 item이 다시 보여졌을때 자동적으로 focus 상태로 되돌려져야 할지를 나타내는 값

### View 이벤트에 응답하기

* _func_ viewWillAppear\(Bool\) view controller가 view 계층에 추가될 것임을 알린다.
* _func_ viewDidAppear\(Bool\) view controller가 view 계층에 추가되었음을 알린다.
* _func_ viewWillDisappear\(Bool\) view controller가 view 계층에서 제거될 것임을 알린다.
* _func_ viewDidDisappear\(Bool\) view controller가 view 계층에서 제거되었음을 알린다.
* _var_ isBeingDismissed: Bool view controller가 해제되는 중인지를 알려주는 
* _var_ isBeingPresented: Bool view controller가 나타나는 중인지를 알려주는 
* _var_ isMovingFromParentViewController: Bool view controller가 상위 view controller에서 제거되는 중인지를 나타내는 값
* _var_ isMovingToParentViewController: Bool view controller가 상위 view controller로 들어가고 있는지를 나타내는 값

### View Safe Area 확장



### View Margin 관리하기



### View 레이아웃 동작 설정



### View 회전 설정



### 환경 변화에 적응하기



### 인터페이스 스타일 조정



### 커스텀 컨테이너 내의 하위 View Controller 관리



### 컨테이너에 포함하는 이벤트에 응답



### 연관된 다른 View Controller 얻기



### 메모리 경고 처리



### 상태 복구 관리



### 앱 확장 지원



### 3D터치 미리보기, 미리보기 퀵 액션과 작업하기



### 시스템 제스처 인식기로 조정



### 상태바 관리



### 제스처 설정



### 네비게이션 인터페이스 설정



### 탭바 아이템 설정



### 뷰 컨트롤러에 에디팅 동작 추가하기



### 사용가능한 키 커맨드에 접근



### Nib 파일 정보 얻기



### 상수Constants



### 알림Notification



### 지원중단Deprecated



## 연관 문서

### 상속받은 상위 클래스



### 준수하는 프로토콜

### 

