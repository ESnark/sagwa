---
description: 앱 모델 내 데이터 흐름과 변경을 제어하고 대응합니다
---

# 상태와 데이터 흐름

> 원문 출처  
> [https://developer.apple.com/documentation/swiftui/state\_and\_data\_flow](https://developer.apple.com/documentation/swiftui/state_and_data_flow)

## Summary

> **Framework**
>
> * SwiftUI

## Overview

State와 Binding은 View를 앱에 내재한 데이터 모델과 연결시킵니다.  SwiftUI는 선언된 State를 저장하고 해당하는 View와의 연결을 관리합니다. State가 업데이트 되면 View는 현재 모습을 무효화하고 자체적으로 업데이트합니다. 또한 애니메이션을 State에 연결하여 변경 사항에 따라 View를 애니메이션 할 수 있습니다.

State 멤버 변수를 각 View에 연결하는 Binding을 생성하세요. Binding은 양방향 연결을 제공하여 화면상의 컨트롤로 State를 변경할 수 있습니다. Binding에는 View 간에 값을 전달하는 트랜잭션 기능도 포함되어 있습니다.

## 주제 <a id="topics"></a>

### Essentials

* 사용자 입력 처리 Landmark 앱에서 사용자는 좋아하는 장소를 표시하고 해당 장소들만 볼 수 있는 리스트를 볼 수 있습니다. 이 기능을 만들기 위해서 사용자들에게 리스트를 필터링 하는 스위치와 좋아하는 장소를 표시할 수 있는 별 모양 버튼을 추가할 것입니다.

### Bindings

* struct Binding 값을 변경할 수 있는 관리자

### Data-Dependent Views

* struct State View가 읽고 모니터 할 수 있는 지속적인 값 
* struct ObservedObject
* struct EnvironmentObject 동적 View 속성으로써, 조상 View로부터 제공받아 사용하는 바인딩 가능한 객체이며 언제든지 변경이 일어나면 현재의 View를 무효화합니다.
* struct FetchRequest
* struct FetchedResults
* protocol DynamicProperty View의 외부 속성을 업데이트하는 저장된 변수

### Environment Values

* struct Environment View의 환경으로부터 읽어오는 동적 View 속성
* struct EnvironmentValues 환경값의 collection

### Preferences

* protocol PreferenceKey View에서 생성된 기명 값
* struct LocalizedStringKey 문자열 파일이나 문자열 dictionary 파일로부터 문자열을 검색하는데 사용되는 키

### Transactions

* struct Transaction 현재 State 프로세싱 업데이트의 컨텍스트

## 같이 보기 <a id="see-also"></a>

### 데이터와 이벤트 <a id="data-and-events"></a>

* 제스처 탭, 클릭, 스와이프부터 세부 제스처까지 상호작용을 정의하세요

