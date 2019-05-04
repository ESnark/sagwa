---
description: 정보를 브로드캐스팅하고 받아보는 방법에 대한 디자인 패턴.
---

# Notification

> 원문 출처  
> [https://developer.apple.com/documentation/foundation/notifications](https://developer.apple.com/documentation/foundation/notifications)

## 주제

### Key-Value Observing

* [NSKeyValueObserving](nskeyvalueobserving.md) 다른 객체의 특정 속성의 변경이 있을 때 알림을 받기 위해서 객체가 채택하는 비공식적인 프로토콜

### Notifications

* struct Notification 등록된 모든 Observer에게 Notification Center\(알림 센터\)를 통해 브로드캐스트되는 정보 컨테이너
* class NotificationCenter 등록된 Observer에게 정보를 브로드캐스트 할 수 있는 notification 발송 매커니즘
* class NotificationQueue 알림 센터 버퍼

### 프로세스 간 노티피케이션

* class DistributedNotificationCenter 태스크 경계를 넘어서 notification을 브로드캐스트 할 수 있는 notification 발송 매커니즘

## 같이 보기

### 앱 지

* [작업 관리](../task-management/)

  사용자와 시스템간 상호 작용과 앱 작업을 관리합니다.

* [리소스](../resources/)

  앱에 번들되어 있는 Asset 과 기타 데이터에 액세스할 수 있습니다.

* 앱 확장 지원

  앱 확장과 호스팅 앱 간의 상호 작용을 관리합니다.

* 오류 및 예외

  API와의 상호 작용에서 문제 상황에 대응하고 더 나은 디버깅을 위해 애플리케이션을 미세 조정합니다.

* 스크립팅 지원

  사용자가 AppleScript 및 기타 자동화 기술로 프로그램을 제어하거나 앱 내에서 스크립트를 실행할 수 있도록 합니다.

