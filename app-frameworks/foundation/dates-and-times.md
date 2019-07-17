---
description: 날짜와 시간을 비교하고 달력 및 시간대 계산을 수행합니다.
---

# 날짜와 시간

> 원문 출처  
> [https://developer.apple.com/documentation/foundation/dates\_and\_times](https://developer.apple.com/documentation/foundation/dates_and_times)

## 주제 <a id="topics"></a>

### 날짜 표현 <a id="date-representations"></a>

* _struct_ Date

  달력이나 시간대에 관계없는 특정 시점

* _struct_ DateInterval 시작 날짜와 종료 날짜 사이의 특정 기간
* _typealias_ TimeInterval 초를 나타내는 숫자

### 달력 계산 <a id="calendrical-calculations"></a>

* _struct_ DateComponents

  달력 시스템과 시간대에서 사용되는 단위로 지정된 날짜 또는 시간

* _struct_ Calendar 달력 단위\(예: 시대, 연도, 주 중\)와 절대 시점 간의 관계 정의. 날짜 계산 및 비교 기능을 제공합니다.
* _struct_ TimeZone 지정학적 지역과 관련된 표준 시간 컨벤션에 대한 정보

### 날짜 형식 <a id="date-formatting"></a>

* _class_ DateFormatter 날짜와 텍스트 표현을 상호 변환하는 formatter
* _class_ DateComponentsFormatter 시간량의 문자열 표현을 생성하는 formatter
* _class_ DateIntervalFormatter

  시간 간격의 문자열 표현을 생성하는 formatter

* _class_ ISO8601DateFormatter 날짜와 ISO 8601 표준 문자열 표현을 상호 변환하는 formatter

### 국제화 <a id="internationalization"></a>

* _struct_ Locale 표시를 위한 데이터 형식화에 사용하기 위한 언어, 문화 및 기술 컨벤션 정보

## 같이 보기 <a id="see-also"></a>

### 기초 <a id="fundamentals"></a>

* [숫자, 데이터와 기본값](numbers-data-and-basic-value.md)

  코코아 전체에서 사용되는 원시 값 및 기타 기본 타입을 사용하여 작업합니다.

* [문자열과 텍스트](strings-and-text.md)

  유니코드 문자의 문자열을 만들며 처리하고, 정규식을 사용하여 패턴을 찾고, 텍스트의 자연어 분석을 수행합니다.

* [컬렉션](collections.md)

  배열, 딕셔너리, 세트 및 특수 집합을 사용하여 체 또는 값 그룹을 저장하고 반복할 수 있습니다.

* 단위와 측정

  로케일에 맞는 포맷과 연관 단위의 변환을 위해서 실제 치수를 숫자로 표현합니다.

* [데이터 포맷](data-formatting.md) 숫자와 날짜, 측정값과 기타 값을 로케일에 맞는 표현으로 변환합니다.
* 필터와 정렬

  predicates, expressions와 sort descriptors를 사용해서 컬렉션이나 다른 서비스의 요소들을 검사합니다.

