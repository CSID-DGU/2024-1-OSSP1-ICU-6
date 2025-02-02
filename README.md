# CCTV 노숙 취객 탐지 프로그램 (ICU)

## 프로젝트 개요

**ICU (I SEE YOU)**는 방범용 CCTV를 활용하여 노숙 취객을 자동으로 탐지하고 관제사에게 알림을 제공하는 시스템입니다.  
본 프로젝트는 Django 기반 웹 애플리케이션으로 개발되었으며, YOLO 및 Pose Estimation AI 모델을 활용하여 사람의 정지 상태 및 자세를 분석합니다.

## 배경 및 필요성

- 한 명의 관제사가 다수의 CCTV를 감시하는 환경에서 실시간 모니터링이 어려움
- 노숙 취객이 범죄의 표적이 되거나 교통사고 위험에 노출됨
- 기존의 지능형 CCTV 관제 시스템은 동적인 이상행동 감지에 초점이 맞춰져 있으며, 정적인 노숙 취객 감지가 어려움

## ICU의 역할

- ✅ **YOLOv5 모델**을 사용하여 사람을 탐지
- ✅ **Pose Estimation 모델**을 이용하여 노숙 취객을 판별
- ✅ 경고 알림을 제공하여 관제사의 대응을 지원
- ✅ **Django 웹 서버**를 활용하여 실시간 CCTV 스트리밍 및 데이터 관리

## 주요 기능

### 🔹 CCTV 실시간 감지

- React 기반 웹페이지에서 실시간으로 CCTV 영상을 스트리밍
- AI 분석을 통해 노숙 취객이 탐지되면 경고 팝업 제공

### 🔹 AI 기반 탐지

- YOLOv5 객체 인식을 통해 영상 속 사람 탐지
- 시간 단위로 영상을 캡쳐, YOLO가 생성한 바운딩 박스의 좌표를 이용한 알고리즘으로 정지된 사람 식별
- Pose Estimation (MediaPipe, AlphaPose) 활용하여 정지된 사람의 자세 분석  
  → 특정 시간 동안 앉아있거나 누워있는 경우 노숙 취객으로 판단

[YOLOv5와 v8 학습 결과 비교, v5 선정]

![10](https://github.com/user-attachments/assets/20569ced-9fac-42a7-aaf6-c3edf536a7da)


[YOLO를 통해 생성된 bounding box를 이용하여 정지된 사람 식별]

![image](https://github.com/user-attachments/assets/03da578a-4175-43e8-9b4b-d3df45d90a6b)



### 🔹 Django REST API

- Django + Django REST Framework (DRF) 기반 백엔드 API 구축
- 실시간 감지 데이터를 저장하고 경고 정보를 프론트엔드에 전달

### 🔹 웹 대시보드

- 사용자 친화적인 React 기반 UI 제공  
  → CCTV 등록 및 관리, 감지 이력 조회 기능 포함

## 기술 스택

### 📌 백엔드

- **Django 5.0.6** (웹 프레임워크)
- **Django REST Framework** (API 서버)
- **OpenCV & FFmpeg** (CCTV 영상 처리)
- **YOLOv5 & Pose Estimation** (AI 분석)

### 📌 프론트엔드

- **React** (웹 인터페이스)
- JavaScript, HTML, CSS
- 웹소켓(WebSocket) 및 API 연동

## 업무 분담

| **역할**     | **이름** | **담당 업무**                             |
|--------------|----------|-------------------------------------------|
| **팀장**     | 고성주   | 프로젝트 총괄, YOLO custom training 및 모델 개발, 객체 인식 알고리즘 구현 및 테스트             |
| **백엔드**   | 이수욱   | Pose estimation 모델 비교 분석, 정지 객체 판별 알고리즘 및 포즈 추정 알고리즘 설계      |
| **백엔드**   | 오진호   | Pose estimation 모델 비교 분석, 객체 탐지 알고리즘 설계 및 포즈 추정 알고리즘 설계       |
| **프론트엔드** | 김동연   | 실시간 스트리밍 구현, React 웹페이지 개발 및 UI 구현             |
| **풀스택**   | 한동호   | 객체 감지 알고리즘 개발, 프론트/백엔드 시스템 구성/통합 및 배포 관리, 협업 관리                   |

## 실행 화면

### 🔹초기 화면

![image](https://github.com/user-attachments/assets/c6f9961e-a126-4ecd-9085-121715b25473)


### 🔹카메라 정보 등록(IP)

![image](https://github.com/user-attachments/assets/8eb5db39-e229-48e6-a115-548de70e2ea8)


### 🔹등록된 카메라

![image](https://github.com/user-attachments/assets/87f59e66-b757-4f66-9a95-3a45f58362bf)


### 🔹탐지 작동 모습

![image](https://github.com/user-attachments/assets/7c65e108-905f-4160-871a-f393a329c25e)


