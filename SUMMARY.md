# Table of contents

* [애플 개발자 문서 한글 번역](README.md)

## App Frameworks

* [Foundation](app-frameworks/foundation/README.md)
  * [숫자, 데이터와 기본값](app-frameworks/foundation/numbers-data-and-basic-value.md)
  * [문자열과 텍스트](app-frameworks/foundation/strings-and-text.md)
  * [컬렉션](app-frameworks/foundation/collections.md)
  * [날짜와 시간](app-frameworks/foundation/dates-and-times.md)
  * [데이터 포맷](app-frameworks/foundation/data-formatting.md)
  * [작업 관리](app-frameworks/foundation/task-management/README.md)
    * [Operation](app-frameworks/foundation/task-management/operation.md)
    * [OperationQueue](app-frameworks/foundation/task-management/operationqueue.md)
    * [Timer](app-frameworks/foundation/task-management/timer.md)
  * [리소스](app-frameworks/foundation/resources/README.md)
    * [Bundle](app-frameworks/foundation/resources/bundle.md)
  * [파일 시스템](app-frameworks/foundation/file-system/README.md)
    * [FileManager](app-frameworks/foundation/file-system/filemanager.md)
  * [Notification](app-frameworks/foundation/notification/README.md)
    * [NSKeyValueObserving](app-frameworks/foundation/notification/nskeyvalueobserving.md)
  * [URL 로딩 시스템](app-frameworks/foundation/url-loading-system/README.md)
    * [웹사이트 데이터를 메모리에 저장하기](app-frameworks/foundation/url-loading-system/fetching-website-data-into-memory.md)
    * [URLSession](app-frameworks/foundation/url-loading-system/urlsession/README.md)
      * [URLSessionConfiguration](app-frameworks/foundation/url-loading-system/urlsession/urlsessionconfiguration/README.md)
        * [urlCache](app-frameworks/foundation/url-loading-system/urlsession/urlsessionconfiguration/urlcache.md)
        * [requestCachePolicy](app-frameworks/foundation/url-loading-system/urlsession/urlsessionconfiguration/requestcachepolicy.md)
      * [configuration](app-frameworks/foundation/url-loading-system/urlsession/configuration.md)
    * [URLSessionTask](app-frameworks/foundation/url-loading-system/urlsessiontask.md)
    * [URLRequest](app-frameworks/foundation/url-loading-system/urlrequest.md)
    * [URLResponse](app-frameworks/foundation/url-loading-system/urlresponse.md)
    * [HTTPURLResponse](app-frameworks/foundation/url-loading-system/httpurlresponse.md)
    * [캐시 데이터에 접근하기](app-frameworks/foundation/url-loading-system/accessing-cached-data.md)
    * [CachedURLResponse](app-frameworks/foundation/url-loading-system/cachedurlresponse.md)
    * [URLCache](app-frameworks/foundation/url-loading-system/urlcache.md)
  * [Object Runtime](app-frameworks/foundation/object-runtime/README.md)
    * [NSValue](app-frameworks/foundation/object-runtime/nsvalue.md)
* [UIKit](app-frameworks/uikit/README.md)
  * [UIKit으로 앱 개발](app-frameworks/uikit/about_app_development_with_uikit.md)
  * [앱과 환경](app-frameworks/uikit/app-and-environment/README.md)
    * [앱 라이프 사이클 관리하기](app-frameworks/uikit/app-and-environment/managing_your_app_s_life_cycle.md)
    * [앱 실행에 대응하기](app-frameworks/uikit/app-and-environment/responding_to_the_launch_of_your_app.md)
    * [UIApplication](app-frameworks/uikit/app-and-environment/uiapplication.md)
  * [문서, 데이터와 클립보드](app-frameworks/uikit/documents-data-pasteboard.md)
  * [Mac Catalyst](app-frameworks/uikit/mac-catalyst/README.md)
    * [iPad 앱을 Mac 버전으로 만들기](app-frameworks/uikit/mac-catalyst/creating-a-mac-version-of-your-ipad-app.md)
    * [아이패드 앱의 맥 최적화](app-frameworks/uikit/mac-catalyst/optimizing-your-ipad-app-for-mac.md)
  * [뷰와 컨트롤](app-frameworks/uikit/views_and_controls/README.md)
    * [UIView](app-frameworks/uikit/views_and_controls/uiview.md)
    * [Table Views](app-frameworks/uikit/views_and_controls/table-views/README.md)
      * [UITableView](app-frameworks/uikit/views_and_controls/table-views/uitableview.md)
      * [UITableViewCell](app-frameworks/uikit/views_and_controls/table-views/uitableviewcell.md)
      * [UIRefreshControl](app-frameworks/uikit/views_and_controls/table-views/uirefreshcontrol.md)
    * [UIScrollView](app-frameworks/uikit/views_and_controls/uiscrollview.md)
  * [View Controllers](app-frameworks/uikit/view-controllers/README.md)
    * [UIViewController](app-frameworks/uikit/view-controllers/uiviewcontroller.md)
    * [UITableViewController](app-frameworks/uikit/view-controllers/uitableviewcontroller.md)
    * [UISearchController](app-frameworks/uikit/view-controllers/uisearchcontroller.md)
  * [애니메이션과 햅틱](app-frameworks/uikit/animation-and-haptics/README.md)
    * [프로퍼티 기반 애니메이션](app-frameworks/uikit/animation-and-haptics/property-based-animations/README.md)
      * [UIViewPropertyAnimator](app-frameworks/uikit/animation-and-haptics/property-based-animations/uiviewpropertyanimator.md)
    * [View controller 전환](app-frameworks/uikit/animation-and-haptics/view-controller.md)
  * [터치, 누르기, 제스처](app-frameworks/uikit/touches_presses_and_gestures/README.md)
    * [UIResponder](app-frameworks/uikit/touches_presses_and_gestures/uiresponder.md)
    * [UIKit 제스처 처리](app-frameworks/uikit/touches_presses_and_gestures/handling_uikit_gestures.md)
    * [다중 제스처 인식기 조정](app-frameworks/uikit/touches_presses_and_gestures/coordinating-multiple-gesture-recognizers.md)
    * [UILongPressGestureRecognizer](app-frameworks/uikit/touches_presses_and_gestures/uilongpressgesturerecognizer.md)
    * [UIPanGestureRecognizer](app-frameworks/uikit/touches_presses_and_gestures/uipangesturerecognizer/README.md)
      * [maximumNumberOfTouches](app-frameworks/uikit/touches_presses_and_gestures/uipangesturerecognizer/maximumnumberoftouches.md)
      * [minimunNumberOfTouches](app-frameworks/uikit/touches_presses_and_gestures/uipangesturerecognizer/minimunnumberoftouches.md)
      * [translation\(in:\)](app-frameworks/uikit/touches_presses_and_gestures/uipangesturerecognizer/translation-in.md)
      * [setTranslation\(\_:in:\)](app-frameworks/uikit/touches_presses_and_gestures/uipangesturerecognizer/settranslation-_-in.md)
      * [velocity\(in:\)](app-frameworks/uikit/touches_presses_and_gestures/uipangesturerecognizer/velocity-in.md)
    * [UIGestureRecognizer](app-frameworks/uikit/touches_presses_and_gestures/uigesturerecognizer.md)
* [Swift](app-frameworks/swift/README.md)
  * [스위프트 표준 라이브러리](app-frameworks/swift/swift-standard-library/README.md)
    * [메모리 직접 관리](app-frameworks/swift/swift-standard-library/manual-memory-management/README.md)
      * [포인터 파라미터를 사용하는 함수 호출](app-frameworks/swift/swift-standard-library/manual-memory-management/calling-functions-with-pointer-parameters.md)
      * [UnsafePointer](app-frameworks/swift/swift-standard-library/manual-memory-management/unsafepointer.md)
      * [UnsafeMutableRawBufferPointer](app-frameworks/swift/swift-standard-library/manual-memory-management/unsafemutablerawbufferpointer.md)
* [SwiftUI](app-frameworks/swiftui/README.md)
  * [뷰와 컨트롤](app-frameworks/swiftui/views-and-controls/README.md)
    * [View](app-frameworks/swiftui/views-and-controls/view.md)
    * [Text](app-frameworks/swiftui/views-and-controls/text.md)
    * [TextField](app-frameworks/swiftui/views-and-controls/textfield.md)
  * [뷰 레이아웃과 표현](app-frameworks/swiftui/view-layout-and-presentation.md)
  * [그리기와 애니메이션](app-frameworks/swiftui/drawing-and-animation.md)
  * [프레임워크 통합](app-frameworks/swiftui/framework-intergration.md)
  * [상태와 데이터 흐름](app-frameworks/swiftui/state-and-data-flow.md)

## Graphics and Games

* [Core Animation](graphics-and-games/core-animation/README.md)
  * [CALayer](graphics-and-games/core-animation/calayer.md)
  * [CAAction](graphics-and-games/core-animation/caaction.md)
  * [CAShapeLayer](graphics-and-games/core-animation/cashapelayer.md)
  * [CADisplayLink](graphics-and-games/core-animation/cadisplaylink.md)
* [Core Graphics](graphics-and-games/core-graphics/README.md)
  * [CGFloat](graphics-and-games/core-graphics/cgfloat.md)
  * [CGPath](graphics-and-games/core-graphics/cgpath.md)

## App Services

* [Combine](app-services/combine.md)
* [WebKit](app-services/webkit/README.md)
  * [WKWebView](app-services/webkit/wkwebview.md)

## Media

* [AVFoundation](media/avfoundation/README.md)
  * [시스템 오디오 상호작용](media/avfoundation/system-audio-interaction/README.md)
    * [AVAudioSession](media/avfoundation/system-audio-interaction/avaudiosession/README.md)
      * [AVAudioSession.Category](media/avfoundation/system-audio-interaction/avaudiosession/avaudiosession.category/README.md)
        * [ambient](media/avfoundation/system-audio-interaction/avaudiosession/avaudiosession.category/ambient.md)
        * [multiRoute](media/avfoundation/system-audio-interaction/avaudiosession/avaudiosession.category/untitled.md)
        * [playAndRecord](media/avfoundation/system-audio-interaction/avaudiosession/avaudiosession.category/playandrecord.md)
        * [playback](media/avfoundation/system-audio-interaction/avaudiosession/avaudiosession.category/playback.md)
        * [record](media/avfoundation/system-audio-interaction/avaudiosession/avaudiosession.category/record.md)
        * [soloAmbient](media/avfoundation/system-audio-interaction/avaudiosession/avaudiosession.category/soloambient.md)
      * [AVAudioSession.Mode](media/avfoundation/system-audio-interaction/avaudiosession/avaudiosession.mode.md)
  * [AVFoundation 자료형](media/avfoundation/avfoundation.md)

## Documentation Archive

* [번들 프로그래밍 가이드](documentation-archive/bundle-programming-guide/README.md)
  * [번들에 대해](documentation-archive/bundle-programming-guide/about-bundles.md)
  * [번들 구조](documentation-archive/bundle-programming-guide/bundle-structures.md)
* [Key-Value Observing 프로그래밍 가이드](documentation-archive/key-value-observing.md)
* [Threading 프로그래밍 가이드](documentation-archive/threading-programming-guide/README.md)
  * [About Threaded Programming](documentation-archive/threading-programming-guide/about-threaded-programming.md)
  * [Thread Management](documentation-archive/threading-programming-guide/thread-management.md)

## ETC

* [Not Found](etc/not-found.md)

