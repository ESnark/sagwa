---
description: '유니코드 문자의 문자열을 만들며 처리하고, 정규식을 사용하여 패턴을 찾고, 텍스트의 자연어 분석을 수행합니다.'
---

# 문자열과 텍스트

> 원문 출처  
> [https://developer.apple.com/documentation/foundation/strings\_and\_text](https://developer.apple.com/documentation/foundation/strings_and_text)

## 주제 <a id="topics"></a>

### 문자열 <a id="strings"></a>

* struct String 문자 집합인 유니코드 문자열 값

### 문자열과 메타데이터 <a id="strings-with-metadata"></a>

* class NSAttributedString 텍스트 일부에 대한 관련 속성\(예: 시각적 스타일, 하이퍼링크, 접근성 데이터\)을 갖는 문자열
* class NSMutableAttributedString 텍스트 여러 부분에 관련된 속성\(예: 시각적 스타일, 하이퍼링크, 접근성 데이터\)을 갖는 변경 가능한 문자열

### 문자 <a id="characters"></a>

* struct CharacterSet 검색 작업에 사용할 유니코드 문자 값 세트
* typealias UnicodeScalar

### 자연어 처리 <a id="natural-language-processing"></a>

* class NSLinguisticTagger 자연어 텍스트를 분석하여 품사 및 어휘 클래스를 태그하고, 이름을 식별하고, 단어를 기본형으로 바꾼 다음 언어와 스크립트를 결정합니다.

### 패턴 매칭 <a id="pattern-matching"></a>

* class Scanner 문자 세트에서 하위 문자열 또는 문자들을 스캔하거나 10진수, 16진수와 부동소수점 표현에서 숫자형 값을 스캔하는 문자열 구문 분석기
* class NSRegularExpression

  유니 코드 문자열에 적용되는 컴파일 된 정규 표현식의 불변 표현

* class NSDataDetector 자연어 텍스트를 미리 정의된 데이터 패턴에 매칭시키는 특수한 정규 표현식 객체
* class NSTextCheckingResult 정규 표현식에 매칭시키는 것과 마찬가지로, 텍스트 블록분석 중에 발견되는 텍스트 컨텐츠
* let NSNotFound: Int 요청된 항목이 발견되지 않았거나 존재하지 않음을 가리키는 값

### 맞춤법과 문법 <a id="spelling-and-grammer"></a>

* class NSSpellServer 앱이 시스템에서 실행중인 다른 앱에 맞춤법 검사 서비스를 제공하기 위해 사용하는 서버
* protocol NSSpellServerDelegate spell server delegate에 의해서 구현되는 선택 메서드

### 지역화 <a id="localization"></a>

* struct Locale 표시를 위한 데이터 포맷 지정에 사용되는 언어, 문화 및 기술 컨벤션에 대한 정보
* class NSOrthography 자연어 텍스트의 언어적 내용 설명. 주로 맞춤법과 문법 검사에 사용됩니다.
* func NSLocalizedString\(String, tableName: String?, bundle: Bundle, value: String, comment: String\) -&gt; String

  지역화된 문자열을 반환합니다. 번들이 지정되지 않은 경우 메인 번들이 사용됩니다.

## 같이 보기 <a id="see-also"></a>

### 기초 <a id="fundamentals"></a>

* [숫자, 데이터와 기본값](numbers-data-and-basic-value.md)

  코코아 전체에서 사용되는 원시 값 및 기타 기본 타입을 사용하여 작업합니다.

* 컬렉션

  배열, 딕셔너리, 세트 및 특수 집합을 사용하여 체 또는 값 그룹을 저장하고 반복할 수 있습니다.

* 날짜와 시간

  날짜와 시간을 비교하고 달력 및 시간대 계산을 수행합니다.

* 단위와 측정

  로케일에 맞는 포맷과 연관 단위의 변환을 위해서 실제 치수를 숫자로 표현합니다.

* [데이터 포맷](data-formatting.md) 숫자와 날짜, 측정값과 기타 값을 로케일에 맞는 표현으로 변환합니다.
* 필터와 정렬

  predicates, expressions와 sort descriptors를 사용해서 컬렉션이나 다른 서비스의 요소들을 검사합니다.

