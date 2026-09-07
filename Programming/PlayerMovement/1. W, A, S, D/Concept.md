키를 누르면 기본적으로 X축에 1.0이 들어옴 (Bool/Digital 입력이 Axis1D로 변환될 때 X로 들어감)
D는 그대로 두면 X+1이 되니 아무것도 안 해도 됨
A는 Negate를 걸어서 X-1로 만듦
W는 X에 들어온 값을 Y로 옮겨야 하니 Swizzle(YXZ)을 적용 → X+1이 Y+1이 됨
S는 Swizzle(YXZ)로 Y로 옮긴 다음, Negate까지 적용해서 Y-1로 만듦

-------------------------------------------------------------------------------------------------------------------------------

Input Mapping Context (IMC)  →  키 ↔ 액션 연결 (하드웨어 ↔ 의미)
        ↓
Input Action (IA)            →  "무엇을 할지"에 대한 추상적 신호
        ↓
Player (Pawn/Controller)     →  신호를 받아 실제로 반응

1. Input Action (IA) — "의미"
   키와 무관한 추상적 액션 ("Move", "Jump", "Fire")
   Value Type만 가짐 (Bool / Axis1D / Axis2D / Axis3D)
   어떤 키인지는 모름 — IA 자체엔 키 정보 없음

2. Input Mapping Context (IMC) — "키 ↔ 액션 연결"
   실제 키/마우스/패드 입력을 IA에 연결하는 테이블
   여러 개 동시에 켤 수 있고 Priority로 우선순위 조절 가능
   상황에 따라 켜고 끌 수 있는 교체 가능한 레이어

3. Player — "실행 주체"
   PlayerController: IMC를 Add(활성화)
   Pawn/Character: IA를 함수에 Bind(실제 동작 실행)

요소			 역할				       비유
IMC			키보드 물리 키 → 액션 이름 변환	통역사    (언어를 의미로 바꿈)
IA			순수한 의미/신호 (키와 무관)		 명령어 자체 ("이동해")
PlayerController	IMC를 켜고 끔 (상황별 교체)		 어떤 통역사를 쓸지 결정
Pawn/Character	        IA를 받아서 실제 동작 실행		 명령을 듣고 움직이는 몸

-------------------------------------------------------------------------------------------------------------------------------

CharacterMovement :
이동, 중력, 점프, 걷기, 달리기, 바닥 판정, 등을 담당
Unity에서 Rigidbody를 직접 조작하던 것과 조금 다름.

-------------------------------------------------------------------------------------------------------------------------------

Swizzle Input Axis Values : 
X/Y/Z에 들어오는 값을 서로 다른 축으로 옮겨주는 노드. YXZ는 XYZ 순서를 바꾼 거, X 자리에 1이 들어오는데 X가 Y로 바뀌었으니 Y에 1 들어옴

-------------------------------------------------------------------------------------------------------------------------------

GetController : Unity의 GetComponent와 동일
Enhanced Input Local Player Subsystem : 현재 플레이어에게 어떤 입력 설정을 적용할지 관리
ex->
Input Mapping Context 추가
Input Mapping Context 제거
여러 Mapping Context의 우선순위 관리
현재 플레이어에게 적용된 입력 설정 관리

-------------------------------------------------------------------------------------------------------------------------------

Get Control Rotation : 현재 플레이어의 조작 방향 가져옴
Add Movement Input  : World Direction에 Scene Value 곱
-World Direction : 어느 방향으로 움직일지
-Scale Value : 얼만큼 움직일지








