---
description: 코코아 전체에서 사용되는 원시 값 및 기타 기본 타입을 사용하여 작업합니다.
---

# 숫자, 데이터와 기본값

> 원문 출처  
> [https://developer.apple.com/documentation/foundation/numbers\_data\_and\_basic\_values](https://developer.apple.com/documentation/foundation/numbers_data_and_basic_values)

## 주제

### 숫자

* _struct_ Int 부호가 있는 정수 타입
* _struct_ Double 배정밀도 부동소수점 타입
* _struct_ Decimal 10진수 숫자를 표현하는 구조체
* _class_ NumberFormatter 숫자값과 텍스트 표현형을 서로 변환시켜주는 formatter

### 이진 데이터

* _struct_ Data 메모리의 바이트 버퍼

### URLs

* _struct_ URL 원격 서버의 항목이나 로컬 파일의 경로처럼 리소스의 위치를 나타내는 식별자 값
* _struct_ URLComponents URL을 구성요소로 파싱하거나 구성요소로부터 URL르 구성해내는 구조체
* _struct_ URLQueryItem URL 쿼리 일부의 단일한 name-value 쌍

### 유일 식별자

* _struct_ UUID 타입, 인터페이스 및 다른 아이템을 구별하는데 사용되는 범용적인 고유값입니다.

### 지오메트리

* _struct_ CGFloat Core Graphics와 관련 프레임워크에서 부동 소수점 스칼라값을 나타내는 기본 타입
* _typealias_ NSPoint 데카르트 좌표계\(직교 좌표계\)의 한 점
* _typealias_ NSSize 2차원 크기
* _typealias_ NSRect 직사각형
* _struct_ AffineTransform 그래픽 좌표 변환
* _struct_ NSEdgeInsets 두 직사각형 사이의 거리를 설명합니다.

### Ranges

* _typealias_ NSRange 문자열의 좌표, 배열 안의 객체와 같이 연속된 값의 일부를 설명하는 구조체

## 같이 보기

### 기초 <a id="fundamentals"></a>

* [문자열과 텍스트](strings-and-text.md)

  유니코드 문자의 문자열을 만들며 처리하고, 정규식을 사용하여 패턴을 찾고, 텍스트의 자연어 분석을 수행합니다.

* [컬렉션](collections.md)

  배열, 딕셔너리, 세트 및 특수 집합을 사용하여 체 또는 값 그룹을 저장하고 반복할 수 있습니다.

* [날짜와 시간](dates-and-times.md)

  날짜와 시간을 비교하고 달력 및 시간대 계산을 수행합니다.

* 단위와 측정

  로케일에 맞는 포맷과 연관 단위의 변환을 위해서 실제 치수를 숫자로 표현합니다.

* [데이터 포맷](data-formatting.md) 숫자와 날짜, 측정값과 기타 값을 로케일에 맞는 표현으로 변환합니다.
* 필터와 정렬

  predicates, expressions와 sort descriptors를 사용해서 컬렉션이나 다른 서비스의 요소들을 검사합니다.

