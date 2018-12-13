# 번들 프로그래밍 가이드

> 원문출처  
> [https://developer.apple.com/library/archive/documentation/CoreFoundation/Conceptual/CFBundles/Introduction/Introduction.html\#//apple\_ref/doc/uid/10000123i-CH1-SW1](https://developer.apple.com/library/archive/documentation/CoreFoundation/Conceptual/CFBundles/Introduction/Introduction.html#//apple_ref/doc/uid/10000123i-CH1-SW1)

## 소개

번들은 코드와 리소스를 캡슐화하는 데 사용되는 MacOS와 iOS의 기본 기술입니다. 번들은 복합 바이너리 파일을 만들 필요성을 완화시키면서 필요한 리소스에 대해 알려진 위치를 제공함으로써 개발자 경험을 단순화합니다. 대신 번들은 디렉토리와 파일을 사용하여 보다 자연스러운 유형의 조직을 제공합니다. 개발 중과 구축 후 모두 쉽게 수정할 수 있습니다.

번들을 지원하기 위해, 코코아와 Core Foundation은 번들 내용에 액세스하기 위한 프로그래밍 인터페이스를 제공합니다. 번들은 조직된 구조를 사용하기 때문에 모든 개발자가 번들의 기본 구성 원칙을 이해하는 것이 중요합니다. 이 문서는 리소스 파일에 액세스하기 위해 개발 중에 번들이 작동하는 방식과 번들을 사용하는 방법을 이해할 수 있는 기반을 제공합니다.

## 문서 구성

본 문서는 다음과 같은 챕터로 구성되어 있습니다:

* [번들에 대해](about-bundles.md) 번들 및 패키지의 개념과 시스템에서의 사용방법을 소개합니다.
* [번들 구조](bundle-structures.md)

  표준 번들 타입의 구조와 컨텐츠를 설명합니다.

* [번들 컨텐츠 액세스  ](../../etc/not-found.md) Cocoa 및 Core Foundation 인터페이스를 사용하여 번들과 그 내용에 대한 정보를 얻는 방법을 보여줍니다.
* [문서 패키지](../../etc/not-found.md)

  문서 패키지에 대한 개념\(번들과 느슨하게 관련되어 있음\)과 사용방법에 대해 설명합니다.

## 같이 보기

본 문서의 정보는 모든 유형의 번들에 적용됩니다. 그러나 \(프레임워크나 플러그인과 같은\) 좀더 전문화된 번들 유형을 사용하는 경우 다음 문서도 참조하는 것이 좋습니다:

* 프레임워크 프로그래밍 가이드 커스텀 프레임워크를 생성하고 사용하는 방법에 대해 자세한 정보를 제공합니다.
* Code Loading Programming Topics Objective-C로 플러그인 작성하는 방법에 대한 정보를 제공합니다.
* 플러그인 프로그래밍   C 언어로 플러그인 작성하는 방법에 대한 정보를 제공합니다.

