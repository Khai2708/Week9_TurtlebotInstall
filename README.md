# Week 9-10 Turtlebot3 installation
#### Setup PC
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
#### SBC setup
```
> Prepare microSD Card and Reader
> Download TurtleBot3 SBC Image
> Unzip the downloaded image file
> Burn the image file
> Raspberry Pi Imager Installation
```
![rpi_imager](https://user-images.githubusercontent.com/90145797/201824177-362652b5-69aa-401f-bf12-bd2c824b07e9.gif)

#### Disks Utility
![disks](https://user-images.githubusercontent.com/90145797/201824350-20ff289e-14a7-4890-8c04-ced33a7199f2.gif)


#### Resize the Partition
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
