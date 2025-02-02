ICU(I see you) 프로젝트
CCTV 노숙 취객 탐지 프로그램
- 실시간으로 방범용 CCTV화면의 노숙취객을 식별
- YOLO 모델을 이용하여 사람 인식
- 화면 내에 사람이 일정 시간 이상 정지해 있을 경우 알고리즘을 통해 감지
- MideaPipe pose estimation을 통해 자세를 판별하여 위험할 경우 알림 제공
  
  
YOLOv5, YOLOv8 3594개의 데이터로 학습. YOLOv5의 학습결과가 더 우수하여 채택.
![10](https://github.com/user-attachments/assets/10588466-966c-499f-89b2-0d203a3f1eff)

영상을 30초 간격으로 캡쳐.
사람 탐지 시 바운딩 박스가 생성되면 바운딩 박스 객체와 카운트 변수 생성.
이후 교집합을 만드는 바운딩 박스 생성 시 카운트 변수를 활용하여 정지된 사람 탐지. 
![image](https://github.com/user-attachments/assets/1fb7746e-7f42-4c38-a576-663cffb82925)

이후 정지된 사람의 이미지를 OpenCV로 전처리하여, mideapipe를 통해 관절 좌표 추출.
좌표를 활용하여 자세 추정. 서 있지 않다면 위험하다고 판별.


초기 화면
![image](https://github.com/user-attachments/assets/c6f9961e-a126-4ecd-9085-121715b25473)

카메라 정보 등록(IP)
![image](https://github.com/user-attachments/assets/8eb5db39-e229-48e6-a115-548de70e2ea8)

등록된 카메라
![image](https://github.com/user-attachments/assets/87f59e66-b757-4f66-9a95-3a45f58362bf)

탐지 작동 모습
![image](https://github.com/user-attachments/assets/7c65e108-905f-4160-871a-f393a329c25e)


