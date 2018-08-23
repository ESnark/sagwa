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

## 뷰 관련 Notification 처리



## 뷰 회전 처리



### 컨테이너 뷰 컨트롤러 구현



### 메모리 관리



### 상태 보존과 복구



## 주제

### 프로그래밍적으로 View Controller 생성하기



### 스토리보드와 Segue로 상호작용



### View 관리



### View Controller 표시하기



### 커스텀 화면 전환과 프레젠테이션



### View 이벤트에 응답하기



### View Safe Area 확장



### View Magin 관리하기



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

