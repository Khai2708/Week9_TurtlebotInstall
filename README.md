# Week 9,10,11 Turtlebot3 installation(Foxy version)
#### 1.Setup PC
```
> Install ROS 2 on Remote PC
----------------------------------------------------------------------------
asadbek@ubuntu:~$  wget https://raw.githubusercontent.com/ROBOTIS-GIT/robotis_tools/master/install_ros2_foxy.sh
--2022-10-26 14:14:20--  https://raw.githubusercontent.com/ROBOTIS-GIT/robotis_tools/master/install_ros2_foxy.sh ...

install_ros2_foxy.s 100%[===================>]   2.28K  --.-KB/s    in 0.004s  

2022-10-26 14:14:20 (549 KB/s) - ‘install_ros2_foxy.sh.1’ saved [2336/2336]

asadbek@ubuntu:~$ sudo chmod 755 ./install_ros2_foxy.sh
[sudo] password for asadbek: 
asadbek@ubuntu:~$ bash ./install_ros2_foxy.sh

[Note] OS version  >>> Ubuntu 20.04 (Focal Fossa)
[Note] Target ROS version >>> ROS 2 Foxy Fitzroy
[Note] Colcon workspace   >>> /home/asadbek/colcon_ws
...

> Install Dependendent ROS 2 Packages
---------------------------------------------------------------------------
> Install Gazebo11
asasadbek@ubuntu:~$ udo apt-get install ros-foxy-gazebo-*
334 packages can be upgraded. Run 'apt list --upgradable' to see them.
Reading package lists... Done
Building dependency tree       
Reading state information... Done
locales is already the newest version (2.31-0ubuntu9.9).
> Install Cartographer
asasadbek@ubuntu:~$ sudo apt install ros-foxy-cartographer
asasadbek@ubuntu:~$ sudo apt install ros-foxy-cartographer-ros
libgazebo11-dev libgpg-error-dev libgpgme-dev libgraphite2-dev libgtk2.0-dev
  libgts-dev libharfbuzz-dev libharfbuzz-gobject0 libignition-cmake2-dev
  libignition-common3 libignition-common3-av libignition-common3-av-dev
  libignition-common3-core-dev libignition-common3-dev
  libignition-common3-events libignition-common3-events-dev
  libignition-common3-graphics libignition-common3-graphics-dev
  libignition-common3-profiler libignition-common3-profiler-dev
  
> Install Navigation2
asasadbek@ubuntu:~$ sudo apt install ros-foxy-navigation2
asasadbek@ubuntu:~$ sudo apt install ros-foxy-nav2-bringup
Use 'sudo apt autoremove' to remove them.
0 upgraded, 0 newly installed, 0 to remove and 334 not upgraded.
[Make the colcon workspace and test colcon build]..

> Install TurtleBot3 Packages
------------------------------------------------------
asasadbek@ubuntu:~$ source ~/.bashrc
asadbek@ubuntu:~/turtlebot_install$ sudo apt install ros-foxy-dynamixel-sdk
[sudo] password for asadbek: 
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following packages were automatically installed and are no longer required:...

asadbek@ubuntu:~/turtlebot_install$  sudo apt install ros-foxy-turtlebot3-msgs
Use 'sudo apt autoremove' to remove them.
The following NEW packages will be installed:
  ros-foxy-dynamixel-sdk
0 upgraded, 1 newly installed, 0 to remove and 334 not upgraded.
Need to get 42.0 kB of archives.
After this operation, 325 kB of ...
asadbek@ubuntu:~/turtlebot_install$  sudo apt install ros-foxy-turtlebot3
[sudo] password for asadbek: 
Reading package lists... Done
Building dependency tree       
Reading state information.
...

> Environment Configuration
-----------------------------------------------------------------------------
asadbek@ubuntu:~/turtlebot_install$ echo 'export ROS_DOMAIN_ID=30 #TURTLEBOT3' >> ~/.bashrc
asadbek@ubuntu:~/turtlebot_install$ source ~/.bashrc
asadbek@ubuntu:~/turtlebot_install$ ..

```
#### 2.SBC setup
```
> Prepare microSD Card and Reader
> Download TurtleBot3 SBC Image
> Unzip the downloaded image file
> Burn the image file
> Raspberry Pi Imager Installation
```
![rpi_imager](https://user-images.githubusercontent.com/90145797/201824177-362652b5-69aa-401f-bf12-bd2c824b07e9.gif)

##### Disks Utility
![disks](https://user-images.githubusercontent.com/90145797/201824350-20ff289e-14a7-4890-8c04-ced33a7199f2.gif)


##### Resize the Partition
![gparted](https://user-images.githubusercontent.com/90145797/201824508-7aeaa336-50bd-42c4-932d-dda27ff8b4ef.gif)

```
> Configure the WiFi Network Setting

asadbek@ubuntu: $ cd /media/$USER/writable/etc/netplan
asadbek@ubuntu: $ sudo nano 50-cloud-init.yaml
```
![image](https://user-images.githubusercontent.com/90145797/201824789-92dd6ae8-4ee9-4f07-a12b-4329cb85cadf.png)

```
> ROS2 Network Configuration 
he default ROS Domain ID for TurtleBot3 is set to 30 in the *.bashrc* file.
... ROS_DOMAIN_ID=12 #TURTLEBOT3

> NEW LDS-02 Configuration
 > Install the LDS-02 driver and update TurtleBot3 package
  
asadbek@ubuntu:  $ sudo apt update
asadbek@ubuntu:  $ sudo apt install libudev-dev
asadbek@ubuntu:  $ cd ~/turtlebot3_ws/src
asadbek@ubuntu:  $ git clone -b ros2-devel https://github.com/ROBOTIS-GIT/ld08_driver.git
asadbek@ubuntu:  $ cd ~/turtlebot3_ws/src/turtlebot3 && git pull
asadbek@ubuntu:  $ rm -r turtlebot3_cartographer turtlebot3_navigation2
asadbek@ubuntu:  $ cd ~/turtlebot3_ws && colcon build --symlink-install


  
 > Export the LDS_MODEL to the bashrc file. Depending on your LDS model, LDS-01 or LDS-02
 
asadbek@ubuntu:   $ echo 'export LDS_MODEL=LDS-02' >> ~/.bashrc
asadbek@ubuntu:  $ source ~/.bashrc
 
-----------------------------------------------------------------
```

#### 3.OpenCR setup
```
> Connect the OpenCR to the Rasbperry Pi using the micro USB cable.
> Install required packages on the Raspberry Pi to upload the OpenCR firmware. 

$ sudo dpkg --add-architecture armhf
$ sudo apt update
$ sudo apt install libc6:armhf

> Depending on the platform, use either burger or waffle for the OPENCR_MODEL name. 
$ export OPENCR_PORT=/dev/ttyACM0
$ export OPENCR_MODEL=burger
$ rm -rf ./opencr_update.tar.bz2

> Download the firmware and loader, then extract the file. 
$ wget https://github.com/ROBOTIS-GIT/OpenCR-Binaries/raw/master/turtlebot3/ROS2/latest/opencr_update.tar.bz2
$ tar -xjf ./opencr_update.tar.bz2

> Upload firmware to the OpenCR.
$ cd ~/opencr_update
$ ./update.sh $OPENCR_PORT $OPENCR_MODEL.opencr
```
##### A successful firmware upload for TurtleBot3 burger
![image](https://user-images.githubusercontent.com/90145797/201826172-685b68b0-7b41-400e-aad0-f5c1c118b0a2.png)

#### 4. Bring up
```
> Bringup TurtleBot3
 > Open a new terminal from PC and connect to Raspberry Pi with its IP address.
$ ssh ubuntu@{IP_ADDRESS_OF_RASPBERRY_PI}

#Bring up basic packages to start TurtleBot3 applications.
$ export TURTLEBOT3_MODEL=burger
$ ros2 launch turtlebot3_bringup robot.launch.py

 > TurtleBot3 model is burger and the terminal will print below messages.
$ export TURTLEBOT3_MODEL=burger
$ ros2 launch turtlebot3_bringup robot.launch.py
[INFO] [launch]: All log files can be found below /home/ubuntu/.ros/log/2019-08-19-01-24-19-009803-ubuntu-15310
[INFO] [launch]: Default logging verbosity is set to INFO
urdf_file_name : turtlebot3_burger.urdf
[INFO] [robot_state_publisher-1]: process started with pid [15320]
[INFO] [hlds_laser_publisher-2]: process started with pid [15321]
[INFO] [turtlebot3_ros-3]: process started with pid [15322]
[robot_state_publisher-1] Initialize urdf model from file: /home/ubuntu/turtlebot_ws/install/turtlebot3_description/share/turtlebot3_description/urdf/turtlebot3_burger.urdf
[robot_state_publisher-1] Parsing robot urdf xml string.
[robot_state_publisher-1] Link base_link had 5 children
[robot_state_publisher-1] Link caster_back_link had 0 children
[robot_state_publisher-1] Link imu_link had 0 children
[robot_state_publisher-1] Link base_scan had 0 children
[robot_state_publisher-1] Link wheel_left_link had 0 children
[robot_state_publisher-1] Link wheel_right_link had 0 children
[robot_state_publisher-1] got segment base_footprint
[robot_state_publisher-1] got segment base_link
[robot_state_publisher-1] got segment base_scan
[robot_state_publisher-1] got segment caster_back_link
[robot_state_publisher-1] got segment imu_link
[robot_state_publisher-1] got segment wheel_left_link
[robot_state_publisher-1] got segment wheel_right_link
[turtlebot3_ros-3] [INFO] [turtlebot3_node]: Init TurtleBot3 Node Main
[turtlebot3_ros-3] [INFO] [turtlebot3_node]: Init DynamixelSDKWrapper
[turtlebot3_ros-3] [INFO] [DynamixelSDKWrapper]: Succeeded to open the port(/dev/ttyACM0)!
[turtlebot3_ros-3] [INFO] [DynamixelSDKWrapper]: Succeeded to change the baudrate!
[robot_state_publisher-1] Adding fixed segment from base_footprint to base_link
[robot_state_publisher-1] Adding fixed segment from base_link to caster_back_link
[robot_state_publisher-1] Adding fixed segment from base_link to imu_link
[robot_state_publisher-1] Adding fixed segment from base_link to base_scan
[robot_state_publisher-1] Adding moving segment from base_link to wheel_left_link
[robot_state_publisher-1] Adding moving segment from base_link to wheel_right_link
[turtlebot3_ros-3] [INFO] [turtlebot3_node]: Start Calibration of Gyro
[turtlebot3_ros-3] [INFO] [turtlebot3_node]: Calibration End
[turtlebot3_ros-3] [INFO] [turtlebot3_node]: Add Motors
[turtlebot3_ros-3] [INFO] [turtlebot3_node]: Add Wheels
[turtlebot3_ros-3] [INFO] [turtlebot3_node]: Add Sensors
[turtlebot3_ros-3] [INFO] [turtlebot3_node]: Succeeded to create battery state publisher
[turtlebot3_ros-3] [INFO] [turtlebot3_node]: Succeeded to create imu publisher
[turtlebot3_ros-3] [INFO] [turtlebot3_node]: Succeeded to create sensor state publisher
[turtlebot3_ros-3] [INFO] [turtlebot3_node]: Succeeded to create joint state publisher
[turtlebot3_ros-3] [INFO] [turtlebot3_node]: Add Devices
[turtlebot3_ros-3] [INFO] [turtlebot3_node]: Succeeded to create motor power server
[turtlebot3_ros-3] [INFO] [turtlebot3_node]: Succeeded to create reset server
[turtlebot3_ros-3] [INFO] [turtlebot3_node]: Succeeded to create sound server
[turtlebot3_ros-3] [INFO] [turtlebot3_node]: Run!
[turtlebot3_ros-3] [INFO] [diff_drive_controller]: Init Odometry
[turtlebot3_ros-3] [INFO] [diff_drive_controller]: Run!
```
##### Topic list
```
$ ros2 topic list
/battery_state
/cmd_vel
/imu
/joint_states
/magnetic_field
/odom
/parameter_events
/robot_description
/rosout
/scan
/sensor_state
/tf
/tf_static
```
##### Service list
```
$ ros2 service list
/diff_drive_controller/describe_parameters
/diff_drive_controller/get_parameter_types
/diff_drive_controller/get_parameters
/diff_drive_controller/list_parameters
/diff_drive_controller/set_parameters
/diff_drive_controller/set_parameters_atomically
/hlds_laser_publisher/describe_parameters
/hlds_laser_publisher/get_parameter_types
/hlds_laser_publisher/get_parameters
/hlds_laser_publisher/list_parameters
/hlds_laser_publisher/set_parameters
/hlds_laser_publisher/set_parameters_atomically
/launch_ros/describe_parameters
/launch_ros/get_parameter_types
/launch_ros/get_parameters
/launch_ros/list_parameters
/launch_ros/set_parameters
/launch_ros/set_parameters_atomically
/motor_power
/reset
/sound
/turtlebot3_node/describe_parameters
/turtlebot3_node/get_parameter_types
/turtlebot3_node/get_parameters
/turtlebot3_node/list_parameters
/turtlebot3_node/set_parameters
/turtlebot3_node/set_parameters_atomically
```

#### Autonomous Driving
##### Getting Started
```
> Install Autorace Packages
#Install AutoRace package on both Remote PC and SBC
$ cd ~/catkin_ws/src/
$ git clone -b kinetic-devel https://github.com/ROBOTISGIT/turtlebot3_autorace_2020.git
$ cd ~/catkin_ws && catkin_make

#Install additional dependent packages on Remote PC
$ sudo apt-get install ros-kinetic-image-transport ros-kinetic-cv-bridge ros-kinetic-vision-opencv python-opencv libopencv-dev ros-kinetic-image-proc

```
##### Camera Calibration
```
> Camera Imaging Calibration
#Launch roscore on Remote PC
$ roscore

#Trigger the camera on SBC
$ roslaunch turtlebot3_autorace_${Autorace_Misson}_camera turtlebot3_autorace_camera_pi.launch

#Execute rqt_image_view on Remote PC
$ rqt_image_view

#Excute rqt_reconfigure on Remote PC
$ rosrun rqt_reconfigure rqt_reconfigure

#Write modified values to the file.
```
![image](https://user-images.githubusercontent.com/90145797/204715893-0041e938-8295-4865-b3da-b74e6854f88f.png)

##### Intrinsic Camera Calibration
```
# Launch roscore on Remote PC & Trigger the camera on SBC
$ roscore
$ roslaunch turtlebot3_autorace_${Autorace_Misson}_camera turtlebot3_autorace_camera_pi.launch

#Run a intrinsic camera calibration launch file on Remote PC
$ export AUTO_IN_CALIB=calibration
$ export GAZEBO_MODE=false
$ roslaunch turtlebot3_autorace_${Autorace_Misson}_camera turtlebot3_autorace_intrinsic_camera_calibration.launch

#UseD the checkerboard to calibrate the camera, and click CALIBRATE &  saved the intrinsic calibration data.

```
![image](https://user-images.githubusercontent.com/90145797/204716457-294dba1b-ab76-4c2e-bfb8-b0dcdff81872.png)
![image](https://user-images.githubusercontent.com/90145797/204716473-b87e126e-5860-489f-bcec-8d10c6b59515.png)
###### Copy and paste the data from ost.yaml to camerav2_320x240_30fps.yaml.
![image](https://user-images.githubusercontent.com/90145797/204716682-d2bb7a76-7028-4a86-81b7-bdfbff94345e.png)

##### Extrinsic Camera Calibration
```
#Launch roscore on Remote PC & Trigger the camera on SBC
$ roslaunch turtlebot3_autorace_${Autorace_Misson}_camera turtlebot3_autorace_camera_pi.launch

#Use the command on Remote PC
$ export AUTO_IN_CALIB=action
$ export GAZEBO_MODE=false
$ roslaunch turtlebot3_autorace_${Autorace_Misson}_camera turtlebot3_autorace_intrinsic_camera_calibration.launch

#Run the extrinsic camera calibration launch file on Remote PC & Execute rqt on Remote PC
$ export AUTO_EX_CALIB=calibration
$ roslaunch turtlebot3_autorace_${Autorace_Misson}_camera turtlebot3_autorace_extrinsic_camera_calibration.launch
$ rqt

#Excute rqt_reconfigure on Remote PC
$ rosrun rqt_reconfigure rqt_reconfigure

#rqt_reconfigure
```
![image](https://user-images.githubusercontent.com/90145797/204718001-1d7357db-1f32-444b-9c0f-0281a00e73b8.png)

##### Checking Calibration Result
```
#Launch roscore on Remote PC & Trigger the camera on SBC
#Run a intrinsic camera calibration launch file on Remote PC
$ export AUTO_IN_CALIB=action
$ roslaunch turtlebot3_autorace_${Autorace_Misson}_camera turtlebot3_autorace_intrinsic_camera_calibration.launch

#Open terminal and use the command on Remote PC
$ export AUTO_EX_CALIB=action
$ roslaunch turtlebot3_autorace_${Autorace_Misson}_camera turtlebot3_autorace_extrinsic_camera_calibration.launch

```

##### Lane Detection
```
#Launch roscore on Remote PC & Trigger the camera on SBC
#Run a intrinsic camera calibration launch file on Remote PC
$ export AUTO_IN_CALIB=action
$ export GAZEBO_MODE=false
$ roslaunch turtlebot3_autorace_${Autorace_Misson}_camera turtlebot3_autorace_intrinsic_camera_calibration.launch

#Execute rqt on Remote PC
$ rqt
```
###### Image view of /detect/image_yellow_lane_marker/compressed topic
![image](https://user-images.githubusercontent.com/90145797/204719281-d546b1f2-
b883-446f-b4ee-b8ab6592d1ae.png)

###### Image view of /detect/image_white_lane_marker/compressed topic
![image](https://user-images.githubusercontent.com/90145797/204719356-263ac170-ff56-46dd-be95-0d768373ca5e.png)

###### Open lane.yaml file & Open lane.yaml file 
![image](https://user-images.githubusercontent.com/90145797/204719621-a61ec01b-ddd3-47bd-b49d-c0cb263c0b39.png)

##### Traffic Sign Detection
```
#Execute rqt_image_view on Remote PC.
$ rqt_image_view

#Open terminal and use the command on Remote PC.
$ roslaunch turtlebot3_autorace_${Autorace_Misson}_detect turtlebot3_autorace_detect_sign.launch

#Open terminal and use the command on Remote PC.
$ rqt_image_view
```

##### Missions & Traffic Lights Detection
```
3Open terminal and use the command on Remote PC.
$ export AUTO_DT_CALIB=calibration
$ roslaunch turtlebot3_autorace_traffic_light_detect turtlebot3_autorace_detect_traffic_light.launch

#Excute rqt on Remote PC.
rqt

#Execute rqt_image_view.
$ rqt_image_view
```

##### Running Traffic Light Mission
```
#Use the command on Remote PC.
$ export AUTO_IN_CALIB=action
$ export GAZEBO_MODE=false
$ roslaunch turtlebot3_autorace_traffic_light_camera turtlebot3_autorace_intrinsic_camera_calibration.launch

#Use the command on Remote PC.
$ rostopic pub -1 /core/decided_mode std_msgs/UInt8 "data: 3"
```

##### Running Intersection Mission
```
#Use the command on Remote PC.
$ export AUTO_IN_CALIB=action
$ roslaunch turtlebot3_autorace_intersection_camera turtlebot3_autorace_intrinsic_camera_calibration.launch

#Use the command on Remote PC.
$ export AUTO_EX_CALIB=action
$ export AUTO_DT_CALIB=action
$ roslaunch turtlebot3_autorace_intersection_core turtlebot3_autorace_core.launch

#Use the command on Remote PC.
$ rostopic pub -1 /core/decided_mode std_msgs/UInt8 "data: 2"
```

##### Running Construction Mission
```
#Use the command on Remote PC.
$ export AUTO_IN_CALIB=action
$ export GAZEBO_MODE=false
$ roslaunch turtlebot3_autorace_construction_camera turtlebot3_autorace_intrinsic_camera_calibration.launch

#Use the command on Remote PC.
$ export AUTO_EX_CALIB=action
$ export AUTO_DT_CALIB=action
$ roslaunch turtlebot3_autorace_construction_core turtlebot3_autorace_core.launch

#Use the command on Remote PC.
$ rostopic pub -1 /core/decided_mode std_msgs/UInt8 "data: 2"
```

##### Running Parking Mission
```
#Use the command on Remote PC.
$ export AUTO_IN_CALIB=action
$ export GAZEBO_MODE=false
$ roslaunch turtlebot3_autorace_parking_camera turtlebot3_autorace_intrinsic_camera_calibration.launch

#Use the command on Remote PC.
$ export AUTO_EX_CALIB=action
$ export AUTO_DT_CALIB=action
$ roslaunch turtlebot3_autorace_parking_core turtlebot3_autorace_core.launch

#Use the command on Remote PC.
$ rostopic pub -1 /core/decided_mode std_msgs/UInt8 "data: 2"
```

##### Level Crossing Detection
```
#Use the command on Remote PC.
$ export AUTO_DT_CALIB=calibration
$ roslaunch turtlebot3_autorace_level_crossing_detect turtlebot3_autorace_detect_level.launch

#Execute rqt
$ rqt

#Run a detect level lanuch file.
$ export AUTO_DT_CALIB=action
$ roslaunch turtlebot3_autorace_detect turtlebot3_autorace_detect_level.launch
```

##### Running Tunnel Mission
```
#Use the command on Remote PC.
$ export AUTO_IN_CALIB=action
$ export GAZEBO_MODE=false
$ roslaunch turtlebot3_autorace_tunnel_camera turtlebot3_autorace_intrinsic_camera_calibration.launch

#Use the command on Remote PC.
$ export AUTO_EX_CALIB=action
$ export AUTO_DT_CALIB=action
$ export TURTLEBOT3_MODEL=burger
$ roslaunch turtlebot3_autorace_tunnel_core turtlebot3_autorace_core.launch

#Use the command on Remote PC.
$ rostopic pub -1 /core/decided_mode std_msgs/UInt8 "data: 2"
```
