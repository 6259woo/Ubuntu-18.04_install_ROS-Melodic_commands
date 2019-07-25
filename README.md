# Ubuntu 18.04 install of ROS Melodic
***

'ROS 공식 위키' 와 'ROS 로봇 프로그래밍 기초 개념부터 프로그래밍 학습, 실제 로봇에 적용까지'에 내용에서 Ubuntu 18.04 환경에서 ROS Melodic 설치에 필요한 부분을 정리한 글입니다.

***


## 1. 기타 설정
***
### 1.1 ifconfig 명령어 사용하기(자신의 아이피를 확인 할때 사용)
`$ sudo apt install net-tools`

### 1.2 NTP 설정 하기
`$ sudo apt install -y chrony ntpdate`
`$ sudo ntpdate -q ntp.ubuntu.com`
***


## 2. ROS 설치 시작
### 2.1 소스 리스트 추가
`$ sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'`


### 2.2 키 설정(서버상태에 따라 바뀔수 있으니 공식위키페이지 참고(http://wiki.ros.org/melodic/Installation/Ubuntu)
`$ sudo apt-key adv --keyserver 'hkp://keyserver.ubuntu.com:80' --recv-key C1CF6E31E6BADE8868B172B4F42ED6FBAB17C654`

### 2.3 패키지 리스트 업데이트 및 모든 패키지 업그레이드
`$ sudo apt update && sudo apt upgrade -y`

### 2.4 ROS Melodic 설치
`$ sudo apt install ros-melodic-desktop`

### 2.5 rqt 관련 모든 패키지 설치(다양한 rqt관련 플러그인 사용 가능)
`$ sudo apt install ros-melodic-rqt*`

### 2.6 rosdep 초기화
`$ sudo rosdep init`
`$ rosdep update`

### 2.7 Dependencies for building packages
`$ sudo apt install python-rosinstall python-rosinstall-generator python-wstool build-essential`

### 2.8 환경설정 파일 불러오기
`$ source /opt/ros/melodic/setup.bash`

### 2.9 ROS 작업 공간 작성 및 초기화
`$ mkdir -p ~/catkin_ws/src`
`$ cd ~/catkin_ws/src`
`$ catkin_init_workspace`

### 2.10 빌드 해보기(build와 devel폴더 생성)
`$ cd ~/catkin_ws/`
`$ catkin_make`

### 2.11 catkin 빌드 시스템과 관련된 환경설정 파일 불러오기
`$ source ~/catkin_ws/devel/setup.bash`

### 2.12 roscore가 정상 작동하는지 확인 -> 에러없이 작동하면 종료 [Ctrl+c]
`$ roscore`

### 2.13 매번 환경설정 명령어를 실행시키는 번거로움을 없애기 위한 환경설정
`$ gedit ~/.bashrc`

### 2.14 편집기가 뜨면 이미 있는 내용은 건들지말고 아래의 내용 추가후 저장 [Ctrl+s]
~~~
# Set ROS Melodic
source /opt/ros/melodic/setup.bash
source ~/catkin_ws/devel/setup.bash

# Set ROS Network
export ROS_HOSTNAME=localhost
export ROS_MASTER_URL=http://${ROS_HOSTNAME}:11311

# Set ROS alias command
alias cw='cd ~/catkin_ws'
alias cs='cd ~/catkin_ws/src'
alias cm='cd ~/catkin_ws && catkin_make'
~~~
### 2.15 현재 열려있는 터미널에 설정 방영
`$ source ~/.bashrc`
