---
description: macOS의 시스템 기능상 장점을 취하면서 여러분의 아이패드 앱을 맥 앱에 가깝게 만들어 보세요
---

# 아이패드 앱의 맥 최적화

> 원문 출처  
> [https://developer.apple.com/documentation/uikit/mac\_catalyst/optimizing\_your\_ipad\_app\_for\_mac](https://developer.apple.com/documentation/uikit/mac_catalyst/optimizing_your_ipad_app_for_mac)

## Summary

> **Framework**
>
> * UIKit

## 개요 <a id="overview"></a>

맥 버전으로 만들어진 iPad 앱은 별다른 노력을 기울이지 않아도 다음과 같은 macOS의 시스템 기능들을 지원합니다:

* 앱 기본 메뉴바
* 트랙패드, 마우스, 키보드 입력 지원
* 윈도우 리사이징과 풀 스크린 디스플레이 지원
* 맥 스타일 스크롤 바
* 복사 붙여넣기 지원
* 드래그 앤 드롭 지원
* 시스템 터치바 컨트롤 지원

그 외에도 더 많은 시스템 기능들을 개발자가 확장 지원할 수 있습니다.

{% hint style="warning" %}
중요

Mac Catalyst로 빌드된 맥 앱은 Mac Catalyst에서 사용 가능한 것으로 명시된 [AppKit](../../../etc/not-found.md) API만 사용할 수 있습니다. \(Ex. [NSToolbar](../../../etc/not-found.md), [NSTouchBar](../../../etc/not-found.md)\) Mac Catalyst는 사용할 수 없는 AppKit API에 대한 액세스를 지원하지 않습니다.
{% endhint %}

## 메뉴바 항목 추가 <a id="add-menu-bar-items"></a>

맥 버전의 앱은 기본적으로 표준 메뉴바를 제공합니다. [UIMenuBuilder](../../../etc/not-found.md)를 사용해서 메뉴를 추가하거나 삭제하는 등의 커스텀이 가능합니다. 더 알고 싶으시면 [메뉴바와 UI에 메뉴 및 단축키 추가](../../../etc/not-found.md) 문서를 읽어보세요.

## 설정창 표시 <a id="show-a-preferences-window"></a>

맥 앱은 일반적으로 설정창을 통해 사용자가 앱 설정을 바꿀 수 있게 해줍니다. 유저는 메뉴바의 환경설정 항목을 클릭해서 이 창을 볼수 있습니다. 여러분의 앱이 Settings 번들을 가지고 있다면 시스템이 알아서 환경설정 창을 제공할 것입니다. 더 알고 싶으시면 [설정창 표시](../../../etc/not-found.md) 문서를 읽어보세요.

## Primary 뷰 컨트롤러에 반투명 배경효과 적용 <a id="apply-a-translucent-background-to-your-primary-view-controller"></a>

스플릿 뷰 컨트롤러를 사용하는 아이패드 앱은 macOS에서 맥 스타일의 스플릿 뷰를 사용할 수 있습니다. 그러나 아이패드 앱을 더 맥 앱처럼 만드려면 데스크탑 배경을 블러처리하여 Primary 뷰 컨트롤러의 배경으로 사용하는 반투명 효과를 사용해보세요. 적용하려면 스플릿 뷰 컨트롤러의 [primaryBackroundStyle](../../../etc/not-found.md)을 [UISplitViewController.BackgroundStyle.sidebar](../../../etc/not-found.md)로 설정하면 됩니다.

> 반투명 배경을 primary 뷰 컨트롤러에 적용하는 예시

```swift
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {

    let splitViewController = window!.rootViewController as! UISplitViewController
    let navigationController = splitViewController.viewControllers[splitViewController.viewControllers.count-1] as! UINavigationController
    navigationController.topViewController!.navigationItem.leftBarButtonItem = splitViewController.displayModeButtonItem
    
    // 반투명 배경을 primary 뷰 컨트롤러에 적용합니다.
    splitViewController.primaryBackgroundStyle = .sidebar
    
    splitViewController.delegate = self
    
    return true
}
```

## 뷰에서 포인터 감지 <a id="detect-the-pointer-in-a-view"></a>

맥 사용자는 텍스트 필드를 선택하거나 창을 옮기는 등 앱과 상호작용하기 위해서 포인터에 의존합니다. 사용자가 포인터를 UI 요소들 위로 움직일때 몇몇 요소들은 모습을 바꿉니다. 예를 들어, 웹 브라우저에서 포인터가 링크위에 올라가면 링크는 하이라이트됩니다.

사용자가 앱 내 뷰에서 포인터를 움직이는 것을 감지하기 위해서는 해당 뷰에 [UIHoverGestureRecognizer](../../../etc/not-found.md)가 추가되어야 합니다. 이 인식기는 포인터가 뷰에 들어오거나 나갈때, 또는 그 위를 움직이는 동안 앱에게 그 사실을 알려줍니다.

> 포인터가 버튼 위를 움직일 때 버튼의 기본 색상을 빨간색으로 바꾸는 예시

```swift
class ViewController: UIViewController {


    @IBOutlet var button: UIButton!


    override func viewDidLoad() {
        super.viewDidLoad()


        let hover = UIHoverGestureRecognizer(target: self, action: #selector(hovering(_:)))
        button.addGestureRecognizer(hover)
    }


    @objc
    func hovering(_ recognizer: UIHoverGestureRecognizer) {
        switch recognizer.state {
        case .began, .changed:
            button.titleLabel?.textColor = #colorLiteral(red: 1, green: 0, blue: 0, alpha: 1)
        case .ended:
            button.titleLabel?.textColor = UIColor.link
        default:
            break
        }
    }
}
```

## 같이 보기 <a id="see-also"></a>

### App Support

* 맥 앱의 User Interface Idiom 선택  Mac Catalyst로 만들어진 Mac 앱에서 iPad UI Idiom과 Mac UI Idiom 중에 하나를 선택하세요

