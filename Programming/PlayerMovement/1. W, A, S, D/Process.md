![alt text](<스크린샷 2026-09-07 151355.png>)
Character 블루 프린트 클래스에는 Character Movement Component같은 필요한 요소들이 들어있기 때문에 이걸 베이스로 플레이어 만듦.



![alt text](<스크린샷 2026-09-07 151517.png>)
Input -> Input Action(IA_Move)
Asix 2D로 설정
입력 타입 Axis 2D 설정 -> WASD는 두 방향을 표현하기 때문, 입력을 숫자 2개로 표현 가능



![alt text](<스크린샷 2026-09-07 152122.png>)
Input → Input Mapping Context(IMC_Player)
IA_Move 추가하고 W,A,S,D 키 설정

키	의미			모디파이어
W	앞으로 (Y+1)	Swizzle Input Axis Values (Order: YXZ)
S	뒤로 (Y-1)		Swizzle Input Axis Values (YXZ) + Negate
D	오른쪽 (X+1)	모디파이어 없음 (기본값 그대로 X축)
A	왼쪽 (X-1)		Negate만 적용



![alt text](<스크린샷 2026-09-07 151322.png>)
현재는 매필 컨텍스트를 만들기만 했지 플레이어와 연결은 안 돼 있기 때문에 연결이 필요
GetController로 자기 자신의 Controller 가지고 온 후 PlayerController에 있는 기능과 변수에 접근하기 위해 캐스팅
Add Mapping Context로 연결


![alt text](<스크린샷 2026-09-07 152645.png>)
Y → 앞/뒤 이동
X → 좌/우 이동
IA_Move : 키 입력값 받을 시 실행되는 이벤트, Action Value는 2차원 입력

![alt text](<스크린샷 2026-09-08 055354.png>)
블루프린트 게임모드 클래스 생성 후, 디폴트 폰 클래스를 BP_Player로 지정
![alt text](<스크린샷 2026-09-08 055346.png>)
월드 세팅의 GameMode override를 BP_GameMode로 지정
이러면 게임 시작 시 플레이어 시점으로 조종 가능해진다.

