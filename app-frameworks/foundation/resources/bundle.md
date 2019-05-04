---
description: 디스크의 번들 디렉토리에 저장된 코드와 리소스들을 나타냅니다.
---

# Bundle

> 원문 출처  
> [https://developer.apple.com/documentation/foundation/bundle](https://developer.apple.com/documentation/foundation/bundle)

## 개요

Apple은 번들을 사용하여 앱, 프레임워크, 플러그인 및 기타 여러 특정 유형의 콘텐츠를 나타냅니다. 번들은 포함된 리소스를 잘 정의된 하위 디렉터리로 구성하고 번들 구조는 번들 유형과 플랫폼 유형에 따라 달라집니다. 번들 객체를 사용하면 번들 리소스에 액세스할때 번들 구조를 알 필요가 없습니다. 번들 객체는 번들 구조, 사용자 기본 설정, 사용 가능한 지역화 및 기타 관련 요소를 고려하여 항목을 찾는 단일 인터페이스를 제공합니다.

모든 실행 파일은 번들 객체를 사용하여 앱 번들 내부나 다른 위치의 알려진 번들 내에서 리소스를 찾을 수 있습니다. 컨테이너 디렉토리나 파일 시스템의 다른 부분의 파일을 찾는데에는 소용이 없습니다.

번들 객체를 사용하는 일반적인 패턴은 다음과 같습니다:

1. 원하는 번들 디렉토리에 대한 번들 객체를 만듭니다.
2. 번들 객체 메서드를 사용하여 필요한 리소스를 찾거나 로드합니다.
3. 다른 시스템 API를 사용하여 리소스와 상호작용합니다.

자주 사용되는 리소스 타입 중 일부는 번들 없이 찾고 열수 있습니다. 예를 들어 이미지를 로드할 때 이미지를 Asset 카탈로그에 저장하고 [UIImage](../../../etc/not-found.md) 또는 [NSImage](../../../etc/not-found.md)의 [init\(named:\)](../../../etc/not-found.md) 메서드를 사용하여 로드합니다. 마찬가지로 문자열 리소스의 경우 [NSLocalizedString](../../../etc/not-found.md)을 사용하여 전체 .strings 파일을 직접 로드하는 대신 개별 문자열을 로드합니다.

{% hint style="info" %}
알림

\(NSString과 CFString과 같이\) Core Foundation 이름에 대응하는 다른 Foundation 클래스와는 다르게 Bundle 객체는 CFBundle 객체로 형변환될 수 없습니다. CFBundle의 기능을 제공하고자 한다면 CFBundle을 생성하고 CFBundle의 API를 사용할 수 있습니다. 더 자세한 내용은 [Toll-Free Bridging](../../../etc/not-found.md) 문서를 확인하세요.
{% endhint %}

## 번들을 찾고 열기

리소스를 찾으려면 먼저 리소스를 포함하는 번들을 지정해야 합니다. 번들 클래스에는 많은 생성자\(constructor\)가 있지만 가장 자주 사용하는 생성자는 [main](../../../etc/not-found.md)입니다. main 번들은 현재 실행 중인 코드가 포함된 번들 디렉토리를 나타냅니다. 따라서 앱의 경우 main 번들 객체를 통해 앱과 함께 제공된 리소스에 액세스할 수 있습니다.

앱이 플러그인, 프레임워크 또는 기타 다른 번들 콘텐츠와 직접적으로 상호작용하는 경우 이 클래스의 메서드를 사용하여 적절한 번들 객체를 생성할 수 있습니다. 알려진 URL 또는 경로에서 번들 개체를 만들 수도 있지만 다른 메서드를 사용하면 앱에서 이미 사용 중인 번들에 쉽게 액세스할 수 있습니다. 예를 들어, 프레임워크에 링크하는 경우 init\(for:\) 방법을 사용하여 해당 프레임워크에 정의된 클래스를 기준으로 프레임워크 번들을 찾을 수 있습니다.

```swift
// 앱의 main 번들 가져오기
let mainBundle = Bundle.main

// 특정 private 클래스를 포함하고 있는 번들 가져오기
let myBundle = Bundle(for: NSClassFromString("MyPrivateClass")!)
```

## 번들 내에 있는 리소스 찾기

번들 객체를 사용하여 번들 내에 있는 특정 리소스의 위치를 가져올 수 있습니다. 리소스를 찾기 위해서는 리소스의 이름과 타입이 필요하고 특정 하위 디렉토리에 있는 리소스에 대해서는 해당 디렉토리를 지정할수도 있습니다. 리소스를 찾은 후 번들 루틴은 파일을 여는데 사용할 수 있는 경로 문자열 또는 URL을 반환합니다.

```objectivec
NSBundle *main = [NSBundle mainBundle];
NSStrnig *resourcePath = [main pathForResource:@"Seagull" ofType:@"jpg"];
```

번들 객체는 디스크에서 리소스를 찾을때 특정 검색 패턴을 따릅니다. 글로벌 리소스\(즉, 언어별 .lproj 디렉토리에 속하지 않는 리소스\)가 먼저 반환된 다음 지역 및 언어별 리소스가 반환됩니다. 이 번들이 리소스를 찾는 검색패턴의 순서는 다음과 같습니다:

1. 글로벌 \(지역화되지 않은\) 리소스
2. 국가별 지역 리소스 \(사용자의 지역 기본설정 기준\)
3. 언어별 지역화된 리소스 \(사용자의 언어 기본설정 기준\)
4. 개발 언어 리소스\(번들의 Info.plist 파일 중 [CFBundleDevelopmentRegion](../../../etc/not-found.md) 키에 지정됨\)

글로벌 리소스가 언어별 리소스보다 우선하기 때문에 리소스의 글로벌 버전과 지역화된 버전을 앱에 모두 포함해서는 안 됩니다. 리소스의 글로벌 버전이 있으면 지역화 버전은 반환되지 않습니다. 이런 우선순위가 존재하는 이유는 성능 때문입니다. 지역화된 리소스를 먼저 검색한다면 번들 객체는 글로벌 리소스를 반환하기 전에 존재하지 않는 지역화된 리소스를 검색하는 데 시간을 낭비할 수 있습니다.

{% hint style="warning" %}
중요

번들 객체는 파일 시스템에서 대/소문자를 구분하지 않더라도 리소스 파일을 검색할때 항상 대/소문자를 구분합니다. 번들객체에서 파일 이름을 지정할 때에는 항상 대/소문자를 구분하세요.
{% endhint %}

번들 객체가 파일을 반환할 때에는 스스로 파일이름 수정자를 고려하여 결정합니다. 리소스는 특정 장치\(~iphone, ~ipad\) 또는 특정 화면 해상도\(@2x, @3x\)에 대해 태그를 지정할 수 있습니다. 원하는 리소스의 이름을 지정할 때 이러한 수정자를 포함하지 마세요. 번들 개체는 디바이스에 가장 적합한 파일을 알아서 선택합니다. 자세한 내용은 [iPhone, iPad 및 Apple Watch의 앱 아이콘](../../../etc/not-found.md)을 참조하세요.

## 번들 구조 이해하기

번들 구조는 타겟 플랫폼이나 번들 타입에 따라 달라집니다. Bundle 클래스는 \(전부는 아니지만\) 대부분의 경우 이러한 기본 구조를 숨깁니다. Bundle에서 리소스를 로드하는데 사용되는 많은 메서드들이 자동으로 적절한 시작 디렉토리를 찾고 알려진 위치에서 리소스를 찾습니다. 또한 Bundle 클래스의 메서드와 프로퍼티를 사용하여 알려진 번들 디렉토리의 위치를 가져오고 해당 디렉토리에서 특별히 리소스를 검색할 수 있습니다.

iOS 및 MacOS 앱의 번들 구조에 대한 자세한 내용은 [번들 프로그래밍 가이드](../../../etc/not-found.md)를 참조하세요.  
프레임워크 번들 구조에 대한 자세한 내용은 [프레임워크 프로그래밍 가이드](../../../etc/not-found.md)를 참조하세요. MacOS 플러그인의 구조에 대한 자세한 내용은 [Code Loading 프로그래밍](../../../etc/not-found.md) 항목을 참조하세요.

## 주제

### 표준 번들객체 가져오기

* class var main: Bundle

  현재 실행파일이 포함된 번들 객체를 반환합니다.

* class var allFrameworks: \[Bundle\]

  프레임워크를 나타내는 모든 애플리케이션 번들의 배열을 반환합니다.

* class var allBundles: \[Bundle\] 프레임워크가 아닌 모든 애플리케이션 번들의 배열을 반환합니다.

### 번들 생성과 초기화

* init\(for: AnyClass\) `for:` 클래스와 연관된 NSBundle 객체를 반환합니다.
* init?\(identifier: String\)

  `identifier:` 번들 식별자가 있는 NSBundle 인스턴스를 반환합니다.

* init?\(url: URL\)

  `url:` 파일 URL에 일치하는 NSBundle 객체를 초기화하여 반환합니다.Returns an NSBundle object initialized to correspond to the specified file URL. 

* init?\(path: String\)

  `path:` 디렉토리 경로와 일치하는 NSBundle 객체를 초기화하여 반환합니다.

### Nib 파일 로딩

* func loadNibNamed\(String, owner: Any?, options: \[UINib.OptionsKey : Any\]? = nil\) -&gt; \[Any\]?

  수신자의 번들에 있는 nib 파일을 불러옵니다.

* func loadNibNamed\(NSNib.Name, owner: Any?, topLevelObjects: AutoreleasingUnsafeMutablePointer?\) -&gt; Bool

  nib 파일 이름과 `owner:` 소유자 정보를 사용하여 nib을 번들에서 블러옵니다.

### 리소스 파일 찾기

* func url\(forResource: String?, withExtension: String?, subdirectory: String?\) -&gt; URL?

  `forResource:` 파일명과 `withExtension:` 확장명을 갖고 있는 파일을 `subdirectory:` 경로에서 찾아서 해당 URL을 반환합니다.

* func url\(forResource: String?, withExtension: String?\) -&gt; URL?

  `forResource:` 파일명과 `withExtension:` 확장명을 갖고 있는 파일의 URL을 반환합니다.

* func urls\(forResourcesWithExtension: String?, subdirectory: String?\) -&gt; \[URL\]?

  `subdirectory:` 경로에 있는 `forResourcesWithExtension:` 확장명을 갖고 있는 모든 파일들의 URL 배열을 반환합니다.

* func url\(forResource: String?, withExtension: String?, subdirectory: String?, localization: String?\) -&gt; URL? `subdirectory:` 경로에서 `forResource:` 파일명과 `withExtension:` 확장명을 갖는 파일들 중 `localization:` 에 맞는 지역화\(또는 글로벌\) 리소스 URL을 반환합니다.
* func urls\(forResourcesWithExtension: String?, subdirectory: String?, localization: String?\) -&gt; \[URL\]?

  `subdirectory:` 경로에서 `withExtension:` 확장명을 갖는 파일들 중 `localization:` 에 맞는 지역화\(또는 글로벌\) 리소스 URL 배열을 반환합니다.

* class func url\(forResource: String?, withExtension: String?, subdirectory: String?, in: URL\) -&gt; URL?

  `in:` URL을 갖는 번들에서 `forResource:` 파일명과 `withExtension:` 확장명을 갖는 파일을  `subdirectory:` 경로에 생성하고 URL을 반환합니다.

* class func urls\(forResourcesWithExtension: String?, subdirectory: String?, in: URL\) -&gt; \[URL\]?

  `in:` URL을 갖는 번들에서 `withExtension:` 확장명을 갖는 파일을  `subdirectory:` 경로에서 모두 찾아 해당 리소스들의 URL을 반환합니다.

* func path\(forResource: String?, ofType: String?\) -&gt; String?

  `forResource:` 파일명과 `ofType:` 확장명을 갖는 리소스를 찾아 해당 리소스의 전체 경로 문자열을 반환합니다.

* func path\(forResource: String?, ofType: String?, inDirectory: String?\) -&gt; String? `inDirectory:` 경로에서 `forResource:` 파일명과 `ofType:` 확장명을 갖는 리소스를 찾아 해당 리소스의 전체 경로 문자열을 반환합니다.
* func path\(forResource: String?, ofType: String?, inDirectory: String?, forLocalization: String?\) -&gt; String? `inDirectory:` 경로에서 `forResource:` 파일명과 `ofType:` 확장명을 갖는 리소스 중 `forLocaliztion:` 에 맞는 지역화\(또는 글로벌\) 리소스의 전체 경로 문자열을 반환합니다.
* func paths\(forResourcesOfType: String?, inDirectory: String?\) -&gt; \[String\]

  `inDirectory:` 경로에서 `ofType:` 확장명을 갖는 모든 리소스의 경로를 나타내는 문자열 배열을 반환합니다.

* func paths\(forResourcesOfType: String?, inDirectory: String?, forLocalization: String?\) -&gt; \[String\] `inDirectory:` 경로에서 `ofType:` 확장명을 갖는 리소스 중에서 `forLocalization:` 에 맞는 모든 지역화\(또는 글로벌\) 리소스의 경로를 나타내는 문자열 배열을 반환합니다.
* class func path\(forResource: String?, ofType: String?, inDirectory: String\) -&gt; String? `inDirectory:` 번들 디렉토리 경로에서 `forResource:` 파일명과 `ofType:` 확장명을 갖는 리소스의 전체 경로 문자열을 반환합니다.
* class func paths\(forResourcesOfType: String?, inDirectory: String\) -&gt; \[String\] `inDirectory:` 번들 디렉토리 경로에서 `ofType:` 확장명을 갖는 모든 리소스의 경로 문자열을 반환합니다.

### 이미지 리소스 찾기

* func urlForImageResource\(NSImage.Name\) -&gt; URL?

  주어진 이미지의 URL을 반환합니다.

* func pathForImageResource\(NSImage.Name\) -&gt; String?

  주어진 이미지의 경로 문자열을 반환합니다.

* func image\(forResource: NSImage.Name\) -&gt; NSImage?

  forResource: 이름에 해당하는 NSImage 인스턴스를 반환합니다. 이 인스턴스는 이미지의 다른 해상도 버전을 가리키는 여러 파일로 백업할 수 있습니다.

### 사운드 리소스 찾기

* func path\(forSoundResource: NSSound.Name\) -&gt; String?

  `forSoundResource:` 에 해당하는 사운드 리소스 파일의 위치를 문자열로 반환합니다.

### 지역화된 문자열 가져오기

* func contextHelp\(forKey: NSHelpManager.ContextHelpKey\) -&gt; NSAttributedString?

  번들의 도움말 파일에서 `forKey:`에 대한 컨텍스트에 해당하는 도움말을 반환합니다.

### 표준 번들 디렉토리 가져오기

* var resourceURL: URL?

  리소스 파일이 들어있는 번들의 하위 디렉토리 URL

* var executableURL: URL?

  수신자의 실행파일 URL

* var privateFrameworksURL: URL? private 프레임워크를 포함하고 있는 번들의 하위 디렉토리 URL
* var sharedFrameworksURL: URL? 공유 프레임워크를 포함하고 있는 수신자의 하위 디렉토리 URL
* var builtInPlugInsURL: URL? 플러그인을 포함하고 있는 수신자의 하위 디렉토리 URL
* func url\(forAuxiliaryExecutable: String\) -&gt; URL? 수신자의 번들에서 `forAuxiliaryExecutable:` 파일명을 갖고 있는 실행 파일 URL을 반환합니다.
* var sharedSupportURL: URL?

  shared support 파일을 포함하고 있는 번들의 하위 디렉토리 URL

* var appStoreReceiptURL: URL? 번들의 앱스토어 영수증 파일 URL
* var resourcePath: String? 리소스를 포함하고 있는 번들 하위 디렉토리의 전체 경로 문자열
* var executablePath: String? 수신자의 실행파일의 전체 경로 문자열
* var privateFrameworksPath: String? private 프레임워크를 포함하고 있는 번들의 하위 디렉토리 전체 경로 문자열
* var sharedFrameworksPath: String?

  공유 프레임워크를 포함하고 있는 번들의 하위 디렉토리 전체 경로 문자열 

* var builtInPlugInsPath: String?

  플러그인을 포함하고 있는 수신자의 하위 디렉토리 전체 경로 문자열

* func path\(forAuxiliaryExecutable: String\) -&gt; String? 수신자의 번들에서 `forAuxiliaryExecutable:` 파일명을 갖고 있는 실행 파일의 전체경로 문자열을 반환합니다.
* var sharedSupportPath: String? shared support 파일을 포함하고 있는 번들 하위 디렉토리의 전체 경로 문자열

### 지역화 정보 가져오기

* var localizations: \[String\]

  번들에 포함된 모든 지역화 리스트

* var preferredLocalizations: \[String\] 번들에 포함된 기본 지역화의 순서 리스트
* var developmentLocalization: String?

  개발 언어의 지역화

* var localizedInfoDictionary: \[String : Any\]?

  번들의 지역화된 프로퍼티 리스트를 나타내는 딕셔너리

* class func preferredLocalizations\(from: \[String\]\) -&gt; \[String\] 번들 객체가 현재 사용자에게 리소스를 찾아주는데 사용할 하나 이상의 지역화를 `from:` 배열 중에서 반환합니다.
* class func preferredLocalizations\(from: \[String\], forPreferences: \[String\]?\) -&gt; \[String\]

  Returns locale identifiers for which a bundle would provide localized content, given a specified list of candidates for a user's language preferences.

### 온 디맨드 리소스의 보존 우선순위 관리

* func setPreservationPriority\(Double, forTags: Set&lt;String&gt;\)

  번들 내에서 태그 지정된 리소스 집합을 제거하기 위한 상대적 순서를 나타냅니다.

* func preservationPriority\(forTag: String\) -&gt; Double 지정된 태그에 대한 현재 보존 우선 순위를 반환합니다.

### 번들로부터 클래스 가져오기

* func classNamed\(String\) -&gt; AnyClass?

  지정된 이름의 클래스 객체를 반환합니다.

* var principalClass: AnyClass? 번들의 principal 클래스
* class let didLoadNotification: NSNotification.Name observer들에게 클래스가 동적 로드되었을때 알려주는 Notification
* let NSLoadedClasses: String [didLoadNotification](../../../etc/not-found.md) 노티피케이션의 userInfo 딕셔너리에서 키로 사용되는 상수. 해당 노티피케이션은 로드된 클래스의 각 이름 배열에 해당합니다.

### 번들로부터 코드 로딩하기

* var executableArchitectures: \[NSNumber\]?

  번들의 실행 파일이 지원하는 아키텍처 유형을 나타내는 숫자 배열

* func preflight\(\) 번들의 실행 코드를 성공적으로 로드할 수 있는지를 나타내는 Boolean 값
* func load\(\) -&gt; Bool 아직 번들의 실행 코드가 로드되지 않았다면 동적으로 로드합니다.
* func loadAndReturnError\(\)

  번들의 실행 코드를 로드하고 에러가 있다면 반환합니다.

* func unload\(\) -&gt; Bool 수신자와 관련된 코드를 언로드합니다.
* var isLoaded: Bool 번들의 로드 상태
* Mach-O Architecture 번들의 실행 코드가 지원하는 CPU 타입을 설명하는 상수

### 에러

* var NSExecutableErrorMinimum: Int

  실행 파일과 관련된 오류를 위해 예약된 오류 코드 범위의 시작

* var NSExecutableNotLoadableError: Int 실행 파일이 현재 프로세스에서 로드할 수 없는 타입입니다.
* var NSExecutableArchitectureMismatchError: Int 실행 파일이 현재 프로세스와 호환되는 아키텍처를 제공하지 않습니다.
* var NSExecutableRuntimeMismatchError: Int 실행 파일이 현재 프로세스와 호환되지 않는 Objective-C 런타임 정보를 포함하고 있습니다.
* var NSExecutableLoadError: Int

  \(라이브러리 종속성 문제와 같은\) 다른 이유로 실행 파일을 로드할 수 없습니다.

* var NSExecutableLinkError: Int 링크 문제로 인해서 실행파일이 실패했습니다.
* var NSExecutableErrorMaximum: Int 실행 파일과 관련된 오류를 위해 예약된 오류 코드 범위의 끝

## 관련 문서

### 상속받은 대상

* NSObject

### 준수하는 프로토콜

* CVarArg
* Equatable
* Hashable



