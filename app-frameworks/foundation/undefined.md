---
description: '숫자와 날짜, 측정값과 기타 값을 로케일에 맞는 표현으로 변환합니다.'
---

# 데이터 포맷

> 원문 출처  
> [https://developer.apple.com/documentation/foundation/data\_formatting](https://developer.apple.com/documentation/foundation/data_formatting)

## 주제

### 숫자 및 통화

* _class_ NumberFomatter 숫자값과 텍스트 표현간의 변환을 지원하는 Formatter.

### 이름

* _class_ PersonNameComponentsFormatter  
  사람 이름의 컴포넌트를 지역화된 표현으로 제공하는 Formatter.

  A formatter that provides localized representations of the components of a person’s name.

* _struct_ PersonNameComponents 개별 부분으로 나누어져, 로케일 포맷을 허용하는 사람 이름입니다.

### 수치

* _class_ MeasurementFormatter 단위 및 수치를 지역화 된 표현으로 제공하는 Formatter.

### 국제화

* _struct_ Locale

  Information about linguistic, cultural, and technological conventions for use in formatting data for presentation.

### 커스텀 포맷

* _class_ Formatter

  An abstract class that declares an interface for objects that create, interpret, and validate the textual representation of values.

### Deprecated

* _class_ LengthFormatter

  A formatter that provides localized descriptions of linear distances, such as length and height measurements.

* _class_ MassFormatter

  A formatter that provides localized descriptions of mass and weight values.

* _class_ EnergyFormatter

  A formatter that provides localized descriptions of energy values.

## 같이 보기

### 기본 <a id="fundamentals"></a>

* [숫자, 데이터와 원시값](undefined-1.md)

  코코아 전체에서 사용되는 원시 값 및 기타 기본 타입을 사용하여 작업합니다.

* 문자열과 텍스트

  유니코드 문자의 문자열을 만들며 처리하고, 정규식을 사용하여 패턴을 찾고, 텍스트의 자연어 분석을 수행합니다.

* 컬렉션

  배열, 딕셔너리, 세트 및 특수 집합을 사용하여 체 또는 값 그룹을 저장하고 반복할 수 있습니다.

* 날짜와 시간

  날짜와 시간을 비교하고 달력 및 시간대 계산을 수행합니다.

* 단위와 측정

  로케일에 맞는 포맷과 연관 단위의 변환을 위해서 실제 치수를 숫자로 표현합니다.

* 필터와 정렬

  predicates, expressions와 sort descriptors를 사용해서 컬렉션이나 다른 서비스의 요소들을 검사합니다.

