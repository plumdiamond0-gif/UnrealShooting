![alt text](<스크린샷 2026-09-09 174553.png>)

Nav Mesh Bounds Volume 액터를 배치해 적들이 돌아다닐 영역을 지정한다.

![alt text](image.png)

적들의 AI 로직과 자체 기능을 분리하기 위해 블루프린트를 두개로 나누었다.

**BlackBoard**

![alt text](image-1.png)

적의 AI가 판단할 때 사용할 공유 데이터 저장소인 BlackBoard와 어떻게 행동할지 알려줄 Behavior Tree를 생성한다.

![alt text](<스크린샷 2026-09-09 180045.png>)

AI가 행동할 기준인 TargetActor 변수를 생성하고 플레이어뿐만 아니라 다른 액터들을 대상으로도 사용할 수 있게 Base Class를 Actor로 지정했다.

**Behavior Tree**

![alt text](image-2.png)

Behavoir Tree는 어떤 행동을 할지만 알고 있고 행동할 기준이 되는 데이터는 모르기 때문에 BlackBoard와 연결시킨다.

![alt text](image-3.png)

MoveTo 테스크를 시퀀스에 연결하고 Blackboard Key를 TargetActor로 지정해 AI가 네브메쉬 경로를 따라 자동으로 이동하게 한다.

**BTService_UpdateTarget**

![alt text](image-6.png)
![alt text](image-5.png)
![alt text](image-4.png)

적이 플레이어를 처음에는 찾을 수 있지만 게임이 진행되며 플레이어의 상태가 변경되면 AI가 플레이어를 다시 확인해야 한다.
그렇기에 0.5초마다 플레이어를 재차 확인하는 BTService_UpdateTarget이라는 서비스를 하나 만들어 그 안에 BlackBoard Key Select Controller타입의 BlackBoardTargetActorKey라는 변수를 선언하고 Behavior Tree의 인스펙터에서 기본값을 블랙보드에서 만든 targetActor로 할당한다.
GetPlayer를 통해 레벨의 플레이어를 가져온 후 TargetActor로 변수 안에 값을 넣는다.

**BP_EnemyAIController**

![alt text](image-7.png)

BP_EnemyAIController가 따를 Behavior Tree를 BeginPlay에서 지정한다.

**BP_Enemy**

![alt text](<스크린샷 2026-09-09 175331.png>)

BP_Enemy는 자신이 어떤 AI 로직을 따라야 할지 알아야 하므로 AIController에 BP_EnemyAIController로 지정한다.
적이 월드에 배치되거나 생성된 순간 AIContoller가 자동으로 작동하게 해주기 위해 Auto Possess AI의 값을 Placed in World or Spawned로 할당한다.



**Behavio Tree**
![alt text](image-8.png)

만약 플레이어가 적의 공격 사거리 안에 들어온다면 BTT_Attack 테스크를 실행시켜 현재 컨트롤되고 있는 적에게 접근해 공격 명령을 내립니다.
공격 사거리 안에는 플레이어가 없지만 감지 사거리 안에는 플레이어가 있다면 언리얼이 제공하는 MoveTo 테스크를 통해 플레이어를 추적합니다.
만약 어느 사거리 안에도 플레이어가 있지 않다면 어느 테스크도 실행하지 않습니다.
이때 시퀀스들은 애니메이션 밸류 또한 전달해줘 각 테스크에 맞는 애니메이션의 실행 명령을 내립니다.

**BlackBoard**

![alt text](image-11.png)

적과 플레이어와의 거리를 확인할 Distance, 공격 유무를 판단할 CanAttack, 어떤 애니메이션을 실행할지 알려줄 AnimSpeed 키를 블랙보드에 선언했다.

**BTService_UpdateTarget**

![alt text](image-10.png)

매 틱마다 블랙보드 Key들에 값을 할당한다.
만약 현재 컨트롤되고 있는 적과 플레이어의 거리가 공격 범위보다도 작으면 공격을 CanAttack을 True로 할당하고 그렇지 않다면 감지 거리를 따져 플레이어를 쫓을지, 아니면 Idle 상태로 있을지 판단한다.

**BTTask_Attack**

![alt text](image-12.png)

실행 시, 플레이어에게 공격 명령을 내리고 다른 시퀀스로 전환됐을 때는 공격 정지 명령을 내립니다.










