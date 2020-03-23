---
description: '숫자와 날짜, 측정값과 기타 값을 로케일에 맞는 표현으로 변환합니다.'
---

# 데이터 포맷

> 원문 출처  
> [https://developer.apple.com/documentation/foundation/data\_formatting](https://developer.apple.com/documentation/foundation/data_formatting)

## 주제

### First Steps

* 스위프트 데이터 타입과 문자열 상호 변환하기 formatter를 사용해서 스위프트 데이터 타입을 문자열 표현으로 바꾸거나 문자열을 데이터로 변환하세요

### 숫자 및 통화

* _class_ NumberFomatter 숫자값과 텍스트 표현간의 변환을 지원하는 Formatter.

### 이름

* _class_ PersonNameComponentsFormatter 사람 이름의 컴포넌트를 지역화된 표현으로 제공하는 Formatter.
* _struct_ PersonNameComponents 개별 부분으로 나누어져, 로케일 포맷을 허용하는 사람 이름입니다.

### 날짜와 시간

* _class_ DateFormatter Date를 텍스트 표현과 상호변환하는 Formatter
* _class_ DateComponentsFormatter \(양적\) 시간의 문자열 표현을 생성하는 Formatter
* _class_ DateIntervalFormatter 시간 간격의 문자열 표현을 생성하는 Formatter
* _class_ ISO8610DateFormatter ISO8610 문자열 표현과 Date를 상호변환하는 Formatter

### 데이터 사이즈

* _class_ ByteCounterFormatter 바이트 카운트 값을 적절한 바이트 수정자\(ex KB, MB, GB 등\)로 지역화 하는 Formatter

### 수치

* _class_ MeasurementFormatter 단위 및 수치를 지역화 된 표현으로 제공하는 Formatter.

### 국제화

* _struct_ Locale

  데이터를 포맷화하는데 사용되는 언어적, 문화적, 기술적 컨벤션에 대한 정보

### 커스텀 포맷

* _class_ Formatter 데이터의 텍스트 표현을 생성, 변환, 검증하는 객체의 인터페이스를 선언하는 추상 클래스

### Deprecated

* _class_ LengthFormatter 길이, 높이와 같은 직선거리 수치를 지역화 된 표현으로 제공하는 Formatter.
* _class_ MassFormatter 질량과 무게값을 지역화 된 표현으로 제공하는 Formatter.
* _class_ EnergyFormatter 에너지값을 지역화 된 표현으로 제공하는 Formatter.

## 같이 보기

### 기본 <a id="fundamentals"></a>

* [숫자, 데이터와 기본값](numbers-data-and-basic-value.md)

  코코아 전체에서 사용되는 원시 값 및 기타 기본 타입을 사용하여 작업합니다.

* [문자열과 텍스트](strings-and-text.md)

  유니코드 문자의 문자열을 만들며 처리하고, 정규식을 사용하여 패턴을 찾고, 텍스트의 자연어 분석을 수행합니다.

* [컬렉션](collections.md)

  배열, 딕셔너리, 세트 및 특수 집합을 사용하여 체 또는 값 그룹을 저장하고 반복할 수 있습니다.

* 날짜와 시간

  날짜와 시간을 비교하고 달력 및 시간대 계산을 수행합니다.

* 단위와 측정

  로케일에 맞는 포맷과 연관 단위의 변환을 위해서 실제 치수를 숫자로 표현합니다.

* 필터와 정렬

  predicates, expressions와 sort descriptors를 사용해서 컬렉션이나 다른 서비스의 요소들을 검사합니다.

