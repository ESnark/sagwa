# Threading 프로그래밍 가이드

> 원문 출처  
> [https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/Multithreading/Introduction/Introduction.html\#//apple\_ref/doc/uid/10000057i-CH1-SW1](https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/Multithreading/Introduction/Introduction.html#//apple_ref/doc/uid/10000057i-CH1-SW1)

## Introduction

스레드는 단일 응용 프로그램 내에서 동시에 여러 코드 경로를 실행할 수있는 여러 기술 중 하나입니다. operation 객체나 Grand Central Dispatch\(GCD\)와 같은 최신 기술들도 동시성을 구현하기 위한 더 현대적이고 효율적인 인프라를 제공하지만 OS X과 iOS에서는 스레드를 생성하고 관리하는 인터페이스 또한 제공되고 있습니다.

이 문서는 OS X에서 사용가능한 스레드 패키지들에 대한 소개와 사용방법을 제공합니다. 또한 스레딩 및 멀티 스레드 코드의 동기화를 지원하는 관련 기술에 대해서도 설명합니다.

{% hint style="info" %}
Important

새로운 어플리케이션을 개발하고 있다면 동시성 구현을 위해 OS X의 대안적인 기술을 탐색하는 것이 권장됩니다. 특히 스레드 어플리케이션을 구현하는데 필요한 디자인 테크닉에 익숙하지 못한 경우에 권장됩니다. 이러한 대안 기술들은 동시적인 실행경로를 구현하는데 필요한 작업량을 단순화시켜주며 전통적인 스레딩보다 더 나은 성능을 제공합니다. 이러한 기술들에 대한 자세한 정보는 [동시성 프로그래밍 가이드](https://developer.apple.com/library/archive/documentation/General/Conceptual/ConcurrencyProgrammingGuide/Introduction/Introduction.html#//apple_ref/doc/uid/TP40008091) 문서를 참조하세요.
{% endhint %}

### 본 문서의 목차

이 문서는 다음 챕터와 부록으로 구성되어 있습니다:

* [About Threaded Programming](about-threaded-programming.md) 문서는 스레드의 개념과 그것이 어플리케이션 디자인에서 하는 역할에 대해 소개합니다.
* [Thread Management](thread-management.md) 문서는 OS X의 스레딩 기술에 대한 정보와 그것을 어떻게 사용하는지에 대한 정보를 제공합니다.
* Run Loops 문서는 event-processing 루프를 부차적인 스레드에서 관리하는 방법을 제공합니다.
* Synchronization 문서는 다중 스레드가 데이터나 프로그램을 손상시키지 않도록 하기 위해 사용하는 도구 및 동기화 이슈에 대해 설명합니다.
* Thread Safety Summary는 OS X과 iOS의 고유한 스레드 안전성과 핵심 프레임워크에 대한 높은 수준의 요약을 제공합니다.

### 같이 보기

스레드의 대안에 대한 정보는 [동시성 프로그래밍 가이드](https://developer.apple.com/library/archive/documentation/General/Conceptual/ConcurrencyProgrammingGuide/Introduction/Introduction.html#//apple_ref/doc/uid/TP40008091)를 참조하세요.

이 문서는 POSIX 스레드 API의 사용에 대한 간단한 설명만을 제공합니다. 사용 가능한 POSIX 스레드 루틴에 대한 자세한 내용은 [pthread](https://developer.apple.com/library/archive/documentation/System/Conceptual/ManPages_iPhoneOS/man3/pthread.3.html#//apple_ref/doc/man/3/pthread) 매뉴얼 페이지를 참조하세요. POSIX 스레드와 그 사용법에 대한 자세한 설명은 David R. Butenhof의 _Programming with POSIX Threads_을 참조하세요.

