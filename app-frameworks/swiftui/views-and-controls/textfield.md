---
description: 편집 가능한 텍스트 인터페이스를 보여주는 컨트롤
---

# TextField

> 원문 출처  
> [https://developer.apple.com/documentation/swiftui/textfield](https://developer.apple.com/documentation/swiftui/textfield)

## Summary

> **SDKs**
>
> * iOS 13.0+
> * macOS 10.15+
> * Mac Catalyst 13.0+
> * tvOS 13.0+
> * watchOS 6.0+
> * Xcode 11.0+
>
> **Framework**
>
> * SwiftUI

## Declaration

{% tabs %}
{% tab title="Swift" %}
```swift
struct TextField<Label> where Label : View
```
{% endtab %}
{% endtabs %}

## 개요 <a id="overview"></a>

텍스트 필드는 TextFieldStyle 인스턴스를 사용하여 디자인과 상호작용을 커스텀할 수 있습니다. 시스템은 런타임 중에 그 설정을 처리합니다. 플랫폼마다 플랫폼 스타일을 반영하는 기본 스타일을 제공하지만 개발자 스스로 특정 환경 내에서 모튼 텍스트 필드를 재정의하는 새로은 스타일을 제공할 수도 있습니다.

## 주제 <a id="topics"></a>

### 새 TextField View 생성 <a id="creating-a-textfield-view"></a>

* init\(LocalizedStringKey, text: Binding, onEditingChanged: \(Bool\) -&gt; Void, onCommit: \(\) -&gt; Void\) Label이 텍스트일 때 사용할 수 있습니다.
* init\(S, text: Binding, onEditingChanged: \(Bool\) -&gt; Void, onCommit: \(\) -&gt; Void\)

  Label이 텍스트일 때 사용할 수 있습니다.

* init\(LocalizedStringKey, value: Binding, formatter: Formatter, onEditingChanged: \(Bool\) -&gt; Void, onCommit: \(\) -&gt; Void\) Label이 텍스트일 때 사용할 수 있습니다.
* init\(S, value: Binding, formatter: Formatter, onEditingChanged: \(Bool\) -&gt; Void, onCommit: \(\) -&gt; Void\) Label이 텍스트일 때 사용할 수 있습니다.

### TextField 스타일링 <a id="styling-text-fields"></a>

* _struct_ PlainTextFieldStyle
* _struct_ RoundedBorderTextFieldStyle
* _struct_ SquareBorderTextFieldStyle
* _struct_ DefaultTextFieldStyle
* _protocol_ TextFieldStyle 텍스트 필드의 모양과 상호작용을 위한 스펙

### 표준 수정자 적용

* View Modifires 뷰와 거기에 포함된 뷰들을 표준 수정자를 적용함으로써 설정합니다

## 관련 문서 <a id="relationships"></a>

### Conforms To

* Equatable
* [View](view.md)

## 같이 보기 <a id="see-also"></a>

### Text

* _struct_ [Text](text.md) 한 줄 이상의 읽기전용 텍스트를 보여주는 View
* _struct_ SecureField 사용자가 노출되지 않는 텍스트를 입력할 수 있는 컨트롤
* _struct_ Font 실행환경에 의존적인 폰트

