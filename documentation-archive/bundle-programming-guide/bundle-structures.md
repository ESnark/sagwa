---
description: 표준 번들 타입의 구조와 컨텐츠를 설명합니다.
---

# 번들 구조

> 원문 출처  
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
      <th style="text-align:left">&#xD30C;&#xC77C;</th>
      <th style="text-align:left">&#xC124;&#xBA85;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">MyApp</td>
      <td style="text-align:left">(&#xD544;&#xC218;) &#xC560;&#xD50C;&#xB9AC;&#xCF00;&#xC774;&#xC158; &#xCF54;&#xB4DC;&#xB97C;
        &#xD3EC;&#xD568;&#xD558;&#xB294; &#xC2E4;&#xD589; &#xD30C;&#xC77C;&#xC785;&#xB2C8;&#xB2E4;.
        &#xC774; &#xD30C;&#xC77C;&#xC758; &#xC774;&#xB984;&#xC740; &#xC560;&#xD50C;&#xB9AC;&#xCF00;&#xC774;&#xC158;
        &#xC774;&#xB984;&#xC5D0;&#xC11C; .app &#xD655;&#xC7A5;&#xC790;&#xB97C;
        &#xBE80; &#xAC83;&#xACFC; &#xAC19;&#xC2B5;&#xB2C8;&#xB2E4;.</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>&#xC560;&#xD50C;&#xB9AC;&#xCF00;&#xC774;&#xC158; &#xC544;&#xC774;&#xCF58;</p>
        <p>(MyAppIcon.png, MySearchIcon.png, and MySettingsIcon.png)</p>
      </td>
      <td style="text-align:left">(&#xD544;&#xC218;/&#xAD8C;&#xC7A5;) &#xC560;&#xD50C;&#xB9AC;&#xCF00;&#xC774;&#xC158;
        &#xC544;&#xC774;&#xCF58;&#xC740; &#xC560;&#xD50C;&#xB9AC;&#xCF00;&#xC774;&#xC158;&#xC744;
        &#xB098;&#xD0C0;&#xB0B4;&#xB294; &#xD2B9;&#xC815; &#xC2DC;&#xC810;&#xC5D0;
        &#xC0AC;&#xC6A9;&#xB429;&#xB2C8;&#xB2E4;. &#xC608;&#xB97C; &#xB4E4;&#xC5B4;,
        &#xD648; &#xC2A4;&#xD06C;&#xB9B0;, &#xAC80;&#xC0C9; &#xACB0;&#xACFC; &#xBC0F;
        &#xC124;&#xC815; &#xC751;&#xC6A9; &#xD504;&#xB85C;&#xADF8;&#xB7A8;&#xC5D0;
        &#xB2E4;&#xC591;&#xD55C; &#xD06C;&#xAE30;&#xC758; &#xC751;&#xC6A9; &#xD504;&#xB85C;&#xADF8;&#xB7A8;
        &#xC544;&#xC774;&#xCF58;&#xC774; &#xD45C;&#xC2DC;&#xB429;&#xB2C8;&#xB2E4;.
        &#xBAA8;&#xB4E0; &#xC544;&#xC774;&#xCF58;&#xC774; &#xD544;&#xC694;&#xD55C;
        &#xAC83;&#xC740; &#xC544;&#xB2C8;&#xC9C0;&#xB9CC; &#xB300;&#xBD80;&#xBD84;&#xC740;
        &#xAD8C;&#xC7A5;&#xB429;&#xB2C8;&#xB2E4;. &#xC751;&#xC6A9; &#xD504;&#xB85C;&#xADF8;&#xB7A8;
        &#xC544;&#xC774;&#xCF58;&#xC5D0; &#xB300;&#xD55C; &#xC790;&#xC138;&#xD55C;
        &#xB0B4;&#xC6A9;&#xC740; <a href="../../etc/not-found.md">&#xC560;&#xD50C;&#xB9AC;&#xCF00;&#xC774;&#xC158; &#xC544;&#xC774;&#xCF58; &#xBC0F; &#xC2E4;&#xD589; &#xC774;&#xBBF8;&#xC9C0;</a>&#xB97C;
        &#xCC38;&#xC870;&#xD558;&#xC138;&#xC694;.</td>
    </tr>
    <tr>
      <td style="text-align:left">Info.plist</td>
      <td style="text-align:left">(&#xD544;&#xC218;) &#xC774; &#xD30C;&#xC77C;&#xC5D0;&#xB294; &#xBC88;&#xB4E4;
        ID, &#xBC84;&#xC804; &#xBC88;&#xD638; &#xBC0F; &#xB514;&#xC2A4;&#xD50C;&#xB808;&#xC774;
        &#xC774;&#xB984;&#xACFC; &#xAC19;&#xC740; &#xC560;&#xD50C;&#xB9AC;&#xCF00;&#xC774;&#xC158;&#xC5D0;
        &#xB300;&#xD55C; &#xAD6C;&#xC131; &#xC815;&#xBCF4;&#xAC00; &#xD3EC;&#xD568;&#xB418;&#xC5B4;
        &#xC788;&#xC2B5;&#xB2C8;&#xB2E4;. &#xC790;&#xC138;&#xD55C; &#xB0B4;&#xC6A9;&#xC740;
        <a
        href="../../etc/not-found.md">Information Property list File</a>&#xC744; &#xCC38;&#xC870;&#xD558;&#xC138;&#xC694;.</td>
    </tr>
    <tr>
      <td style="text-align:left">Launch images (Default.png)</td>
      <td style="text-align:left">(&#xAD8C;&#xC7A5;) &#xC560;&#xD50C;&#xB9AC;&#xCF00;&#xC774;&#xC158;&#xC758;
        &#xCD08;&#xAE30; &#xC778;&#xD130;&#xD398;&#xC774;&#xC2A4;&#xB97C; &#xD2B9;&#xC815;
        &#xBC29;&#xD5A5;&#xC73C;&#xB85C; &#xD45C;&#xC2DC;&#xD558;&#xB294; &#xD558;&#xB098;
        &#xC774;&#xC0C1;&#xC758; &#xC774;&#xBBF8;&#xC9C0;&#xC785;&#xB2C8;&#xB2E4;.
        &#xC2DC;&#xC2A4;&#xD15C;&#xC740; &#xC560;&#xD50C;&#xB9AC;&#xCF00;&#xC774;&#xC158;&#xC774;
        &#xCC3D;&#xACFC; &#xC0AC;&#xC6A9;&#xC790; &#xC778;&#xD130;&#xD398;&#xC774;&#xC2A4;&#xB97C;
        &#xB85C;&#xB4DC;&#xD560; &#xB54C;&#xAE4C;&#xC9C0; Launch &#xC774;&#xBBF8;&#xC9C0;
        &#xC911; &#xD558;&#xB098;&#xB97C; &#xC784;&#xC2DC; &#xBC30;&#xACBD;&#xC73C;&#xB85C;
        &#xC0AC;&#xC6A9;&#xD569;&#xB2C8;&#xB2E4;. &#xC560;&#xD50C;&#xB9AC;&#xCF00;&#xC774;&#xC158;&#xC5D0;&#xC11C;
        Launch &#xC774;&#xBBF8;&#xC9C0;&#xB97C; &#xC81C;&#xACF5;&#xD558;&#xC9C0;
        &#xC54A;&#xC73C;&#xBA74; &#xC560;&#xD50C;&#xB9AC;&#xCF00;&#xC774;&#xC158;&#xC774;
        &#xC2DC;&#xC791;&#xB418;&#xB294; &#xB3D9;&#xC548; &#xAC80;&#xC740; &#xBC30;&#xACBD;&#xC774;
        &#xD45C;&#xC2DC;&#xB429;&#xB2C8;&#xB2E4;. &#xC560;&#xD50C;&#xB9AC;&#xCF00;&#xC774;&#xC158;
        &#xC544;&#xC774;&#xCF58;&#xC5D0; &#xB300;&#xD55C; &#xC790;&#xC138;&#xD55C;
        &#xB0B4;&#xC6A9;&#xC740; <a href="../../etc/not-found.md">&#xC560;&#xD50C;&#xB9AC;&#xCF00;&#xC774;&#xC158; &#xC544;&#xC774;&#xCF58; &#xBC0F; &#xC2E4;&#xD589; &#xC774;&#xBBF8;&#xC9C0;</a>&#xB97C;
        &#xCC38;&#xC870;&#xD558;&#xC138;&#xC694;.</td>
    </tr>
    <tr>
      <td style="text-align:left">MainWindow.nib</td>
      <td style="text-align:left">(&#xAD8C;&#xC7A5;) &#xC560;&#xD50C;&#xB9AC;&#xCF00;&#xC774;&#xC158;&#xC758;
        main <a href="../../etc/not-found.md">nib &#xD30C;&#xC77C;</a>&#xC740; &#xC2DC;&#xC791;
        &#xC2DC; &#xB85C;&#xB4DC;&#xD560; &#xAE30;&#xBCF8; &#xC778;&#xD130;&#xD398;&#xC774;&#xC2A4;
        &#xAC1D;&#xCCB4;&#xB97C; &#xD3EC;&#xD568;&#xD558;&#xACE0; &#xC788;&#xC2B5;&#xB2C8;&#xB2E4;.
        &#xC77C;&#xBC18;&#xC801;&#xC73C;&#xB85C; &#xC774; nib &#xD30C;&#xC77C;&#xC5D0;&#xB294;
        &#xC560;&#xD50C;&#xB9AC;&#xCF00;&#xC774;&#xC158;&#xC758; &#xAE30;&#xBCF8;
        &#xCC3D; &#xAC1D;&#xCCB4;&#xC640; App <a href="../../etc/not-found.md">delegate</a> &#xAC1D;&#xCCB4;&#xC758;
        &#xC778;&#xC2A4;&#xD134;&#xC2A4;&#xAC00; &#xD3EC;&#xD568;&#xB429;&#xB2C8;&#xB2E4;.
        &#xADF8;&#xB7F0; &#xB2E4;&#xC74C; &#xB2E4;&#xB978; &#xC778;&#xD130;&#xD398;&#xC774;&#xC2A4;
        &#xAC1D;&#xCCB4;&#xB294; &#xCD94;&#xAC00; nib &#xD30C;&#xC77C;&#xC5D0;&#xC11C;
        &#xB85C;&#xB4DC;&#xB418;&#xAC70;&#xB098; &#xC560;&#xD50C;&#xB9AC;&#xCF00;&#xC774;&#xC158;&#xC5D0;
        &#xC758;&#xD574; &#xD504;&#xB85C;&#xADF8;&#xB798;&#xBC0D; &#xBC29;&#xC2DD;&#xC73C;&#xB85C;
        &#xC0DD;&#xC131;&#xB429;&#xB2C8;&#xB2E4;. (main nib &#xD30C;&#xC77C;&#xC758;
        &#xC774;&#xB984;&#xC740; Info.plist &#xD30C;&#xC77C;&#xC758; NSMainNibFile
        &#xD0A4;&#xC5D0; &#xB2E4;&#xB978; &#xAC12;&#xC744; &#xD560;&#xB2F9;&#xD558;&#xC5EC;
        &#xBCC0;&#xACBD;&#xD560; &#xC218; &#xC788;&#xC2B5;&#xB2C8;&#xB2E4;. &#xC790;&#xC138;&#xD55C;
        &#xB0B4;&#xC6A9;&#xC740; Informatioin Property list &#xD30C;&#xC77C;&#xC744;
        &#xCC38;&#xC870;&#xD558;&#xC138;&#xC694;.)</td>
    </tr>
    <tr>
      <td style="text-align:left">Settings.bundle</td>
      <td style="text-align:left">Setting &#xBC88;&#xB4E4;&#xC740; &#xC124;&#xC815; &#xC560;&#xD50C;&#xB9AC;&#xCF00;&#xC774;&#xC158;&#xC5D0;
        &#xCD94;&#xAC00;&#xD560; &#xC560;&#xD50C;&#xB9AC;&#xCF00;&#xC774;&#xC158;&#xBCC4;
        &#xAE30;&#xBCF8; &#xC124;&#xC815;&#xC774; &#xD3EC;&#xD568;&#xB41C; &#xD2B9;&#xBCC4;&#xD55C;
        &#xC720;&#xD615;&#xC758; &#xD50C;&#xB7EC;&#xADF8;&#xC778;&#xC785;&#xB2C8;&#xB2E4;.
        &#xC774; &#xBC88;&#xB4E4;&#xC5D0;&#xB294; &#xAE30;&#xBCF8; &#xC124;&#xC815;&#xC744;
        &#xAD6C;&#xC131;&#xD558;&#xACE0; &#xD45C;&#xC2DC;&#xD560; <a href="../../etc/not-found.md">&#xD504;&#xB85C;&#xD37C;&#xD2F0; &#xB9AC;&#xC2A4;&#xD2B8;</a>&#xC640;
        &#xAE30;&#xD0C0; &#xB9AC;&#xC18C;&#xC2A4; &#xD30C;&#xC77C;&#xC774; &#xD3EC;&#xD568;&#xB418;&#xC5B4;
        &#xC788;&#xC2B5;&#xB2C8;&#xB2E4;.</td>
    </tr>
    <tr>
      <td style="text-align:left">&#xCEE4;&#xC2A4;&#xD140; &#xB9AC;&#xC18C;&#xC2A4; &#xD30C;&#xC77C;</td>
      <td
      style="text-align:left">&#xC9C0;&#xC5ED;&#xD654;&#xB418;&#xC9C0; &#xC54A;&#xC740; &#xB9AC;&#xC18C;&#xC2A4;&#xB294;
        &#xCD5C;&#xC0C1;&#xC704; &#xB514;&#xB809;&#xD130;&#xB9AC;&#xC5D0; &#xBC30;&#xCE58;&#xB418;&#xACE0;
        &#xC9C0;&#xC5ED;&#xD654;&#xB41C; &#xB9AC;&#xC18C;&#xC2A4;&#xB294; &#xC560;&#xD50C;&#xB9AC;&#xCF00;&#xC774;&#xC158;
        &#xBC88;&#xB4E4;&#xC758; &#xC5B8;&#xC5B4;&#xBCC4; &#xD558;&#xC704; &#xB514;&#xB809;&#xD130;&#xB9AC;&#xC5D0;
        &#xBC30;&#xCE58;&#xB429;&#xB2C8;&#xB2E4;. &#xB9AC;&#xC18C;&#xC2A4;&#xB294;
        nib &#xD30C;&#xC77C;, &#xC774;&#xBBF8;&#xC9C0;, &#xC0AC;&#xC6B4;&#xB4DC;
        &#xD30C;&#xC77C;, &#xC124;&#xC815; &#xD30C;&#xC77C;, &#xBB38;&#xC790;&#xC5F4;
        &#xD30C;&#xC77C; &#xBC0F; &#xC560;&#xD50C;&#xB9AC;&#xCF00;&#xC774;&#xC158;&#xC5D0;
        &#xD544;&#xC694;&#xD55C; &#xAE30;&#xD0C0; &#xCEE4;&#xC2A4;&#xD140; &#xB370;&#xC774;&#xD130;
        &#xD30C;&#xC77C;&#xB85C; &#xAD6C;&#xC131;&#xB429;&#xB2C8;&#xB2E4;. &#xB9AC;&#xC18C;&#xC2A4;&#xC5D0;
        &#xB300;&#xD55C; &#xC790;&#xC138;&#xD55C; &#xB0B4;&#xC6A9;&#xC740; <a href="../../etc/not-found.md">iOS &#xC560;&#xD50C;&#xB9AC;&#xCF00;&#xC774;&#xC158;&#xC758; &#xB9AC;&#xC18C;&#xC2A4;</a>&#xB97C;
        &#xCC38;&#xC870;&#xD558;&#xC138;&#xC694;.</td>
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
      <td style="text-align:left">Bundle display name&#xC774;&#xB780; &#xC560;&#xD50C;&#xB9AC;&#xCF00;&#xC774;&#xC158;
        &#xC544;&#xC774;&#xCF58; &#xC544;&#xB798;&#xC5D0; &#xD45C;&#xC2DC;&#xB418;&#xB294;
        &#xC774;&#xB984;&#xC744; &#xB73B;&#xD569;&#xB2C8;&#xB2E4;. &#xC774; &#xAC12;&#xC740;
        &#xC9C0;&#xC6D0;&#xD558;&#xB294; &#xBAA8;&#xB4E0; &#xC5B8;&#xC5B4;&#xC5D0;
        &#xB300;&#xD574; &#xC9C0;&#xC5ED;&#xD654;&#xB418;&#xC5B4;&#xC57C; &#xD569;&#xB2C8;&#xB2E4;.</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>CFBundleIdentifier</p>
        <p>(Bundle identifier)</p>
      </td>
      <td style="text-align:left">
        <p>Bundle identifier &#xBB38;&#xC790;&#xC5F4;&#xC740; &#xC2DC;&#xC2A4;&#xD15C;&#xC774;
          &#xC560;&#xD50C;&#xB9AC;&#xCF00;&#xC774;&#xC158;&#xC744; &#xC2DD;&#xBCC4;&#xD558;&#xB294;&#xB370;
          &#xC0AC;&#xC6A9;&#xB429;&#xB2C8;&#xB2E4;. &#xC774; &#xBB38;&#xC790;&#xC5F4;&#xC740;
          &#xC601;&#xC22B;&#xC790;(A-Z,a-z,0-9), &#xD558;&#xC774;&#xD508;(-) &#xBC0F;
          &#xB9C8;&#xCE68;&#xD45C;(.)&#xB9CC; &#xD3EC;&#xD568;&#xD558;&#xB294; Uniform
          type identifier(UTI)&#xD615;&#xC2DD; &#xC5ED;&#xBC29;&#xD5A5; DNS &#xD615;&#xC2DD;&#xC744;
          &#xB530;&#xB77C;&#xC57C;&#xD569;&#xB2C8;&#xB2E4;. &#xC608;&#xB97C; &#xB4E4;&#xC5B4;,
          &#xD68C;&#xC0AC;&#xC758; &#xB3C4;&#xBA54;&#xC778;&#xC774; Ajax.com&#xC774;&#xACE0;
          Hello&#xB77C;&#xB294; &#xC560;&#xD50C;&#xB9AC;&#xCF00;&#xC774;&#xC158;&#xC744;
          &#xC0DD;&#xC131;&#xD558;&#xB294; &#xACBD;&#xC6B0; com.Ajax.Hello &#xBB38;&#xC790;&#xC5F4;&#xC744;
          &#xD560;&#xB2F9;&#xD560; &#xC218; &#xC788;&#xC2B5;&#xB2C8;&#xB2E4;.</p>
        <p>&#xBC88;&#xB4E4; &#xC2DD;&#xBCC4;&#xC790;&#xB294; &#xC751;&#xC6A9; &#xD504;&#xB85C;&#xADF8;&#xB7A8;
          &#xC11C;&#xBA85;&#xC744; &#xAC80;&#xC99D;&#xD558;&#xB294; &#xB370; &#xC0AC;&#xC6A9;&#xB429;&#xB2C8;&#xB2E4;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>CFBundleVersion</p>
        <p>(Bundle version)</p>
      </td>
      <td style="text-align:left">Bundle version &#xBB38;&#xC790;&#xC5F4;&#xC740; &#xBC88;&#xB4E4;&#xC758;
        &#xBE4C;&#xB4DC; &#xBC84;&#xC804; &#xBC88;&#xD638;&#xB97C; &#xC9C0;&#xC815;&#xD569;&#xB2C8;&#xB2E4;.
        &#xC774; &#xAC12;&#xC740; &#xD55C; &#xAC1C; &#xC774;&#xC0C1;&#xC758; &#xB9C8;&#xCE68;&#xD45C;&#xB85C;
        &#xAD6C;&#xBD84;&#xB418;&#xB294; &#xC815;&#xC218;&#xB85C; &#xAD6C;&#xC131;&#xB41C;
        &#xBB38;&#xC790;&#xC5F4;&#xC785;&#xB2C8;&#xB2E4;. &#xC774; &#xAC12;&#xC740;
        &#xC9C0;&#xC18D;&#xC801;&#xC73C;&#xB85C; &#xC99D;&#xAC00;&#xD558;&#xAC8C;
        &#xB418;&#xC5B4;&#xC788;&#xC73C;&#xBA70; &#xC9C0;&#xC5ED;&#xD654;&#xD560;
        &#xC218; &#xC5C6;&#xC2B5;&#xB2C8;&#xB2E4;.</td>
    </tr>
    <tr>
      <td style="text-align:left">CFBundleIconFiles</td>
      <td style="text-align:left">
        <p>&#xC560;&#xD50C;&#xB9AC;&#xCF00;&#xC774;&#xC158;&#xC758; &#xB2E4;&#xC591;&#xD55C;
          &#xC544;&#xC774;&#xCF58;&#xC5D0; &#xC0AC;&#xC6A9;&#xB418;&#xB294; &#xC774;&#xBBF8;&#xC9C0;&#xC758;
          &#xD30C;&#xC77C; &#xC774;&#xB984;&#xC774; &#xD3EC;&#xD568;&#xB41C; &#xBB38;&#xC790;&#xC5F4;
          &#xBC30;&#xC5F4;&#xC785;&#xB2C8;&#xB2E4;. &#xAE30;&#xC220;&#xC801;&#xC73C;&#xB85C;
          &#xD544;&#xC218;&#xC801;&#xC778; &#xAC12;&#xC740; &#xC544;&#xB2C8;&#xC9C0;&#xB9CC;,
          &#xC0AC;&#xC6A9;&#xD558;&#xB294; &#xAC83;&#xC774; &#xC88B;&#xC2B5;&#xB2C8;&#xB2E4;.</p>
        <p>&#xC774; &#xD0A4;&#xB294; iOS 3.2 &#xC774;&#xC0C1;&#xC5D0;&#xC11C; &#xC9C0;&#xC6D0;&#xB429;&#xB2C8;&#xB2E4;.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>LSRequiresIPhoneOS</p>
        <p>(Application requires iOS environment)</p>
      </td>
      <td style="text-align:left">&#xBC88;&#xB4E4;&#xC774; iOS&#xC5D0;&#xC11C;&#xB9CC; &#xC2E4;&#xD589;&#xAC00;&#xB2A5;&#xD55C;&#xC9C0;&#xB97C;
        &#xB098;&#xD0C0;&#xB0B4;&#xB294; BOOL &#xAC12;&#xC785;&#xB2C8;&#xB2E4;.
        Xcode&#xB294; &#xC774; &#xD0A4;&#xB97C; &#xC790;&#xB3D9;&#xC73C;&#xB85C;
        &#xCD94;&#xAC00;&#xD558;&#xACE0; &#xAC12;&#xC744; true&#xB85C; &#xC124;&#xC815;&#xD569;&#xB2C8;&#xB2E4;.
        &#xC774; &#xD0A4;&#xC758; &#xAC12;&#xC740; &#xBCC0;&#xACBD;&#xD558;&#xC9C0;
        &#xB9C8;&#xC138;&#xC694;.</td>
    </tr>
    <tr>
      <td style="text-align:left">UIRequiredDeviceCapabilities</td>
      <td style="text-align:left">
        <p>iTunes&#xC640; App Store&#xAC00; &#xC560;&#xD50C;&#xB9AC;&#xCF00;&#xC774;&#xC158;&#xC744;
          &#xC2E4;&#xD589;&#xD558;&#xAE30; &#xC704;&#xD574; &#xD544;&#xC694;&#xB85C;
          &#xD558;&#xB294; &#xB514;&#xBC14;&#xC774;&#xC2A4; &#xAE30;&#xB2A5;&#xC744;
          &#xC54C;&#xB824;&#xC8FC;&#xB294; &#xD0A4;&#xC785;&#xB2C8;&#xB2E4;. iTunes&#xC640;
          Mobile App Store&#xB294; &#xC774; &#xBAA9;&#xB85D;&#xC744; &#xC0AC;&#xC6A9;&#xD558;&#xC5EC;
          &#xACE0;&#xAC1D;&#xC774; &#xD574;&#xB2F9; &#xAE30;&#xB2A5;&#xC744; &#xC9C0;&#xC6D0;&#xD558;&#xC9C0;
          &#xC54A;&#xB294; &#xAE30;&#xAE30;&#xC5D0; &#xC560;&#xD50C;&#xB9AC;&#xCF00;&#xC774;&#xC158;&#xC744;
          &#xC124;&#xCE58;&#xD558;&#xC9C0; &#xBABB;&#xD558;&#xB3C4;&#xB85D; &#xD569;&#xB2C8;&#xB2E4;.</p>
        <p>&#xC774; &#xD0A4;&#xC758; &#xAC12;&#xC740; &#xBC30;&#xC5F4; &#xB610;&#xB294;
          &#xB515;&#xC154;&#xB108;&#xB9AC;&#xC785;&#xB2C8;&#xB2E4;. &#xBC30;&#xC5F4;&#xC744;
          &#xC0AC;&#xC6A9;&#xD558;&#xB294; &#xACBD;&#xC6B0; &#xC9C0;&#xC815;&#xB41C;
          &#xD0A4;&#xAC00; &#xD3EC;&#xD568;&#xB418;&#xC5B4;&#xC788;&#xC73C;&#xBA74;
          &#xD574;&#xB2F9; &#xAE30;&#xB2A5;&#xC774; &#xD544;&#xC694;&#xD558;&#xB2E4;&#xB294;
          &#xAC83;&#xC744; &#xB098;&#xD0C0;&#xB0B4;&#xBA70;, &#xB515;&#xC154;&#xB108;&#xB9AC;&#xB97C;
          &#xC0AC;&#xC6A9;&#xD560; &#xACBD;&#xC6B0; &#xAC01; &#xD0A4;&#xC5D0; &#xB300;&#xD574;
          BOOL &#xAC12;&#xC744; &#xC9C0;&#xC815;&#xD574;&#xC11C; &#xD574;&#xB2F9;
          &#xAE30;&#xB2A5;&#xC758; &#xD544;&#xC694; &#xC5EC;&#xBD80;&#xB97C; &#xD45C;&#xC2DC;&#xD569;&#xB2C8;&#xB2E4;.
          &#xB450; &#xACBD;&#xC6B0; &#xBAA8;&#xB450; &#xD0A4;&#xB97C; &#xD3EC;&#xD568;&#xD558;&#xC9C0;
          &#xC54A;&#xC73C;&#xBA74; &#xAE30;&#xB2A5;&#xC774; &#xD544;&#xC694;&#xD558;&#xC9C0;
          &#xC54A;&#xC74C;&#xC744; &#xB098;&#xD0C0;&#xB0C5;&#xB2C8;&#xB2E4;.</p>
        <p>&#xB515;&#xC154;&#xB108;&#xB9AC;&#xC5D0; &#xD3EC;&#xD568;&#xD560; &#xD0A4;
          &#xBAA9;&#xB85D;&#xC740; Information Property List &#xD0A4;&#xB97C; &#xCC38;&#xC870;&#xD558;&#xC138;&#xC694;.
          &#xC774; &#xD0A4;&#xB294; iOS 3.0 &#xC774;&#xC0C1;&#xC5D0;&#xC11C; &#xC9C0;&#xC6D0;&#xB429;&#xB2C8;&#xB2E4;.</p>
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
      <td style="text-align:left">&#xC560;&#xD50C;&#xB9AC;&#xCF00;&#xC774;&#xC158;&#xC758; &#xAE30;&#xBCF8;
        nib &#xD30C;&#xC77C; &#xC774;&#xB984;&#xC744; &#xC2DD;&#xBCC4;&#xD558;&#xB294;
        &#xBB38;&#xC790;&#xC5F4;. &#xD504;&#xB85C;&#xC81D;&#xD2B8;&#xC5D0; &#xB300;&#xD574;
        &#xC0DD;&#xC131;&#xB41C; &#xAE30;&#xBCF8; nib &#xD30C;&#xC77C;&#xC774;
        &#xC544;&#xB2CC; &#xB2E4;&#xB978; nib &#xD30C;&#xC77C;&#xC744; &#xC0AC;&#xC6A9;&#xD558;&#xB824;&#xBA74;
        &#xD574;&#xB2F9; nib &#xD30C;&#xC77C;&#xC758; &#xC774;&#xB984;&#xC744;
        &#xC774; &#xD0A4;&#xC640; &#xC5F0;&#xACB0;&#xC2DC;&#xCF1C;&#xC57C; &#xD569;&#xB2C8;&#xB2E4;.
        nib &#xD30C;&#xC77C; &#xC774;&#xB984;&#xC5D0;&#xB294; .nib &#xD30C;&#xC77C;
        &#xC774;&#xB984; &#xD655;&#xC7A5;&#xBA85;&#xC774; &#xD3EC;&#xD568;&#xB418;&#xC9C0;
        &#xC54A;&#xC544;&#xC57C; &#xD569;&#xB2C8;&#xB2E4;.</td>
    </tr>
    <tr>
      <td style="text-align:left">UIStatusBarStyle</td>
      <td style="text-align:left">
        <p>&#xC751;&#xC6A9; &#xD504;&#xB85C;&#xADF8;&#xB7A8;&#xC774; &#xC2DC;&#xC791;&#xB420;
          &#xB54C; &#xC0C1;&#xD0DC; &#xD45C;&#xC2DC;&#xC904;&#xC758; &#xC2A4;&#xD0C0;&#xC77C;&#xC744;
          &#xC2DD;&#xBCC4;&#xD558;&#xB294; &#xBB38;&#xC790;&#xC5F4;. &#xC774; &#xAC12;&#xC740;
          UIApplication.h &#xD5E4;&#xB354; &#xD30C;&#xC77C;&#xC5D0; &#xC120;&#xC5B8;&#xB41C;
          UIStatusBarStyle &#xC0C1;&#xC218;&#xB97C; &#xAE30;&#xBC18;&#xC73C;&#xB85C;
          &#xD569;&#xB2C8;&#xB2E4;. &#xAE30;&#xBCF8; &#xC2A4;&#xD0C0;&#xC77C;&#xC740;
          UIStatusBarStyleDefault&#xC785;&#xB2C8;&#xB2E4;. &#xC560;&#xD50C;&#xB9AC;&#xCF00;&#xC774;&#xC158;&#xC774;
          &#xC2E4;&#xD589;&#xC744; &#xB9C8;&#xCE60; &#xB54C;(didFinishLaunching)&#xC774;
          &#xCD08;&#xAE30; &#xC0C1;&#xD0DC; &#xD45C;&#xC2DC;&#xC904; &#xC2A4;&#xD0C0;&#xC77C;&#xC744;
          &#xBCC0;&#xACBD;&#xD560; &#xC218; &#xC788;&#xC2B5;&#xB2C8;&#xB2E4;.</p>
        <p>&#xC774; &#xD0A4;&#xB97C; &#xC9C0;&#xC815;&#xD558;&#xC9C0; &#xC54A;&#xC73C;&#xBA74;
          iOS&#xC5D0;&#xC11C; &#xAE30;&#xBCF8; &#xC0C1;&#xD0DC; &#xD45C;&#xC2DC;&#xC904;&#xC744;
          &#xD45C;&#xC2DC;&#xD569;&#xB2C8;&#xB2E4;.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">UIStatusBarHidden</td>
      <td style="text-align:left">&#xC560;&#xD50C;&#xB9AC;&#xCF00;&#xC774;&#xC158;&#xC774; &#xC2DC;&#xC791;&#xB420;
        &#xB54C; &#xC0C1;&#xD0DC; &#xD45C;&#xC2DC;&#xC904;&#xC744; &#xCC98;&#xC74C;&#xBD80;&#xD130;
        &#xC228;&#xAE38; &#xAC83;&#xC778;&#xC9C0;&#xB97C; &#xACB0;&#xC815;&#xD558;&#xB294;
        BOOL &#xAC12;&#xC785;&#xB2C8;&#xB2E4;. &#xC0C1;&#xD0DC; &#xD45C;&#xC2DC;&#xC904;&#xC744;
        &#xC228;&#xAE30;&#xB824;&#xBA74; &#xC774; &#xAC12;&#xC744; true&#xB85C;
        &#xC124;&#xC815;&#xD569;&#xB2C8;&#xB2E4;. &#xAE30;&#xBCF8;&#xAC12;&#xC740;
        false&#xC785;&#xB2C8;&#xB2E4;.</td>
    </tr>
    <tr>
      <td style="text-align:left">UIInterfaceOrientation</td>
      <td style="text-align:left">&#xC560;&#xD50C;&#xB9AC;&#xCF00;&#xC774;&#xC158; UI&#xC758; &#xCD08;&#xAE30;
        &#xBC29;&#xD5A5;&#xC744; &#xC2DD;&#xBCC4;&#xD558;&#xB294; &#xBB38;&#xC790;&#xC5F4;.
        &#xC774; &#xAC12;&#xC740; UIApplication.h &#xD5E4;&#xB354; &#xD30C;&#xC77C;&#xC5D0;
        &#xC120;&#xC5B8;&#xB41C; UIInterfaceOrientation &#xC0C1;&#xC218;&#xB97C;
        &#xAE30;&#xBC18;&#xC73C;&#xB85C; &#xD569;&#xB2C8;&#xB2E4;. &#xAE30;&#xBCF8;
        &#xC2A4;&#xD0C0;&#xC77C;&#xC740; UIInterfaceOrientationPortrait&#xC785;&#xB2C8;&#xB2E4;.</td>
    </tr>
    <tr>
      <td style="text-align:left">UIPrerenderedIcon</td>
      <td style="text-align:left">&#xC560;&#xD50C;&#xB9AC;&#xCF00;&#xC774;&#xC158; &#xC544;&#xC774;&#xCF58;&#xC5D0;
        &#xC774;&#xBBF8; gloss &#xB610;&#xB294; bevel &#xD6A8;&#xACFC;&#xAC00;
        &#xD3EC;&#xD568;&#xB418;&#xC5B4; &#xC788;&#xB294;&#xC9C0;&#xB97C; &#xB098;&#xD0C0;&#xB0B4;&#xB294;
        BOOL &#xAC12;&#xC785;&#xB2C8;&#xB2E4;. &#xAE30;&#xBCF8;&#xAC12;&#xC740;
        false&#xC785;&#xB2C8;&#xB2E4;. &#xC2DC;&#xC2A4;&#xD15C;&#xC774; &#xBE44;&#xC2B7;&#xD55C;
        &#xD6A8;&#xACFC;&#xB97C; &#xC544;&#xC774;&#xCF58;&#xC5D0; &#xC801;&#xC6A9;&#xD558;&#xC9C0;
        &#xC54A;&#xAE30;&#xB97C; &#xBC14;&#xB780;&#xB2E4;&#xBA74; &#xC774;&#xAC83;&#xC744;
        true&#xB85C; &#xC124;&#xC815;&#xD558;&#xC138;&#xC694;.</td>
    </tr>
    <tr>
      <td style="text-align:left">UIRequiresPersistentWiFi</td>
      <td style="text-align:left">
        <p>&#xC560;&#xD50C;&#xB9AC;&#xCF00;&#xC774;&#xC158;&#xC774; Wi-Fi &#xB124;&#xD2B8;&#xC6CC;&#xD06C;&#xB97C;
          &#xC0AC;&#xC6A9;&#xD558;&#xC5EC; &#xD1B5;&#xC2E0;&#xD55C;&#xB2E4;&#xB294;
          &#xAC83;&#xC744; &#xC2DC;&#xC2A4;&#xD15C;&#xC5D0; &#xC54C;&#xB824;&#xC8FC;&#xB294;
          BOOL &#xAC12;&#xC785;&#xB2C8;&#xB2E4;. Wi-Fi&#xB97C; &#xC77C;&#xC815;&#xC2DC;&#xAC04;
          &#xC0AC;&#xC6A9;&#xD558;&#xB294; &#xC560;&#xD50C;&#xB9AC;&#xCF00;&#xC774;&#xC158;&#xC740;
          &#xC774; &#xD0A4;&#xB97C; true&#xB85C; &#xC124;&#xC815;&#xD574;&#xC57C;
          &#xD569;&#xB2C8;&#xB2E4;. &#xADF8;&#xB807;&#xC9C0; &#xC54A;&#xC73C;&#xBA74;
          &#xAE30;&#xAE30;&#xB294; &#xC804;&#xC6D0;&#xC744; &#xC808;&#xC57D;&#xD558;&#xAE30;
          &#xC704;&#xD574; 30&#xBD84; &#xD6C4;&#xC5D0; Wi-Fi &#xC5F0;&#xACB0;&#xC744;
          &#xC885;&#xB8CC;&#xD569;&#xB2C8;&#xB2E4;. &#xB610;&#xD55C; &#xC774; &#xD50C;&#xB798;&#xADF8;&#xB97C;
          &#xC124;&#xC815;&#xD558;&#xBA74; &#xC2DC;&#xC2A4;&#xD15C;&#xC774; Wi-Fi&#xB97C;
          &#xC0AC;&#xC6A9;&#xD560; &#xC218; &#xC788;&#xC9C0;&#xB9CC; &#xD604;&#xC7AC;
          &#xC0AC;&#xC6A9;&#xB418;&#xC9C0; &#xC54A;&#xC744; &#xB54C; &#xB124;&#xD2B8;&#xC6CC;&#xD06C;
          &#xC120;&#xD0DD; &#xB300;&#xD654; &#xC0C1;&#xC790;&#xB97C; &#xD45C;&#xC2DC;&#xD574;&#xC57C;
          &#xD568;&#xC744; &#xC54C; &#xC218; &#xC788;&#xC2B5;&#xB2C8;&#xB2E4;. &#xAE30;&#xBCF8;&#xAC12;&#xC740;
          false&#xC785;&#xB2C8;&#xB2E4;.</p>
        <p>&#xC774; &#xC18D;&#xC131;&#xC758; &#xAC12;&#xC774; true&#xC778; &#xACBD;&#xC6B0;&#xC5D0;&#xB3C4;
          &#xAE30;&#xAE30;&#xAC00; &#xC720;&#xD734; &#xC0C1;&#xD0DC;(&#xC989;, &#xC2A4;&#xD06C;&#xB9B0;
          &#xC7A0;&#xAE08;)&#xC77C; &#xB54C;&#xB294; &#xC774; &#xD0A4;&#xB294; &#xD6A8;&#xACFC;&#xAC00;
          &#xC5C6;&#xC2B5;&#xB2C8;&#xB2E4;. &#xC774; &#xC2DC;&#xAC04; &#xB3D9;&#xC548;
          &#xC560;&#xD50C;&#xB9AC;&#xCF00;&#xC774;&#xC740; &#xBE44;&#xD65C;&#xC131;
          &#xC0C1;&#xD0DC;&#xB85C; &#xAC04;&#xC8FC;&#xB418;&#xBA70;, &#xC77C;&#xBD80;
          &#xC218;&#xC900;&#xC5D0;&#xC11C; &#xC791;&#xB3D9;&#xD560; &#xC218; &#xC788;&#xC9C0;&#xB9CC;
          Wi-Fi &#xC5F0;&#xACB0;&#xC740; &#xB418;&#xC9C0; &#xC54A;&#xC2B5;&#xB2C8;&#xB2E4;.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">UILaunchImageFile</td>
      <td style="text-align:left">&#xC560;&#xD50C;&#xB9AC;&#xCF00;&#xC774;&#xC158;&#xC758; &#xC2DC;&#xC791;
        &#xC774;&#xBBF8;&#xC9C0;&#xC5D0; &#xC0AC;&#xC6A9;&#xB418;&#xB294; &#xAE30;&#xBCF8;
        &#xD30C;&#xC77C; &#xC774;&#xB984;&#xC744; &#xD3EC;&#xD568;&#xD558;&#xB294;
        &#xBB38;&#xC790;&#xC5F4;. &#xC774; &#xD0A4;&#xB97C; &#xC9C0;&#xC815;&#xD558;&#xC9C0;
        &#xC54A;&#xC73C;&#xBA74; &#xAE30;&#xBCF8; &#xD30C;&#xC77C; &#xC774;&#xB984;&#xC740; <code>Default</code> &#xBB38;&#xC790;&#xC5F4;&#xB85C;
        &#xAC04;&#xC8FC;&#xB429;&#xB2C8;&#xB2E4;.</td>
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
      <th style="text-align:left">&#xB514;&#xB809;&#xD1A0;&#xB9AC;</th>
      <th style="text-align:left">&#xC124;&#xBA85;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">MacOS</td>
      <td style="text-align:left">&#xC560;&#xD50C;&#xB9AC;&#xCF00;&#xC774;&#xC158;&#xC758; &#xB3C5;&#xB9BD;&#xC2E4;&#xD589;&#xD615;
        &#xCF54;&#xB4DC;&#xAC00; &#xB4E4;&#xC5B4; &#xC788;&#xC2B5;&#xB2C8;&#xB2E4;.
        &#xC77C;&#xBC18;&#xC801;&#xC73C;&#xB85C; &#xC774; &#xB514;&#xB809;&#xD1A0;&#xB9AC;&#xC5D0;&#xB294;
        &#xC560;&#xD50C;&#xB9AC;&#xCF00;&#xC774;&#xC158;&#xC758; &#xAE30;&#xBCF8;
        &#xC9C4;&#xC785;&#xC810;&#xACFC; &#xC815;&#xC801;&#xC73C;&#xB85C; &#xB9C1;&#xD06C;&#xB41C;
        &#xCF54;&#xB4DC;&#xAC00; &#xD3EC;&#xD568;&#xB41C; &#xC774;&#xC9C4; &#xD30C;&#xC77C;
        &#xD558;&#xB098;&#xB9CC; &#xD3EC;&#xD568;&#xB418;&#xC5B4; &#xC788;&#xC9C0;&#xB9CC;
        &#xB2E4;&#xB978; &#xB3C5;&#xB9BD;&#xC2E4;&#xD589;&#xD615; &#xC2E4;&#xD589;&#xD30C;&#xC77C;(&#xC608;
        : &#xBA85;&#xB839;&#xC904; &#xB3C4;&#xAD6C;)&#xB3C4; &#xB4E4;&#xC5B4;&#xAC08;
        &#xC218; &#xC788;&#xC2B5;&#xB2C8;&#xB2E4;.</td>
    </tr>
    <tr>
      <td style="text-align:left">Resources</td>
      <td style="text-align:left">&#xBAA8;&#xB4E0; &#xC751;&#xC6A9; &#xD504;&#xB85C;&#xADF8;&#xB7A8;&#xC758;
        &#xB9AC;&#xC18C;&#xC2A4; &#xD30C;&#xC77C;&#xC744; &#xD3EC;&#xD568;&#xD569;&#xB2C8;&#xB2E4;.
        &#xC774; &#xB514;&#xB809;&#xD1A0;&#xB9AC;&#xC758; &#xB0B4;&#xC6A9;&#xC740;
        &#xC9C0;&#xC5ED;&#xD654; &#xB41C; &#xB9AC;&#xC18C;&#xC2A4;&#xC640; &#xADF8;&#xB807;&#xC9C0;
        &#xC54A;&#xC740; &#xB9AC;&#xC18C;&#xC2A4;&#xB97C; &#xAD6C;&#xBD84;&#xD558;&#xAE30;
        &#xC704;&#xD574; &#xB354; &#xCCB4;&#xACC4;&#xD654;&#xB418;&#xC5B4; &#xC788;&#xC2B5;&#xB2C8;&#xB2E4;.
        &#xC774; &#xB514;&#xB809;&#xD1A0;&#xB9AC;&#xC758; &#xAD6C;&#xC870;&#xC5D0;
        &#xB300;&#xD55C; &#xC790;&#xC138;&#xD55C; &#xB0B4;&#xC6A9;&#xC740; Resources
        &#xB514;&#xB809;&#xD1A0;&#xB9AC;&#xB97C; &#xCC38;&#xC870;&#xD558;&#xC2ED;&#xC2DC;&#xC624;.</td>
    </tr>
    <tr>
      <td style="text-align:left">Frameworks</td>
      <td style="text-align:left">
        <p>&#xC2E4;&#xD589; &#xD30C;&#xC77C;&#xC5D0; &#xC0AC;&#xC6A9;&#xB418;&#xB294;
          &#xAC1C;&#xC778; &#xACF5;&#xC720; &#xB77C;&#xC774;&#xBE0C;&#xB7EC;&#xB9AC;
          &#xBC0F; &#xD504;&#xB808;&#xC784;&#xC6CC;&#xD06C;&#xB97C; &#xD3EC;&#xD568;&#xD569;&#xB2C8;&#xB2E4;.
          &#xC774; &#xB514;&#xB809;&#xD1A0;&#xB9AC;&#xC758; &#xD504;&#xB808;&#xC784;&#xC6CC;&#xD06C;&#xB294;
          &#xC560;&#xD50C;&#xB9AC;&#xCF00;&#xC774;&#xC158;&#xC5D0; &#xB9AC;&#xBE44;&#xC804;
          &#xC7A0;&#xAE08;&#xB418;&#xBA70; &#xC6B4;&#xC601;&#xCCB4;&#xC81C;&#xC5D0;&#xC11C;
          &#xC0AC;&#xC6A9;&#xD560; &#xC218; &#xC788;&#xB294; &#xB2E4;&#xB978; &#xCD5C;&#xC2E0;
          &#xBC84;&#xC804;&#xC73C;&#xB85C; &#xB300;&#xCCB4;&#xB420; &#xC218; &#xC5C6;&#xC2B5;&#xB2C8;&#xB2E4;.
          &#xC989;, &#xC774; &#xB514;&#xB809;&#xD1A0;&#xB9AC;&#xC5D0; &#xD3EC;&#xD568;&#xB41C;
          &#xD504;&#xB808;&#xC784;&#xC6CC;&#xD06C;&#xB294; &#xC6B4;&#xC601;&#xCCB4;&#xC81C;&#xC758;
          &#xB2E4;&#xB978; &#xBD80;&#xBD84;&#xC5D0;&#xC11C; &#xBC1C;&#xACAC;&#xB418;&#xB294;
          &#xBE44;&#xC2B7;&#xD55C; &#xC774;&#xB984;&#xC758; &#xD504;&#xB808;&#xC784;&#xC6CC;&#xD06C;&#xBCF4;&#xB2E4;
          &#xC6B0;&#xC120;&#xD569;&#xB2C8;&#xB2E4;.</p>
        <p>&#xC560;&#xD50C;&#xB9AC;&#xCF00;&#xC774;&#xC158; &#xBC88;&#xB4E4;&#xC5D0;
          &#xAC1C;&#xC778; &#xD504;&#xB808;&#xC784;&#xC6CC;&#xD06C;&#xB97C; &#xCD94;&#xAC00;&#xD558;&#xB294;
          &#xBC29;&#xBC95;&#xC5D0; &#xB300;&#xD55C; &#xC815;&#xBCF4;&#xB294; <a href="../../etc/not-found.md">Framework Programming Guide</a>&#xB97C;
          &#xCC38;&#xC870;&#xD558;&#xC2ED;&#xC2DC;&#xC624;.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">PlugIns</td>
      <td style="text-align:left">&#xC560;&#xD50C;&#xB9AC;&#xCF00;&#xC774;&#xC158;&#xC758; &#xAE30;&#xBCF8;
        &#xAE30;&#xB2A5;&#xC744; &#xD655;&#xC7A5;&#xD558;&#xB294; &#xB85C;&#xB4DC;
        &#xAC00;&#xB2A5;&#xD55C; &#xBC88;&#xB4E4;&#xC744; &#xD3EC;&#xD568;&#xD569;&#xB2C8;&#xB2E4;.
        &#xC774; &#xB514;&#xB809;&#xD1A0;&#xB9AC;&#xB97C; &#xC0AC;&#xC6A9;&#xD558;&#xC5EC;
        &#xC560;&#xD50C;&#xB9AC;&#xCF00;&#xC774;&#xC158;&#xC758; &#xD504;&#xB85C;&#xC138;&#xC2A4;
        &#xACF5;&#xAC04;&#xC5D0; &#xB85C;&#xB4DC;&#xD574;&#xC57C; &#xD558;&#xB294;
        &#xCF54;&#xB4DC; &#xBAA8;&#xB4C8;&#xC744; &#xD3EC;&#xD568;&#xD560; &#xC218;
        &#xC788;&#xC2B5;&#xB2C8;&#xB2E4;. &#xB3C5;&#xB9BD; &#xC2E4;&#xD589;&#xD615;
        &#xC2E4;&#xD589; &#xD30C;&#xC77C;&#xC744; &#xC800;&#xC7A5;&#xD558;&#xB294;
        &#xC6A9;&#xB3C4;&#xB85C;&#xB294; &#xC0AC;&#xC6A9;&#xB418;&#xC9C0; &#xC54A;&#xC2B5;&#xB2C8;&#xB2E4;.</td>
    </tr>
    <tr>
      <td style="text-align:left">SharedSupport</td>
      <td style="text-align:left">&#xC560;&#xD50C;&#xB9AC;&#xCF00;&#xC774;&#xC158; &#xC2E4;&#xD589; &#xAE30;&#xB2A5;&#xC5D0;
        &#xC601;&#xD5A5;&#xC744; &#xC8FC;&#xC9C0; &#xC54A;&#xB294; &#xBD80;&#xAC00;&#xC801;&#xC778;
        &#xB9AC;&#xC18C;&#xC2A4;&#xAC00; &#xD3EC;&#xD568;&#xB418;&#xC5B4; &#xC788;&#xC2B5;&#xB2C8;&#xB2E4;.
        &#xC774; &#xB514;&#xB809;&#xD1A0;&#xB9AC;&#xB97C; &#xC0AC;&#xC6A9;&#xD558;&#xC5EC;
        &#xC560;&#xD50C;&#xB9AC;&#xCF00;&#xC774;&#xC158;&#xC758; &#xC2E4;&#xD589;&#xC5D0;
        &#xC601;&#xD5A5;&#xC744; &#xC8FC;&#xC9C0; &#xC54A;&#xB294; &#xBB38;&#xC11C;
        &#xD15C;&#xD50C;&#xB9BF;, &#xD074;&#xB9BD; &#xC544;&#xD2B8; &#xBC0F; &#xD29C;&#xD1A0;&#xB9AC;&#xC5BC;&#xC744;
        &#xD3EC;&#xD568;&#xC2DC;&#xD0AC; &#xC218; &#xC788;&#xC2B5;&#xB2C8;&#xB2E4;.</td>
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
      <td style="text-align:left">&#xBC88;&#xB4E4;&#xC758; &#xC9E7;&#xC740; &#xC774;&#xB984;&#xC785;&#xB2C8;&#xB2E4;.
        &#xC774; &#xD0A4;&#xC758; &#xAC12;&#xC740; &#xC77C;&#xBC18;&#xC801;&#xC73C;&#xB85C;
        &#xC560;&#xD50C;&#xB9AC;&#xCF00;&#xC774;&#xC158;&#xC758; &#xC774;&#xB984;&#xC73C;&#xB85C;
        &#xC0AC;&#xC6A9;&#xB429;&#xB2C8;&#xB2E4;. Xcode&#xB294; &#xC0C8; &#xD504;&#xB85C;&#xC81D;&#xD2B8;&#xB97C;
        &#xB9CC;&#xB4E4;&#xB54C; &#xAE30;&#xBCF8;&#xC801;&#xC73C;&#xB85C; &#xC774;
        &#xD0A4;&#xC758; &#xAC12;&#xC744; &#xC124;&#xC815;&#xD569;&#xB2C8;&#xB2E4;.</td>
    </tr>
    <tr>
      <td style="text-align:left">CFBundleDisplayName
        <br />(Bundle display name)</td>
      <td style="text-align:left">&#xC560;&#xD50C;&#xB9AC;&#xCF00;&#xC774;&#xC158; &#xC774;&#xB984;&#xC758;
        &#xC9C0;&#xC5ED;&#xD654;&#xB41C; &#xBC84;&#xC804;&#xC785;&#xB2C8;&#xB2E4;.
        &#xC77C;&#xBC18;&#xC801;&#xC73C;&#xB85C; &#xAC01; &#xC5B8;&#xC5B4;&#xBCC4;
        &#xB9AC;&#xC18C;&#xC2A4; &#xB514;&#xB809;&#xD1A0;&#xB9AC;&#xC758; InfoPlist.strings
        &#xD30C;&#xC77C;&#xC5D0; &#xC774; &#xD0A4;&#xC758; &#xC9C0;&#xC5ED;&#xD654;&#xB41C;
        &#xAC12;&#xC744; &#xD3EC;&#xD568;&#xC2DC;&#xD0B5;&#xB2C8;&#xB2E4;.</td>
    </tr>
    <tr>
      <td style="text-align:left">CFBundleIdentifier
        <br />(Bundle identifier)</td>
      <td style="text-align:left">
        <p>&#xC2DC;&#xC2A4;&#xD15C;&#xC5D0;&#xC11C; &#xC560;&#xD50C;&#xB9AC;&#xCF00;&#xC774;&#xC158;&#xC744;
          &#xC2DD;&#xBCC4;&#xD560;&#xB54C; &#xC0AC;&#xC6A9;&#xD558;&#xB294; &#xBB38;&#xC790;&#xC5F4;&#xC785;&#xB2C8;&#xB2E4;.
          &#xC774; &#xBB38;&#xC790;&#xC5F4;&#xC740; &#xC601;&#xC22B;&#xC790; (A-Z,
          a-z, 0-9), &#xD558;&#xC774;&#xD508; (-) &#xBC0F; &#xB9C8;&#xCE68;&#xD45C;
          (.) &#xBB38;&#xC790; &#xB9CC; &#xD3EC;&#xD568;&#xD558;&#xB294; Uniform
          type identifier(UTI)&#xD615;&#xC2DD;&#xACFC; &#xC5ED; DNS &#xD615;&#xC2DD;&#xC744;
          &#xB530;&#xB77C;&#xC57C; &#xD569;&#xB2C8;&#xB2E4;. &#xC608;&#xB97C; &#xB4E4;&#xC5B4;,
          &#xD68C;&#xC0AC; &#xB3C4;&#xBA54;&#xC778;&#xC774; Ajax.com&#xC774;&#xACE0;
          Hello&#xB77C;&#xB294; &#xC560;&#xD50C;&#xB9AC;&#xCF00;&#xC774;&#xC158;&#xC744;
          &#xC791;&#xC131;&#xD558;&#xB294; &#xACBD;&#xC6B0; com.Ajax.Hello &#xBB38;&#xC790;&#xC5F4;&#xC744;
          &#xC560;&#xD50C;&#xB9AC;&#xCF00;&#xC774;&#xC158;&#xC758; &#xBC88;&#xB4E4;
          &#xC2DD;&#xBCC4;&#xC790;&#xB85C; &#xD560;&#xB2F9;&#xD560; &#xC218; &#xC788;&#xC2B5;&#xB2C8;&#xB2E4;.</p>
        <p>&#xBC88;&#xB4E4; &#xC2DD;&#xBCC4;&#xC790;&#xB294; &#xC751;&#xC6A9; &#xD504;&#xB85C;&#xADF8;&#xB7A8;
          &#xC11C;&#xBA85;&#xC744; &#xD655;&#xC778;&#xD558;&#xB294; &#xB370; &#xC0AC;&#xC6A9;&#xB429;&#xB2C8;&#xB2E4;.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">CFBundleVersion
        <br />(Bundle version)</td>
      <td style="text-align:left">&#xBC88;&#xB4E4;&#xC758; &#xBE4C;&#xB4DC; &#xBC84;&#xC804; &#xBC88;&#xD638;&#xB97C;
        &#xC9C0;&#xC815;&#xD569;&#xB2C8;&#xB2E4;. &#xC774; &#xAC12;&#xC740; &#xD55C;
        &#xAC1C; &#xC774;&#xC0C1;&#xC758; &#xB9C8;&#xCE68;&#xD45C;&#xB85C; &#xAD6C;&#xBD84;&#xB418;&#xB294;
        &#xC815;&#xC218;&#xB85C; &#xAD6C;&#xC131;&#xB41C; &#xBB38;&#xC790;&#xC5F4;&#xC785;&#xB2C8;&#xB2E4;.
        &#xC774; &#xAC12;&#xC740; &#xC9C0;&#xC18D;&#xC801;&#xC73C;&#xB85C; &#xC99D;&#xAC00;&#xD558;&#xAC8C;
        &#xB418;&#xC5B4;&#xC788;&#xC73C;&#xBA70; &#xC9C0;&#xC5ED;&#xD654;&#xD560;
        &#xC218; &#xC5C6;&#xC2B5;&#xB2C8;&#xB2E4;.</td>
    </tr>
    <tr>
      <td style="text-align:left">CFBundlePackageType
        <br />(Bundle OS Type code)</td>
      <td style="text-align:left">&#xBC88;&#xB4E4; &#xC720;&#xD615;&#xC785;&#xB2C8;&#xB2E4;. &#xC560;&#xD50C;&#xB9AC;&#xCF00;&#xC774;&#xC158;&#xC758;
        &#xACBD;&#xC6B0; &#xC774; &#xD0A4;&#xC758; &#xAC12;&#xC740; &#xD56D;&#xC0C1;
        4&#xC790; &#xBB38;&#xC790;&#xC5F4; <code>APPL</code>&#xC785;&#xB2C8;&#xB2E4;.</td>
    </tr>
    <tr>
      <td style="text-align:left">CFBundleSignature
        <br />(Bundle creator OS Type code)</td>
      <td style="text-align:left">&#xBC88;&#xB4E4;&#xC758; &#xC791;&#xC131;&#xC790; &#xCF54;&#xB4DC;&#xC785;&#xB2C8;&#xB2E4;.
        &#xC774; &#xBB38;&#xC790;&#xC5F4;&#xC740; &#xBC88;&#xB4E4;&#xACFC; &#xAD00;&#xB828;&#xB41C;
        4&#xC790; &#xBB38;&#xC790;&#xC5F4;&#xC785;&#xB2C8;&#xB2E4;. &#xC608;&#xB97C;
        &#xB4E4;&#xC5B4; TextEdit &#xC560;&#xD50C;&#xB9AC;&#xCF00;&#xC774;&#xC158;&#xC758;
        &#xC2DC;&#xADF8;&#xB2C8;&#xCC98;&#xB294; ttxt&#xC785;&#xB2C8;&#xB2E4;.</td>
    </tr>
    <tr>
      <td style="text-align:left">CFBundleExecutable
        <br />(Executable file)</td>
      <td style="text-align:left">&#xC8FC; &#xC2E4;&#xD589; &#xD30C;&#xC77C;&#xC758; &#xC774;&#xB984;. &#xC774;&#xAC83;&#xC740;
        &#xC0AC;&#xC6A9;&#xC790;&#xAC00; &#xC560;&#xD50C;&#xB9AC;&#xCF00;&#xC774;&#xC158;&#xC744;
        &#xC2DC;&#xC791;&#xD560; &#xB54C; &#xC2E4;&#xD589;&#xB418;&#xB294; &#xCF54;&#xB4DC;&#xC785;&#xB2C8;&#xB2E4;.
        &#xC77C;&#xBC18;&#xC801;&#xC73C;&#xB85C; Xcode&#xB294; &#xBE4C;&#xB4DC;&#xC2DC;
        &#xC774; &#xD0A4;&#xC758; &#xAC12;&#xC744; &#xC790;&#xB3D9;&#xC73C;&#xB85C;
        &#xC124;&#xC815;&#xD569;&#xB2C8;&#xB2E4;.</td>
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

