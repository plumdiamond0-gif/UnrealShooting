IA_Jump에서 값 타입을 bool로 설정

![alt text](<스크린샷 2026-09-08 051400.png>)

Started -> Jump
Completed -> Stop Jumping

계속 누르고 있음으로써 값이 매 프레임마다 바뀌어야 하는 일반적인 움직임과 달리 처음 한 번 클릭했을 때만 값이 반영되면 되므로 Triggered 대신 Started로 연결

