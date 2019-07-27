---
description: '파일 시스템에서 파일 및 폴더를 생성, 읽기, 쓰기 및 검사합니다.'
---

# 파일 시스템

> 원문 출처  
> [https://developer.apple.com/documentation/foundation/file\_system](https://developer.apple.com/documentation/foundation/file_system)

## 주제 <a id="overview"></a>

### 파일 시스템 작업 <a id="file_system_operations"></a>

* 애플 파일 시스템에 대해 Apple 파일 시스템을 최대한 활용하려면 고급 API를 사용하세요.
* class [FileManager](filemanager.md) 파일 시스템 내용에 대한 편리한 인터페이스를 제공하는 객체
* protocol FileManagerDelegate 작업 중 또는 에러 발생시 FileManager의 delegate가 개입할때 사용되는 인터페이스

### 관리되는 파일 액세스 <a id="managed_file_access"></a>

* class FileHandle

  파일 설명자에 대한 객체지향 래퍼wrapper

* class NSFileSecurity

  파일에 대한 보안정보를 캡슐화 하는 stub class

* class NSFileVersion

  특정 시점의 파일 스냅샷

* class FileWrapper

  파일 시스템의 노드\(파일, 디렉토리, 심볼릭 링크\)를 나타냅니다.

### 공유 파일 <a id="shared_files"></a>

* protocol NSFilePresenter

  FileCoodinator가 사용하는 인터페이스로써, 시스템 상 어딘가의 파일에 변경이 발생할때 파일을 가리키는 객체에 알리는 역할을 합니다.

* class NSFileAccessIntent

  조정된 읽기/쓰기 작업의 상세 내역

* class NSFileCoordinator

  파일 표시자 간의 파일 및 디렉토리의 읽기/쓰기를 조정하는 객체

### 에러 <a id="errors"></a>

* 파일 시스템 에러코드 파일 시스템 작업에 의해 생성되는 일반적인 오류 코드를 인식합니다.

## 같이 보기 <a id="see_also"></a>

### 파일 및 데이터 지속성 <a id="files_and_data_persistence"></a>

* 보관과 Serialization

  객체와 값을 속성 목록, JSON 및 기타 플랫 이진 표현으로 변환합니다.

* Preference

  앱을 구성하는 데 사용되는 도메인 범위의 정보를 영구적으로 저장합니다.

* Spotlight

  로컬 장치에서 파일 및 기타 항목을 검색하고 앱의 컨텐츠를 인덱싱합니다.

* iCloud

  사용자의 iCloud 장치 간에 자동으로 동기화되는 파일 및 키 값 데이터를 관리합니다.

