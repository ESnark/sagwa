# FileManager

> 원문 출처  
> [https://developer.apple.com/documentation/foundation/filemanager](https://developer.apple.com/documentation/foundation/filemanager)

## 개요

FileManager 객체를 사용하면 파일 시스템의 내용을 검사하고 변경할 수 있습니다. FileManager 클래스는 대부분의 파일 관련 조작 유형에 적합한 공유 파일 관리자 객체에 대한 편리한 액세스를 제공합니다.  
FileManager 객체는 일반적으로 파일 시스템과 상호 작용하는 기본 모드입니다. 파일 및 디렉리를 찾고, 생성하고, 복사하고, 이동할 때 사용합니다. 또한 파일이나 디렉터리에 대한 정보를 가져오거나 일부 속성을 변경할 때도 사용합니다.

파일 위치를 명시할 때 NSURL 또는 NSString 개체를 사용할 수 있습니다. 경로 정보가 내부에서 보다 효율적인 표현으로 변환될 수 있으므로 일반적으로 파일 시스템 항목을 지정할 때에는NSURL 클래스를 사용하는 것이 좋습니다. 또한 NSURL 객체에서 북마크를 가져올 수 있습니다. 이 북마크 객체는 별칭과 비슷하며 나중에 파일이나 디렉리를 찾는 보다 확실한 방법을 제공합니다.

파일이나 디렉토리를 이동, 복사, 연결 또는 제거하는 경우 delegate를 사용하여 파일 관리자 객체와 함께 해당 작업들을 관리할 수 있습니다. delegate의 역할은 동작을 확인하고 오류가 발생할 때 계속해서 작업을 진행할지 여부를 결정하는 것입니다. macOS 10.7 이상에서는 delegate가 [FileManagerDelegate](../../../etc/not-found.md) 프로토콜을 준수해야 합니다.

iOS 5.0 이상 및 MacOS 10.7 이상에서 FileManager는 iCloud에 저장된 항목을 관리하는 메서드를 포함하고 있습니다. 클라우드 스토리지용으로 태그가 지정된 파일과 디렉토리는 사용자의 iOS 기기 및 Macintosh 컴퓨터에서 사용할 수 있도록 iCloud와 동기화됩니다. 한 위치의 항목에 대한 변경 내용이 다른 모든 위치로 전파되어 항목이 동기화 상태를 유지합니다.

## 스레딩 고려사항

공유된 FileManager 객체의 메서드는 여러 스레드에서 안전하게 호출할 수 있습니다. 그러나 delegate를 사용하여 이동, 복사, 제거 및 링크 작업의 상태에 대한 알림을 받고 있다면 FileManager 객체의 고유한 인스턴스를 생성하고 해당 객체에 delegate를 할당한 다음 해당 FileManager를 사용하여 작업을 시작해야 합니다.

## 주제

### 파일매니저 생성하기

* _class var_ `default`: FileManager

  프로세스에 대한 공유 파일 관리자 객체를 반환합니다.

### 유저 디렉터리 액세스

* _var_ temporaryDirectory: URL

  현재 사용자의 임시 디렉리를 반환합니다.

* _var_ homeDirectoryForCurrentUser: URL

  `forUser:` 사용자의 홈 디렉리를 반환합니다.

* _func_ homeDirectory\(forUser: String\) -&gt; URL?

  `forUser:` 사용자의 홈 디렉리를 반환합니다.

### 시스템 디렉터리 위치 찾기

* _func_ url\(for: FileManager.SearchPathDirectory, in: FileManager.SearchPathDomainMask, appropriateFor: URL?, create: Bool\) -&gt; URL

  `in:` 도메인 상에 `for:` 디렉토리를 찾아서 선택적으로 생성합니다.

* _func_ urls\(for: FileManager.SearchPathDirectory, in: FileManager.SearchPathDomainMask\) -&gt; \[URL\]

  `in:` 도메인 상의 `for:` 디렉터리에 대한 URL 배열을 반환합니다.

### 어플리케이션 그룹 컨테이너 디렉터리 위치

* _func_ containerURL\(forSecurityApplicationGroupIdentifier: String\) -&gt; URL? 보안 애플리케이션 그룹 식별자와 \(`forSecurityApplicationGroupIdentifier:`\) 연결된 컨테이너 디렉터리를 반환합니다.

### 디렉터리 컨텐츠 찾기

* _func_ contentsOfDirectory\(at: URL, includingPropertiesForKeys: \[URLResourceKey\]?, options: FileManager.DirectoryEnumerationOptions = \[\]\) -&gt; \[URL\]

  `at:` 디렉터리에 대한 얕은 검색을 수행하고 포함된 항목에 대한 URL을 반환합니다.

* _func_ contentsOfDirectory\(atPath: String\) -&gt; \[String\]

  `at:` 디렉리에 대한 얕은 검색을 수행하고 포함된 항목의 경로 문자열을 반환합니다.

* _func_ enumerator\(atPath: String\) -&gt; FileManager.DirectoryEnumerator?

  Returns a directory enumerator object that can be used to perform a deep enumeration of the directory at the specified path.

* _class_ FileManager.DirectoryEnumerator

  An NSDirectoryEnumerator object enumerates the contents of a directory, returning the pathnames of all files and directories contained within that directory. These pathnames are relative to the directory.

* _func_ mountedVolumeURLs\(includingResourceValuesForKeys: \[URLResourceKey\]?, options: FileManager.VolumeEnumerationOptions = \[\]\) -&gt; \[URL\]?

  기기에 마운트 되어 사용가능한 볼륨들의 URL 배열을 반환합니다.

* _func_ subpathsOfDirectory\(atPath: String\) -&gt; \[String\]

  Performs a deep enumeration of the specified directory and returns the paths of all of the contained subdirectories.

* _func_ subpaths\(atPath: String\) -&gt; \[String\]?

  `atPath:` 문자열 상의 디렉리에 있는 모든 항목의 경로를 문자열 배열로 반환합니다.

### 항목 생성과 삭제

* _func_ createDirectory\(at: URL, withIntermediateDirectories: Bool, attributes: \[FileAttributeKey : Any\]? = nil\)

  `at:` URL에 `attributes:` 속성을 갖는 디렉리를 생성합니다.

* _func_ createDirectory\(atPath: String, withIntermediateDirectories: Bool, attributes: \[FileAttributeKey : Any\]? = nil\)

  `at:` 문자열 경로에 `attributes:` 속성을 갖는 디렉터리를 생성합니다.

* _func_ createFile\(atPath: String, contents: Data?, attributes: \[FileAttributeKey : Any\]? = nil\) -&gt; Bool

  `contents:` 컨텐츠와 `attributes:` 속성, `atPath:` 문자열 경로를 갖는 파일을 생성합니다.

* _func_ removeItem\(at: URL\) `at:` URL의 파일이나 디렉리를 삭제합니다.
* _func_ removeItem\(atPath: String\)

  `atPath:` 문자열 경로의 파일이나 디렉리를 삭제합니다.

* _func_ replaceItem\(at: URL, withItemAt: URL, backupItemName: String?, options: FileManager.ItemReplacementOptions = \[\], resultingItemURL: AutoreleasingUnsafeMutablePointer?\) 데이터 손실이 발생하지 않도록 `at:` URL의 항목 내용을 대체합니다.
* _func_ trashItem\(at: URL, resultingItemURL: AutoreleasingUnsafeMutablePointer?\)

  항목을 휴지통으로 이동시킵니다.

### 항목 이동과 복사

* _func_ copyItem\(at: URL, to: URL\)

  `at:` URL의 파일을 `to:` URL에 새로 동기식 복사합니다.

* _func_ copyItem\(atPath: String, toPath: String\) `at:` 문자열 경로의 파일을 `to:` 경로에  새로 동기식 복사합니다.
* _func_ moveItem\(at: URL, to: URL\) `at:` URL의 파일이나 디렉리를 `to:` URL에 동기적으로 이동시킵니다.
* _func_ moveItem\(atPath: String, toPath: String\) `at:` 문자열 경로의 파일이나 디렉리를 `to:` 경로에 동기적으로 이동시킵니다.

### iCloud 기반 항목 관리

* _var_ ubiquityIdentityToken: \(NSCoding & NSCopying & NSObjectProtocol\)?

  현재 사용자의 iCloud ID를 나타내는 opaque 토큰

* _func_ url\(forUbiquityContainerIdentifier: String?\) -&gt; URL?

  `forUbiquityContainerIdentifier:` 식별자와 연결된 iCloud 컨테이너의 URL을 반환하고 해당 컨테이너에 대한 액세스 권한을 설정합니다.

* _func_ isUbiquitousItem\(at: URL\) -&gt; Bool

  `at:` URL의 항목이 iCloud 저장 대상인지 나타내는 Boolean 값을 반환합니다.

* _func_ setUbiquitous\(Bool, itemAt: URL, destinationURL: URL\) `at:` URL의 항목을 클라우드에 저장할 것인지 지정합니다.
* _func_ startDownloadingUbiquitousItem\(at: URL\) \(필요한 경우\) `at:` 항목을 로컬 시스템에 다운로드합니다.
* _func_ evictUbiquitousItem\(at: URL\)

  지정된 클라우드 기반의 로컬 복사본을 삭제합니다.

* _func_ url\(forPublishingUbiquitousItemAt: URL, expiration: AutoreleasingUnsafeMutablePointer?\) -&gt; URL

  클라우드 기반의 파일을 다운받을 수 있는 URL을 반환합니다. 이 URL은 email로 전송가능합니다.

### 파일 공급자 서비스에 액세스

* _func_ getFileProviderServicesForItem\(at: URL, completionHandler: \(\[NSFileProviderServiceName : NSFileProviderService\]?, Error?\) -&gt; Void\)

  at: URL의 항목을 관리하는 서비스를 반환합니다.  
  이 서비스는 File Provider extension\(파일 공급자 확장\)이 제공합니다.

* _class_ NSFileProviderService 앱과 File Provider extensioin 사이에서 커스텀 통신채널을 제공하는 서비스
* _struct_ NSFileProviderServiceName

  File Provider service\(파일 공급자 서비스\)를 식별하는데 사용되는 이름

### 심볼릭 링크와 하드 링크 생성

* _func_ createSymbolicLink\(at: URL, withDestinationURL: URL\) `withDestinationalURL:` URL의 항목을 가리키는 심볼릭 링크를 `at:` URL에 생성합니다.
* _func_ createSymbolicLink\(atPath: String, withDestinationPath: String\)

  `withDestinationalPath:` 문자열 경로의 항목을 가리키는 심볼릭 링크를 `atPath:` 문자열 경로에 생성합니다.

* _func_ linkItem\(at: URL, to: URL\)

  지정된 URL에 해당되는 두 항목을 하드링크로 연결합니다.

* _func_ linkItem\(atPath: String, toPath: String\) 지정된 문자열 경로에 해당하는 두 항목을 하드링크로 연결합니다.
* _func_ destinationOfSymbolicLink\(atPath: String\) -&gt; String `atPath:` 의 항목이 심볼릭 링크로 가리키는 문자열 경로를 반환합니다.

### 파일 액세스 가능성

* _func_ fileExists\(atPath: String\) -&gt; Bool `atPath:`에 파일 또는 디렉리가 있는지 나타내는 Boolean 값을 반환합니다.
* _func_ fileExists\(atPath: String, isDirectory: UnsafeMutablePointer?\) -&gt; Bool `atPath:`에 파일 또는 디렉터리가 있는지 나타내는 Boolean 값을 반환합니다. `isDirectory:`는 경로가 디렉리인지 일반 파일인지를 묻습니다.
* _func_ isReadableFile\(atPath: String\) -&gt; Bool 호출하는 객체가 `atPath:`의 파일을 읽을 수 있는지 나타내는 Boolean 값을 반환합니다.
* _func_ isWritableFile\(atPath: String\) -&gt; Bool

  호출하는 객체가 `atPath:`파일에 쓸 수 있는지 나타내는 Boolean 값을 반환합니다.

* _func_ isExecutableFile\(atPath: String\) -&gt; Bool

  운영체제가 `atPath:`파일을 실행할 수 있는지 나타내는 Boolean 값을 반환합니다.

* _func_ isDeletableFile\(atPath: String\) -&gt; Bool

  호출하는 객체가 `atPath:`파일을 삭제할 수 있는지 나타내는 Boolean 값을 반환합니다.

### 속성정보 읽기/쓰기 <a id="getting-and-setting-attributes"></a>

* _func_ componentsToDisplay\(forPath: String\) -&gt; \[String\]?

  `forPath:` 경에서 사용자가 볼 수 있는 항목들의 문자열 배열을 반환합니다.

* _func_ displayName\(atPath: String\) -&gt; String

  `atPath:` 경로에 있는 파일이나 디렉리의 이름을 반환합니다.

* _func_ attributesOfItem\(atPath: String\) -&gt; \[FileAttributeKey : Any\]

  `atPath:` 경로에 있는 항목의 속성을 반환합니다.

* _func_ attributesOfFileSystem\(forPath: String\) -&gt; \[FileAttributeKey : Any\] 지정된 경로가 있는 마운트된 파일 시스템의 속성을 설명하는 딕셔너리를 반환합니다
* _func_ setAttributes\(\[FileAttributeKey : Any\], ofItemAtPath: String\) `ofItemAtPath:` 경로의 파일 또는 디렉터리의 속성을 설정합니다.

### 파일 내용 가져오고 비교하기

* _func_ contents\(atPath: String\) -&gt; Data? `atPath:` 경로에 있는 파일의 내용을 반환합니다.
* _func_ contentsEqual\(atPath: String, andPath: String\) -&gt; Bool `atPath:` 와 `andPath:` 경로에 있는 파일 또는 디렉터리의 컨텐츠가 동일한지를 나타내는 Boolean 값을 반환합니다.

### 항목 간 관계 가져오기

* _func_ getRelationship\(UnsafeMutablePointer, ofDirectoryAt: URL, toItemAt: URL\)

  디렉토리와 항목 사이에 존재하는 관계 유형을 결정합니다.

* _func_ getRelationship\(UnsafeMutablePointer, of: FileManager.SearchPathDirectory, in: FileManager.SearchPathDomainMask, toItemAt: URL\)

  시스템 디렉토리와 지정된 항목 사이에 존재하는 관계 유형을 결정합니다.

### 파일경로를 문자열로 변환하기

* _func_ fileSystemRepresentation\(withPath: String\) -&gt; UnsafePointer

  파일 시스템에서 사용하기 위해서 유니코드 문자열을 올바르게 인코딩하는 `withPath:` 경로의 C 문자열 표현을 반환합니다.

* _func_ string\(withFileSystemRepresentation: UnsafePointer, length: Int\) -&gt; String

  C 문자열 경로에서\(`withFileSystemRepresentation:`\) 내용이 파생 된 NSString 객체를 반환합니다.

### Delegate 관리하기

* _var_ delegate: FileManagerDelegate?

  파일 관리자 객체의 delegate

### 현재 디렉터리 관리

* _func_ changeCurrentDirectoryPath\(String\) -&gt; Bool

  현재 작업중인 디렉터리 경로를 지정된 경로로 변경합니다.

* _var_ currentDirectoryPath: String

  프로그램의 현재 디렉터리

### Deprecated Methods

> 생략

### 상수Constants

* _struct_ FileManager.VolumeEnumerationOptions

  Options for enumerating mounted volumes with the mountedVolumeURLs\(includingResourceValuesForKeys:options:\) method.

* _struct_ FileManager.DirectoryEnumerationOptions

  Options for enumerating the contents of directories with the contentsOfDirectory\(at:includingPropertiesForKeys:options:\) method.

* _struct_ FileManager.ItemReplacementOptions

  [replaceItem\(at:withItemAt:backupItemName:options:resultingItemURL:\)](../../../etc/not-found.md) 메서드에서 대체 동작을 지정하는 상수

* _enum_ FileManager.SearchPathDirectory [urls\(for:in:\)](../../../etc/not-found.md)와 [url\(for:in:appropriateFor:create:\)](../../../etc/not-found.md) 같은 FileManager 메서드에서 다양한 디렉터리의 위치를 나타내는 상수
* _struct_ FileManager.SearchPathDomainMask 검색 경로 도메인 상수는 [FileManager.SearchPathDirectory](../../../etc/not-found.md) 타입에서 기본 위치를 나타냅니다. 이 상수들은 [urls\(for:in:\)](../../../etc/not-found.md)와 [url\(for:in:appropriateFor:create:\)](../../../etc/not-found.md) 같은 FileManager 메서드에서 사용됩니다.
* _struct_ FileAttributeKey [속성정보 읽기/쓰기](filemanager.md#getting-and-setting-attributes)에 나열된 메서드들에 쓰이는 딕셔너리의 키
* _struct_ FileAttributeType

  이 문자열들은 [attributesOfItem\(atPath:\)](../../../etc/not-found.md) 메서드가 반환하는 딕셔너리 객체가 포함하는 [type](../../../etc/not-found.md) 속성 키입니다.

* _struct_ FileProtectionType

  [protectionKey](../../../etc/not-found.md) 키와 연관될 수 있는 값

* _enum_ FileManager.URLRelationship

  디렉터리와 항목의 관계를 나타내는 정수

* _var_ NSFoundationVersionWithFileManagerResourceForkSupport: Int32

  NSFileManager가 처음으로 리소스 포크를 지원하는 Foundation 프레임워크의 버전

* _struct_ URLFileProtection
* _let_ NSFileManagerUnmountDissentingProcessIdentifierErrorKey: String
* _struct_ FileManager.UnmountOptions

### 파일경로 함수

* _func_ NSFullUserName\(\) -&gt; String

  현재 사용자의 전체 이름이 포함된 문자열을 반환합니다.

* _func_ NSHomeDirectory\(\) -&gt; String

  플랫폼에 따라 사용자 또는 애플리케이션의 홈 디렉터리 경로를 반환합니다.

* _func_ NSHomeDirectoryForUser\(String?\) -&gt; String?

  지정된 사용자의 홈 디렉토리에 대한 경로를 반환합니다.

* _func_ NSOpenStepRootDirectory\(\) -&gt; String
* 사용자 시스템의 루트 디렉터리를 반환합니다
* _func_ NSSearchPathForDirectoriesInDomains\(FileManager.SearchPathDirectory, FileManager.SearchPathDomainMask, Bool\) -&gt; \[String\]

  디렉터리 검색 경로 리스트를 생성합니다.

* _func_ NSTemporaryDirectory\(\) -&gt; String

  현재 사용자의 임시 디렉터리 경로를 반환합니다.

* _func_ NSUserName\(\) -&gt; String

  현재 사용자의 로그온 이름을 반환합니다.

### HFS 파일타입 함수

* _func_ NSFileTypeForHFSTypeCode\(OSType\) -&gt; String!

  파일 형식 코드를 인코딩하는 문자열을 반환합니다.

* _func_ NSHFSTypeCodeFromFileType\(String!\) -&gt; OSType

  파일 형식 코드를 반환합니다.

* _func_ NSHFSTypeOfFile\(String!\) -&gt; String!

  파일 형식을 인코딩하는 문자열을 반환합니다.

### Notifications

* _static let_ NSUbiquityIdentityDidChange: NSNotification.Name

  iCloud \(“ubiquity”\) ID가 변경된 후에 발송됩니다.

### Initializers

* init\(authorization: NSWorkspace.Authorization\)

### 인스턴스 메서드

* _func_ enumerator\(at: URL, includingPropertiesForKeys: \[URLResourceKey\]?, options: FileManager.DirectoryEnumerationOptions, errorHandler: \(\(URL, Error\) -&gt; Bool\)?\) -&gt; FileManager.DirectoryEnumerator?
* _func_ replaceItemAt\(URL, withItemAt: URL, backupItemName: String?, options: FileManager.ItemReplacementOptions\) -&gt; URL?
* ~~_func_ replaceItemAtURL\(originalItemURL: NSURL, withItemAtURL: NSURL, backupItemName: String?, options: FileManager.ItemReplacementOptions\) -&gt; NSURL?~~ `Deprecated`
* _func_ unmountVolume\(at: URL, options: FileManager.UnmountOptions = \[\], completionHandler: \(Error?\) -&gt; Void\)

## 관련 문서

### 상속받은 대상

* NSObject

### 준수하는 프로토콜

* CVarArg
* Equatable
* Hashable

## 같이 보기

### 파일 시스템 작업

* 애플 파일 시스템에 대해 Apple 파일 시스템을 최대한 활용하려면 고급 API를 사용하세요.
* _protocol_ FileManagerDelegate 작업 중 또는 에러 발생시 FileManager의 delegate가 개입할때 사용되는 인터페이스

