---
description: 앱의 데이터를 구조화하고 클립보드에서 공유하세요
---

# 문서, 데이터와 클립보드

> 원문 출처  
> [https://developer.apple.com/documentation/uikit/documents\_data\_and\_pasteboard](https://developer.apple.com/documentation/uikit/documents_data_and_pasteboard)

## 주제

### 문서 <a id="documents"></a>

* _class_ UIDocument

  앱 데이터의 개별 부분을 관리하기위한 추상 기본 클래스

* _class_ UIManagedDocument

  Core Data와 통합되는 관리문서 객체

### 데이터 관리 <a id="data-management"></a>

* _protocol_ UIDataSourceModelAssociation 앱 데이터 객체에 대한 지속적인 참조가 가능하도록 인터페이스를 정의하는 메서드 집합

### 클립보드\(pasteboard\)

* _class_ UIPasteboard

  사용자가 앱 내에서 또는 앱에서 다른 앱으로 데이터를 공유할 수 있도록 도와주는 객체

* _class_ UIPasteConfiguration 드래그 앤 드롭 작업을 위해 객체가 구현하는 인터페이스입니다. 특정 데이터 형식을 받아들이는 기능을 선언합니다.
* _protocol_ UIPasteConfigurationSupporting

  응답자 객체의 붙여넣기 설정 지원 여부를 결정하는 인터페이스입니다.

## 같이 보기

* [앱과 환경](app-and-environment/) 라이프 사이클 이벤트와 앱 UI Scene을 관리하고 특성과 앱이 실행중인 환경에 대한 정보를 얻으세요
* 리소스 관리 메인 실행 파일 외부에 저장된 이미지, 문자열, 스토리 보드 및 nib 파일을 관리하세요
* 앱 확장

  앱의 기본 기능을 시스템의 다른 부분으로 확장하세요

* 프로세스 간 통신 Handoff를 통해서 데이터를 공유하고 유니버설 링크로 앱의 컨텐츠를 지원하며 행동기반의 서비스를 사용자에게 보여주세요
* Mac Catalyst 맥 기기에서 사용자가 실행할 수 있는 버전의 아이패드 앱을 만드세요.

