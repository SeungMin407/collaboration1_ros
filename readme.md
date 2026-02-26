# [디지털 이미지 기반 로봇 점묘 생성 시스템]
> **조 이름:** [F-1 - ROKEY]
> **팀원:** [문홍일_박지훈_이승민_이창석_최대혁]

## 1. 🎨 시스템 설계 및 플로우 차트
프로젝트의 전체적인 구조와 소프트웨어 흐름도입니다.

### 1-1. 시스템 설계도 (System Architecture)
<p align="center">
  <img src="./images/system_design.png" alt="시스템 설계도 이미지" width="400">
</p>
* *설명: [예: PC와 매니퓰레이터 간의 통신 구조를 나타냅니다.]*

### 1-2. 플로우 차트 (Flow Chart)
main flow
<img width="306" height="594" alt="image" src="https://github.com/user-attachments/assets/8487c8e2-3dd8-445b-a47a-9036ed5b424e" />

기능 1. 카메라 촬영 이미지로 점묘화 작업 수행
<img width="792" height="647" alt="image" src="https://github.com/user-attachments/assets/11e19c15-5866-4b98-9d3c-a01a2ac9f2a9" />

기능 2. 갤러리 내부 이미지로 점묘화 작업 수행

기능 3. 선택한 작품 이미지로 점묘화 작업 수행

통합 flow

점묘화 view 생성 로직(알고리즘)

---

## 2. 🖥️ 운영체제 환경 (OS Environment)
이 프로젝트는 다음 환경에서 개발하였습니다.

* **OS:** Ubuntu 22.04 LTS  
* **ROS Version:** ROS2 Humble  
* **Language:** Python, HTML, JavaScript, CSS  
* **Backend Framework:** FastAPI, Flask  
* **IDE:** VS Code  
* **Cloud:** Firebase  
* **Computer Vision:** OpenCV  
* **Communication:** ROS2 Action 기반 로봇 제어 통신  

---

## 3. 🛠️ 사용 장비 목록 (Hardware List)
프로젝트에 사용된 주요 하드웨어 장비입니다.

| 장비명 (Model) | 수량 | 비고 |
|:---:|:---:|:---|
| Doosan Robot M0609 | 1 | 점묘화 수행 매니퓰레이터 |
| Robot Gripper | 1 | 드로잉 도구 장착 |
| Drawing Tool (수성 사인펜 18색) | 1 Set | 색상 표현 |
| Custom Jig (그리퍼 부착형) | 1 | 펜 고정용 |
| Control PC | 1 | 알고리즘 연산 및 제어 |

---

## 4. 📦 의존성 (Dependencies)
프로젝트 실행에 필요한 라이브러리입니다.

* Python >= 3.10
* ROS2 Humble
* rclpy

### Vision & Image Processing
* opencv-python
* numpy
* rembg
* Pillow

### Backend
* FastAPI
* Flask

### Cloud
* firebase_admin


---
## 5. ▶️ 실행 순서 (Usage Guide)
프로젝트를 실행하기 위한 순서입니다. 터미널 명령어를 순서대로 입력해 주세요.

---

### Step 1. ROS DOMAIN 설정
ROS2 통신을 위한 네트워크 ID를 설정합니다.  
※ 모든 터미널에서 동일하게 설정해야 합니다.

```bash
echo $ROS_DOMAIN_ID
export ROS_DOMAIN_ID=16
```

### Step 2. 로봇 실행

```
로봇 드라이버 및 RVIZ를 실행합니다.

▶ 시뮬레이션 모드
ros2 launch dsr_bringup2 dsr_bringup2_rviz.launch.py mode:=virtual host:=127.0.0.1 port:=12345 model:=m0609
▶ 실제 로봇 모드
ros2 launch dsr_bringup2 dsr_bringup2_rviz.launch.py mode:=real host:=192.168.1.100 port:=12345 model:=m0609
```

### Step 3. 점묘화 액션 서버 실행

로봇의 점묘화 동작을 수행하는 제어 노드를 실행합니다.

```
ros2 run cobot1 dot_drawer_action_dev
```

### Step 4. 액션 브릿지 실행

웹과 ROS2 간 명령 전달을 담당하는 브릿지 노드를 실행합니다.

```
ros2 run cobot1 action_bridge_node
```
### Step 5. 사용자 웹 실행

이미지 업로드 및 작업 실행을 위한 UI를 실행합니다.
```
cd client
python3 -m venv venv
source venv/bin/activate
pip install opencv-python numpy rembg pillow
python3 app.py
```

### Step 6. 관리자 웹 실행

로봇 상태 확인 및 제어용 관리자 페이지를 실행합니다.

```
cd admin
pip install opencv-python numpy rembg pillow
python3 app.py
```

✔ 실행 순서 요약

ROS DOMAIN 설정

로봇 실행 (실제 또는 시뮬레이션)

점묘화 액션 서버 실행

액션 브릿지 실행

사용자 웹 실행

관리자 웹 실행
