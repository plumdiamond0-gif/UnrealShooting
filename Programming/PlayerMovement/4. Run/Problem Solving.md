![alt text](<스크린샷 2026-09-07 180744.png>)
![alt text](<스크린샷 2026-09-07 180946.png>)

Add Movement Input의 Scale Value의 값을 증가시킨다고 해도 실제 속도가 그만큼 증가되는 게 아님.
속도를 계속 증가시키는 게 아닌 이동 입력의 크기를 결정함.

CharacterMovement에는 Max Walk Speed라는 제한이 있음
입력 크기를 아무리 키워도 걷기 이동 속도가 무한히 증가하는 식으로 작동하지 않는다.
최대 속도 제한은 둘 다 동일하기 때문.
입력 크기는 CharacterMovement의 가속도에 영향을 주지만 CM이 입력값을 그대로 속도로 사용하는 건 아니며 여러 과정을 걸쳐 실제 속도를 계산함.

ex ->
Scale Value
= 엑셀을 얼마나 밟느냐

Max Acceleration
= 자동차가 얼마나 빨리 가속할 수 있느냐

Max Walk Speed
= 자동차의 최고속도