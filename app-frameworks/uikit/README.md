# UIKit

> 원문 출처  
> [https://developer.apple.com/documentation/uikit](https://developer.apple.com/documentation/uikit)

## 개요 <a id="overview"></a>

UIKit 프레임워크는 iOS 또는 tvOS 앱에 필요한 인프라를 제공합니다.  
인터페이스 구현을 위한 window 및 view 아키텍쳐, 애플리케이션에 멀티 터치 및 기타 유형의 입력을 제공하는 이벤트 처리 인프라와 사용자, 시스템 및 앱 간의 상호 작용을 관리하는 데 필요한 기본 실행 루프를 제공합니다.

프레임워크가 제공하는 다른 기능으로는 애니메이션 지원, 문서 지원, 그리기 및 인쇄 지원, 현재 기기에 대한 정보, 텍스트 관리 및 디스플레이, 검색 지원, 접근성 지원, 앱 확장 지원 및 리소스 관리가 있습니다.

{% hint style="warning" %}
중요

별도로 명시되지 않은 한, 앱의 메인 스레드 또는 메인 디스패치 큐에서만 UIKit 클래스를 사용하십시오. 이 제한은 특히 UIResponder를 상속받았거나 앱의 사용자 인터페이스를 조작하는 클래스에 적용됩니다.
{% endhint %}

## 주제 <a id="topics"></a>

### 첫 시작 <a id="first_steps"></a>

* [UIKit으로 앱 개발](about_app_development_with_uikit.md) iOS/tvOS 앱 개발을 위해 UIKit과 Xcode가 제공하는 기본기능에 대해서 알아보세요
* 유저 사생활 보호 사용자 데이터를 보호하며, 데이터 용도에 대한 사용자 설정을 따라주세요

### 앱 구조 <a id="app_structure"></a>

UIKit은 앱과 시스템의 상호작용을 관리하고 앱의 데이터 및 리소스를 관리할 수 있는 클래스를 제공합니다.

* [앱과 환경](app-and-environment/) 라이프 사이클 이벤트와 앱 UI Scene을 관리하고 특성과 앱이 실행중인 환경에 대한 정보를 얻으세요.
* [문서, 데이터와 클립보드](documents-data-pasteboard.md) 앱의 데이터를 구조화하고 클립보드에서 공유하세요.
* 리소스 관리 메인 실행 파일 외부에 저장된 이미지, 문자열, 스토리 보드 및 nib 파일을 관리하세요.
* 앱 확장

  앱의 기본 기능을 시스템의 다른 부분으로 확장하세요.

* 프로세스 간 통신 Handoff를 통해서 데이터를 공유하고 유니버설 링크로 앱의 컨텐츠를 지원하며 행동기반의 서비스를 사용자에게 보여주세요.
* [Mac Catalyst](mac-catalyst.md) 맥 기기에서 사용자가 실행할 수 있는 버전의 아이패드 앱을 만드세요.

### 유저 인터페이스 <a id="user_interface"></a>

View는 화면에 내용을 표시하고 사용자 상호 작용을 용이하게 합니다. View Controller는 뷰와 인터페이스 구조를 관리하는데 도움이 됩니다.

* [뷰와 컨트롤](views_and_controls/) 화면에 컨텐츠를 표시하고 해당 컨텐츠에 상호작용을 지정하세요.
* [View Controllers](view-controllers/) View Controller로 인터페이스를 관리하고 앱 컨텐츠 탐색을 수월하게 만드세요.
* 뷰 레이아웃 Stack View를 사용해서 인터페이스를 자동으로 배치하고 View를 정교하게 배치해야 하는 경우 자동 레이아웃을 사용하세요.
* Appearance Customization Add Dark Mode support to your app, customize the appearance of bars, and use appearance proxies to modify your UI.
* [애니메이션과 햅틱](animation-and-haptics/) 뷰 기반 애니메이션 햅틱을 사용하여 사용자에게 피드백을 제공합니다.
* 윈도우와 스크린

   뷰 계층 구조 및 기타 컨텐츠를 위한 컨테이너를 제공합니다.

### 유저 상호작용 <a id="user_interactions"></a>

Responder와 gesture recognizer는 터치, 키보드 입력 또는 다른 이벤트의 처리를 돕습니다. 드래그앤 드롭, 포커스, peek&pop 또는 접근성 도구들을 사용해서 다른 유형의 상호작용을 처리하세요

* [터치, 누르기, 제스쳐](touches_presses_and_gestures/) 제스처 인식기에서 앱의 이벤트 처리 로직을 캡슐화하여 앱 전체에서 해당 코드를 재사용 할 수 있습니다.
* 드래그 앤 드롭 View와 상호작용 API를 사용해서 앱에서 드래그 앤 드롭 기능을 사용하세요.
* 펜슬 상호작용 애플 펜슬의 더블 탭 동작을 처리하세요.
* 포커스 기반 네비게이션

   원격 또는 게임 컨트롤러를 사용해서 UIKit 앱 인터페이스를 탐색합니다.

* 메뉴와 단축키 메뉴 시스템, 컨텍스트 메뉴, 홈 화면 퀵 액션과 키보드 단축키를 이용하여 앱의 상호작용을 단순화하세요.
* 접근성 도구 장애인을 포함한 모든 사용자가 앱에 접근하도록 만드세요.

### 그래픽, 드로잉, 프린팅 <a id="graphics_drawing_and_printing"></a>

UIKit은 드로잉 환경을 구성하고 콘텐츠를 렌더링하는데 도움이 되는 클래스와 프로토콜을 제공합니다.

* 이미지와 PDF 비트맵을 포함한 각종 이미지와 PDF를 생성하고 관리합니다.
* 그리기

   렌더러를 사용하여 앱의 드로잉 환경을 구성하고 경로, 문자열 및 그림자를 그립니다.

* 프린팅

   시스템 인쇄 패널을 표시하고 인쇄 프로세스를 관리합니다.

### 텍스트 <a id="text"></a>

UIKit에는 텍스트를 앱에 쉽게 표시할수 있는 텍스트 뷰 외에도 시스템 키보드를 지원하는 사용자 정의 텍스트 관리 및 렌더링 기능이 있습니다.

* 텍스트 디스플레이와 폰트 UIKit View를 사용해서 텍스트를 표시하고 폰트를 관리하고 맞춤법 검사를 할 수 있습니다.
* 텍스트 스토리지 텍스트 스토리지를 관리하고 텍스트 레이아웃을 조정합니다.
* 키보드와 입력

   시스템 키보드를 설정하거나 직접 키보드를 만들고 입력을 처리하세요.

### Deprecated <a id="d"></a>

더 이상 사용되지 않는 클래스와 프로토콜들

* Deprecated Symbols

### 구조체 <a id="structures"></a>

* _struct_ NSDiffableDataSourceSnapshot

### 클래스

* _class_ UIActivityItemsConfiguration
* _class_ UITitlebar

### 프로토콜

* _protocol_ UIActivityItemsConfigurationReading
* _protocol_ UIContextMenuInteractionAnimating

### Reference

* UIKit Enumerations
* UIKit 상수
* UIKit 함수
* UIKit 데이터 타입

