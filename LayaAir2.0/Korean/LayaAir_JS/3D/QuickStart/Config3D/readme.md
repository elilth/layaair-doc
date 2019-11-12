#Config3D 소개

###### *version :2.2.0  Update:2019-8-24*

###Config3D 관련 소개

이 종류는 3D 초기화 설정을 만드는 데 사용된다

유네스코 데이터 유형
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
일렉트릭
1244사이드
124사 (하) 화보 (하) 를 설치하다
1244테네일 화포를 열어 모듈 버퍼
124471 ocreeCulling
일렉트로닉스 isize
1244트reeIntialCenter
1244트reeMinnodesize
12444터렉트 로즈니스 (Number) 사이클
1244사 다블러쉬 컬렉션

**시추 장르 디버깅 시 주의:**

팔차나무 재단하면 빨간색 픽셀을 사용하여 고층차 팔차나무 노드 포위상자를 그립니다.보기가 팔자나무 노드를 완전히 포함하면 팔자나무의 노드 함과 요정 포위함은 파란색으로 변한다.완전히 포함된 팔차나무의 노드 가 없는 픽셀선은 심도치에 따라 색을 계산한다.요정 포위함과 소속 팔차나무 노드 포위함 색깔이 일치하지만 팔차나무 노드 포위상자의 픽셀선은 반투명하다.

[] (img/1.png)<br>(그림 1)을 사용했습니다.

팔차나무 재단을 하지 않으면 녹색 픽셀 선으로 요정 포위상자를 그립니다.

[] (img/2.png)<br>(그림 2)을 사용하지 않았습니다.

> Method Detail


 `defaultPhysicsMemory`물리 기능은 메모리를 초기화하고 단위는 M 이다.

주의: 메모리는 16m보다 커야 한다

​**Implemention**

public function set defaultPhyscsMemory (value: int):void

public function get defaultPhysicsMemory ():int



###Config3D 설정

먼저 config3D 를 만들어서 필요한 인자를 설정한 후 레이야a3D 초기화에 사용합니다.


```typescript

//创建一个config3D
var _config:Config3D = new Config3D();
//设置不开启抗锯齿
_config.isAntialias = false;
//设置画布不透明
_config.isAlpha = false;
//使用创建的config3d
Laya3D.init(0, 0, _config);
```


**주의: Config3D 가 설치되면 수정할 수 없습니다.처음부터 설정해야 합니다.**