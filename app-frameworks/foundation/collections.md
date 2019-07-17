---
description: '배열, 딕셔너리, 세트 및 특수 집합을 사용하여 체 또는 값 그룹을 저장하고 반복할 수 있습니다.'
---

# 컬렉션

> 원문 출처  
> [https://developer.apple.com/documentation/foundation/collections](https://developer.apple.com/documentation/foundation/collections)

## 주제 <a id="topics"></a>

### 기본 컬렉션들 <a id="basic-collections"></a>

* _struct_ Array 정렬된 랜덤 액세스 컬렉션
* _struct_ Dictionary 키-값 쌍의 요소로 구성된 컬렉션
* _struct_ Set 정렬되지 않은 고유한 요소들의 컬렉션

### 인덱스들 <a id="indexes"></a>

* _struct_ IndexPath

  중첩된 배열 트리의 특정 위치에 대한 경로를 함께 나타내는 인덱스 목록

* _struct_ IndexSet 다른 컬렉션 내 요소들의 인덱스를 나타내는 고유한 정수값들의 컬렉션

### 특화된 세트 <a id="specialized-sets"></a>

* _class_ NSCountedSet

  컬렉션에 한 번 이상 나올 수 있는 개별 객체들의 컬렉션으로써 변경 가능하고 정렬되지 않습니다.

* _class_ NSOrderedSet 고유한 객체들의 컬렉션으로써 정적static이고, 정렬된ordered 컬렉션
* _class_ NSMutableOrderedSet 고유한 객체들의 컬렉션으로써 동적dynamic이고, 정렬된ordered 컬렉션

### 제거 가능한 컬렉션들 <a id="purgeable-collections"></a>

* _class_ NSCache 임시 키-값 쌍을 저장하는 컬렉션입니다. 리소스가 부족하면 제거되며 변경 가능합니다.
* _class_ NSPurgeableData 바이트를 포함하는 변경 가능한 데이터 객체로써 더 이상 필요하지 않을때 삭제 가능합니다.

### 포인터 컬렉션들 <a id="pointer-collections"></a>

* _class_ NSPointerArray

  배열과 비슷하지만 사용가능한 메모리 시멘틱의 범위가 더 넓은 컬렉션

* _class_ NSMapTable 딕셔너리와 비슷하지만 사용가능한 메모리 시멘틱의 범위가 더 넓은 컬렉션
* _class_ NSHashTable 세트와 비슷하지만 사용가능한 메모리 시멘틱의 번위가 더 넓은 컬렉션

### 반복 <a id="iteration"></a>

* _class_ NSEnumerator 추상 클래스로써 서브 클래스는 배열이나 딕셔너리와 같이 컬렉션 객체들을 열거할 수 있습니다.
* _protocol_ NSFastEnumeration 빠른 열거를 지원하기 위해서 객체가 준수하는 프로토콜
* _struct_ NSFastEnumerationIterator
* _struct_ NSIndexSetIterator

  인덱스 셋의 요소들을 열거하는데 적합한 반복자iterator

* _struct_ NSEnumerationOptions 블록 열거 작업을 위한 옵션
* _struct_ NSSortOptions 블록 정렬 작업을 위한 옵션

### 특수 시멘틱 값 <a id="special-sementic-values"></a>

* _class_ NSNull

  nil 값을 허용하지 않는 컬렉션 객체에서 null 값을 나타내기 위한 싱글톤 객체

* _let_ NSNotFound: Int
* _let_ NSNotFound: Int 요청한 항목을 찾을 수 없거나 존재하지 않음을 가리키는 값

## 같이 보기

### 기초 <a id="fundamentals"></a>

* [숫자, 데이터와 기본값](numbers-data-and-basic-value.md)

  코코아 전체에서 사용되는 원시 값 및 기타 기본 타입을 사용하여 작업합니다.

* [문자열과 텍스트](strings-and-text.md)

  유니코드 문자의 문자열을 만들며 처리하고, 정규식을 사용하여 패턴을 찾고, 텍스트의 자연어 분석을 수행합니다.

* [날짜와 시간](dates-and-times.md)

  날짜와 시간을 비교하고 달력 및 시간대 계산을 수행합니다.

* 단위와 측정

  로케일에 맞는 포맷과 연관 단위의 변환을 위해서 실제 치수를 숫자로 표현합니다.

* [데이터 포맷](data-formatting.md) 숫자와 날짜, 측정값과 기타 값을 로케일에 맞는 표현으로 변환합니다.
* 필터와 정렬

  predicates, expressions와 sort descriptors를 사용해서 컬렉션이나 다른 서비스의 요소들을 검사합니다.

