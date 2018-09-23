---
description: 사용자와 시스템간 상호 작용과 앱 작업을 관리합니다.
---

# 작업 관리

> 원본출처  
> [https://developer.apple.com/documentation/foundation/task\_management](https://developer.apple.com/documentation/foundation/task_management)

## 주제

### Undo

* _class_ UndoManager

  실행 취소와 다시 실행 작업을 가능하게 하는 범용 레코더

### Progress

* _protocol_ ProgressReporting

  단일 progress 인스턴스를 사용하여 진행률을 보고하는 객체의 인터페이스

* _class_ Progress

  지정된 작업에 대해 진행 상황을 사용자에게 전달하는 객체

### Operations

* _class_ [Operation](operation.md)

  단일 태스크와 관련된 코드 및 데이터를 나타내는 추상 클래스

* _class_ [OperationQueue](operationqueue.md)

  작업 실행을 제어하는 대기열\(queue\)

* _class_ BlockOperation

  한 개 이상의 블록의 동시 실행을 관리하는 operation

### Scheduling

* _class_ Timer

  특정 시간 간격이 경과한 후 호출되어 지정된 메세지를 target 객체에 보낸다.

### 액티비티 공유

* class NSUserActivity

  앱의 상태를 한번에 보여줍니다.

* protocol NSUserActivityDelegate

  UserActivity 인스턴스가 인스턴스의 delegate에게 업데이트를 알리는 인터페이스

### 시스템 상호작용

* class ProcessInfo

  현재 프로세스에 대한 정보 컬렉션

* class NSBackgroundActivityScheduler

  백그라운드에서 실행할 수 있는 낮은 우선 순위 작업에 적합한 작업 스케줄러

### 유저 노티피케이션

* ~~class NSUserNotification~~

  ~~A notification that can be scheduled for display in the notification center.~~

  `Deprecated`

* ~~class NSUserNotificationAction~~

  ~~An action that the user can take in response to receiving a notification.~~

  `Deprecated`

* ~~class NSUserNotificationCenter~~

  ~~An object that delivers notifications from apps to the user.~~

  `Deprecated`

* protocol NSUserNotificationCenterDelegate

  기본 노티피케이션 센터의 동작을 커스터마이징 할 수 있는 인터페이스

## 같이 보기

### 앱 지원

* 리소스

  앱에 번들되어 있는 Asset 과 기타 데이터에 액세스할 수 있습니다.

* Notification

  정보를 브로드캐스팅하고 받아보는 방법에 대한 디자인 패턴.

* 앱 확장 지원

  앱 확장과 호스팅 앱 간의 상호 작용을 관리합니다.

* 오류 및 예외

  API와의 상호 작용에서 문제 상황에 대응하고 더 나은 디버깅을 위해 애플리케이션을 미세 조정합니다.

* 스크립팅 지원

  사용자가 AppleScript 및 기타 자동화 기술로 프로그램을 제어하거나 앱 내에서 스크립트를 실행할 수 있도록 합니다.

