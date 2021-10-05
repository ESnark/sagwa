# Thread Management

> 원문 출처  
> [https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/Multithreading/CreatingThreads/CreatingThreads.html\#//apple\_ref/doc/uid/10000057i-CH15-SW2](https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/Multithreading/CreatingThreads/CreatingThreads.html#//apple_ref/doc/uid/10000057i-CH15-SW2)

OS X와 iOS의 각 프로세스\(애플리케이션\)는 하나 이상의 스레드로 이루어져 있으며 각 스레드는 어플리케이션 코드를 통한 단일 실행경로를 나타냅니다. 모든 애플리케이션은 _main_ 함수를 실행하는 하나의 스레드로 시작합니다. 애플리케이션은 보조 스레드를 생성할 수 있으며 각 보조 스레드는 특정 기능을 하는 코드를 실행합니다.

애플리케이션이 새 스레드를 생성하면 이 스레드는 애플리케이션 프로세스 영역 내에서 독립적인 요소가 되며 커널에 의해서 별도의 런타임에 예약되는 자체적인 실행 스택을 갖게 됩니다. 스레드는 다른 스레드 및 프로세스와 통신하거나 입출력 작업을 수행하는 등 여러분이 필요하다고 생각되는 것은 무엇이든지 할 수 있습니다. 다만 모든 스레드는 속해있는 프로세스와 같은 가상 메모리 공간과 권한을 공유합니다.

{% hint style="info" %}
Note

Mac OS의 스레딩 아키텍쳐 역사와 추가적인 배경 지식을 원하신다면 기술자고 TN2028, "Threading Architectures"를 참조하세요.
{% endhint %}

## 스레드 비용 <a id="thread-costs"></a>

스레딩은 메모리 사용량과 성능에 있어서 여러분의 프로그램에 \(그리고 시스템에\) 실질적인 비용을 초래합니다. 각 스레드는 커널 메모리 공간과 프로그램 메모리 공간 할당을 필요로 합니다. 스레드를 관리하고 스케줄링을 조정하는데 필요한 코어 구조는 wired memory를 사용하여 커널 안에 저장되고, 스레드의 스택과 스레드별 데이터는 프로그램 메모리 영역 안에 저장됩니다. 이 구조들의 대부분은 스레드를 처음 만들때 생성되고 초기되는데 이 과정에서 커널과의 상호작용이 요구되기 때문에 프로세스로써는 상대적으로 큰 작업입니다.

표 2-1은 사용자 레벨의 스레드를 새로 만들때 소요되는 대략적인 비용을 나타냅니다. 이 중에는 보조 스레드의 스택 영역처럼 설정 가능한 비용도 있습니다. 스레드 생성의 시간 비용을 따지자면, 매우 임의적이며 대략적인 값이기 때문에 상대적인 비교를 통해서 쓰여야 할 것입니다. 스레드 생성 시간은 프로세서의 부하 상태, 컴퓨터의 속도, 사용가능한 시스템/프로그램 메모리의 양에 따라 괸장히 달라질수 있기 때문입니다.

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#xD56D;&#xBAA9;</th>
      <th style="text-align:left">&#xB300;&#xB7B5;&#xC801;&#xC778; &#xBE44;</th>
      <th style="text-align:left">&#xCC38;&#xACE0;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">&#xCEE4;&#xB110; &#xB370;&#xC774;&#xD130; &#xAD6C;&#xC870;</td>
      <td style="text-align:left">&#xC57D; 1KB</td>
      <td style="text-align:left">&#xC774; &#xBA54;&#xBAA8;&#xB9AC;&#xB294; &#xC2A4;&#xB808;&#xB4DC; &#xB370;&#xC774;&#xD130;&#xC640;
        attribute&#xB97C; &#xC800;&#xC7A5;&#xD558;&#xB294;&#xB370; &#xC0AC;&#xC6A9;&#xB429;&#xB2C8;&#xB2E4;.
        &#xC774; &#xC911;&#xC5D0; &#xB9CE;&#xC740; &#xC591;&#xC774; wired memory&#xC5D0;
        &#xD560;&#xB2F9;&#xB418;&#xAE30; &#xB54C;&#xBB38;&#xC5D0; &#xB514;&#xC2A4;&#xD06C;&#xC5D0;
        &#xD398;&#xC774;&#xC9D5;&#xD560; &#xC218; &#xC5C6;&#xC2B5;&#xB2C8;</td>
    </tr>
    <tr>
      <td style="text-align:left">&#xC2A4;&#xD0DD; &#xC601;&#xC5ED;</td>
      <td style="text-align:left">
        <p>512 KB (&#xBCF4;&#xC870; &#xC2A4;&#xB808;&#xB4DC;)</p>
        <p>8 MB (OS X &#xBA54;&#xC778; &#xC2A4;&#xB808;&#xB4DC;)</p>
        <p>1 MB (iOS &#xBA54;&#xC778; &#xC2A4;&#xB808;&#xB4DC;)</p>
      </td>
      <td style="text-align:left">&#xBCF4;&#xC870; &#xC2A4;&#xB808;&#xB4DC;&#xC5D0; &#xD5C8;&#xC6A9;&#xB418;&#xB294;
        &#xCD5C;&#xC18C; &#xC2A4;&#xD0DD; &#xD06C;&#xAE30;&#xB294; 16 KB&#xC774;&#xBA70;
        4 KB&#xC529; &#xD0A4;&#xC6B8; &#xC218; &#xC788;&#xC2B5;&#xB2C8;&#xB2E4;.
        &#xC774; &#xBA54;&#xBAA8;&#xB9AC; &#xACF5;&#xAC04;&#xC740; &#xC2A4;&#xB808;&#xB4DC;&#xAC00;
        &#xC0DD;&#xC131;&#xB420; &#xB54C; &#xD504;&#xB85C;&#xC138;&#xC2A4; &#xC601;&#xC5ED;&#xC5D0;
        &#xB530;&#xB85C; &#xC124;&#xC815;&#xB418;&#xC9C0;&#xB9CC; &#xD574;&#xB2F9;
        &#xBA54;&#xBAA8;&#xB9AC;&#xC640; &#xC5F0;&#xACB0;&#xB41C; &#xC2E4;&#xC81C;
        &#xD398;&#xC774;&#xC9C0;&#xB294; &#xD544;&#xC694;&#xD560;&#xB54C;&#xAE4C;&#xC9C0;
        &#xC0DD;&#xC131;&#xB418;&#xC9C0; &#xC54A;&#xC2B5;&#xB2C8;&#xB2E4;.</td>
    </tr>
    <tr>
      <td style="text-align:left">&#xC0DD;&#xC131; &#xC2DC;&#xAC04;</td>
      <td style="text-align:left">&#xC57D; 90 &#xB9C8;&#xC774;&#xD06C;&#xB85C;&#xCD08;</td>
      <td style="text-align:left">&#xC774; &#xAC12;&#xC740; &#xC2A4;&#xB808;&#xB4DC; &#xC0DD;&#xC131;&#xC744;
        &#xC704;&#xD55C; &#xD638;&#xCD9C;&#xC774; &#xC77C;&#xC5B4;&#xB098;&#xB294;
        &#xC2DC;&#xC810;&#xBD80;&#xD130; &#xC2A4;&#xB808;&#xB4DC; &#xC5D4;&#xD2B8;&#xB9AC;
        &#xD3EC;&#xC778;&#xD2B8; &#xB8E8;&#xD2F4;&#xC774; &#xC2E4;&#xD589;&#xB418;&#xB294;
        &#xC2DC;&#xC810;&#xAE4C;&#xC9C0;&#xC758; &#xC2DC;&#xCC28;&#xB97C; &#xBC18;&#xC601;&#xD569;&#xB2C8;&#xB2E4;.
        90 &#xB9C8;&#xC774;&#xD06C;&#xB85C;&#xCD08;&#xB77C;&#xB294; &#xC2DC;&#xAC04;&#xC740;
        OS X v10.5&#xB97C; &#xC6B4;&#xC6A9;&#xD558;&#xB294; &#xC778;&#xD154; &#xAE30;&#xBC18;
        (2Ghz &#xCF54;&#xC5B4; &#xB4C0;&#xC624; &#xD504;&#xB85C;&#xC138;&#xC11C;&#xC640;
        1GB &#xB7A8;) iMac&#xC5D0;&#xC11C; &#xC2A4;&#xB808;&#xB4DC;&#xB97C; &#xC0DD;&#xC131;&#xD560;&#xB54C;&#xC758;
        &#xAC12;&#xC744; &#xCE21;&#xC815;&#xD558;&#xC5EC; &#xD3C9;&#xADE0;&#xAC12;&#xACFC;
        &#xC911;&#xAC04;&#xAC12;&#xC744; &#xD1A0;&#xB300;&#xB85C; &#xC0B0;&#xCD9C;&#xD574;&#xB0B8;
        &#xAC12;&#xC785;&#xB2C8;&#xB2E4;.</td>
    </tr>
  </tbody>
</table>

{% hint style="info" %}
Note

기본 커널 지원으로 인해 작업 객체가 더 빠르게 스레드를 생성하는 일이 생길 수 있습니다. 이 경우 스레드를 생성할 때마다 매번 처음부터 작업하는 것이 아니라 할당 시간을 절약하기 위해 커널에 이미 있는 스레드 풀을 사용합니다. 작업 객체 사용에 대한 더 자세한 정보는 [동시성 프로그래밍 가이드](../../etc/not-found.md)를 참조하세요.
{% endhint %}

스레딩 관련 코드를 작성할때 고려해야할 또 다른 비용은 생산성 문제입니다. 스레드를 사용하는 애플리케이션을 디자인하는 일은 종종 애플리케이션 데이터를 구조화하는 방식에 근본적인 변화를 요구하게됩니다. 아마 이 변화들은 발생하게 될 동기화 문제를 해결하기 위해 필수불가결하겠지만 잘 설계되지 못한 애플리케이션에는 심각한 성능 저하를 불러일으킬 것입니다. 스레드 맞춤 설계된 데이터 구조를 디자인하고 디버깅하는 것은 애플리케이션 개발 기간을 지연시킬 수 있습니다. 그러나 이 문제를 회피한다면 스레드가 락을 기다리거나 아무것도 하지 않는 시간이 늘어나서 런타임 시 더 큰 문제가 발생할 수 있습니다.

## 스레드 생성하기 <a id="creating-a-thread"></a>

로우 레벨 스레드를 생성하는 것은 상대적으로 간단합니다. 어떤 경우에든 여러분은 스레드의 메인 엔트리 역할을 하는 함수나 메소드를 만들어야 하며, 그 중에서 사용가능한 스레드 루틴을 사용해야 합니다. 다음 섹션은 일반적으로 사용되는 스레드 기술을 사용한 기초적인 생성 프로세스를 보여줍니다. 이 기술들을 사용해서 생성된 스레드들은 해당 기술이 기본값으로 지정한 속성 세트를 상속받습니다. 스레드를 설정하는 방법에 대한 정보는 [스레드 속성 설정](thread-management.md#configuring-thread-attributes)을 참조하세요.

### NSThread <a id="using-nsthread"></a>

NSThread 클래스를 사용하여 스레드를 생성하는 방법은 두 가지가 있습니다.

* [detachNewThreadSelector:toTarget:withObject:](../../etc/not-found.md) 클래스 메소드
* 새 _NSThread_ 객체를 만들고 _start_ 메소드를 호출하기 \(OS X v10.5 이상, iOS 지원\)

두 기술 모두 애플리케이션 내에서 분리된 스레드를 생성합니다. 분리된 스레드란 스레드가 종료될 때 해당 스레드의 리소스가 시스템에 의해 자동으로 회수됨을 의미합니다. 또한 코드가 나중에 스레드와 명시적으로 조인할 필요가 없다는 의미이기도 합니다.

_detacheNewThreadSelector:toTarget:withObject:_ 메소드는 모든 버전의 OS X에서 지원되기 때문에 스레드를 사용되는 코코아 애플리케이션에서 종종 발견됩니다. 새 스레드를 분리하기 위해서는 스레드의 엔트리 포인트로 사용하고자 하는 \(selector로 지정되는\) 메소드의 이름, 해당 메소드를 정의하는 객체, 시작 시 스레드에 전달할 데이터를 제공하기만 하면 됩니다. 다음 코드는 현재 객체의 커스텀 메소드를 사용하여 스레드를 생성하는 기본 요청 예시입니다.

```text
[NSThread detachNewThreadSelector:@selector(myThreadMainMethod:) toTarget:self withObject:nil];
```

OS X v10.5 이전에는 스레드를 생성할 때 주로 _NSThread_를 사용했습니다. _NSThread_ 객체와 몇몇 스레드 속성에 대한 접근을 얻어낼 수는 있지만 그것은 스레드가 실행된 이후에만 가능한 일이었습니다. OS X v10.5 부터는 새 스레드를 즉시 생성해내지 않으면서도 _NSThread_ 객체를 생성하는 기능이 지원되기 시작했습니다. \(이는 iOS에서도 사용가능합니다.\) 이 기능을 통해 스레드가 실행되기에 앞서서 속성을 읽고 쓰는 것이 가능해졌습니다.

10.5 버전 이후의 OS X에서 _NSThread_ 객체를 초기화 하는 간단한 방법은 [initWithTarget:selector:object:](../../etc/not-found.md) 메소드를 사용하는 것입니다. 이 메소드는 _detachNewThreadSelector:toTarget:withObject:_ 메소드와 완전히 동일한 정보를 입력받아서 새 N_SThread_ 인스턴스를 초기화합니다. 그러나 스레드를 시작하려면 다음 예제와 같이 스레드 객체의 _start_ 메소드를 호출해야 합니다:

```text
NSThread* myThread = [[NSThread alloc] initWithTarget:self
                                        selector:@selector(myThreadMainMethod:)
                                        object:nil];
[myThread start];  // Actually create the thread
```

{% hint style="info" %}
Note

initWithTarget:selector:object: 메소드의 대안은 NSThread를 서브클래싱하여 main메소드를 오버라이딩 하는것입니다. 이 메소드의 오버라이드 된 버전을 사용하여 스레드의 메인 엔트리 포인트를 구현할 수 있습니다. 더 자세한 정보를 보려면 NSThread Class Reference의 서브클래싱 노트를 읽어보세요
{% endhint %}

이미 실행 중인 NSThread 객체가 있다면 애플리케이션 내 거의 모든 객체에 있는 [perforemSelector:onThread:withObject:waitUntilDone:](../../etc/not-found.md) 메소드를 사용하여 해당 스레드에 메세지를 전달할 수 있습니다. \(메인 스레드 외의\) 스레드 상에서 셀렉터를 실행하는 기능은 OS X v10.5부터 지원되었으며 스레드 간 통신에는 매우 편리한 방법입니다. 이 기술을 사용하여 전달된 메세지는 해당 스레드의 일반 런루프 프로세스의 일부로서 즉시 실행됩니다. \(물론 이것은 타겟 스레드가 런루프에서 실행되고 있어야 함을 전제로 합니다. [런 루프 설정](thread-management.md#setting-up-a-run-loop)을 읽어보세요.\) 아직 동기화와 같은 문제가 남아 있긴 하지만 스레드간 통신 포트를 설정하는 방식에 비하면 여전히 쉬운 방법입니다.

{% hint style="info" %}
Note

스레드 간 통신이 가끔씩 일어나는 경우에는 performSelector:onThread:withObject:waitUntilDone: 메소드가 좋은 방법이 될 수 있지만 시간이 중요한 통신이나 자주 일어나는 통신에는 사용해서는 안됩니다.
{% endhint %}

스레드 통신에 대한 다른 옵션들을 보고 싶으시면 [분리된 상태의 스레드 설정](thread-management.md#setting-the-detached-state-of-a-thread) 참조하세요.

### POSIX 스레드 <a id="using-posix-threads"></a>

OS X과 iOS는 POSIX 스레드 API를 사용해서 스레드를 생성하는 C 기반의 지원을 제공합니다. 이 기술은 \(코코아와 코코아 터치 애플리케이션을 포함한\) 어떤 종류의 애플리케이션에서도 사용할 수 있으며 여러 플랫폼에 사용될 소프트웨어를 만들 것이라면 편리한 방법이 될것입니다. 스레드를 생성하는 POSIX 루틴은 그 이름도 적절한 _pthread\_create_입니다.

```c
#include <assert.h>
#include <pthread.h>
 
void* PosixThreadMainRoutine(void* data)
{
    // Do some work here.
 
    return NULL;
}
 
void LaunchThread()
{
    // Create the thread using POSIX routines.
    pthread_attr_t  attr;
    pthread_t       posixThreadID;
    int             returnVal;
 
    returnVal = pthread_attr_init(&attr);
    assert(!returnVal);
    returnVal = pthread_attr_setdetachstate(&attr, PTHREAD_CREATE_DETACHED);
    assert(!returnVal);
 
    int     threadError = pthread_create(&posixThreadID, &attr, &PosixThreadMainRoutine, NULL);
 
    returnVal = pthread_attr_destroy(&attr);
    assert(!returnVal);
    if (threadError != 0)
    {
         // Report an error.
    }
}
```

이 코드를 소스코드 파일 중 하나에 삽입한 후 LaunchThread 함수를 호출하면 해당 애플리케이션에 새 분리된 스레드가 생성됩니다. 물론 이 코드로 생성된 스레드는 어떤 작업도 하지 않은채로 거의 즉시 종료됩니다. 좀더 흥미로운 코드를 만들기 위해서는 좀더 실제적인 작업을 수행하는 PosixThreadMainRoutine 함수가 추가되어야 합니다. 해당 스레드가 생성될 때 데이터 포인터를 전달해서 해야할 일을 알려줄 수 있습니다. 이 포인터는 pthread\_create 함수의 마지막 파라미터로 전달됩니다.

POSIX 스레드 함수에 대한 정보를 더 알고 싶으시다면 [pthread](../../etc/not-found.md) 메뉴얼 페이지를 참조하세요.

### NSObject로 스레드 생성하기 <a id="using-nsobject-to-spawn-a-thread"></a>

iOS와 10.5이상의 OS X에서는 모든 객체들이 새 스레드를 만들어 자체 메소드를 실행할 수 있게 되었습니다. [performSelectorInBackground:withObject:](../../etc/not-found.md) 메소드는 분리된 메소드를 생성해서 지정된 메소드를 새 스레드의 엔트리 포인트로 사용하게 됩니다. 예를 들어 _doSomething_이라는 메소드를 갖는 어떤 객체\(_myObj_\)가 있다면 다음 코드로 해당 메소드를 백그라운드에서 실행할 수 있습니다.

```text
[myObj performSelectorInBackground:@selector(doSomething) withObject:nil];
```

이 메소드는 [NSThread](../../etc/not-found.md)의 [detachNewThreadSelector:toTarget:withObject:](../../etc/not-found.md) 메소드에 현재 객체, 셀렉터, 파라미터를 대입한 것과 같은 기능을 합니다. 이 새 스레드는 생성 즉시 기본 설정을 사용하여 즉시 실행됩니다. 셀렉터 내부에서는 다른 스레드에서 하던것과 마찬가지로 해당 스레드를 설정해주어야 합니다. 예를 들어, \(가비지 콜렉션을 사용하지 않는다면\) 오토릴리즈 풀을 설정해주어야 할 것이며, 런 루프를 사용할 예정이라면 그것도 설정해주어야 합니다. 새 스레드를 설정하는 방법에 대한 정보는 [스레드 속성 설정](thread-management.md#configuring-thread-attributes)을 참조하세요.

### 코코아 애플리케이션에서 POSIX 스레드 사용하기 <a id="using-posix-threads-in-a-cocoa-application"></a>

NSThread 클래스는 코코아 애플리케이션에서 스레드 생성을 위한 주요 인터페이스지만 편의에 따라 POSIX 스레드를 사용해도 됩니다. 예를 들어, 이미 POSIX 스레드를 사용하는 코드가 있고 그것을 재작성하고 싶지 않다면 그대로 사용할 수 있습니다. 코코아 애플리케이션에서 POSIX 스레드를 사용할 계획이라면 코코아와 스레드간의 상호작용관계를 알고 다음 섹션의 지침을 준수해야 합니다.

#### 코코아 프레임워크 보호 <a id="protecting-the-cocoa-frameworks"></a>

멀티 스레드 애플리케이션의 정상적인 동작을 위해서 코코아 프레임워크는 lock과 내부 동기화 형식을 갖추고 있습니다. lock은 싱글 스레드 환경에서 성능 저하를 유발할 수 있기 때문에 코코아 프레임워크는 [NSThread](../../etc/not-found.md) 클래스를 사용해 첫번째 새 스레드가 생성되기 전까지 lock을 거는 것을 막습니다. POSIX 스레드 루틴만을 사용해서 스레드를 생성할 경우 코코아 프레임워크는 애플리케이션이 이제 멀티스레드로 동작한다는 것을 알려주는 노티피케이션을 받을 수 없습니다. 이 경우, 코코아 프레임워크와 관련된 동작이 불안정해지고 애플리케이션의 크래시를 발생시킬수도 있습니다.

코코아 프레임워크에 멀티 스레드 사용을 알려주기 위해서는 _NSThread_ 클래스로 즉시 종료되는 스레드를 하나 생성하면 됩니다. 이 스레드의 엔트리 포인트는 아무것도 할 필요가 없으며 _NSThread_는 그저 스레드를 생성하는 동작을 하는 것만으로 코코아 프레임워크에 lock이 필요하다는 것을 알려줄 수 있습니다.

만약 코코아 프레임워크가 애플리케이션의 멀티 스레드 여부를 인지하고 있는지 확신할 수 없다면 _NSThread_의 [isMultiThreaded](../../etc/not-found.md) 메소드를 사용할 수 있습니다.

#### POSIX와 Cocoa Locks 혼용

같은 애플리케이션 내에서 POSIX와 코코아 lock을 같이 사용하는 것이 안전합니다. 코코아 lock과 조건 객체는 기본적으로 POSIX 뮤텍스와 컨디션의 레퍼입니다. 그러나 lock을 생성하고 조작할 때에는 언제나 같은 인터페이스를 사용해야 합니다. 다시 말해서, Cocoa [NSLock](../../etc/not-found.md) 객체로는 _pthread\_mutex\_init_ 함수를 사용하여 만들어진 mutex를 조작할 수 없으며 그 반대도 마찬가지입니다.

## 스레드 속성 설정 <a id="configuring-thread-attributes"></a>

여러분들은 스레드를 생성한 이후나, 혹은 이전에 스레드 환경의 다른 부분들을 설정하고 싶으실지 모릅니다. 다음 섹션에서는 여러분이 원할때 바꿀 수 있는 것들에 대해서 설명합니다.

### 스레드의 스택 크기 설정 <a id="configurig-the-stack-size-of-a-thread"></a>

새 스레드가 만들어질 때마다 시스템은 프로세스 공간에 스레드 스택을 저장할 메모리를 할당합니다. 스택은 스택 프레임을 관리하고 스레드를 위한 로컬 변수가 선언되는 곳이기도 합니다. 스레드에 할당되는 메모리 양에 대해서는 [스레드 비용](thread-management.md#thread-costs)에 설명되어 있습니다.

| 기술 | 옵션 |
| :--- | :--- |
| 코코아 | iOS / OS X 10.5 이상 환경에서 \([detacheNewThreadSelector:toTarget:withObject:](../../etc/not-found.md)를 사용하지 않고\) NSThread 객체를 할당하고 초기화하세요. 스레드 객체의 start 메소드를 호출하기 전에 [setStackSize:](../../etc/not-found.md) 메소드로 새 스택 크기를 지정하세요. |
| POSIX | 새 _pthread\_attr\_t_ 구조체를 만들고 _pthread\_attr\_setstacksize_ 함수를 사용해서 기본 스택 크기를 변경하세요. 스레드를 생성할 때 해당 attribute를 _pthread\_create_ 함수에 전달하세요. |
| 멀티 프로세싱 서비스 | 스레드 생성시 적당한 스택 크기값을 [MPCreateTask](../../etc/not-found.md) 함수에 전달하세요. |

### 스레드 로컬 저장소 설정 <a id="configuring-thread-local-storage"></a>

각 스레드에는 키-값 쌍의 딕셔너리가 있고 스레드 내 어디서든 접근할 수 있습니다. 이 딕셔너리를 사용하면 스레드 실행 시간동안 원하는 정보를 저장할 수 있습니다. 예를 들어, 스레드의 런 루프가 여러번 반복되는 동안 상태 정보를 저장하는데 사용할 수 있습니다.

코코아 프레임워크와 POSIX는 다른 방법으로 스레드 딕셔너리를 저장하기 때문에 두 방식을 섞어서 사용할 수는 없습니다. 그러나 스레드 코드 내에서 하나의 기술을 고수하는 한 최종 결과는 비슷해야 합니다. 코코아 프레임워크에서 [NSThread](../../etc/not-found.md) 객체의 [threadDictionary](../../etc/not-found.md) 메소드를 사용하면 _NSMutableDictionary_ 객체를 불러와서 스레드에 필요로 하는 어떤 키라도 추가할 수 있습니다. POSIX 스레드에서는 _pthread\_setspecific_과 _pthread\_getspecific_ 함수를 사용해서 스레드의 키/값을 읽고 쓸 수 있습니다.

### 분리된 상태의 스레드 설정 <a id="setting-the-detached-state-of-a-thread"></a>

가장 고수준의 스레드 기술은 기본적으로 분리된 스레드를 생성합니다. 대부분의 경우 분리된 스레드는 스레드가 완료되는 즉시 시스템에서 스레드의 데이터 구조를 해제할 수 있기 때문에 선호됩니다. 분리된 스레드는 프로그램과의 명시적인 상호작용을 필수적으로 요구하지 않습니다. 즉, 스레드 결과값을 불러오는 것은 개발자의 선택이라는 의미입니다. 그에 비해 시스템은 다른 스레드가 해당 스레드와 명시적으로 조인할 때까지 조인 가능한 스레드에 대한 리소스를 회수하지 않습니다. 이 프로세스는 조인을 수행하는 스레드를 차단할 수 있습니다.

{% hint style="info" %}
Important

애플리케이션 종료 시 분리된 스레드는 즉시 종료될 수 있지만 조인 가능한 스레드는 그렇지 않습니다. 조인 가능한 각 스레드는 프로세스가 종료되기 전에 조인되어야 합니다. 따라서 데이터를 디스크에 쓰는 것과 같이 도중에 중단되어서는 안되는 중요한 일을 하는 경우에는 조인 가능한 스레드가 선호됩니다.
{% endhint %}

결합 가능한 스레드를 생성하는 방법은 POSIX 스레드가 유일합니다. POSIX는 기본적으로 조인 가능한 스레드를 생성합니다. 분리된 스레드인지, 조인 가능한 스레드인지를 명시하려면 _pthread\_attr\_setdetachstate_ 함수를 사용해서 스레드가 생성되기 전에 스레드 속성을 미리 수정해야 합니다. 스레드가 생성된 이후, 조인 가능한 스레드를 분리된 스레드로 전환하고자 한다면 _pthread\_detach_ 함수를 호출하세요. 이들 POSIX 스레드 함수에 대해 더 알고 싶다면 [pthread](../../etc/not-found.md) 메뉴얼 페이지를, 스레드 조인 방법에 대해서 알고 싶다면 [pthread\_join](../../etc/not-found.md) 메뉴얼 페이지를 읽어보세요

### 스레드 우선순위 설정 <a id="setting-the-thread-priority"></a>

생성된 모든 스레드에는 연관된 기본 우선순위가 있습니다. 커널의 스케줄링 알고리즘은 우선순위를 반영하여 스레드를 실행할 때 높은 우선순위의 스레드가 더 낮은 우선순위의 스레드보다 우선적으로 실행되도록 합니다. 높은 우선순위가 반드리 특정 길이의 실행 시간을 보장하는 것은 아닙니다. 그저 낮은 우선순위의 스레드와 비교하여 스케줄러가 선택할 확률을 높여줄 뿐입니다.

{% hint style="info" %}
Important

일반적인 상황에서는 기본 우선 순위값을 그대로 사용하는 편이 낫습니다. 일부 스레드의 우선순위를 높이는 것은 낮은 우선순위 스레드간의 기아 상태를 발생시킬 수 있습니다. 만약 같은 애플리케이션 내에서 반드시 상호작용해야 하는 높은 우선순위의 스레드와 낮은 우선순위가 공존한다면 기아상태에 있는 낮은 우선순위의 스레드가 다른 스레드의 작업을 블록하고 성능 병목현상을 초래할 것입니다.
{% endhint %}

POSIX와 코코아 프레임워크 둘다 스레드 우선순위 조정 기능을 제공합니다. 코코아 프레임워크에서는 [NSThread](../../etc/not-found.md)의 클래스 메소드인 [setThreadPriority:](../../etc/not-found.md)를 사용해서 현재 실행중인 스레드의 우선순위를 조정할 수 있고 POSIX 스레드는 _pthread\_setschedparam_ 함수를 사용할 수 있습니다.더 자세한 정보는 [_NSThread class Reference_](../../etc/not-found.md)나 [pthread\_setschedparam](../../etc/not-found.md) 메뉴얼 페이지를 참조하세요.

## 스레드 엔트리 루틴 작성하기 <a id="writing-your-thread-entry-routine"></a>

대부분의 경우 스레드의 엔트리 루틴 구조는 다른 플랫폼에서와 마찬가지로 OS X에서도 동일합니다. 데이터 구조를 초기화하고, 작업을 하거나 선택적으로 런 루프를 설정합니다. 그리고 스레드 코드가 완료되면 정리합니다. 설계하기에 따라 필요한 몇 단계의 작업이 엔트리 루틴에 추가될 것입니다.

### 오토 릴리즈 풀 생성 <a id="creating-an-autorelease-pool"></a>

Objective-C 프레임워크에서 연결되는 애플리케이션은 보통 스레드당 하나 이상의 오토 릴리즈 풀을 만들어야 합니다. 만약 애플리케이션이 Managed memory 모델\(애플리케이션이 객체의 retain과 release를 관리함\)을 사용한다면 해당 오토 릴리즈 풀은 스레드에서 오토릴리즈되는 모든 객체를 잡아낼 것입니다.

애플리케이션이 Managed memory model이 아니라 가비지 콜렉션을 사용한다면 오토 릴리즈 풀이 반드시 생성되어야 하는 것은 아닙니다. 가비지 콜렉션을 사용하는 애플리케이션에서 오토릴리즈 풀의 존재는 무해하며, 대부분은 무시됩니다. 오토 릴리즈 풀은 Managed memory 모델과 가비지 콜렉션이 둘다 필요한 경우를 위해서 허용됩니다. 이런 경우, 오토 릴리즈 풀은 Managed memory 모델 코드를 지원하기 위해서 존재해야 하며 가비지 콜렉션이 활성화된 상태에서 애플리케이션이 실행되는 경우 무시됩니다.

애플리케이션이 Managed memory 모델을 사용한다면 오토 릴리즈 풀 생성은 스레드 엔트리 루틴에 반드시 추가되어야 할 첫번째 작업입니다. 비슷하게, 이 오토 릴리즈 풀을 제거하는 것은 스레드에서 가장 마지막에 수행되어야 합니다. 이 풀은 스레드 자체가 종료될 때까지 오토 릴리즈 된 객체를 잡아내되, 해제하지는 않습니다. 다음 코드는 오토 릴리즈 풀을 사용하는 기본 스레드 엔트리 루틴의 구조를 보여줍니다.

```text
- (void)myThreadMainRoutine
{
    NSAutoreleasePool *pool = [[NSAutoreleasePool alloc] init]; // 최고 레벨 풀
    
    // 스레드 작업 수행
    
    [pool release]; // 풀의 객체를 해제
}
```

최고 레벨 오토 릴리즈 풀이 스레드 종료 시까지 보유한 객체를 해제하지 않기 때문에 장기간 유지되는 스레드는 부가적인 오토릴리즈 풀을 생성하여 더 자주 객체를 해제시켜주어야 합니다. 예를 들어 런 루프를 사용하는 스레드라면 매 런 루프마다 오토릴리즈 풀을 생성하고 해제할 수 있을 것입니다. 객체를 더 자주 해제해 주는 것은 매플리케이션의 메모리 발자국이 커지는 것을 막고 성능 이슈로 번지는 일을 방지해줍니다. 성능 관련 동작과 마찬가지로 코드의 실제 성능을 측정하고 오토릴리즈 풀의 사용을 적절하게 조정해줄 필요가 있습니다.

메모리 관리 및 오토릴리즈 풀에 대한 더 자세한 정보는 [_Advanced Memory Management Programming Guide_](https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/MemoryMgmt/Articles/MemoryMgmt.html#//apple_ref/doc/uid/10000011i)를 참조하세요.

### 예외 처리기 설정 <a id="setting-up-an-exception-handler"></a>

애플리케이션에서  예외를 잡아내고 처리하고 있다면 스레드 코드에서도 예외 처리를 준비해야 합니다. 가장 좋은 일은 예외가 발생한 지점에서 처리하는 것이겠지만 스레드 내에서 발생한 예외를 잡아내지 못한다면 애플리케이션 종료로 이어지게 됩니다. 스레드 엔트리 루틴에 최종적인 try/catch 블록을 작성하는 것은 알려지지 않은 예외에 적절한 응답을 제공해줄 수 있습니다.

Xcode에서 프로젝트를 빌드할 때 C++나 Objective-C의 예외 처리 스타일을 사용할 수 있습니다. Objective-C에서 예외를 발생시키고 catch하는 방법을 어떻게 설정하는지 알고 싶다면 [_Exception Programming_](https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/Exceptions/Exceptions.html#//apple_ref/doc/uid/10000012i) 주제를 참조하세요.

### 런 루프 설정 <a id="setting-up-a-run-loop"></a>

분리된 스레드의 코드를 작성할 때에는 두가지 방법이 있습니다. 첫번째는 인터럽트를 최소화하며 하나의 작업을 길게 수행하다가 완료되면 스레드를 종료하는 것입니다. 두번째는 스레드를 루프에 집어넣고 들어오는 요청을 동적으로 수행하는 방법입니다. 첫번째는 코드에 특별한 셋업이 필요없고 원하는 작업을 시작하기만 하면 되지만 두번째의 경우 런 루프를 설정하는 작업이 수반됩니다.

OS X과 iOS에는 모든 스레드에 런 루프를 구현하는 내장된 지원을 제공합니다. 앱 프레임워크는 애플리케이션의 메인 스레드에서 런 루프를 자동적으로 실행하는데, 보조 스레드에서는 런 루프를 설정하고 직접 실행해야 합니다.

런 루프의 사용 및 설정에 대해서는 [Run Loops](https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/Multithreading/RunLoopManagement/RunLoopManagement.html#//apple_ref/doc/uid/10000057i-CH16-SW1)를 참조하세요. 

## 스레드 종료 <a id="terminating-a-thread"></a>

 스레드를 종료시키는 방법으로 추천하는 것은 엔트리 포인트 루틴이 정상적으로 종료되게 하는 것입니다. 코코아 POSIX, 멀티프로세싱 서비스에서 스레드를 직접적으로 죽이는 루틴을 제공하긴 하지만 강력히 비권장되는 방법입니다. 스레드를 죽이면 스레드가 스스로 정리할 수가 없게 됩니다. 스레드에 할당된 메모리는 잠재적으로 누수되며, 스레드가 사용하던 리소스는 적절히 정리되지 못해서 추후에 문제를 발생할 소지가 생깁니다.

스레드를 작업 도중에 중단시키고자 한다면 처음 스레드를 설계할 때부터 취소 또는 종료 메세지에 대응하도록 만들어야 합니다. 장시간 작업에 이를 구현한다면 주기적으로 작업을 멈추고 이러한 메세지가 들어왔는지 확인하게 될 것입니다. 스레드에게 종료할 것을 요청하는 메세지가 들어왔다면 스레드는 필요한 정리작업을 마치고 정상적으로 종료할 기회를 얻게 됩니다. 그런 메세지가 없다면, 다시 작업으로 되돌아가서 다음 데이터 청크를 처리하게 됩니다.

취소 메세지에 대응하도록 하는 방법 중 하나는 메세지를 받는 런 루프를 사용하는 것입니다. 다음은 이런 코드들이 스레드 메인 루틴에서 어떻게 보여지는지 알려줍니다. \(여기서는 메인 루프에 대한 부분만을 보여주며 오토릴리즈 풀 설정이나 실제 작업에 대한 코드는 포함하지 않습니다.\) 이 예제에서는 다른 스레드에서 메세지를 보낼 런 루프에 커스텀 입력 소스를 설치합니다. 입력 소스 설정에 대해서는 [Configuring Run Loop Sources](https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/Multithreading/RunLoopManagement/RunLoopManagement.html#//apple_ref/doc/uid/10000057i-CH16-SW7)를 참조하세요. 총 작업량의 일부를 수행한 다음 스레드는 런 루프를 실행해서 입력 소스에 도착한 메세지가 있는지 확인하고 없으면 런 루프를 즉시 종료한 다음 다음 작업 청크를 위한 루프를 계속합니다. 핸들러에는 exitNot 지역 변수에 직접적으로 접근할 방법이 없기 때문에 스레드 딕셔너리의 키-값 쌍을 통해서 종료 조건값을 통신해야 합니다.

```text
- (void)threadMainRoutine
{
    BOOL moreWorkToDo = YES;
    BOOL exitNow = NO;
    NSRunLoop* runLoop = [NSRunLoop currentRunLoop];
 
    // 스레드 딕셔너리에 exitNow BOOL 추가
    NSMutableDictionary* threadDict = [[NSThread currentThread] threadDictionary];
    [threadDict setValue:[NSNumber numberWithBool:exitNow] forKey:@"ThreadShouldExitNow"];
 
    // Install an input source.
    [self myInstallCustomInputSource];
 
    while (moreWorkToDo && !exitNow)
    {
        // 작업 청크 하나를 여기서 수행함
        // 작업이 끝나면 moreWorkToDo Boolean값을 변경
 
        // 런 루프를 실행하고 입력 소스가 실행 대기 중이 아니면 곧바로 timeout
        [runLoop runUntilDate:[NSDate date]];
 
        // 입력 소스 핸들러가 exitNot 값을 변경했는지 확인
        exitNow = [[threadDict valueForKey:@"ThreadShouldExitNow"] boolValue];
    }
}
```

