---
description: View Controller로 인터페이스를 관리하고 앱 컨텐츠 탐색을 수월하게 만드세요.
---

# View Controllers

> 원문 출처[  
> https://developer.apple.com/documentation/uikit/view\_controllers](https://developer.apple.com/documentation/uikit/view_controllers)

## 개요

View Controller는 UIKit 앱의 인터페이스를 관리합니다. View Controller는 단일 루트 뷰를 관리하고 단일 뷰에는 여러 개의 하위 뷰가 포함될 수 있습니다.  
이와 같은 뷰 계층구조와의 유저 상호작용은 View Controller에 의해서 처리되며 View Controller는 필요에 따라 앱의 다른 객체와 함께 조율됩니다.  
앱 컨텐츠가 화면에 표시할 수 있는 것보다 많은 경우 여러개의 View Controller를 사용해서 컨텐츠를 나누어 관리하는 것이 좋습니다.

**컨테이너 뷰 컨트롤러**는 다른 뷰 컨트롤러의 내용을 자체 루트 뷰에 포함합니다. 컨테이너 뷰 컨트롤러는 탐색을 용이하게하거나 고유한 인터페이스를 만들기 위해 커스텀 뷰에 하위 View Controller 컨텐츠를 혼합 할 수 있습니다.  
예를 들어, UINavigationController 객체는 네비게이션 바와 하위 View Controller 스택 \(한 번에 하나씩만 표시됨\)을 관리하고 스택에서 하위 View Controller를 추가하거나 제거하는 API를 제공합니다.

UIKit은 특정 유형의 콘텐츠를 탐색하고 관리하기 위한 몇 개의 표준 View Controller를 제공합니다. 앱의 커스텀 콘텐츠를 포함하는 뷰 컨트롤러와 커스텀 컨테이너 뷰 컨트롤러를 정의하여 새 네비게이션 체계를 구현할 수도 있습니다.

## 주제

### 커스텀 뷰 컨트롤러

커스텀 인터페이스를 관리하기 위해서 view controller를 상속합니다.

* _class_ [UIViewController](uiviewcontroller.md) UIKit 앱의 View 계층구조를 관리하는 객체
* _class_ [UITableViewController](uitableviewcontroller.md) Table View 관리에 특화된 view controller
* _class_ UICollectionViewController Collection View 관리에 특화된 view controller
* _protocol_ UIContentContainer view controller의 컨텐츠를 뷰 사이즈와 제약사항에 맞게 조정하는 메서드들

### 스플릿 뷰 컨트롤러

* _class_ UISplitViewController master-detail 인터페이스를 구현하는 컨테이너 뷰 컨트롤러

### 네비게이션 인터페이스

* _class_ UINavigationController 계층적 컨텐츠를 탐색하기 위한 스택기반 스키마를 정의하는 컨테이너 뷰 컨트롤러
* _class_ UINavigationBar 탐색 컨트롤러와 함께 화면 상단에 주로 표시되는 네비게이션 바
* _class_ UINavigationItem 연관된 뷰 컨트롤러가 화면에 나타날때 화면 네비게이션 바에 나타나는 항목

### 페이지 뷰 인터페이스

* _class_ UIPageViewController

  하위 뷰 컨트롤러로 컨텐츠 페이지와 페이지의 탐색을 관리하는 컨테이너 뷰 컨트롤러

### 탭 뷰 인터페이스

* _class_ UITabBarController 라디오 스타일의 선택 인터페이스를 관리하는 컨테이너 뷰 컨트롤러. 선택에 따라서 표시할 하위 뷰 컨트롤러가 결정됩니다.
* _class_ UITabBar 탭 바에 다른 하위 작업, 뷰 또는 모드를 선택할 수 있는 버튼을 표시하는 컨트롤
* _class_ UITabBarItem 탭 바의 항목

### 검색 인터페이스

* _class_ UISearchContainerViewController 인터페이스상의 검색결과 표시를 관리하는 view controller
* _class_ [UISearchController](uisearchcontroller.md) 검색창과의 상호작용을 기반으로 검색결과 표시를 관리하는 view controller
* _class_ UISearchBar 사용자로부터 검색 관련 정보를 받기위한 특수 뷰.
* _protocol_ UISearchResultsUpdating 사용자가 검색창에 입력한 정보를 기반으로 검색결과를 업데이트 할 수 있는 메서드들
* 검색 컨트롤러를 사용하여 검색가능한 컨텐츠 표시하기 검색가능한 컨텐츠와 테이블 뷰를 사용하여 사용자 인터페이스를 생성하세요

### 이미지와 비디오

* _class_ UIImagePickerController 사진을 찍고, 동영상을 녹화하고, 사용자의 미디어 라이브러리에서 항목을 선택하기 위한 시스템 인터페이스를 관리하는 view controller
* _class_ UIVideoEditorController 비디오 프레임을 편집하고 녹화된 동영상을 인코딩하기 위한 시스템 인터페이스를 관리하는 view controller

### 디렉토리 접근

* 문서 브라우저를 앱에 추가하기 사용자가 앱 내에서 로컬 또는 원격 문서에 액세스 할수 있도록 하세요
* 디렉토리 접근기능 제공 Document picker를 사용하여 앱 컨테이너 외부의 디렉토리 컨텐츠에 접근하세요
* 문서 브라우저 기반의 앱 빌드 문서 브라우저를 사용하여 사용자의 텍스트 파일에 대한 액세스를 제공하세요
* _class_ UIDocumentBrowserViewController 로컬 디바이스와 클라우드에 저장된 문서를 찾아보고 작업을 수행할 수 있는 view controller
* _class_ UIDocumentPickerViewController 앱 샌드박스 외부의 문서나 경로에 대한 액세스를 제공하는 view controller
* Document Browser View Controller에 기반한 앱 개발 다른 클라우드 저장소 공급자의 파일과의 사용자 상호 작용을 관리하는 사용자 지정 문서 파일 형식을 구현합니다.

### 문서 미리보기

* _class_ UIDocumentInteractionController 앱에서 직접 처리할 수 없는 파일 형식을 미리 보거나 열거나 인쇄하는 view controller

### iCloud 공유

* _class_ UICloudSharingController CloudKit 데이터베이스에 공유대상\(사람\)을 추가하거나 제거하기 위한 표준적인 화면을 제공하는 view controller

### 액티비티 인터페이스

* _class_ UIActivityViewController 앱에서 표준 서비스를 제공하는데 사용되는 view controller
* _class_ UIActivityItemProvider ActivityViewController에 전달되는 데이터의 프록시
* _protocol_ UIActivityItemSource ActivityViewController가 데이터를 검색하는데 사용하는 메서드들
* _class_ UIActivity 앱 특화 서비스를 구현하기 위해서 상속하는 추상 클래스

### Font Picker

* _class_ UIFontPickerViewController `Beta`
* _protocol_ UIFontPickerViewControllerDelegate `Beta`
* _class_ UIFontPickerViewControllerConfiguration `Beta`

### 단어 조회

* _class_ UIReferenceLibraryViewController 단어나 용어의 정의를 조회하기 위한 표준 인터페이스를 표시하는 view controller

### 프린터 선택

* _class_ UIPrinterPickerController 프린터 선택용 표준 인터페이스를 보여주는 view controller

### 프레젠테이션 컨트롤러

* Disabling Pulling Down a Sheet Disable the sheet pull-down gesture when dismissal would be destructive.
* _class_ UIPresentationController 전환 애니메이션과 화면상 view controller의 표시를 관리하는 객체

### 인터페이스 복원

* 앱 시작시 UI 유지하기 시스템에 의해서 앱이 종료된 이후에도 이전 상태를 반환합니다.
* _protocol_ UIViewControllerRestoration view controller들이 상태 복원중에 "복원 클래스"로 동작할수 있도록 객체가 채택하는 메서드들
* _protocol_ UIObjectRestoration 복원 클래스가 보존된 객체를 복원하는데 사용하는 인터페이스
* _protocol_ UIStateRestoring 상태 복원 아카이브에 객체를 추가하는 메서드들

### 인터페이스 방향

* _func_ UIInterfaceOrientationIsPortrait\(UIInterfaceOrientation\) 유저 인터페이스가 현재 세로 방향으로 표시되고 있는지 Boolean값을 반환하는 함수
* _func_ UIInterfaceOrientationIsLandscape\(UIInterfaceOrientation\) 유저 인터페이스가 현재 세로 방향으로 표시되고 있는지 Boolean값을 반환하는 함수

## 같이 보기

* [뷰와 컨트롤](../views_and_controls/) 화면에 컨텐츠를 표시하고 해당 컨텐츠에 상호작용을 지정하세요.
* 뷰 레이아웃 Stack View를 사용해서 인터페이스를 자동으로 배치하고 View를 정교하게 배치해야 하는 경우 자동 레이아웃을 사용하세요.
* Appearance Customization Add Dark Mode support to your app, customize the appearance of bars, and use appearance proxies to modify your UI.
* [애니메이션과 햅틱](../animation-and-haptics/) 뷰 기반 애니메이션 햅틱을 사용하여 사용자에게 피드백을 제공합니다.
* 윈도우와 스크린

   뷰 계층 구조 및 기타 컨텐츠를 위한 컨테이너를 제공합니다.

