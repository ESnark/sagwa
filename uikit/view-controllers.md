---
description: View Controller로 인터페이스를 관리하고 앱 컨텐츠 탐색을 수월하게 만드세요
---

# View Controllers

## 개요

View Controller는 UIKit 앱의 인터페이스를 관리합니다. View Controller는 단일 루트 뷰를 관리하고 단일 뷰에는 여러 개의 하위 뷰가 포함될 수 있습니다.  
이와 같은 뷰 계층구조와의 유저 상호작용은 View Controller에 의해서 처리되며 View Controller는 필요에 따라 앱의 다른 객체와 함께 조율됩니다.  
앱 컨텐츠가 화면에 표시할 수 있는 것보다 많은 경우 여러개의 View Controller를 사용해서 컨텐츠를 나누어 관리하는 것이 좋습니다.

**컨테이너 뷰 컨트롤러**는 다른 뷰 컨트롤러의 내용을 자체 루트 뷰에 포함합니다. 컨테이너 뷰 컨트롤러는 탐색을 용이하게하거나 고유한 인터페이스를 만들기 위해 커스텀 뷰에 하위 View Controller 컨텐츠를 혼합 할 수 있습니다.  
예를 들어, UINavigationController 객체는 네비게이션 바와 하위 View Controller 스택 \(한 번에 하나씩만 표시됨\)을 관리하고 스택에서 하위 View Controller를 추가하거나 제거하는 API를 제공합니다.

UIKit은 특정 유형의 콘텐츠를 탐색하고 관리하기 위한 몇 개의 표준 View Controller를 제공합니다. 앱의 사용자 지정 콘텐츠를 포함하는 뷰 컨트롤러를 정의합니다. 또한 사용자 정의 컨테이너 뷰 컨트롤러를 정의하여 새 탐색 체계를 구현할 수도 있습니다.

