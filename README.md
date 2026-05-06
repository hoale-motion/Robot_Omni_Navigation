# Hospital Robot Navigation (ROS2 Jazzy)
Dự án điều hướng robot thông minh trong bệnh viện, chạy trên nền tảng Ubuntu 24.04 và ROS 2 Jazzy Jalisco. Hệ thống cho phép robot di chuyển chính xác đến các phòng bệnh thông qua tọa độ định sẵn.  
**Tác giả:** Lê Thế Hòa - MSSV:23134023 & Nguyễn Văn Nam - MSSV: 23134038 & Hồ Quốc Việt - MSSV:23134065  
**Email:** le6403810@gmail.com, vannamngguyen205@gmail.com, hoquocviet45667@gmail.com

<hr style="height:6px;border:none;background-color:#ccc;">

## Phạm vi của dự án bao gồm:
1. Xây dựng mô hình robot và môi trường mô phỏng vật lý có độ tin cậy cao.    
2. Xử lý tín hiệu đầu vào từ cảm biến (LiDAR, IMU, Camera) và dữ liệu Odometry.      
3. Thiết lập hệ thống TF tree chuẩn xác.    
4. Xây dựng bản đồ trong môi trường phức tạp (SLAM & Mapping). Sử dụng các thuật toán SLAM hiện đại trên ROS 2 để quét và xây dựng bản đồ Occupancy Grid 2D từ môi trường AWS Hospital World, xử lý nhiễu từ các hành lang dài và các phòng bệnh có cấu trúc giống nhau.  
5. Cấu hình các sever phục vụ cho Nav2 để tối ưu hóa quỹ đạo di chuyển và khả năng tránh vật cản động/tĩnh.

<hr style="height:6px;border:none;background-color:#ccc;">

## Setup
### 1.Yêu cầu hệ thống:  
- HĐH: Ubuntu 24.04 LTS  
- ROS 2: Jazzy Jalisco  
- Mô phỏng: Gazebo Harmonic / Ignition  
- Python 3.12+
### Tạo Workspace và cài đặt thư viện:
\# Tạo ROS 2 workspace  
mkdir -p ~/ros2_ws/src  
cd ~/ros2_ws/src 

\# Clone repository của dự án  
git clone https://github.com/hoale-motion/Robot_Omni_Navigation.git     
cd Robot_Omni_Navigation 

\# Sửa các đường link tại các file thành đường link của bạn:  
-Dòng 770 file omni_base.urdf:     <parameters>/home/thehoa/hospital_robot_nav/install/hospital_robot/share/hospital_robot/config/configuration.yaml</parameters>   
-Sửa dòng đầu của file run_hospital_robot.sh: cd /home/thehoa/hospital_robot_nav  

\# Build & run  
Lần lượt chạy các câu lệnh sau để có thể sử dụng mã nguồn:  
1. Ctr+'~' để mở terminal và chạy: ./run_hospital_robot.sh  
2. Mở thêm 1 terminal mới:  
    colcon build --symlink-instal  
    source install/setup.bash  
    ros2 launch nav2_simple_navigation navigation2.launch.py   
3. Chạy file: navigation_gui.py  

<hr style="height:6px;border:none;background-color:#ccc;">

## Cấu trúc thư mục
---

```bash
Robot_Omni_Navigation/
├── README.md
├── run_ekf.sh
├── run_hospital_robot.sh
├── run_slam.sh
├── save_map.sh
└── src/
    ├── hospital_robot/
    │   ├── CMakeLists.txt
    │   ├── config/
    │   │   ├── bridge_config.yaml
    │   │   └── configuration.yaml
    │   ├── launch/
    │   │   ├── display.launch.py
    │   │   └── gazebo_control.launch.py
    │   ├── package.xml
    │   ├── scripts/
    │   ├── urdf/
    │   │   └── omni_base.urdf
    │   └── worlds/
    │       ├── empty.sdf
    │       ├── models/
    │       └── worlds/
    └── nav2_simple_navigation/
        ├── CMakeLists.txt
        ├── config/
        │   ├── ekf.yaml
        │   ├── hospital_map.pgm
        │   ├── hospital_map.yaml
        │   ├── mapper_params.yaml
        │   ├── nav2_hospital_params.yaml
        │   ├── nav2_params.yaml
        │   ├── nav2_params_wo_BT.yaml
        │   ├── navigate_to_pose_w_replanning_and_recovery.xml
        │   └── rooms.yaml
        ├── launch/
        │   ├── ekf.launch.py
        │   ├── go_to_room.launch.py
        │   ├── nav2_control.launch.py
        │   └── navigation2.launch.py
        ├── nav2_simple_navigation/
        │   ├── __init__.py
        │   ├── map.png
        │   └── navigation_gui.py
        ├── package.xml
        ├── resource/
        │   └── nav2_simple_navigation
        ├── rviz/
        │   └── tb3_navigation2.rviz
        ├── setup.cfg
        └── setup.py
```

---

## Sử dụng
Sửa các đường link tại các file thành đường link của bạn:  
-Dòng 770 file omni_base.urdf:     <parameters>/home/thehoa/hospital_robot_nav/install/hospital_robot/share/hospital_robot/config/configuration.yaml</parameters>   
-Sửa dòng đầu của file run_hospital_robot.sh: cd /home/thehoa/hospital_robot_nav  
Lần lượt chạy các câu lệnh sau để có thể sử dụng mã nguồn:  
1. Ctr+'~' để mở terminal và chạy: ./run_hospital_robot.sh  
2. Mở thêm 1 terminal mới:  
    colcon build --symlink-instal  
    source install/setup.bash  
    ros2 launch nav2_simple_navigation navigation2.launch.py   
3. Chạy file: navigation_gui.py  

