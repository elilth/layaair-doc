#FlashDevelop 개발 환경 설정

###첫걸음: 레이어잉

####1.1 엔진 다운로드

LayaiairIDE 개발을 사용하면 LayairIDE 자체 엔진 가방을 다운로드합니다.개발자가 제3자 도구 개발을 사용하면 우선 엔진을 다운로드해야 한다.홈페이지나 개발자 중심 메뉴 중 엔진 다운로드 링크 입구를 갖고 링크 를 열 때 엔진 각 버전의 다운로드 목록이 나타납니다. 1개 버전마다 AS3, TS, JS 3가지 개발 언어를 제공합니다. 대응하는 개발언어가방을 선택하여 바로 다운로드 가능()[http://new.ldc.layabox.com/download/?type=layaair-LayaAir](http://new.ldc.layabox.com/download/?type=layaair-LayaAir)무엇

####1.2 엔진 가방 디렉터리 구조 소개

이 편 소개는 플래쉬드 블록이 개발 환경이기 때문에 AS3 버전의 엔진 가방을 다운로드합니다.다운로드 해압 후 AS3 버전의 디렉터리 구조가 아래와 같이 표시됩니다:

​![图片1.jpg](img/1.png)< br >>
그림 (1)

-'Layair Flash'디렉토리에는 플래쉬 버전이 나와야 필요한 엔진 라이브러리 코드.

-'libs'엔진 코드 디렉토리, Layaiair 엔진 라이브러리 코드 코드가 이 디렉터리에 처해 있는 src 카탈로그에 있습니다.

-'laya.js.exe'는 윈도우 시스템 아래 AS3 코드 디코딩을 JS 코드로 편집하는 데 사용됩니다.

-'LayaJSMac'는 애플MAC 시스템 아래 AS3 코드 디코딩을 JS 코드로 번역하는 데 사용된다.

-'playerglobal.swc'는 AS3 원생 편집기 SDK, 원생 API 문법 제시, 엔진 API 힌트 추가.

​



###2단계 설치 Google Chrome 브라우저

AS3 코드 컴파일을 실행한 후 기본값으로 Chrome 브라우저로 실행 프로젝트를 실행하려면 이 브라우저 설치 프로그램을 설치해야 합니다.설치된 것은 본 단계를 뛰어넘을 수 있습니다.



 



###3단계 플래쉬 Develop 속의 AS3 번역 환경

​**절차 1**FlashDevelop 열기 메뉴 표시줄에서 '매크로 편집' 패널 열기.

​![blob.png](img/2.png)< br >>
그림 (2)

​**절차 2**우선'더하기'를 클릭하고'오버 명령'을 추가한 다음'Label'을 선택하면'LayaCompiler'를 수정하는 메뉴 이름'Shortcut'에 매크로 메뉴 단축키를'Alt + F5'로 설정합니다.

​![blob.png](img/3.png)< br >>
그림 (3)

​**절차 3**"Entries" 란 표시줄의 오른쪽 위치에 "..." 동작 영역을 누르고 "문자열 집합 편집기" 창을 엽니다.

​![blob.png](img/4.png)< br >>
그림 (4)

​**순서**문자열 집합 패널에 매크로 명령을 입력하십시오:


```

SaveAllModified
RunProcessCaptured|D:\LayaBox\LayaAirAs3_1.5.5\as\laya.js.exe;"$(ProjectPath)";iflash=false;
```


​![blob.png](img/5.png)< br >>
그림 (5)

**Tips: “D:레이보이스Layayas3u1.5.5laya.js.exe’는 laya.js.exexexexe의 실제 경로가 되어야 합니다.******
****



​**단계 5**클릭: '매크로 명령을 완료한 후' 레이야아 JsCompiler '의 모든 설정을 완료하고' 닫기 '단추를 바로 누르면 됩니다.****
****

  



**이에 따라 프로젝트를 구성하기 전 Layair 엔진 다운로드, 브라우저 다운로드, FlashDevelop 환경 아래 AS3 편집기 설정이 끝났습니다.개발자는 다른 장절에서 계속 공부하는 것을 환영합니다.**

