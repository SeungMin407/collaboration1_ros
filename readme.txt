[기능 요약]
이미지를 입력받아 점묘화 경로를 생성하고, 로봇이 이를 따라 실제로 그림을 그리도록 제어하는 시스템

--------------------------------------------------
[실행 방법]
--------------------------------------------------

※ 모든 터미널에서 동일한 ROS_DOMAIN_ID 설정 필요

1. ROS DOMAIN 설정

ROS2 통신을 위한 네트워크 ID 설정

echo $ROS_DOMAIN_ID
export ROS_DOMAIN_ID=16


2. 로봇 구동

로봇 드라이버 및 RVIZ 실행

- 시뮬레이션 사용 시

ros2 launch dsr_bringup2 dsr_bringup2_rviz.launch.py mode:=virtual host:=127.0.0.1 port:=12345 model:=m0609

- 실제 로봇 사용 시

ros2 launch dsr_bringup2 dsr_bringup2_rviz.launch.py mode:=real host:=192.168.1.100 port:=12345 model:=m0609


3. 점묘화 액션 서버 실행

로봇 제어 담당

ros2 run cobot1 dot_drawer_action_dev


4. 액션 브릿지 실행 (필수)

웹 ↔ ROS2 간 명령 전달

ros2 run cobot1 action_bridge_node


--------------------------------------------------
[웹 실행 방법]
--------------------------------------------------

5. 사용자 웹 실행

이미지 업로드 및 작업 실행 UI 제공

client 폴더 이동 후

가상환경 생성 (최초 1회)
python3 -m venv venv

가상환경 실행
source venv/bin/activate

필요 패키지 설치 (최초 1회)
pip install opencv-python numpy rembg pillow

웹 실행
python3 app.py


6. 관리자 웹 실행

로봇 상태 확인 및 제어용 관리자 페이지

admin 폴더 이동 후

pip install opencv-python numpy rembg pillow
python3 app.py


--------------------------------------------------
[실행 순서 요약]
--------------------------------------------------

1) ROS DOMAIN 설정  
2) 로봇 실행 (실제 or 시뮬레이션)  
3) 액션 서버 실행  
4) 액션 브릿지 실행  
5) 사용자 웹 실행  
6) 관리자 웹 실행