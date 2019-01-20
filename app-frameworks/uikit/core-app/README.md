# Core App

> 원문 출처  
> [https://developer.apple.com/documentation/uikit/core\_app](https://developer.apple.com/documentation/uikit/core_app)

## 주제

### Application

* [앱 라이프 사이클 관리하기](managing_your_app_s_life_cycle.md) 앱 delegate가 앱의 상위 수준 동작을 관리하는 방식을 이해합니다.
* _class_ [UIApplication](uiapplication.md) iOS에서 실행되는 앱의 제어와 조정의 중심점
* _protocol_ UIApplicationDelegate 앱 라이프 타임동안 발생하는 중요한 이벤트에 대해 응답하기 위해서 UIApplication 싱글턴 객체가 호출하는 메서드 세트
* 앱과 웹에서 컨텐츠에 링크하도록 허용하기 유니버설 링크를 사용하여 앱 내의 콘텐츠에 연결하고 데이터를 안전하게 공유하세요
* _func_ UIApplicationMain\(Int32, UnsafeMutablePointer?&gt;, String?, String?\) -&gt; Int32 어플리케이션 객체와 delegate를 생성하고 이벤트 사이클을 설정합니다.

### 기기 환경

* 애플 TV에서의 디스플레이 모드 변경에 대응하기 기기 변경에 의 화면 색역 변경에 따라 이미지와 리소스를 동적으로 변경시킵니다.
* _class_ UIDevice 현재 기기 표시
* _class_ UITraitCollection 수평 및 수직 사이즈 클래스, 디스플레이 스케일 및 사용자 인터페이스 종류\(phone, pad, tv 등\)와 같은 특성에 의해 정의된 앱용 iOS 인터페이스 환경.
* _protocol_ UITraitEnvironment 앱에서 iOS 인터페이스 환경을 사용할 수 있도록 하는 메서드 집합
* _protocol_ UIAdaptivePresentationControllerDelegate 프레젠테이션 컨트롤러와 함께 앱의 특성 변화에 대응하는 방법을 결정하는 메서드 집합

### 문서

* _class_ UIDocument

  앱 데이터의 개별 부분을 관리하기위한 추상 기본 클래스

* _class_ UIManagedDocument

  Core Data와 통합되는 관리문서 객체

### 클립보드\(Pasteboard\)

* _class_ UIPasteboard

  사용자가 앱 내에서 또는 앱에서 다른 앱으로 데이터를 공유할 수 있도록 도와주는 객체

* _class_ UIPasteConfiguration 드래그 앤 드롭 작업을 위해 객체가 구현하는 인터페이스입니다. 특정 데이터 형식을 받아들이는 기능을 선언합니다.
* _protocol_ UIPasteConfigurationSupporting

  응답자 객체의 붙여넣기 설정 지원 여부를 결정하는 인터페이스입니다.

### 데이터 관리

* 사용자 개인정보 보호 개인 데이터를 보호하고 데이터 용도에 대한 사용자 요구를 존중하여 사용자 개인정보를 보호합니다.
* _protocol_ UIDataSourceModelAssociation 앱 데이터 객체에 대한 지속적인 참조가 가능하도록 인터페이스를 정의하는 메서드 집합

### 유저 활동

* _class_ NSUserActivity

  앱의 상태를 한 번에 표시합니다.

* _protocol_ UIUserActivityRestoring

### 서비스

* _class_ UIActivity

  앱 특화 서비스를 구현하기 위해 상속하는 추상 클래스

* _class_ UIActivityViewController 앱에서 표준 서비스를 제공하기 위해서 사용하는 view controller
* _protocol_ UIActivityItemSource

  activity view controller가 작업할 데이터 항목을 검색하는데 사용되는 메서드 집합

* _class_ UIActivityItemProvider

  activity view controller에 데이터를 전달하는 프록시

### 엑세스 안내

* _protocol_ UIGuidedAccessRestrictionDelegate

  개발자가 Guided Access 기능에 커스텀 제한사항을 추가하는데 사용되는 메서드 집합

* _static func_ guidedAccessRestrictionState\(forIdentifier: String\) -&gt; UIAccessibility.GuidedAccessRestrictionState

  지정된 Guided access 제한에 대한 제한 상태를 반환합니다.

## 같이 보기

### 앱 구조

* 리소스 관리 메인 실행 파일 외부에 저장된 이미지, 문자열, 스토리 보드 및 nib 파일을 관리하세요
* 앱 확장 앱의 기본 기능을 시스템의 다른 부분으로 확장하세요



