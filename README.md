CCTV 노숙 취객 탐지 프로그램(ICU)

프로젝트 개요

**ICU (Intelligent CCTV Unit)**는 방범용 CCTV를 활용하여 노숙 취객을 자동으로 탐지하고 관제사에게 알림을 제공하는 시스템입니다.
본 프로젝트는 Django 기반 웹 애플리케이션으로 개발되었으며, YOLO 및 Pose Estimation AI 모델을 활용하여 사람의 정지 상태 및 자세를 분석합니다.

배경 및 필요성

한 명의 관제사가 다수의 CCTV를 감시하는 환경에서 실시간 모니터링이 어려움

노숙 취객이 범죄의 표적이 되거나 교통사고 위험에 노출됨

기존의 지능형 CCTV 관제 시스템은 동적인 이상행동 감지에 초점이 맞춰져 있으며, 정적인 노숙 취객 감지가 어려움

ICU의 역할

✅ YOLOv5 모델을 사용하여 사람을 탐지
✅ Pose Estimation 모델을 이용하여 노숙 취객을 판별
✅ 경고 알림을 제공하여 관제사의 대응을 지원
✅ Django 웹 서버를 활용하여 실시간 CCTV 스트리밍 및 데이터 관리

주요 기능

🔹 CCTV 실시간 감지

React 기반 웹페이지에서 실시간으로 CCTV 영상을 스트리밍

AI 분석을 통해 노숙 취객이 탐지되면 경고 팝업 제공

🔹 AI 기반 탐지

YOLOv5 객체 인식을 통해 영상 속 사람 탐지

Pose Estimation (MediaPipe, AlphaPose) 활용하여 사람의 자세 분석

특정 시간 동안 앉아있거나 누워있는 경우 노숙 취객으로 판단

🔹 Django REST API

Django + Django REST Framework(DRF) 기반 백엔드 API 구축

실시간 감지 데이터를 저장하고 경고 정보를 프론트엔드에 전달

🔹 웹 대시보드

사용자 친화적인 React 기반 UI 제공

CCTV 등록 및 관리, 감지 이력 조회 기능 포함

기술 스택

📌 백엔드

Django 5.0.6 (웹 프레임워크)

Django REST Framework (API 서버)

OpenCV & FFmpeg (CCTV 영상 처리)

YOLOv5 & Pose Estimation (AI 분석)

📌 프론트엔드

React (웹 인터페이스)

JavaScript, HTML, CSS

웹소켓(WebSocket) 및 API 연동

📌 배포 및 운영

AWS EC2 (서버 배포)

Gunicorn & Nginx (웹 서버 운영)

Docker (컨테이너화 예정)

실행 방법

1️⃣ 백엔드 실행 (Django 서버)

# 가상 환경 생성
python -m venv venv
source venv/bin/activate  # (Windows의 경우 venv\Scripts\activate)

# 필수 패키지 설치
pip install -r requirements.txt

# 서버 실행
python manage.py runserver

2️⃣ 프론트엔드 실행 (React 서버)

cd frontend
npm install
npm start

3️⃣ 웹 대시보드 접속

기본 URL: http://127.0.0.1:8000/

관리 페이지: http://127.0.0.1:8000/admin/

프로젝트 팀원

역할

이름

담당 업무

팀장

고성주

프로젝트 총괄, YOLO 모델 개발

백엔드

이수욱

Pose Estimation 모델 구현 및 API 개발

백엔드

오진호

객체 탐지 알고리즘 설계 및 예외 처리

프론트엔드

김동연

React 웹페이지 개발 및 UI 구현

풀스택

한동호

시스템 통합 및 배포 관리

참고 자료

ICU 시연 영상

배포된 서비스 URL
  
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


