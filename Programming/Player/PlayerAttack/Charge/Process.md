![alt text](image-1.png)
![alt text](image-10.png)

Triggered(계속 눌려있을 때)에서는 차지 유무를 판단하고 만약 차지일 시, elapsed seconds를 받아와 현재 차지량에 더하고 Clamp를 통해 최대 차지량과 0사이의 값으로 조정한다.
그 값을 최대 차지량으로 나눈 후 1이하의 값, 즉 차지 비율을 받아와 HUD에 넘겨준다.





