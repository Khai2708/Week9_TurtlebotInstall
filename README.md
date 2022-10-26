# Week9 Turtlebot3 installation
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
