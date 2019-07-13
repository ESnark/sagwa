# About Threaded Programming

> 원문 출처  
> [https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/Multithreading/AboutThreads/AboutThreads.html\#//apple\_ref/doc/uid/10000057i-CH6-SW2](https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/Multithreading/AboutThreads/AboutThreads.html#//apple_ref/doc/uid/10000057i-CH6-SW2)

오랜 기간동안 컴퓨터 성능의 최대치는 컴퓨터 중심에 있는 단일 마이크로 프로세서의 속도에 의해 크게 제한되었습니다. 그러나 개별 프로세서의 속도가 실제 한계에 도달하기 시작하자 칩 제조업체는 멀티 코어 설계로 전환하여 여러 작업을 동시에 수행할 수 있는 기회를 컴퓨터에 제공했습니다. OS X은 시스템 관련 작업을 할 때 멀티 코어를 활용하고 있으며 응용프로그램들 또한 스레드를 사용하여 활용하는 것이 가능합니다.

## 스레드란? <a id="what-are-threads"></a>

스레드는 응용 프로그램 내에서 여러 실행 경로를 구현하는 비교적 간단한 방법입니다. 시스템 수준에서 프로그램은 나란히 실행되고 프로그램들의 요구에 따라 실행 시간을 계산하여 분배합니다. 그러나 각 프로그램 안에는 하나 이상의 실행 스레드가 있으며, 이는 동시적으로 다른 작업을 수행하는 데 사용될 수 있습니다. 시스템은 자체적으로 이러한 실행 스레드를 관리하고 사용 가능한 코어에서 실행되도록 미리 스케줄링하며 다른 스레드가 실행될 수 있도록 필요에 따라 사전에 중단시킵니다.

기술적 관점에서 볼 때 스레드는 코드 실행을 관리하는 데 필요한 커널 수준 및 응용 프로그램 수준 데이터 구조체의 조합입니다. 커널 수준 구조체는 스레드에 대한 이벤트 발송 및 사용 가능한 코어 중 하나에서 스레드의 선점 예약을 조정합니다. 응용 프로그램 수준 구조체에는 함수 호출을 저장하기위한 호출 스택과 응용 프로그램이 스레드의 특성 및 상태를 관리하고 조작하는 데 필요한 구조체가 포함됩니다.

비동시적인 응용 프로그램에는 단 하나의 실행 스레드만이 존재합니다. 이 스레드는 응용프로그램의 main 루틴에서 시작되고 끝나며, 응용 프로그램의 전반적인 동작을 구현하기 위해서 메서드 또는 함수에 하나씩 분기합니다. 반면에 동시성을 지원하는 응용프로그램은 하나의 스레드에서 시작하여 필요에 따라 추가적인 실행 경로를 생성하고 추가합니다. 각각의 새 경로는 고유한 커스텀 시작 루틴을 가지고 있으며 응용프로그램의 main 루틴과 별도로 동작합니다. 응용 프로그램이 다중 스레드를 갖는 경우 중요하고도 잠재적인 두 가지 장점을 제공합니다:

* 다중 스레드는 응용 프로그램의 인식된 응답성을 향상시킬 수 있습니다.
* 다중 스레드는 멀티코어 시스템상에서 응용 프로그램의 실시간 성능을 향상시킬 수 있습니다.

응용 프로그램에 스레드가 하나만 있다면 그 하나의 스레드가 모든 일을 다 처리해야만 합니다. 이 스레드는 이벤트에 응답하고, 응용 프로그램의 window를 업데이트하고, 응용 프로그램의 동작을 구현하는데 필요한 모든 계산을 수행해야 합니다. 문제는 스레드가 한번에 하나의 일만 할 수 있다는 것입니다. 만약 이 계산들 중에 끝내기까지 시간이 오래 걸리는 것이 있다면 어떻게 될까요? 코드가 필요한 값을 계산하느라 바쁜 도중에 응용 프로그램은 사용자 이벤트에 응답하거나 window를 업데이트 하는 일을 중단하게 됩니다. 이런 상태가 오래 지속되면 사용자는 응용 프로그램이 멈춘 것으로 생각하고 강제 종료할 것입니다. 그러나 사용자 지정 계산을 별도의 스레드로 옮기면 응용 프로그램의 main 스레드는 사용자 상호작용에 보다 신속하게 응답할 수 있습니다.

오늘날 멀티코어 컴퓨터는 스레드가 특정 유형의 응용 프로그램에서 성능을 향상시킬 수있는 방법을 제공합니다. 다른 작업을 수행하는 스레드는 서로 다른 프로세서 코어에서 동시에 실행될 수 있으므로 응용 프로그램은 주어진 시간 내에 수행하는 작업량을 늘릴 수 있습니다.

물론 스레드는 응용 프로그램의 성능 문제를 해결하기위한 만병 통치약이 아닙니다. 스레드는 이점을 제공하기도 하지만 잠재적인 문제점 또한 존재합니다. 응용 프로그램에서 여러 실행 경로를 사용하면 코드에 상당한 복잡성이 추가될 수 있습니다. 각 스레드는 응용 프로그램의 상태 정보가 손상되지 않도록 다른 스레드와 동작을 조정해야 합니다. 단일 응용 프로그램 내의 모든 스레드들은 동일한 메모리 공간을 공유하므로 동일한 데이터 구조에 액세스 할 수 있습니다. 두 개의 스레드가 동시에 같은 데이터 구조를 조작하려고하면 한 스레드가 결과 데이터 구조를 손상시키는 방식으로 다른 스레드의 변경 사항을 덮어 쓸 수 있습니다. 적절한 보호조치가 취해졌더라도, 코드에 감지하기 어려운 \(그리고 그렇지 않은\) 버그를 삽입하는 컴파일러 최적화를 주의해야합니다.

## 스레딩 전문용어 <a id="threading-terminology"></a>

스레드와 지원 기술에 대해 깊이 논의를 하기 전에 몇 가지 기본 용어를 정의해야합니다.

여러분이 UNIX 시스템에 익숙하시다면 이 문서에서 "task"라는 용어가 다르게 사용된다는 것을 알 수 있으실겁니다. UNIX 시스템에서 "task"라는 용어는 실행중인 프로세스를 지칭할 때 사용됩니다.

이 문서는 다음과 같은 용어를 사용합니다:

* 스레드_thread_ 라는 용어는 별도의 코드 실행경로를 뜻합니다.
* 프로세스_process_ 라는 용어는 실행 가능한 실행 파일을 나타내며 여러개의 실행 파일을 포함할 수 있습니다.
* 작업_task_ 이라는 용어는 수행되어야 할 작업의 추상적인 개념입니다.

## 스레드의 대안들 <a id="alternatives-to-threads"></a>

스레드 생성의 문제점은 이것이 코드에 불확실성 또한 추가한다는 것입니다. 스레드는 상대적으로 저수준의 복잡한 방법으로 응용 프로그램의 동시성을 지원합니다. 개발자가 자신이 선택한 디자인이 초래할 결과에 대해서 온전히 이해하지 못한다면 동기화나 타이밍 문제를 마주치기 쉬워집니다. 심각도는 미묘한 동작 변경에서 응용 프로그램 충돌 및 사용자 데이터 손상까지 다양합니다.

고려해야 할 다른 요소는 정말 스레드나 동시성이 필요한지를 판단하는 것입니다. 스레드는 동일한 프로세스 내에서 동시에 여러 코드 경로를 실행해야 하는 문제를 해결합니다. 그렇지만 수행중인 작업의 양이 동시성을 보장하지 않는 경우가 발생할 수 있습니다. 스레드는 메모리 사용과 CPU 시간에 있어서 프로세스에 상당한 양의 오버헤드를 발생시킵니다. 개발자는 이 오버헤드가 의도한 작업에 비해 너무 크거나 다른 옵션을 구현하는 게 더 쉽다는 것을 알 수 있을 것입니다.

표 1-1은 스레드의 몇가지 대안을 나열하고 있습니다. 이 표는 \(operation 객체나 GCD와 같은\) 스레드의 대체 기술과 이미 가지고 있는 단일 스레드를 효율적으로 사용할 수 있는 대안을 모두 포함하고 있습니다.

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#xAE30;&#xC220;</th>
      <th style="text-align:left">&#xC124;&#xBA85;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Operation &#xAC1D;&#xCCB4;</td>
      <td style="text-align:left">
        <p>OS X 10.5&#xBD80;&#xD130; &#xB3C4;&#xC785;&#xB41C; operation &#xAC1D;&#xCCB4;&#xB294;
          &#xBD80;&#xCC28;&#xC801;&#xC778; &#xC2A4;&#xB808;&#xB4DC;&#xC5D0;&#xC11C;
          &#xC2E4;&#xD589;&#xB420; &#xC791;&#xC5C5;&#xC758; &#xB798;&#xD37C;Wrapper&#xC785;&#xB2C8;&#xB2E4;.
          &#xC774; &#xB798;&#xD37C;&#xB294; &#xC791;&#xC5C5; &#xC218;&#xD589;&#xC911;&#xC5D0;&#xC11C;
          &#xC2A4;&#xB808;&#xB4DC; &#xAD00;&#xB9AC; &#xBD80;&#xBD84;&#xC744; &#xC228;&#xAE30;&#xACE0;
          &#xC791;&#xC5C5; &#xC790;&#xCCB4;&#xC5D0; &#xC9D1;&#xC911;&#xD560; &#xC218;
          &#xC788;&#xB3C4;&#xB85D; &#xB3D5;&#xC2B5;&#xB2C8;&#xB2E4;. &#xC774; &#xAC1D;&#xCCB4;&#xB294;
          &#xC77C;&#xBC18;&#xC801;&#xC73C;&#xB85C; operation queue &#xAC1D;&#xCCB4;&#xC640;
          &#xACB0;&#xD569;&#xB418;&#xC5B4; &#xAC19;&#xC774; &#xC0AC;&#xC6A9;&#xB418;&#xBA70;
          operation queue&#xB294; &#xD558;&#xB098; &#xC774;&#xC0C1;&#xC758; &#xC2A4;&#xB808;&#xB4DC;
          &#xC0C1;&#xC5D0;&#xC11C; operation &#xAC1D;&#xCCB4;&#xC758; &#xC2E4;&#xD589;&#xC744;
          &#xAD00;&#xB9AC;&#xD558;&#xB294; &#xC5ED;&#xD560;&#xC744; &#xD569;&#xB2C8;&#xB2E4;.</p>
        <p>&#xC790;&#xC138;&#xD55C; &#xB0B4;&#xC6A9;&#xC740; <a href="https://developer.apple.com/library/archive/documentation/General/Conceptual/ConcurrencyProgrammingGuide/Introduction/Introduction.html#//apple_ref/doc/uid/TP40008091">&#xB3D9;&#xC2DC;&#xC131; &#xD504;&#xB85C;&#xADF8;&#xB798;&#xBC0D; &#xAC00;&#xC774;&#xB4DC;</a>&#xB97C;
          &#xC77D;&#xC5B4;&#xBCF4;&#xC138;&#xC694;.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Grand Central Dispatch (GCD)</td>
      <td style="text-align:left">
        <p>OS X 10.6&#xBD80;&#xD130; &#xB3C4;&#xC785;&#xB41C; Grand Ceentral Dispatch&#xB294;
          &#xC2A4;&#xB808;&#xB4DC; &#xAD00;&#xB9AC;&#xBCF4;&#xB2E4; &#xC791;&#xC5C5;&#xC5D0;
          &#xC9D1;&#xC911;&#xD558;&#xB3C4;&#xB85D; &#xB3D5;&#xB294; &#xB610;&#xB2E4;&#xB978;
          &#xB300;&#xC548;&#xC785;&#xB2C8;&#xB2E4;. GCD&#xB97C; &#xC0AC;&#xC6A9;&#xD558;&#xBA74;
          &#xC218;&#xD589;&#xD558;&#xACE0;&#xC790; &#xD558;&#xB294; &#xC791;&#xC5C5;&#xC744;
          &#xC815;&#xC758;&#xD558;&#xACE0; &#xC791;&#xC5C5; &#xB300;&#xAE30;&#xC5F4;Work
          Queue&#xC5D0; &#xCD94;&#xAC00;&#xD560; &#xC218; &#xC788;&#xC2B5;&#xB2C8;&#xB2E4;.
          &#xC791;&#xC5C5; &#xB300;&#xAE30;&#xC5F4;&#xC740; &#xC801;&#xC808;&#xD55C;
          &#xC2A4;&#xB808;&#xB4DC;&#xC5D0; &#xC791;&#xC5C5;&#xC744; &#xC608;&#xC57D;&#xD558;&#xB294;
          &#xC77C;&#xC744; &#xCC98;&#xB9AC;&#xD569;&#xB2C8;&#xB2E4;. &#xC791;&#xC5C5;
          &#xB300;&#xAE30;&#xC5F4;&#xC740; &#xC0AC;&#xC6A9; &#xAC00;&#xB2A5;&#xD55C;
          &#xCF54;&#xC5B4; &#xC218;&#xC640; &#xD604;&#xC7AC; &#xB85C;&#xB4DC;&#xC5D0;
          &#xB530;&#xB77C; &#xC2A4;&#xB808;&#xB4DC;&#xB97C; &#xC0AC;&#xC6A9;&#xD558;&#xC5EC;
          &#xC791;&#xC5C5;&#xC744; &#xBCF4;&#xB2E4; &#xD6A8;&#xC728;&#xC801;&#xC73C;&#xB85C;
          &#xC2E4;&#xD589;&#xD569;&#xB2C8;&#xB2E4;.</p>
        <p>GCD&#xC758; &#xC0AC;&#xC6A9;&#xBC29;&#xBC95;&#xACFC; &#xC791;&#xC5C5;
          &#xB300;&#xAE30;&#xC5F4;&#xC5D0; &#xB300;&#xD55C; &#xC815;&#xBCF4;&#xB294;
          <a
          href="https://developer.apple.com/library/archive/documentation/General/Conceptual/ConcurrencyProgrammingGuide/Introduction/Introduction.html#//apple_ref/doc/uid/TP40008091">&#xB3D9;&#xC2DC;&#xC131; &#xD504;&#xB85C;&#xADF8;&#xB798;&#xBC0D; &#xAC00;&#xC774;&#xB4DC;</a>&#xB97C;
            &#xC77D;&#xC5B4;&#xBCF4;&#xC138;&#xC694;.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Idle-time &#xB178;&#xD2F0;&#xD53C;&#xCF00;&#xC774;&#xC158;</td>
      <td style="text-align:left">idle time &#xB178;&#xD2F0;&#xD53C;&#xCF00;&#xC774;&#xC158;&#xC740; &#xC0C1;&#xB300;&#xC801;&#xC73C;&#xB85C;
        &#xC9E7;&#xAC8C; &#xC2E4;&#xD589;&#xB418;&#xACE0; &#xC6B0;&#xC120;&#xC21C;&#xC704;&#xAC00;
        &#xB0AE;&#xC740; &#xC791;&#xC5C5;&#xB4E4;&#xC744; &#xC751;&#xC6A9;&#xD504;&#xB85C;&#xADF8;&#xB7A8;&#xC774;
        &#xBC14;&#xC058;&#xC9C0; &#xC54A;&#xC740; &#xC2DC;&#xAC04;&#xC5D0; &#xC2E4;&#xD589;&#xB420;
        &#xC218; &#xC788;&#xB3C4;&#xB85D; &#xD574;&#xC90D;&#xB2C8;&#xB2E4;. &#xCF54;&#xCF54;&#xC544;
        &#xD504;&#xB808;&#xC784;&#xC6CC;&#xD06C;&#xB294; <a href="https://developer.apple.com/library/archive/documentation/LegacyTechnologies/WebObjects/WebObjects_3.5/Reference/Frameworks/ObjC/Foundation/Classes/NSNotificationQueue/Description.html#//apple_ref/occ/cl/NSNotificationQueue">NSNotificationQueue</a> &#xAC1D;&#xCCB4;&#xB97C;
        &#xD1B5;&#xD574; item-time &#xB178;&#xD2F0;&#xD53C;&#xCF00;&#xC774;&#xC158;&#xC744;
        &#xC9C0;&#xC6D0;&#xD569;&#xB2C8;&#xB2E4;. idle-time &#xB178;&#xD2F0;&#xD53C;&#xCF00;&#xC774;&#xC158;&#xC744;
        &#xC694;&#xCCAD;&#xD558;&#xAE30; &#xC704;&#xD574;&#xC11C;&#xB294; &#xAE30;&#xBCF8;
        NSNotificationQueue &#xAC1D;&#xCCB4;&#xC5D0; <a href="https://developer.apple.com/library/archive/documentation/LegacyTechnologies/WebObjects/WebObjects_3.5/Reference/Frameworks/ObjC/Foundation/TypesAndConstants/FoundationTypesConstants/Description.html#//apple_ref/c/econst/NSPostWhenIdle">NSPostWhenIdle</a> &#xC635;&#xC158;&#xC744;
        &#xC0AC;&#xC6A9;&#xD558;&#xC5EC; &#xB178;&#xD2F0;&#xD53C;&#xCF00;&#xC774;&#xC158;&#xC744;
        &#xBC1C;&#xC1A1;&#xD574;&#xC57C; &#xD569;&#xB2C8;&#xB2E4;. &#xC774; queue&#xB294;
        &#xB7F0; &#xB8E8;&#xD504;&#xAC00; idle &#xC0C1;&#xD0DC;&#xAC00; &#xB418;&#xAE30;
        &#xC804;&#xAE4C;&#xC9C0; &#xB178;&#xD2F0;&#xD53C;&#xCF00;&#xC774;&#xC158;
        &#xAC1D;&#xCCB4;&#xC758; &#xC804;&#xB2EC;&#xC744; &#xC9C0;&#xC5F0;&#xC2DC;&#xD0B5;&#xB2C8;&#xB2E4;.
        <br
        />&#xB354; &#xC790;&#xC138;&#xD55C; &#xB0B4;&#xC6A9;&#xC740; <a href="https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/Notifications/Introduction/introNotifications.html#//apple_ref/doc/uid/10000043i">&#xB178;&#xD2F0;&#xD53C;&#xCF00;&#xC774;&#xC158; &#xD504;&#xB85C;&#xADF8;&#xB798;&#xBC0D; &#xC8FC;&#xC81C;</a>&#xB97C;
        &#xC77D;&#xC5B4;&#xBCF4;&#xC138;&#xC694;.</td>
    </tr>
    <tr>
      <td style="text-align:left">&#xBE44;&#xB3D9;&#xAE30; &#xD568;&#xC218;</td>
      <td style="text-align:left">&#xC2DC;&#xC2A4;&#xD15C; &#xC778;&#xD130;&#xD398;&#xC774;&#xC2A4;&#xC5D0;&#xB294;
        &#xC790;&#xB3D9;&#xC801;&#xC73C;&#xB85C; &#xB3D9;&#xC2DC;&#xC131;&#xC744;
        &#xC81C;&#xACF5;&#xD558;&#xB294; &#xB9CE;&#xC740; &#xBE44;&#xB3D9;&#xAE30;
        &#xD568;&#xC218;&#xB4E4;&#xC774; &#xC788;&#xC2B5;&#xB2C8;&#xB2E4;. &#xC774;
        API&#xB4E4;&#xC740; &#xC791;&#xC5C5;&#xC744; &#xC218;&#xD589;&#xD558;&#xACE0;
        &#xACB0;&#xACFC;&#xAC12;&#xC744; &#xBC18;&#xD658;&#xD558;&#xAE30; &#xC704;&#xD574;&#xC11C;
        &#xC2DC;&#xC2A4;&#xD15C; &#xB370;&#xBAAC;&#xC774;&#xB098; &#xD504;&#xB85C;&#xC138;&#xC2A4;&#xB97C;
        &#xC0AC;&#xC6A9;&#xD558;&#xACE0; &#xCEE4;&#xC2A4;&#xD140; &#xC2A4;&#xB808;&#xB4DC;&#xB97C;
        &#xC0DD;&#xC131;&#xD569;&#xB2C8;&#xB2E4;. (&#xC2E4;&#xC81C; &#xAD6C;&#xD604;&#xC740;
        &#xC5EC;&#xB7EC;&#xBD84;&#xC758; &#xCF54;&#xB4DC;&#xC640; &#xBCC4;&#xB3C4;&#xB85C;
        &#xBD84;&#xB9AC;&#xB418;&#xC5B4; &#xC788;&#xAE30; &#xB54C;&#xBB38;&#xC5D0;
        &#xC804;&#xD600; &#xC0C1;&#xAD00;&#xC774; &#xC5C6;&#xC2B5;&#xB2C8;&#xB2E4;.)
        &#xC751;&#xC6A9; &#xD504;&#xB85C;&#xADF8;&#xB7A8;&#xC744; &#xB514;&#xC790;&#xC778;
        &#xD560;&#xB54C; &#xBE44;&#xB3D9;&#xAE30; &#xB3D9;&#xC791;&#xC744; &#xC81C;&#xACF5;&#xD558;&#xB294;
        &#xD568;&#xC218;&#xB97C; &#xCC3E;&#xC544;&#xC11C; &#xC0AC;&#xC6A9;&#xC790;
        &#xC815;&#xC758; &#xC2A4;&#xB808;&#xB4DC;&#xC5D0;&#xC11C; &#xB3D9;&#xAE30;&#xC801;&#xC778;
        &#xD568;&#xC218; &#xB300;&#xC2E0;&#xC5D0; &#xC0AC;&#xC6A9;&#xD558;&#xB294;
        &#xAC83;&#xC774; &#xC88B;&#xC2B5;&#xB2C8;&#xB2E4;.</td>
    </tr>
    <tr>
      <td style="text-align:left">&#xD0C0;&#xC774;&#xBA38;</td>
      <td style="text-align:left">&#xC2A4;&#xB808;&#xB4DC;&#xB97C; &#xC0DD;&#xC131;&#xD558;&#xAE30;&#xC5D0;&#xB294;
        &#xB108;&#xBB34; &#xC0AC;&#xC18C;&#xD558;&#xC9C0;&#xB9CC; &#xADF8;&#xB798;&#xB3C4;
        &#xC815;&#xAE30;&#xC801;&#xC778; &#xC2DC;&#xAC04; &#xAC04;&#xACA9;&#xC73C;&#xB85C;
        &#xD544;&#xC694;&#xD55C; &#xC791;&#xC5C5;&#xC744; &#xC218;&#xD589;&#xD560;
        &#xB54C;&#xC5D0;&#xB294; &#xC751;&#xC6A9; &#xD504;&#xB85C;&#xADF8;&#xB7A8;&#xC758;
        main &#xC2A4;&#xB808;&#xB4DC;&#xC5D0;&#xC11C; &#xD0C0;&#xC774;&#xBA38;&#xB97C;
        &#xC0AC;&#xC6A9;&#xD558;&#xB294; &#xAC83;&#xC774; &#xC88B;&#xC2B5;&#xB2C8;&#xB2E4;.
        &#xD0C0;&#xC774;&#xBA38;&#xC5D0; &#xB300;&#xD55C; &#xC790;&#xC138;&#xD55C;
        &#xB0B4;&#xC6A9;&#xC740; <a href="https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/Multithreading/RunLoopManagement/RunLoopManagement.html#//apple_ref/doc/uid/10000057i-CH16-SW21">Timer Sources</a>&#xB97C;
        &#xC77D;&#xC5B4;&#xBCF4;&#xC138;&#xC694;.</td>
    </tr>
    <tr>
      <td style="text-align:left">&#xBCC4;&#xB3C4; &#xD504;&#xB85C;&#xC138;&#xC2A4;</td>
      <td style="text-align:left">&#xC2A4;&#xB808;&#xB4DC;&#xBCF4;&#xB2E4; &#xB354; &#xBB34;&#xAC70;&#xC6B4;
        &#xBC29;&#xBC95;&#xC774;&#xC9C0;&#xB9CC; &#xC791;&#xC5C5;&#xACFC; &#xC560;&#xD50C;&#xB9AC;&#xCF00;&#xC774;&#xC158;&#xC758;
        &#xAD00;&#xB828;&#xC774; &#xC801;&#xC740; &#xACBD;&#xC6B0; &#xBCC4;&#xB3C4;&#xC758;
        &#xD504;&#xB85C;&#xC138;&#xC2A4;&#xB97C; &#xC0DD;&#xC131;&#xD558;&#xB294;
        &#xAC83;&#xC774; &#xB354; &#xC720;&#xC6A9;&#xD560; &#xC218; &#xC788;&#xC2B5;&#xB2C8;&#xB2E4;.
        &#xC791;&#xC5C5;&#xC774; &#xC0C1;&#xB2F9;&#xD55C; &#xC591;&#xC758; &#xBA54;&#xBAA8;&#xB9AC;&#xB97C;
        &#xD544;&#xC694;&#xB85C; &#xD558;&#xAC70;&#xB098; &#xB8E8;&#xD2B8; &#xAD8C;&#xD55C;&#xC73C;&#xB85C;
        &#xC2E4;&#xD589;&#xB418;&#xC5B4;&#xC57C; &#xD560; &#xB54C;&#xC5D0;&#xB294;
        &#xD504;&#xB85C;&#xC138;&#xC2A4;&#xB97C; &#xC0AC;&#xC6A9;&#xD558;&#xB294;&#xAC83;&#xC774;
        &#xC88B;&#xC2B5;&#xB2C8;&#xB2E4;. &#xC608;&#xB97C; &#xB4E4;&#xC5B4; 64&#xBE44;&#xD2B8;
        &#xC11C;&#xBC84; &#xD504;&#xB85C;&#xC138;&#xC2A4;&#xB97C; &#xC0AC;&#xC6A9;&#xD574;&#xC11C;
        &#xB300;&#xC6A9;&#xB7C9;&#xC758; &#xB370;&#xC774;&#xD130; &#xC14B;&#xC744;
        &#xACC4;&#xC0B0;&#xD558;&#xACE0; 32&#xBE44;&#xD2B8; &#xC5B4;&#xD50C;&#xB9AC;&#xCF00;&#xC774;&#xC158;&#xC5D0;&#xC11C;
        &#xC0AC;&#xC6A9;&#xC790;&#xC5D0;&#xAC8C; &#xACB0;&#xACFC;&#xAC12;&#xC744;
        &#xBCF4;&#xC5EC;&#xC8FC;&#xB294; &#xAC83;&#xC774; &#xAC00;&#xB2A5;&#xD569;&#xB2C8;&#xB2E4;.</td>
    </tr>
  </tbody>
</table>{% hint style="warning" %}
Warning

fork 함수를 사용하여 별도 프로세스를 실행할 때에는 반드시 exec 또는 유사한 함수를 뒤이어 실행해야 합니다. Core Foundation, Cocoa 또는 Core Data 프레임워크에 의존적인 어플리케이션은 곧바로 exec와 같은 함수들을 실행하지 않으면 올바르지 않게 동작할 수 있습니다.
{% endhint %}

## 스레딩 지원 <a id="threading-support"></a>

OS X과 iOS에서는 애플리케이션에 스레드를 생성하는 몇가지 기술을 제공함으로써 코드에 스레드를 적용시킬 수 있도록 돕고 있습니다. 또한 두 시스템 모두 스레드 내 작업의 동기화 및 관리를 지원합니다. 다음 섹션부터는 OS X과 iOS의 스레드 작업시 알아두어야 할 몇가지 핵심 기술에 대해서 설명하도록 하겠습니다.

### 스레딩 패키지 <a id="threading-packages"></a>

스레드의 기본 구현 매커니즘은 Mach 스레드지만 Mach 레벨에서 스레드를 사용할 일은 거의 없습니다. 대부분의 경우에는 더 편리한 POSIX API나 그 파생 기술을 사용하게 됩니다. Mach 구현은 스레드들을 서로 독립적으로 스케줄링하는 기능과, 선제적 실행 기능을 포함하여 모든 스레드의 기본 기능을 제공합니다.

표 1-2는 애플리케이션에서 사용가능한 스레딩 기술을 설명합니다.

**표 1-2** 스레드 기술들

| 기술 | 설명 |
| :--- | :--- |
| Cocoa threads | 코코아는 [NSThread](../../etc/not-found.md) 클래스를 사용하여 스레드를 구현하며, 또한 [NSObject](../../etc/not-found.md)를 통해 새로운 스레드를 생성하고 이미 실행중인 스레드의 코드를 실행하는 메서드를 제공합니다. 더 자세한 내용은 [NSThread 사용](https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/Multithreading/CreatingThreads/CreatingThreads.html#//apple_ref/doc/uid/10000057i-CH15-SW11)과 [NSObject로 스레드 생성하기](https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/Multithreading/CreatingThreads/CreatingThreads.html#//apple_ref/doc/uid/10000057i-CH15-SW13)를 참조하세요 |
| POSIX threads | POSIX threads 기술은 스레드를 생성하기 위해서 C 기반 인터페이스를 제공합니다. 작성중인 코드가 코코아 애플리케이션이 아니라면 스레드를 생성하기 위한 최선의 선택이 될 수 있습니다. POSIX 인터페이스는 상대적으로 사용하기 쉬우며 스레드를 설정하는데 있어 충분한 유연성을 제공합니다. 더 자세한 내용은 [POSIX 스레드 사용](https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/Multithreading/CreatingThreads/CreatingThreads.html#//apple_ref/doc/uid/10000057i-CH15-SW12)을 참조하세요. |
| Multiprocessing Service | Multiprocessing Service는 이전 버전의 Mac OS 애플리케이션에서 사용되는 레거시 C 기반 인터페이스입니다. 이 기술은 OS X에서만 사용가능하고 새로 개발시에는 지양되어야 합니다. 대신에 NSThread 클래스나 POSIX threads를 사용할 것을 권장합니다. 이 기술에 대한 더 자세한 내용은 [Multiprocessing Services 프로그래밍 가이드](https://developer.apple.com/library/archive/documentation/Carbon/Conceptual/Multitasking_MultiproServ/01introduction/introduction.html#//apple_ref/doc/uid/TP40000853)를 참조하세요. |



애플리케이션 수준에서 모든 스레드는 본질적으로 다른 플랫폼과 동일한 방식으로 동작합니다. 스레드는 시작한 이후 실행, 준비, 블록 세가지 주요한 상태 중 하나로 작동합니다. 스레드가 실행중이 아니라면 입력을 기다리는 블록 상태이거나, 아직 스케줄링되지 않은 준비 상태일 것입니다. 스레드는 이 상태들간의 전환을 계속하다가 결국에는 중단 상태로 전환하여 종료됩니다.

새 스레드를 만들 때에는 반드시 스레드의 진입 함수\(코코아 스레드의 경우에는 진입 메서드\)를 지정해야 합니다. 진입 함수는 스레드에서 실행할 코드를 구성하는 역할을 합니다. 함수가 리턴을하거나 스레드를 명시적으로 종료하면 스레드가 영구히 정지되고 시스템에서 회수됩니다. 스레드를 생성하는 것은 메모리 및 시간 면에서 비싸기 때문에 진입 함수는 충분히 많은 양의 작업을 실행시키거나 반복작업을 위한 런 루프를 설정할 때 사용하는 것을 권장합니다.

사용가능한 스레딩 기술들에 대한 더 자세한 정보는 [Thread 관리 문서](https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/Multithreading/CreatingThreads/CreatingThreads.html#//apple_ref/doc/uid/10000057i-CH15-SW2)를 확인하세요

### 런 루프 <a id="run-loop"></a>

런 루프란 스레드 상에 비동기적으로 전달되는 이벤트를 관리하는데 사용되는 하나의 작은 인프라입니다. 런 루프는 하나 이상의 이벤트 소스를 관찰하는 일을 합니다. 이벤트가 도착하면 시스템은 스레드를 깨워 런 루프에 이벤트를 보내고 런 루프는 사용자가 지정한 핸들러에 이벤트를 전달합니다. 전달할 이벤트가 없고 처리할 준비가 되었다면 런 루프는 스레드를 슬립시킵니다.

런 루프를 사용하기 위해서 반드시 스레드를 생성할 필요는 없지만 그렇게 하면 사용자에게 더 나은 경험을 제공할 수 있습니다. 런 루프는 적은 자원으로도 스레드를 오랫동안 살려놓을 수 있습니다. 런 루프는 스레드가 할 일이 없을때 슬립시키기 때문에 CPU 사이클을 낭비하는 폴링Polling을 방지하고 프로세서가 자체적으로 절전모드에 들어가는 것을 막습니다.

런 루프를 설정하기 위해서는 스레드를 실행하고, 런 루프 객체의 참조를 얻어낸 다음, 이벤트 핸들러를 지정하고 런 루프에 실행을 명령하면 됩니다. OS X에서 제공하는 인프라는 메인 스레드의 런 루프를 자동으로 처리합니다. 그러나 장시간 유지되는 부 스레드를 생성하고자 한다면 해당 스레드에 런 루프를 직접 설정해야 합니다.

런 루프에 대한 상세 내용 및 사용 예제에 대한 내용은 [Run Loops](https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/Multithreading/RunLoopManagement/RunLoopManagement.html#//apple_ref/doc/uid/10000057i-CH16-SW1)를 참조하세요.

### 동기화 도구 <a id="synchronization-tools"></a>

스레드 프로그래밍의 위험 중 하나는 여러 스레드 간에 발생하는 리소스 경쟁입니다. 여러개의 스레드가 동시에 같은 자원을 사용 또는 수정하고자 하는 경우 문제가 발생할 수 있습니다. 이 문제를 해소하는 한가지 방법으로써 공유되는 리소스를 제거하고 각 스레드마다 고유한 리소스 집합을 갖도록 하는 것입니다. 완전히 별개의 리소스를 유지하는 것이 불가능한 상황이라면 잠금lock, 조건condition, 원자적atomic 연산 및 기타 기술을 사용하여 리소스에 대한 접근을 동기화하는 것이 좋습니다.

Lock은 한번에 하나의 스레드만 실행 가능한 코드에 대해 brute force 형태의 보호를 제공합니다. 가장 일반적인 타입의 lock은 Mutex라고도 알려지는 상호 배제 잠금Mutual exclusion lock입니다. 스레드가 현재 다른 스레드가 보유한 mutex를 획득하려고 하면 다른 스레드가 잠금을 해제할 때까지 해당 스레드를 블록시킵니다. 여러 시스템 프레임워크들이 동일한 기술에 기반한 mutex lock을 제공합니다. 또한 코코아는 다양한 유형의 mutex lock을 제공하여 재귀와 같은 여러 종류의 동작을 지원합니다. 사용가능한 lock 타입에 대한 더 자세한 정보는 [Locks](https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/Multithreading/ThreadSafety/ThreadSafety.html#//apple_ref/doc/uid/10000057i-CH8-126320)를 참조하세요.

시스템은 Lock 뿐만 아니라 조건에 따라 작업의 순서를 보장하는 기능 또한 지원합니다. Condition은 문지기와 같이 동작하여 조건이 참이 될 때까지 주어진 스레드를 블록시킵니다. 조건이 충족되면 Condition은 해당 스레드를 풀어주고 실행이 계속될 수 있도록 합니다. POSIX 레이어와 파운데이션 프레임워크 모두 조건 기능을 직접적으로 지원합니다. \(만약 operation 객체를 객체 간의 의존성을 설정하여 Condition과 매우 흡사한 동작을 할 수 있습니다.\)

Lock과 Condition은 아주 일반적인 동시성 디자인 방법이지만 atomic 연산은 다른 방법으로 데이터에 대한 접근을 보호하고 동기화합니다. atomic 연산은 스칼라 데이터를 산술/논리 연산할 때 경량의 lock을 대안적으로 제공합니다. 또한 atomic 연산은 아주 특별한 하드웨어 명령어를 사용하여 다른 스레드가 접근하기 전에 변수에 대한 수정이 완료되었는지 확인합니다.

사용가능한 동기화 도구에 대한 자세한 설명은 [동기화 도구들](../../etc/not-found.md) 문서를 참조하세요.

### 스레드 간 통신 <a id="inter-thread-communication"></a>

좋은 디자인이란 통신을 최소화하는 것이긴 하지만 어느 시점엔가는 스레드 간 통신이 필요해지는 때가 옵니다. \(스레드가 하는 일은 어플리케이션의 작업을 처리해 주는 것인데 결과값이 전혀 쓰이질 않는다면 무슨 소용이 있을까요?\) 스레드는 새로운 작업 요청을 처리하거나 작업 진행상황을 애플리케이션의 메인 스레드에 보고해야 할 때가 있습니다. 이 경우 정보를 한 스레드에서 다른 스레드로 전달할 방법이 필요합니다. 다행히도 스레드들은 같은 프로세스 공간을 공유하기 때문에 통신을 위한 옵션은 아주 많이 존재합니다.

스레드 간의 통신 방법은 많이 있지만 각 방법마다 장단점은 있습니다. Configuring Thread-Local Storage는 OS X에서 사용할 수 있는 가장 일반적인 통신 커니즘을 나열하고 있습니다. \(Message queues와 Cocoa distributed objects는 예외입니다. 이 기술들은 iOS에서도 사용가능합니다.\) 다음 표에서는 이러한 기술들을 기술 복잡도 순서대로 설명합니다.

**표 1-3** 통신 매커니즘

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#xCEE4;&#xB2C8;&#xC998;</th>
      <th style="text-align:left">&#xC124;&#xBA85;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Direct messaging</td>
      <td style="text-align:left">&#xCF54;&#xCF54;&#xC544; &#xC560;&#xD50C;&#xB9AC;&#xCF00;&#xC774;&#xC158;&#xC740;
        &#xC140;&#xB809;&#xD130;&#xB97C; &#xB2E4;&#xB978; &#xC2A4;&#xB808;&#xB4DC;&#xC5D0;&#xC11C;
        &#xC2E4;&#xD589;&#xC2DC;&#xD0AC; &#xC218; &#xC788;&#xB294; &#xAE30;&#xB2A5;&#xC744;
        &#xAC00;&#xC9C0;&#xACE0; &#xC788;&#xC2B5;&#xB2C8;&#xB2E4;. &#xC774; &#xAE30;&#xB2A5;&#xC740;
        &#xD55C; &#xC2A4;&#xB808;&#xB4DC;&#xAC00; &#xB2E4;&#xB978; &#xC2A4;&#xB808;&#xB4DC;&#xC5D0;&#xC11C;
        &#xBA54;&#xC11C;&#xB4DC;&#xB97C; &#xC2E4;&#xD589;&#xD560; &#xC218; &#xC788;&#xC74C;&#xC744;
        &#xC758;&#xBBF8;&#xD569;&#xB2C8;&#xB2E4;. &#xC774; &#xBA54;&#xC11C;&#xB4DC;&#xB4E4;&#xC740;
        &#xD0C0;&#xAC9F; &#xC2A4;&#xB808;&#xB4DC;&#xC758; &#xCEE8;&#xD14D;&#xC2A4;&#xD2B8;
        &#xB0B4;&#xC5D0;&#xC11C; &#xC2E4;&#xD589;&#xB418;&#xAE30; &#xB54C;&#xBB38;&#xC5D0;
        &#xC774;&#xB807;&#xAC8C; &#xC804;&#xC1A1;&#xB41C; &#xBA54;&#xC138;&#xC9C0;&#xB294;
        &#xADF8; &#xC2A4;&#xB808;&#xB4DC;&#xC5D0; &#xC790;&#xB3D9;&#xC73C;&#xB85C;
        serialize &#xB429;&#xB2C8;&#xB2E4;. &#xC785;&#xB825; &#xC18C;&#xC2A4;&#xC5D0;
        &#xB300;&#xD55C; &#xB354; &#xC790;&#xC138;&#xD55C; &#xB0B4;&#xC6A9;&#xC740;
        <a
        href="https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/Multithreading/RunLoopManagement/RunLoopManagement.html#//apple_ref/doc/uid/10000057i-CH16-SW44">Cocoa Perform Selector Sources</a>&#xB97C; &#xCC38;&#xC870;&#xD558;&#xC138;&#xC694;.</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>Global variables,</p>
        <p>shared memory,</p>
        <p>and objects</p>
      </td>
      <td style="text-align:left">&#xC2A4;&#xB808;&#xB4DC; &#xAC04;&#xC5D0; &#xD1B5;&#xC2E0;&#xD560; &#xC218;
        &#xC788;&#xB294; &#xB2E4;&#xB978; &#xAC04;&#xB2E8;&#xD55C; &#xBC29;&#xBC95;&#xC73C;&#xB85C;&#xB294;
        &#xC804;&#xC5ED;&#xBCC0;&#xC218;&#xB098; &#xACF5;&#xC720;&#xAC1D;&#xCCB4;,
        &#xB610;&#xB294; &#xACF5;&#xC720; &#xBA54;&#xBAA8;&#xB9AC; &#xBE14;&#xB85D;&#xC744;
        &#xC0AC;&#xC6A9;&#xD558;&#xB294; &#xAC83;&#xC785;&#xB2C8;&#xB2E4;. &#xACF5;&#xC720;
        &#xBCC0;&#xC218;&#xB294; &#xBE60;&#xB974;&#xACE0; &#xAC04;&#xB2E8;&#xD55C;
        &#xBC29;&#xBC95;&#xC774;&#xC9C0;&#xB9CC; &#xB2E4;&#xC774;&#xB809;&#xD2B8;
        &#xBA54;&#xC138;&#xC9C0;&#xC5D0; &#xBE44;&#xD574;&#xC11C; &#xAE68;&#xC9C0;&#xAE30;
        &#xC27D;&#xC2B5;&#xB2C8;&#xB2E4;. &#xACF5;&#xC720; &#xBCC0;&#xC218;&#xB294;
        &#xCF54;&#xB4DC;&#xC758; &#xC815;&#xD655;&#xC131;&#xC744; &#xBCF4;&#xC7A5;&#xD558;&#xAE30;
        &#xC704;&#xD574; lock&#xC774;&#xB098; &#xB2E4;&#xB978; &#xB3D9;&#xAE30;&#xD654;
        &#xBA54;&#xCEE4;&#xB2C8;&#xC998;&#xC744; &#xD1B5;&#xD574;&#xC11C; &#xC870;&#xC2EC;&#xC2A4;&#xB7FD;&#xAC8C;
        &#xBCF4;&#xD638;&#xB418;&#xC5B4;&#xC57C; &#xD569;&#xB2C8;&#xB2E4;. &#xC5EC;&#xAE30;&#xC5D0;
        &#xB300;&#xD55C; &#xC2E4;&#xD328;&#xB294; &#xACBD;&#xC7C1;&#xC0C1;&#xD0DC;,
        &#xB370;&#xC774;&#xD130; &#xC624;&#xC5FC; &#xB610;&#xB294; &#xD06C;&#xB798;&#xC2DC;&#xB85C;
        &#xC774;&#xC5B4;&#xC9D1;&#xB2C8;&#xB2E4;.</td>
    </tr>
    <tr>
      <td style="text-align:left">Conditions</td>
      <td style="text-align:left">Condition&#xC740; &#xC2A4;&#xB808;&#xB4DC;&#xAC00; &#xD2B9;&#xC815; &#xBD80;&#xBD84;&#xC758;
        &#xCF54;&#xB4DC;&#xB97C; &#xC2E4;&#xD589;&#xD560; &#xB54C; &#xC0AC;&#xC6A9;&#xD560;
        &#xC218; &#xC788;&#xB294; &#xB3D9;&#xAE30;&#xD654; &#xB3C4;&#xAD6C;&#xC785;&#xB2C8;&#xB2E4;.
        Condition&#xC740; &#xB9C8;&#xCE58; &#xBB38;&#xC9C0;&#xAE30;&#xCC98;&#xB7FC;
        &#xC870;&#xAC74;&#xC774; &#xB9CC;&#xC871;&#xB420; &#xB54C;&#xC5D0;&#xB9CC;
        &#xC2A4;&#xB808;&#xB4DC;&#xAC00; &#xC2E4;&#xD589;&#xB420; &#xC218; &#xC788;&#xB3C4;&#xB85D;
        &#xD569;&#xB2C8;&#xB2E4;. condition&#xC744; &#xC0AC;&#xC6A9;&#xD558;&#xB294;
        &#xBC29;&#xBC95;&#xC5D0; &#xB300;&#xD574;&#xC11C;&#xB294; <a href="https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/Multithreading/ThreadSafety/ThreadSafety.html#//apple_ref/doc/uid/10000057i-CH8-SW4">Using Conditions</a>&#xB97C;
        &#xCC38;&#xC870;&#xD558;&#xC138;&#xC694;</td>
    </tr>
    <tr>
      <td style="text-align:left">Run loop sources</td>
      <td style="text-align:left">&#xCEE4;&#xC2A4;&#xD140; &#xB7F0; &#xB8E8;&#xD504; &#xC18C;&#xC2A4;&#xB294;
        &#xC2A4;&#xB808;&#xB4DC;&#xC5D0;&#xC11C; &#xC560;&#xD50C;&#xB9AC;&#xCF00;&#xC774;&#xC158;
        &#xC9C0;&#xC815; &#xBA54;&#xC138;&#xC9C0;&#xB97C; &#xC218;&#xC2E0;&#xD558;&#xB3C4;&#xB85D;
        &#xC124;&#xC815;&#xB429;&#xB2C8;&#xB2E4;. &#xB7F0; &#xB8E8;&#xD504; &#xC18C;&#xC2A4;&#xB294;
        &#xC774;&#xBCA4;&#xD2B8; &#xC8FC;&#xB3C4;&#xC801;&#xC73C;&#xB85C; &#xB3D9;&#xC791;&#xD558;&#xAE30;
        &#xB54C;&#xBB38;&#xC5D0; &#xD574;&#xC57C; &#xD560; &#xC791;&#xC5C5;&#xC774;
        &#xC5C6;&#xB2E4;&#xBA74; &#xC790;&#xB3D9;&#xC801;&#xC73C;&#xB85C; &#xC2A4;&#xB808;&#xB4DC;&#xB97C;
        &#xC2AC;&#xB9BD;&#xC2DC;&#xD0A4;&#xACE0; &#xC2A4;&#xB808;&#xB4DC;&#xC758;
        &#xD6A8;&#xC728;&#xC131;&#xC744; &#xD5A5;&#xC0C1;&#xC2DC;&#xD0B5;&#xB2C8;&#xB2E4;.
        &#xB7F0; &#xB8E8;&#xD504;&#xC640; &#xB7F0;&#xB8E8;&#xD504; &#xC18C;&#xC2A4;&#xC5D0;
        &#xB300;&#xD55C; &#xB0B4;&#xC6A9;&#xC740; <a href="https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/Multithreading/RunLoopManagement/RunLoopManagement.html#//apple_ref/doc/uid/10000057i-CH16-SW1">Run Loops</a>&#xB97C;
        &#xC77D;&#xC5B4;&#xBCF4;&#xC138;&#xC694;.</td>
    </tr>
    <tr>
      <td style="text-align:left">Ports and sockets</td>
      <td style="text-align:left">&#xD3EC;&#xD2B8; &#xAE30;&#xBC18; &#xD1B5;&#xC2E0;&#xC740; &#xC2A4;&#xB808;&#xB4DC;
        &#xAC04; &#xD1B5;&#xC2E0;&#xC744; &#xD558;&#xB294; &#xB354; &#xBCF5;&#xC7A1;&#xD558;&#xC9C0;&#xB9CC;
        &#xC544;&#xC8FC; &#xC2E0;&#xB8B0;&#xC131; &#xB192;&#xC740; &#xAE30;&#xC220;&#xC785;&#xB2C8;&#xB2E4;.
        &#xB354; &#xC911;&#xC694;&#xD55C; &#xAC83;&#xC740; &#xD3EC;&#xD2B8;&#xC640;
        &#xC18C;&#xCF13;&#xC740; &#xB2E4;&#xB978; &#xD504;&#xB85C;&#xC138;&#xC2A4;&#xB098;
        &#xC11C;&#xBE44;&#xC2A4;&#xC640; &#xAC19;&#xC740; &#xC678;&#xBD80; &#xAC1C;&#xCCB4;&#xC640;&#xB3C4;
        &#xD1B5;&#xC2E0;&#xD558;&#xB294; &#xAC83;&#xC774; &#xAC00;&#xB2A5;&#xD569;&#xB2C8;&#xB2E4;.
        &#xD6A8;&#xC728;&#xC131;&#xC744; &#xC704;&#xD574;&#xC11C; &#xD3EC;&#xD2B8;&#xB294;
        &#xB7F0; &#xB8E8;&#xD504; &#xC18C;&#xC2A4;&#xB97C; &#xC0AC;&#xC6A9;&#xD558;&#xC5EC;
        &#xAD6C;&#xD604;&#xB429;&#xB2C8;&#xB2E4;. &#xB530;&#xB77C;&#xC11C; &#xD3EC;&#xD2B8;&#xAC00;
        &#xAE30;&#xB2E4;&#xB9AC;&#xB294; &#xB370;&#xC774;&#xD130;&#xAC00; &#xC5C6;&#xB2E4;&#xBA74;
        &#xD574;&#xB2F9; &#xC2A4;&#xB808;&#xB4DC;&#xB294; &#xC2AC;&#xB9BD;&#xC73C;&#xB85C;
        &#xC804;&#xD658;&#xB429;&#xB2C8;&#xB2E4;. &#xB7F0; &#xB8E8;&#xD504;&#xC640;
        &#xD3EC;&#xD2B8; &#xAE30;&#xBC18; &#xC785;&#xB825; &#xC18C;&#xC2A4;&#xC5D0;
        &#xB300;&#xD574;&#xC11C;&#xB294; <a href="https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/Multithreading/RunLoopManagement/RunLoopManagement.html#//apple_ref/doc/uid/10000057i-CH16-SW1">Run Loops</a>&#xB97C;
        &#xC77D;&#xC5B4;&#xBCF4;&#xC138;&#xC694;.</td>
    </tr>
    <tr>
      <td style="text-align:left">Message queues</td>
      <td style="text-align:left">&#xB808;&#xAC70;&#xC2DC; &#xBA40;&#xD2F0; &#xD504;&#xB85C;&#xC138;&#xC2F1;
        &#xC11C;&#xBE44;&#xC2A4;&#xB294; &#xB4E4;&#xC5B4;&#xC624;&#xACE0; &#xB098;&#xAC00;&#xB294;
        &#xB370;&#xC774;&#xD130;&#xB97C; &#xAD00;&#xB9AC;&#xD558;&#xB294; first-in,
        first-out (FIFO) &#xCD94;&#xC0C1; &#xD050;&#xC785;&#xB2C8;&#xB2E4;. &#xBA54;&#xC138;&#xC9C0;
        &#xD050;&#xB294; &#xAC04;&#xB2E8;&#xD558;&#xACE0; &#xD3B8;&#xB9AC;&#xD558;&#xC9C0;&#xB9CC;
        &#xB2E4;&#xB978; &#xD1B5;&#xC2E0; &#xAE30;&#xC220;&#xCC98;&#xB7FC; &#xD6A8;&#xC728;&#xC801;&#xC774;&#xC9C0;&#xB294;
        &#xC54A;&#xC2B5;&#xB2C8;&#xB2E4;. &#xBA54;&#xC138;&#xC9C0; &#xD050;&#xC5D0;
        &#xB300;&#xD55C; &#xB354; &#xC790;&#xC138;&#xD55C; &#xB0B4;&#xC6A9;&#xC740;
        <a
        href="https://developer.apple.com/library/archive/documentation/Carbon/Conceptual/Multitasking_MultiproServ/01introduction/introduction.html#//apple_ref/doc/uid/TP40000853">Multiprocessing Services &#xD504;&#xB85C;&#xADF8;&#xB798;&#xBC0D; &#xAC00;&#xC774;&#xB4DC;</a>&#xB97C;
          &#xCC38;&#xC870;&#xD558;&#xC138;&#xC694;.</td>
    </tr>
    <tr>
      <td style="text-align:left">Cocoa distributed objects</td>
      <td style="text-align:left">Distributed objects&#xB294; &#xD3EC;&#xD2B8;&#xAE30;&#xBC18; &#xD1B5;&#xC2E0;&#xC758;
        &#xACE0;&#xAE09; &#xAD6C;&#xD604;&#xC744; &#xC81C;&#xACF5;&#xD558;&#xB294;
        &#xCF54;&#xCF54;&#xC544; &#xAE30;&#xC220;&#xC785;&#xB2C8;&#xB2E4;. &#xC774;
        &#xAE30;&#xC220;&#xC744; &#xC0AC;&#xC6A9;&#xD558;&#xBA74; &#xC2A4;&#xB808;&#xB4DC;&#xAC04;
        &#xD1B5;&#xC2E0;&#xC774; &#xAC00;&#xB2A5;&#xD558;&#xAE34; &#xD558;&#xC9C0;&#xB9CC;
        &#xC0C1;&#xB2F9;&#xD55C; &#xC624;&#xBC84;&#xD5E4;&#xB4DC;&#xAC00; &#xBC1C;&#xC0DD;&#xD558;&#xAE30;
        &#xB54C;&#xBB38;&#xC5D0; &#xC9C0;&#xC591;&#xD558;&#xB294; &#xAC83;&#xC744;
        &#xAD8C;&#xC7A5;&#xD569;&#xB2C8;&#xB2E4;. &#xD504;&#xB85C;&#xC138;&#xC2A4;
        &#xAC04;&#xC758; &#xD1B5;&#xC2E0;&#xC740; &#xC774;&#xBBF8; &#xC0C1;&#xB2F9;&#xD55C;
        &#xC624;&#xBC84;&#xD5E4;&#xB4DC;&#xB97C; &#xD544;&#xC694;&#xB85C; &#xD558;&#xB294;
        &#xC791;&#xC5C5;&#xC73C;&#xB85C;&#xC368; Distributed objects&#xB294; &#xC5EC;&#xAE30;&#xC5D0;
        &#xD6E8;&#xC52C; &#xB354; &#xC801;&#xD569;&#xD569;&#xB2C8;&#xB2E4;. &#xB354;
        &#xC790;&#xC138;&#xD55C; &#xB0B4;&#xC6A9;&#xC740; <a href="https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/DistrObjects/DistrObjects.html#//apple_ref/doc/uid/10000102i">Distributed Objects Programming Topics</a>&#xB97C;
        &#xCC38;&#xC870;&#xD558;&#xC138;&#xC694;.</td>
    </tr>
  </tbody>
</table>

## 디자인 팁 <a id="design-tips"></a>

다음 섹션들은 코드의 정확성을 보장하면서 스레드를 구현하는 방법에 대한 가이드를 제공합니다. 몇몇 가이드 라인은 스레드된 코드들의 성능까지도 향상히킵니다. 다른 성능 향상 팁과 마찬가지로 코드를 변경하기 전, 변경 중, 변경 후에는 관련 성능 통계를 수집하세요.

### 명시적인 스레드 생성 피하기

스레드 생성 코드를 직접 작성하는 것은 지루하고 에러가 발생하기 쉬운 방법입니다. 가능하다면 피하세요. OS X과 iOS는 다른 API들을 통해 동시성을 암묵적으로 지원합니다. 스레드를 직접 생성하기보다는 비동기 API, GCD 또는 operation 객체를 사용하세요. 이 기술들은 여러분 대신 뒤에서 스레드 관련 작업들을 수행하며 올바르게 동작할 것을 보장합니다. 또한 GCD나 operation 객체와 같은 기술들은 현재 시스템 로드에 기반하여 활성화된 스레드의 갯수를 조정하기 때문에 직접 코드를 작성하는 것보다 훨씬 더 효율적입니다. GCD와 operation 객체에 대한 더 자세한 내용은 [동시성 프로그래밍 가이드](https://developer.apple.com/library/archive/documentation/General/Conceptual/ConcurrencyProgrammingGuide/Introduction/Introduction.html#//apple_ref/doc/uid/TP40008091)를 참조하세요.

### 스레드를 계속 활용할 것

스레드를 직접 생성하고 관리하기로 결정했다면 스레드는 귀중한 시스템 자원을 소모한다는 사실을 잊지 마세요. 스레드에 할당된 모든 작업이 합리적인 방식으로 장시간, 생산성을 유지하도록 최선을 다해야 합니다. 그러는 동시에 대부분의 시간을 아이들 상태로 소비하는 스레드를 종료시키는 것을 두려워하지 마세요. 스레드는 무시할 수 없는 양의 메모리를 사용하며 그 중의 일부는 램에 상주합니다.\(Wired memory\) 그러므로 아이들 스레드를 해제하는 것은 애플리케이션의 메모리 사용량 줄일 뿐만 아니라 다른 시스템 프로세스들이 사용할 수 있는 더 많은 물리적 메모리를 확보하게 됩니다.

{% hint style="info" %}
Important

아이들 스레드를 종료하기 전에 항상 현재 애플리케이션의 기본 측정 세트를 기록해야 합니다. 변경을 시도한 후에는 추가적인 측정을 함으로써 실질적으로 성능이 향상되었는지 아니면 오히려 저하되었는지를 확인하세요.
{% endhint %}

### 공유 데이터 구조 피하기

스레드 관련 리소스 충돌을 회피하는 가장 간단하고 쉬운 방법은 프로그램의 각 스레드에 필요한 모든 데이터 복사본을 제공하는 것입니다. 병렬 코드는 스레드 간의 통신 및 리소스 경쟁을 최소화하는 최고의 방법입니다.

멀티 스레드 어플리케이션을 만드는 일은 어렵습니다. 아주 조심스럽게 코드상에서 적절한 시점의 모든 공유 데이터에 lock을 걸어도 의미론적으로 안전하지 않을 수 있습니다. 예를 들어 공유 데이터 구조가 특정 순서로 수정될 것을 기대한다면 문제가 발생할 수 있습니다. 보완을 위해 코드를 트랜잭션 기반 모델로 바꾸면 멀티 스레드를 생성하면서 생기는 성능상의 이점이 사라집니다. 애초에 리소스 경쟁을 제거하는 것이 단순하면서도 성능이 우수한 디자인이 되는 경우가 많습니다.

### 스레드와 유저 인터페이스

응용프로그램에 그래픽 유저 인터페이스\(GUI\)가 있다면 사용자 관련 인터페이스를 받거나 인터페이스 업데이트를 시작할 경우 메인스레드에서 처리하는 것을 권장합니다. 이러한 접근법은 유저 이벤트 처리와 window 컨텐츠를 그리는 작업에 연관된 동기화 이슈를 피하는데 도움이 됩니다. 코코아와 같은 몇몇 프레임워크들은 일반적으로 이러한 동작방식을 필요로 하지만 그렇지 않은 경우라고 하더라도 메인 스레드에서 이런 동작을 수행하는 것은 UI 관리 로직을 단순화 시켜준다는 장점이 있습니다.

다른 스레드에서 그래픽 작업을 수행하는 것이 장점이 되는 몇가지 주목할 만한 예외들이 있습니다. 예를 들어 보조 스레드를 이용하여 이미지를 생성, 처리하고 다른 이미지 관련 계산을 할 수 있습니다. 이런 작업을 할 때 보조 스레드를 사용하는 것은 굉장한 성능 향상을 가져다 줍니다. 그러나 확신이 서지 않는 그래픽 작업이라면 메인 스레드에서 수행하세요.

코코아 스레드 안전성에 대한 정보는 [Thread Safety Summary](https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/Multithreading/ThreadSafetySummary/ThreadSafetySummary.html#//apple_ref/doc/uid/10000057i-CH12-SW1)를, 코코아 drawing에 대해서는 [코코아 드로잉 가이드](https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/CocoaDrawingGuide/Introduction/Introduction.html#//apple_ref/doc/uid/TP40003290)를 참조하세요.

### 종료 시의 스레드 동작을 인지할 것

프로세스는 분리되지 않은 모든 스레드들이 종료될 때까지 계속해서 실행됩니다. 기본적으로 애플리케이션의 메인 스레드만이 분리되지 않은 상태로 생성되지만 다른 스레드들도 그렇게 만들 수 있습니다. 사용자가 애플리케이션을 종료할 때 분리된 모든 스레드들은 즉시 종료시키는 것이 적합한 동작으로 여겨집니다. 그것은 분리된 스레드에서 수행되는 작업은 필수 작업이 아닌 것으로 간주되기 때문입니다. 애플리케이션이 백그라운드 스레드를 사용해서 데이터를 디스크에 저장하거나 다른 중요한 작업을 한다면 분리되지 않은 스레드로 생성하여 애플리케이션이 종료될 때의 데이터 손실을 방지하세요.

\(joinable이라고도 하는\) 분리되지 않은 스레드를 만드려면 추가적인 작업이 필요합니다. 대부분의 고급 스레드 기술들은 기본으로 joinable 스레드를 생성하지 않기 때문에 POSIX API를 사용해서 스레드를 만들어야 합니다. 또한 애플리케이션의 메인 스레드에 코드를 추가하여 마지막으로 종료할때 분리되지 않은 스레드와 결합해야 합니다. joinable 스레드를 만드는 방법에 대한 자세한 정보는 [Setting the Detached State of a Thread](https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/Multithreading/CreatingThreads/CreatingThreads.html#//apple_ref/doc/uid/10000057i-CH15-SW3) 문서를 참고하세요.

코코아 애플리케이션을 만든다면 [applicationShouldTerminate:](https://developer.apple.com/documentation/appkit/nsapplicationdelegate/1428642-applicationshouldterminate) 델리게이트 메서드를 사용하여 애플리케이션의 종료를 미루거나 취소할 수 있습니다. 종료를 지연시키는 경우 애플리케이션은 중요한 스레드들이 작업을 끝날 때까지 기다렸다가 [replyToApplicationShouldTerminate:](https://developer.apple.com/documentation/appkit/nsapplication/1428594-reply) 메서드를 호출해야 합니다. 이들 메서드에 대한 자세한 내용은 [NSApplication Class Reference](https://developer.apple.com/documentation/appkit/nsapplication)를 읽어보세요.

### 예외 처리

예외 처리 메커니즘은 발생한 예외를 처리하기 위해서 현재 콜 스택에 의존합니다. 각 스레드는 자체적인 콜 스택을 가지고 있기 때문에 스레드에서 발생한 예외를 잡아내야\(catch\) 할 책임이 있습니다. 보조 스레드에서 예외를 잡지 못하면 메인 스레드에서 예외를 잡지 못했을 때와 마찬가지로 해당 스레드를 소유한 프로세스가 종료됩니다. 처리되지 않은 예외를 처리하기 위해서 다른 스레드에 던질 수는\(throw\) 없습니다.

{% hint style="info" %}
Note

코코아에서 NSException 객체는 일단 잡히면 다른 스레드로 전달될 수 있는 독립형 객체입니다.
{% endhint %}

 어떤 경우에는 예외 처리기가 자동으로 생성되기도 합니다. 예를 들어 Objective-C의 @synchronized 지시자에는 암묵적인 예외 처리기가 포함되어 있습니다.

### 스레드를 깔끔하게 종료할 것

스레드를 종료하는 가장 좋은 방법은 자연스럽게 메인 진입 루틴\(진입함수, 진입 메서드\)의 끝까지 도달하도록 하는 것입니다. 스레드를 즉시 종료시키는 함수들이 있지만 이런 함수들은 최후의 수단으로 사용해야 합니다. 자연스럽게 마지막 지점에 도달하기 전에 스레드를 종료하면 스레드가 자체적으로 정리되지 않습니다. 스레드가 메모리를 할당했거나 파일을 열었거나 다른 종류의 리소스를 획득한 경우 코드가 해당 리소스를 회수하지 못하여 메모리 누수나 다른 잠재적인 문제가 발생할 수 있습니다.

적절하게 스레드를 종료하는 방법에 대한 정보는 [Terminating a Thread](https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/Multithreading/CreatingThreads/CreatingThreads.html#//apple_ref/doc/uid/10000057i-CH15-SW10)에서 확인할 수 있습니다.

### 라이브러리의 스레드 안전성

애플리케이션 개발자는 멀티 스레드 실행 여부에 대한 결정권이 있지만 라이브러리 개발자는 그렇지 않습니다. 라이브러리를 개발할 때에는 해당 라이브러리를 호출하는 애플리케이션이 멀티스레드로 개발되었거나 아니면 언제든지 멀티스레드로 전환될 수 있다고 가정해야 합니다. 결론적으로 라이브러리를 개발할 때에는 항상 코드의 중요한 부분에 lock을 사용해야 합니다.

 라이브러리 개발자의 경우 애플리케이션이 멀티스레드가 될 때에만 lock을 생성하는 것은 현명하지 않습니다. 어느 시점에는 잠가야 할 필요가 있는 코드라면 그냥 라이브러리 초기에 lock 객체를 생성하도록 하세요. 초기화를 위해서 명시적으로 호출을 하는 것이 바람직합니다. lock을 만들기 위해 라이브러리 초기화를 위해 정적 함수를 사용할 수도 있겠지만 다른 방법이 없을 때만 하는 것이 좋습니다. 초기화 함수를 실행하면 라이브러리를 불러오는데 필요한 시간이 추가되고 성능을 저하시킬 수 있습니다.

{% hint style="info" %}
Note

라이브러리 내의 mutex 잠금과 잠금 해제 호출의 균형을 유지해야 합니다. 또한 스레드 안전한 환경을 제공하기 위해서는 코드 호에 의존하기 보다는 라이브러리 데이터 구조를 잠그는 것이 좋습니다.
{% endhint %}

코코아 라이브러리를 개발할 경우 [NSWillBecomeMultiThreadedNotification](https://developer.apple.com/documentation/foundation/nsnotification/name/1417567-nswillbecomemultithreaded)의 옵저버로 등록하여 애플리케이션이 멀티스레드가 될때 통지를 받을 수 있습니다. 그렇지만 이 노티피케이션은 라이브러리 코드가 호출되기 전에 발송될 수 있으므로 노티피케이션에만 의존해서는 안됩니다.

