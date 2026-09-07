![alt text](image.png)
왼쪽 컨트롤 키를 눌러 이벤트가 실행될 때마다 조건문으로 현재가 달리는 상태인지 걷는 상태인지 체크
걷는 상태 -> IsRunning을 true로 만들고 CharacterMovement의 최대 걷기 속도를 600으로 지정
뛰는 상태 -> IsRunning을 false로 만들고 CharacterMovement의 최대 걷기 속도를 300으로 지정

