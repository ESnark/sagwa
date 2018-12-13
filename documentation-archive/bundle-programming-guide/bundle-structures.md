# 번들 구조

> 원문출처  
> [https://developer.apple.com/library/archive/documentation/CoreFoundation/Conceptual/CFBundles/BundleTypes/BundleTypes.html\#//apple\_ref/doc/uid/10000123i-CH101-SW1](https://developer.apple.com/library/archive/documentation/CoreFoundation/Conceptual/CFBundles/BundleTypes/BundleTypes.html#//apple_ref/doc/uid/10000123i-CH101-SW1)

번들 구조는 번들 유형과 타겟 플랫폼에 따라 달라질 수 있습니다. 다음 섹션에서는 MacOS와 iOS 모두에서 가장 일반적으로 사용되는 번들 구조를 설명합니다.

{% hint style="info" %}
알림

번들이 실행 가능한 코드를 패키징하는 한 가지 방법이기는 하지만, 지원되는 유일한 방법은 아닙니다. UNIX 셸 스크립트 및 커맨드라인 도구는 번들 구조를 사용하지 않으며 정적/동적 공유 라이브러리도 사용하지 않습니다.
{% endhint %}

## 애플리케이션 번들 <a id="application-bundles"></a>

애플리케이션 번들은 개발자가 생성하는 가장 일반적인 유형의 번들입니다. 애플리케이션 번들은 애플리케이션의 성공적인 작동에 필요한 모든 것을 저장합니다. 애플리케이션 번들의 구조는 애플리케이션 플랫폼에 따라 다르지만, 번들을 사용하는 방법은 두 플랫폼 모두에서 동일합니다. 이 장에서는 iOS 애플리케이션과 MacOS 애플리케이션의 번들 구조를 둘 다 설명합니다.

### 애플리케이션 번들에는 무슨 파일이 들어가나요? <a id="what-files-go-into-an-application-bundle"></a>

다음 표에는 애플리케이션 번들 내에서 찾을 수 있는 파일 유형이 요약되어 있습니다. 이러한 파일의 정확한 위치는 플랫폼마다 다르며 일부 리소스는 전혀 지원되지 않을 수 있습니다. 예제와 자세한 내용은 이 장의 [플랫폼별 번들 섹션](../../etc/not-found.md)을 참조하세요.

| 파일 | 설명 |
| :--- | :--- |
| Info.plist 파일 | \(필수\) Information Property list 파일은 응용 프로그램에 대한 구성 정보가 들어 있는 [구조화된 파일](../../etc/not-found.md)입니다. 시스템은 이 파일의 존재 여부에 따라 애플리케이션 및 관련 파일에 대한 관련 정보를 식별합니다. |
| 실행파일 | \(필수\) 모든 응용 프로그램에는 실행 가능한 파일이 있어야 합니다. 이 파일에는 애플리케이션의 메인 엔트리 포인트와 애플리케이션 타겟에 정적으로 연결된 모든 코드가 포함되어 있습니다. |
| 리소스 파일 | 리소스는 애플리케이션의 실행 파일 외부에 있는 데이터 파일입니다. 리소스는 일반적으로 이미지, 아이콘, 소리, nib 파일, 문자열 파일, 설정 파일 및 데이터 파일\(기타\) 등으로 구성됩니다. 대부분의 리소스 파일은 특정 언어나 지역에 대해 지역화되거나 모든 지역에 대해 공유될 수 있습니다. |
| 기타 서포트 파일 | Mac 앱은 private 프레임워크, 플러그인, 문서 템플릿 및 애플리케이션에 필수적인 기타 커스텀 데이터 리소스와 같은 고급 리소스를 추가로 포함할 수 있습니다. iOS 애플리케이션 번들에 커스텀 데이터 리소스를 포함할 수 있지만 커스텀 프레임워크나 플러그인을 포함할 수는 없습니다. |

애플리케이션 번들에 포함된 대부분의 리소스가 선택 사항이지만 항상 그런것은 아닙니다. 예를 들어 iOS 애플리케이션에는 일반적으로 애플리케이션 아이콘과 기본 화면에 대한 추가 이미지 리소스가 필요합니다. 또한 대부분의 Mac 앱에는 시스템에서 제공하는 기본 아이콘 대신 커스텀 아이콘이 포함되어 있습니다.

### iOS 애플리케이션 분석 <a id="anatomy-of-an-ios-application-bundle"></a>

Xcode에서 제공하는 프로젝트 템플릿은 iPhone 또는 iPad 애플리케이션의 번들을 설정하는 데 필요한 대부분의 작업을 수행합니다. 그러나 번들 구조를 이해하면 사용자 지정 파일을 저장할 위치를 결정하는 데 도움이 됩니다. iOS 애플리케이션의 번들 구조는 모바일 장치의 요구에 더 잘 맞춰져 있습니다. 외부 디렉토리가 거의 없는 비교적 평평한 구조를 사용하여 디스크 공간을 절약하고 파일에 대한 액세스를 간소화합니다.

#### iOS 애플리케이션 번들 구조 <a id="the-ios-application-bundle-structure"></a>

일반적인 iOS 애플리케이션 번들에는 실행 파일과 애플리케이션에서 사용하는 모든 리소스\(예: 응용프로그램 아이콘, 기타 이미지 및 지역화된 콘텐츠\)가 최상위 번들 디렉토리에 포함되어 있습니다. 다음 예제는 MyApp이라는 간단한 iPhone 애플리케이션의 구조를 보여줍니다. 하위 디렉터리에 있어야 하는 파일은 지역화해야 하는 파일뿐이지만 사용자 자신의 응용 프로그램에 추가 하위 디렉터리를 생성하여 리소스 및 기타 관련 파일을 구성할 수 있습니다.

> MyApp
>
> | MyApp.app |
> | :--- |
> |    MyApp |
> |    MyAppIcon.png |
> |    MySearchIcon.png |
> |    Info.plist |
> |    Default.png |
> |    MainWindow.nib |
> |    Settings.bundle |
> |    MySettingsIcon.png |
> |    iTunesArtwork |
> |    en.lproj |
> |       MyImage.png |
> |    fr.lproj |
> |       MyImage.png |

다음 표는 MyApp의 내용을 설명합니다. 이 애플리케이션 자체는 데모용으로만 사용할 수 있지만 포함된 많은 파일은 애플리케이션 번들로 검색할 때 iOS에서 찾을 수 있는 특정 파일들을 나타냅니다. 지원하는 기능에 따라 자신의 번들에 이러한 파일의 일부 또는 전체가 포함됩니다.

<table>
  <thead>
    <tr>
      <th style="text-align:left">파일</th>
      <th style="text-align:left">설명</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">MyApp</td>
      <td style="text-align:left">(필수) 애플리케이션 코드를 포함하는 실행 파일입니다. 이 파일의 이름은 애플리케이션 이름에서 .app 확장자를 뺀 것과 같습니다.</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>애플리케이션 아이콘</p>
        <p>(MyAppIcon.png, MySearchIcon.png, and MySettingsIcon.png)</p>
      </td>
      <td style="text-align:left">(필수/권장) 애플리케이션 아이콘은 애플리케이션을 나타내는 특정 시점에 사용됩니다. 예를 들어, 홈 스크린, 검색 결과 및 설정
        응용 프로그램에 다양한 크기의 응용 프로그램 아이콘이 표시됩니다. 모든 아이콘이 필요한 것은 아니지만 대부분은 권장됩니다. 응용
        프로그램 아이콘에 대한 자세한 내용은 <a href="../../etc/not-found.md">애플리케이션 아이콘 및 실행 이미지</a>를
        참조하세요.</td>
    </tr>
    <tr>
      <td style="text-align:left">Info.plist</td>
      <td style="text-align:left">(필수) 이 파일에는 번들 ID, 버전 번호 및 디스플레이 이름과 같은 애플리케이션에 대한 구성 정보가 포함되어 있습니다. 자세한
        내용은 <a href="../../etc/not-found.md">Information Property list File</a>을
        참조하세요.</td>
    </tr>
    <tr>
      <td style="text-align:left">Launch images (Default.png)</td>
      <td style="text-align:left">(권장) 애플리케이션의 초기 인터페이스를 특정 방향으로 표시하는 하나 이상의 이미지입니다. 시스템은 애플리케이션이 창과 사용자
        인터페이스를 로드할 때까지 Launch 이미지 중 하나를 임시 배경으로 사용합니다. 애플리케이션에서 Launch 이미지를 제공하지
        않으면 애플리케이션이 시작되는 동안 검은 배경이 표시됩니다. 애플리케이션 아이콘에 대한 자세한 내용은 <a href="../../etc/not-found.md">애플리케이션 아이콘 및 실행 이미지</a>를
        참조하세요.</td>
    </tr>
    <tr>
      <td style="text-align:left">MainWindow.nib</td>
      <td style="text-align:left">(권장) 애플리케이션의 main <a href="../../etc/not-found.md">nib 파일</a>은 시작 시 로드할
        기본 인터페이스 객체를 포함하고 있습니다. 일반적으로 이 nib 파일에는 애플리케이션의 기본 창 객체와 App <a href="../../etc/not-found.md">delegate</a> 객체의
        인스턴스가 포함됩니다. 그런 다음 다른 인터페이스 객체는 추가 nib 파일에서 로드되거나 애플리케이션에 의해 프로그래밍 방식으로
        생성됩니다. (main nib 파일의 이름은 Info.plist 파일의 NSMainNibFile 키에 다른 값을 할당하여 변경할
        수 있습니다. 자세한 내용은 Informatioin Property list 파일을 참조하세요.)</td>
    </tr>
    <tr>
      <td style="text-align:left">Settings.bundle</td>
      <td style="text-align:left">Setting 번들은 설정 애플리케이션에 추가할 애플리케이션별 기본 설정이 포함된 특별한 유형의 플러그인입니다. 이 번들에는
        기본 설정을 구성하고 표시할 <a href="../../etc/not-found.md">프로퍼티 리스트</a>와 기타 리소스 파일이
        포함되어 있습니다.</td>
    </tr>
    <tr>
      <td style="text-align:left">커스텀 리소스 파일</td>
      <td style="text-align:left">지역화되지 않은 리소스는 최상위 디렉터리에 배치되고 지역화된 리소스는 애플리케이션 번들의 언어별 하위 디렉터리에 배치됩니다.
        리소스는 nib 파일, 이미지, 사운드 파일, 설정 파일, 문자열 파일 및 애플리케이션에 필요한 기타 커스텀 데이터 파일로 구성됩니다.
        리소스에 대한 자세한 내용은 <a href="../../etc/not-found.md">iOS 애플리케이션의 리소스</a>를 참조하세요.</td>
    </tr>
  </tbody>
</table>{% hint style="info" %}
알림

iOS 앱 번들에는 "Resources"라는 이름의 사용자 지정 폴더가 포함될 수 없습니다.
{% endhint %}

iOS 애플리케이션은 국제화되어야 하며 지원하는 각 언어에 대한 language.lproj 폴더가 있어야 합니다. 국제화를 위해 애플리케이션 커스텀 리소스의 지역화 버전을 제공하거나 언어별 프로젝트 디렉터리에 동일한 이름의 파일을 배치하여 Launch 이미지를 로컬화할 수도 있습니다. 그러나 지역화 버전을 제공하는 경우에도 항상 해당 파일의 기본 버전을 애플리케이션 번들의 최상위 수준에 포함해야 합니다. 기본 버전은 특정 위치 지정을 사용할 수 없는 경우에 사용됩니다. 지역화된 리소스에 대한 자세한 내용은 [번들의 지역화된 리소스](../../etc/not-found.md)를 참조하세요.

**The Information Property List File**

모든 iOS 애플리케이션에는 애플리케이션의 구성 정보가 포함된 Information Property list\(Info.plist\) 파일이 있어야 합니다. 새 iOS 애플리케이션 프로젝트를 만들 때 Xcode는 자동으로 이 파일을 생성하고 일부 주요 프로퍼티 값을 설정합니다. 표 2-3에는 명시적으로 설정해야 하는 몇 가지 추가 키가 나열되어 있습니다. \(키에는 비교적 모호한 실제 이름과 Xcode상에서 표시되는 이름이 있습니다. Xcode상에서 표시되는 이름은 괄호안에 명시되어있고 편집기에서 Information Property를 마우스 우클릭해서 나타나는 메뉴에서 Show Raw keys/values를 선택하여 모든 키의 실제 이름을 볼 수 있습니다.\)

_표 2-3 Info.plist 파일의 필수 키_

<table>
  <thead>
    <tr>
      <th style="text-align:left">Key</th>
      <th style="text-align:left">Value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">CFBundleDisplayName
        <br />(Bundle display name)</td>
      <td style="text-align:left">Bundle display name이란 애플리케이션 아이콘 아래에 표시되는 이름을 뜻합니다. 이 값은 지원하는 모든 언어에 대해
        지역화되어야 합니다.</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>CFBundleIdentifier</p>
        <p>(Bundle identifier)</p>
      </td>
      <td style="text-align:left">
        <p>Bundle identifier 문자열은 시스템이 애플리케이션을 식별하는데 사용됩니다. 이 문자열은 영숫자(A-Z,a-z,0-9),
          하이픈(-) 및 마침표(.)만 포함하는 Uniform type identifier(UTI)형식 역방향 DNS 형식을 따라야합니다.
          예를 들어, 회사의 도메인이 Ajax.com이고 Hello라는 애플리케이션을 생성하는 경우 com.Ajax.Hello 문자열을
          할당할 수 있습니다.</p>
        <p>번들 식별자는 응용 프로그램 서명을 검증하는 데 사용됩니다</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>CFBundleVersion</p>
        <p>(Bundle version)</p>
      </td>
      <td style="text-align:left">Bundle version 문자열은 번들의 빌드 버전 번호를 지정합니다. 이 값은 한 개 이상의 마침표로 구분되는 정수로 구성된
        문자열입니다. 이 값은 지속적으로 증가하게 되어있으며 지역화할 수 없습니다.</td>
    </tr>
    <tr>
      <td style="text-align:left">CFBundleIconFiles</td>
      <td style="text-align:left">
        <p>애플리케이션의 다양한 아이콘에 사용되는 이미지의 파일 이름이 포함된 문자열 배열입니다. 기술적으로 필수적인 값은 아니지만, 사용하는
          것이 좋습니다.</p>
        <p>이 키는 iOS 3.2 이상에서 지원됩니다.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>LSRequiresIPhoneOS</p>
        <p>(Application requires iOS environment)</p>
      </td>
      <td style="text-align:left">번들이 iOS에서만 실행가능한지를 나타내는 BOOL 값입니다. Xcode는 이 키를 자동으로 추가하고 값을 true로 설정합니다.
        이 키의 값은 변경하지 마세요.</td>
    </tr>
    <tr>
      <td style="text-align:left">UIRequiredDeviceCapabilities</td>
      <td style="text-align:left">
        <p>iTunes와 App Store가 애플리케이션을 실행하기 위해 필요로 하는 디바이스 기능을 알려주는 키입니다. iTunes와
          Mobile App Store는 이 목록을 사용하여 고객이 해당 기능을 지원하지 않는 기기에 애플리케이션을 설치하지 못하도록 합니다.</p>
        <p>이 키의 값은 배열 또는 딕셔너리입니다. 배열을 사용하는 경우 지정된 키가 포함되어있으면 해당 기능이 필요하다는 것을 나타내며,
          딕셔너리를 사용할 경우 각 키에 대해 BOOL 값을 지정해서 해당 기능의 필요 여부를 표시합니다. 두 경우 모두 키를 포함하지
          않으면 기능이 필요하지 않음을 나타냅니다.</p>
        <p>딕셔너리에 포함할 키 목록은 Information Property List 키를 참조하세요. 이 키는 iOS 3.0 이상에서
          지원됩니다.</p>
      </td>
    </tr>
  </tbody>
</table>표 2-4에는 방금 설명된 키 외에 iOS 애플리케이션에서 일반적으로 사용하는 몇 가지 키가 나열되어 있습니다. 이러한 키는 필수적이지는 않지만 대부분은 시작 시 애플리케이션의 구성을 조정하는 방법을 제공합니다. 이러한 키를 제공하면 응용 프로그램이 시스템에서 적절하게 제시되도록 할 수 있습니다.

_표 2-4 Info.plist 파일에 일반적으로 포함되는 키_

<table>
  <thead>
    <tr>
      <th style="text-align:left">Key</th>
      <th style="text-align:left">Value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">
        <p>NSMainNibFile</p>
        <p>(Main nib file base name)</p>
      </td>
      <td style="text-align:left">애플리케이션의 기본 nib 파일 이름을 식별하는 문자열. 프로젝트에 대해 생성된 기본 nib 파일이 아닌 다른 nib 파일을
        사용하려면 해당 nib 파일의 이름을 이 키와 연결시켜야 합니다. nib 파일 이름에는 .nib 파일 이름 확장명이 포함되지 않아야
        합니다.</td>
    </tr>
    <tr>
      <td style="text-align:left">UIStatusBarStyle</td>
      <td style="text-align:left">
        <p>응용 프로그램이 시작될 때 상태 표시줄의 스타일을 식별하는 문자열. 이 값은 UIApplication.h 헤더 파일에 선언된
          UIStatusBarStyle 상수를 기반으로 합니다. 기본 스타일은 UIStatusBarStyleDefault입니다. 애플리케이션이
          실행을 마칠 때(didFinishLaunching)이 초기 상태 표시줄 스타일을 변경할 수 있습니다.</p>
        <p>이 키를 지정하지 않으면 iOS에서 기본 상태 표시줄을 표시합니다.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">UIStatusBarHidden</td>
      <td style="text-align:left">애플리케이션이 시작될 때 상태 표시줄을 처음부터 숨길 것인지를 결정하는 BOOL 값입니다. 상태 표시줄을 숨기려면 이 값을 true로
        설정합니다. 기본값은 false입니다.</td>
    </tr>
    <tr>
      <td style="text-align:left">UIInterfaceOrientation</td>
      <td style="text-align:left">애플리케이션 UI의 초기 방향을 식별하는 문자열. 이 값은 UIApplication.h 헤더 파일에 선언된 UIInterfaceOrientation
        상수를 기반으로 합니다. 기본 스타일은 UIInterfaceOrientationPortrait입니다.</td>
    </tr>
    <tr>
      <td style="text-align:left">UIPrerenderedIcon</td>
      <td style="text-align:left">애플리케이션 아이콘에 이미 gloss 또는 bevel 효과가 포함되어 있는지를 나타내는 BOOL 값입니다. 기본값은 false입니다.
        시스템이 비슷한 효과를 아이콘에 적용하지 않기를 바란다면 이것을 true로 설정하세요.</td>
    </tr>
    <tr>
      <td style="text-align:left">UIRequiresPersistentWiFi</td>
      <td style="text-align:left">
        <p>애플리케이션이 Wi-Fi 네트워크를 사용하여 통신한다는 것을 시스템에 알려주는 BOOL 값입니다. Wi-Fi를 일정시간 사용하는
          애플리케이션은 이 키를 true로 설정해야 합니다. 그렇지 않으면 기기는 전원을 절약하기 위해 30분 후에 Wi-Fi 연결을 종료합니다.
          또한 이 플래그를 설정하면 시스템이 Wi-Fi를 사용할 수 있지만 현재 사용되지 않을 때 네트워크 선택 대화 상자를 표시해야 함을
          알 수 있습니다. 기본값은 false입니다.</p>
        <p>이 속성의 값이 true인 경우에도 기기가 유휴 상태(즉, 스크린 잠금)일 때는 이 키는 효과가 없습니다. 이 시간 동안 애플리케이은
          비활성 상태로 간주되며, 일부 수준에서 작동할 수 있지만 Wi-Fi 연결은 되지 않습니다.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">UILaunchImageFile</td>
      <td style="text-align:left">애플리케이션의 시작 이미지에 사용되는 기본 파일 이름을 포함하는 문자열. 이 키를 지정하지 않으면 기본 파일 이름은 <code>Default</code> 문자열로
        간주됩니다.</td>
    </tr>
  </tbody>
</table>#### 애플리케이션 아이콘과 이미지

애플리케이션 아이콘과 시작 이미지는 모든 애플리케이에 있어야 하는 표준 그래픽입니다. 모든 애플리케이션은 기기의 홈 화면과 앱 스토어에 표시할 아이콘을 지정해야 합니다. 또한 여러 가지 상황에서 사용할 수 있는 아이콘들을 지정할 수 있습니다. 예를 들어 애플리케이션은 검색 결과를 표시할 때 사용할 아이콘의 작은 버전을 제공할 수 있으며 시작 이미지는 앱이 시작될때 사용자에게 시각적 피드백을 제공합니다.

아이콘 및 시작 이미지를 나타내는 데 사용되는 이미지 파일은 모두 번들의 루트 레벨에 있어야 합니다. 시스템에서 이러한 이미지를 식별하는 방법은 여러가지가 있지만 애플리케이션 아이콘을 지정하는 권장 방법은 CFBundleIconFiles 키를 사용하는 것입니다. 애플리케이션에서 아이콘을 지정하고 이미지를 시작하는 방법에 대한 자세한 내용은 [iOS용 앱 프로그래밍 가이드의 고급 앱 트릭](../../etc/not-found.md)에서 이러한 항목에 대한 설명을 참조하십시오.

{% hint style="info" %}
참고

번들 루트 레벨의 아이콘과 시작 이미지 외에도 애플리케이션의 언어별 프로젝트 하위 디렉토리에 지역화된 버전의 시작 이미지를 포함할 수도 있습니다. 애플리케이션에 지역화된 리소스를 포함하는 방법에 대한 자세한 내용은 [번들의 지역화된 리소스](../../etc/not-found.md)를 참조하십시오.
{% endhint %}

#### iOS 애플리케이션 리소스

iOS 애플리케이션에서 로컬이 아닌 리소스는 애플리케이션 실행 파일 및 Info.plist 파일과 함께 번들 디렉토리의 루 레벨에 위치합니다. 대부분의 iOS 애플리케이션에는 루트 레벨에 애플리케이션 아이콘, 시작 이미지 및 하나 이상의 nib 파일을 포함하고 있습니다. 대부분의 비로컬 리소스는 이 최상위 디렉터리에 배치해야 하지만 하위 디렉터리를 생성하여 리소스 파일을 구성할 수도 있습니다. 지역화된 리소스는 하나 이상의 언어별 하위 디렉토리에 배치되어야 하며, 이 하위 디렉터리는 번들의 지역화된 리소스에 대해 자세히 설명합니다.

목록 2-2는 지역화된 리소스와 지역화되지 않은 리소스를 모두 포함하는 가상 애플리케이을 보여 줍니다. 지역화되지 않은 리소스는 Hand.png, MainWindow.nib, MyAppViewController.nib와 WaterSounds 디렉토리 컨텐츠들이고 en.lproj 및 jp.lproj 디렉토리에 있는 항목들은 지역화된 리소스에 해당됩니다.

_목록 2-2 애플리케이션 내의 지역화된 리소스와 지역화되지 않은 리소스들_

```text
MyApp.app/
   Info.plist
   MyApp
   Default.png
   Icon.png
   Hand.png
   MainWindow.nib
   MyAppViewController.nib
   WaterSounds/
      Water1.aiff
      Water2.aiff
   en.lproj/
      CustomView.nib
      bird.png
      Bye.txt
      Localizable.strings
   jp.lproj/
      CustomView.nib
      bird.png
      Bye.txt
      Localizable.strings
```

애플리케이션 번들에서 리소스 파일을 찾는 방법에 대한 자세한 내용은 번[들 콘텐츠 액세스를](../../etc/not-found.md) 참조하세요. 리소스 파일을 로드하고 프로그램에서 사용하는 방법에 대한 자세한 내용은 [리소스 프로그래밍 가이드](../../etc/not-found.md)를 참조하세요.

### macOS 애플리케이션 분석 <a id="anatomy-of-a-macos-application-bundle"></a>

Xcode에서 제공하는 프로젝트 템플릿은 개발 중에 Mac 앱 번들을 설정하는 데 필요한 대부분의 작업을 수행합니다. 그러나 번들 구조를 이해하면 사용자 지정 파일을 저장할 위치를 결정하는 데 도움이 됩니다. MacOS 번들은 조직된 구조를 사용하여 번들 로드 코드가 번들에서 리소스와 기타 중요한 파일을 쉽게 찾을 수 있도록 합니다. 또한 계층적 특성은 시스템이 다른 애플리케이션의 \(문서 유형을 구현하기 위해 사용하는\) 디렉토리 패키지와 같은 코드 번들을 구별하는 데 도움이 됩니다.

#### macOS 애플리케이션 번들 구조 <a id="the-structure-of-a-macos-application-bundle"></a>

Mac 애플리케이션 번들의 기본 구조는 매우 간단합니다. 번들의 최상위에는 `Contents`라는 디렉터리가 있습니다. 이 디렉토리에는 애플리케이션에 필요한 리소스, 실행 파일, 개인 프레임워크, 개인 플러그인 및 지원 파일을 비롯한 모든 항목이 포함됩니다. `Contents` 디렉토리는 불필요하게 보일 수 있지만 이전 버전의 Mac OS에서 볼 수 있는 레거시 번들 또는 문서 유형과 모던 스타일 번들을 구분짓는 역할을 합니다.

Listing 2-3은 Contents 디렉토리에서 찾을 가능성이 있는 즉각적인 파일과 디렉토리를 포함하여 일반적인 애플리케이션 번들의 상위 레벨 구조를 보여줍니다. 이 구조는 모든 Mac 애플리케이션의 핵심을 나타냅니다.

_목록 2-3 Mac App의 기본 구조_

```text
MyApp.app/
   Contents/
      Info.plist
      MacOS/
      Resources/
```

표 2-5는 Contents 디렉토리에서 찾을 수있는 디렉토리와 각 디렉토리의 목적을 나열합니다. 이 목록은 엄격하게 구분된 것은 아니지만 공통된 용도로 사용되는 디렉토리를 나타냅니다.

_표 2-5 Contents 디렉토리의 하위 디렉토리_

<table>
  <thead>
    <tr>
      <th style="text-align:left">디렉토리</th>
      <th style="text-align:left">설명</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">MacOS</td>
      <td style="text-align:left">애플리케이션의 독립실행형 코드가 들어 있습니다. 일반적으로 이 디렉토리에는 애플리케이션의 기본 진입점과 정적으로 링크된 코드가
        포함된 이진 파일 하나만 포함되어 있지만 다른 독립실행형 실행파일(예 : 명령줄 도구)도 들어갈 수 있습니다.</td>
    </tr>
    <tr>
      <td style="text-align:left">Resources</td>
      <td style="text-align:left">모든 응용 프로그램의 리소스 파일을 포함합니다. 이 디렉토리의 내용은 지역화 된 리소스와 그렇지 않은 리소스를 구분하기 위해
        더 체계화되어 있습니다. 이 디렉토리의 구조에 대한 자세한 내용은 Resources 디렉토리를 참조하십시오.</td>
    </tr>
    <tr>
      <td style="text-align:left">Frameworks</td>
      <td style="text-align:left">
        <p>실행 파일에 사용되는 개인 공유 라이브러리 및 프레임워크를 포함합니다. 이 디렉토리의 프레임워크는 애플리케이션에 리비전 잠금되며
          운영체제에서 사용할 수 있는 다른 최신 버전으로 대체될 수 없습니다. 즉, 이 디렉토리에 포함된 프레임워크는 운영체제의 다른 부분에서
          발견되는 비슷한 이름의 프레임워크보다 우선합니다.</p>
        <p>애플리케이션 번들에 개인 프레임워크를 추가하는 방법에 대한 정보는 <a href="../../etc/not-found.md">Framework Programming Guide</a>를
          참조하십시오.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">PlugIns</td>
      <td style="text-align:left">애플리케이션의 기본 기능을 확장하는 로드 가능한 번들을 포함합니다. 이 디렉토리를 사용하여 애플리케이션의 프로세스 공간에 로드해야
        하는 코드 모듈을 포함할 수 있습니다. 독립 실행형 실행 파일을 저장하는 용도로는 사용되지 않습니다.</td>
    </tr>
    <tr>
      <td style="text-align:left">SharedSupport</td>
      <td style="text-align:left">애플리케이션 실행 기능에 영향을 주지 않는 부가적인 리소스가 포함되어 있습니다. 이 디렉토리를 사용하여 애플리케이션의 실행에
        영향을 주지 않는 문서 템플릿, 클립 아트 및 튜토리얼을 포함시킬 수 있습니다.</td>
    </tr>
  </tbody>
</table>애플리케이션 번들은 수년간 발전해 왔지만 전반적인 목표는 같았습니다. 번들 구조는 애플리케이션이 리소스를 더 쉽게 찾을 수 있도록 하는 동시에 사용자가 이러한 리소스에 간섭하는 것을 더 어렵게 만듭니다.. Finder는 대부분의 번들을 불투명 엔터티로 처리하므로, 일반 사용자가 애플리케이션에 필요한 리소스를 이동하거나 삭제하기가 어렵습니다.

#### **The Information Property List File**

Finder에서 애플리케이션 번들을 인식하게 하려면 Information Property List \(Info.plist\) 파일을 포함시켜야합니다. 이 파일에는 번들 구성을 식별하는 XML 특성 목록 데이터가 들어 있습니다. 최소 번들의 경우 이 파일에는 거의 정보가 없으며 대부분 번들의 이름과 식별자뿐입니다. 더 복잡한 번들의 경우, Info.plist 파일은 더 많은 정보를 포함합니다.

{% hint style="info" %}
중요

번들 리소스는 검색시 대소문자를 구분합니다. 따라서 Information Proper 파일의 이름은 대문자 "I"로 시작해야합니다.
{% endhint %}

표 2-6은 Info.plist 파일에 항상 포함해야 하는 키를 나열합니다. Xcode는 새 프로젝트를 만들 때 이러한 모든 키를 자동으로 제공합니다. \(키에는 비교적 모호한 실제 이름과 Xcode상에서 표시되는 이름이 있습니다. Xcode상에서 표시되는 이름은 괄호안에 명시되어있고 편집기에서 Information Property를 마우스 우클릭해서 나타나는 메뉴에서 Show Raw keys/values를 선택하여 모든 키의 실제 이름을 볼 수 있습니다.\)

표 2-6 Inf_o.plist 파일에 필요한 키_

<table>
  <thead>
    <tr>
      <th style="text-align:left">Key</th>
      <th style="text-align:left">Value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">
        <p>CFBundleName</p>
        <p>(Bundle name)</p>
      </td>
      <td style="text-align:left">번들의 짧은 이름입니다. 이 키의 값은 일반적으로 애플리케이션의 이름으로 사용됩니다. Xcode는 새 프로젝트를 만들때 기본적으로
        이 키의 값을 설정합니다.</td>
    </tr>
    <tr>
      <td style="text-align:left">CFBundleDisplayName
        <br />(Bundle display name)</td>
      <td style="text-align:left">애플리케이션 이름의 지역화된 버전입니다. 일반적으로 각 언어별 리소스 디렉토리의 InfoPlist.strings 파일에 이 키의
        지역화된 값을 포함시킵니다.</td>
    </tr>
    <tr>
      <td style="text-align:left">CFBundleIdentifier
        <br />(Bundle identifier)</td>
      <td style="text-align:left">
        <p>시스템에서 애플리케이션을 식별할때 사용하는 문자열입니다. 이 문자열은 영숫자 (A-Z, a-z, 0-9), 하이픈 (-) 및
          마침표 (.) 문자 만 포함하는 Uniform type identifier(UTI)형식과 역 DNS 형식을 따라야 합니다. 예를
          들어, 회사 도메인이 Ajax.com이고 Hello라는 애플리케이션을 작성하는 경우 com.Ajax.Hello 문자열을 애플리케이션의
          번들 식별자로 할당할 수 있습니다.</p>
        <p>번들 식별자는 응용 프로그램 서명을 확인하는 데 사용됩니다.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">CFBundleVersion
        <br />(Bundle version)</td>
      <td style="text-align:left">번들의 빌드 버전 번호를 지정합니다. 이 값은 한 개 이상의 마침표로 구분되는 정수로 구성된 문자열입니다. 이 값은 지속적으로
        증가하게 되어있으며 지역화할 수 없습니다.</td>
    </tr>
    <tr>
      <td style="text-align:left">CFBundlePackageType
        <br />(Bundle OS Type code)</td>
      <td style="text-align:left">번들 유형입니다. 애플리케이션의 경우 이 키의 값은 항상 4자 문자열 <code>APPL</code>입니다.</td>
    </tr>
    <tr>
      <td style="text-align:left">CFBundleSignature
        <br />(Bundle creator OS Type code)</td>
      <td style="text-align:left">번들의 작성자 코드입니다. 이 문자열은 번들과 관련된 4자 문자열입니다. 예를 들어 TextEdit 애플리케이션의 시그니처는
        ttxt입니다.</td>
    </tr>
    <tr>
      <td style="text-align:left">CFBundleExecutable
        <br />(Executable file)</td>
      <td style="text-align:left">주 실행 파일의 이름. 이것은 사용자가 애플리케이션을 시작할 때 실행되는 코드입니다. 일반적으로 Xcode는 빌드시 이 키의
        값을 자동으로 설정합니다.</td>
    </tr>
  </tbody>
</table>_표 2-7 Info.plist 파일에 권장되는 키_

| Key | 설 |
| :--- | :--- |
| CFBundleDocumentTypes \(Document types\) | 응용프로그램에서 지원하는 문서 유형. 이 유형은 딕셔너리 배열로 구성되어 있으며 각각은 특정 문서 유형에 대한 정보를 제공합니. |
| CFBundleShortVersionString \(Bundle versions string, short\) | 애플리케이션의 릴리즈 버전입니다. 이 키의 값은 마침표로 구분되는 세개의 정수로 구성된 문자열입니다. |
| LSMinimumSystemVersion \(Minimum system version\) | 이 애플리케이을 실행하는데 필요한 macOS의 최소 버전입니다. 이 키의 값은 n.n.n 형식의 문자열이며, 여기서 각 n은 필요한 macOS의 주 버전 번호 또는 부 버전 번호를 나타냅니다. 예를 들어, 10.1.5 값은 MacOS v10.1.5를 나타냅니다. |
| NSHumanReadableCopyright \(Copyright \(human-readable\)\) | 애플리케이에 대한 저작권 알림. 이 문자열은 사람이 읽을 수 있는 문자열이며 언어별 프로젝트 디렉터리의 InfoPlist.strings 파일에 키를 추가하여 현지화할 수 있습니다. |
| NSMainNibFile \(Main nib file base name\) | 애플리케이이 시작될 때 로드할 nib 파일입니다\(.nib 확장자명을 제외한 파일 이름\) 기본 nib 파일은 시작 시 필요한 객체\(main window, App Delegate 등\)를 포함하는 Interface Builder 아카이브입니다. |
| NSPrincipalClass \(Principal class\) | 동적으로 로드되는 Objective-C 코드의 진입점. 애플리케이션 번들의 경우, 이것은 거의 항상 NSApplication 클래스 또는 커스텀 서브 클래스입니다. |

The exact information you put into your Info.plist file is dependent on your bundle’s needs and can be localized as necessary. For more information on this file, see [Runtime Configuration Guidelines](../../etc/not-found.md).

#### **리소스 디렉토리** <a id="the-resources-directory"></a>

리소스 디렉토리에는 모든 이미지, 음원, nib 파일, 문자열 리소스, 아이콘 파일, 데이터 파일 및 구성 파일이 포함됩니다. 이 디렉터리의 내용은 지역화된 리소스 파일과 지역화되지 않은 리소스 파일을 저장할 수 있는 영역으로 추가로 세분화됩니다. 로컬이 아닌 리소스는 리소스 디렉토리 자체의 최상위 수준 또는 사용자가 정의하는 하위 디렉토리에 있습니다. 로컬화된 리소스는 언어별 프로젝트 하위 디렉토리에 상주하며, 특정 지역화와 일치하도록 이름이 지정됩니다.

Resources 디렉토리가 어떻게 구성되어 있는지 확인하는 가장 좋은 방법은 예제를 살펴 보는 것입니다. Listing 2-4는 지역화 된 리소스와 그렇지 않은 리소스를 모두 포함하는 가상의 애플리케이션을 보여줍니다. Hand.tiff, MyApp.icns 및 WaterSounds 디렉토리의 컨텐츠는 지역화되지 않은 리소스이고, en.lproj 디렉토리와 jp.lproj 디렉토리, 그리고 해당 디렉토리의 컨텐츠들이 모두 지역화된 리소스에 해당합니다.

목록 2-4 Mac App의 지역화된 리소스와 지역화되지 않은 리소스들

```text
MyApp.app/
   Contents/
      Info.plist
      MacOS/
         MyApp
      Resources/
         Hand.tiff
         MyApp.icns
         WaterSounds/
            Water1.aiff
            Water2.aiff
         en.lproj/
            MyApp.nib
            bird.tiff
            Bye.txt
            InfoPlist.strings
            Localizable.strings
            CitySounds/
               city1.aiff
               city2.aiff
         jp.lproj/
            MyApp.nib
            bird.tiff
            Bye.txt
            InfoPlist.strings
            Localizable.strings
            CitySounds/
               city1.aiff
               city2.aiff
```

각 언어별 프로젝트 디렉토리에는 동일한 리소스 파일 세트가 포함되어야하며 단일 리소스 파일의 이름은 모든 지역화에서 동일해야합니다. 즉, 특정 파일의 이름은 동일하고 내용만 한 지역에서 다른 지역으로 변경되는 것입니다. 코드에서 리소스 파일을 요청할 때는 원하는 파일의 이름만 지정하면 됩니다. 번들 로드 코드는 사용자의 현재 언어 기본 설정을 참고하여 요청 파일을 검색할 디렉토리를 결정합니다.

애플리케이션 번들에서 리소스 파일을 찾는 방법에 대한 자세한 내용은 [번들 컨텐츠 액세스](../../etc/not-found.md)를 참조하세요. 리소스 파일을로드하고 프로그램에서 사용하는 방법에 대한 자세한 내용은 [리소스 프로그래밍 가이드](../../etc/not-found.md)를 참조하세요.

**애플리케이션 아이콘 파일**  
최상위 레벨 Resources 디렉토리에 속한 특별한 리소스 중 하나가 애플리케이션 아이콘 파일입니다. 규칙에 따라 이 파일에는 번들의 이름과 .icns의 확장자가 사용됩니다. 이미지 형식은 지원되는 모든 유형이 될 수 있지만 확장자가 지정되지 않으면 시스템은 .icns로 간주합니다.

**Information Property List 지역화**  
애플리케이션의 Info.plist 파일에 있는 키 중 일부는 사용자에게 보여지는 문자열을 포함하기 때문에 macOS는 해당 문자열의 지역화 된 버전을 지정하는 메커니즘을 제공합니다. 각 언어별 프로젝트 디렉토리에는 적절한 현지화를 지정하는 InfoPlist.strings 파일을 포함 할 수 있습니다. 이 파일은 지역화하려는 Info.plist 키와 적절한 변환으로 구성된 항목이 들어있는 문자열 파일\(property list가 아님\)입니다. 예를 들어, 텍스트 편집기 애플리케이션에서 InfoPlist.strings의 독일어 버전은 다음 문자열을 포함합니다.

```text
CFBundleDisplayName = "TextEdit";
NSHumanReadableCopyright = "Copyright © 1995-2009 Apple Inc.\nAlle Rechte vorbehalten.";
```

### 애플리케이션 번들 만들기

애플리케이션 번들을 만드는 가장 간단한 방법은 Xcode를 사용하는 것입니다. 모든 새 애플리케이션 프로젝트에는 적절하게 구성된 애플리케이션 타겟이 포함됩니다. 애플리케이션 타겟은 컴파일 할 소스 파일, 번들에 복사 할 리소스 파일 등을 포함하여 애플리케이션 번들을 작성하는데 필요한 규칙을 정의합니다. 새로운 프로젝트에는 미리 구성된 Info.plist 파일과 일반적으로 몇가지 다른 파일이 포함되어있어 신속하게 시작할 수 있습니다. 프로젝트 윈도우를 사용하여 필요에 따라 사용자화 파일을 추가하고 Info 또는 Inspector 윈도우를 사용하여 해당 파일을 구성 할 수 있습니다. 예를 들어 정보창을 사용하여 번들 내의 리소스 파일에 대한 사용자 지정 위치를 지정할 수 있습니다.

Xcode에서 대상을 구성하는 방법에 대한 정보는 [Xcode 빌드 시스템 가이드](../../etc/not-found.md)를 참조하십시오.

## 프레임워크 번들

### 프레임워크 번들 분석

### 프레임워크 번들 만들기

## 로드 가능한 번들

### 로드 가능한 번들 분석

### 로드 가능한 번들 만들기

## 번들의 지역화된 리소스

