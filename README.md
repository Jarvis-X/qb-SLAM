# qb-SLAM
This repository serves as the SLAM module of the quadrotor-blimp project. We are using the LiDAR sensor product LD06 of [ldrobot](https://www.ldrobot.com/en) that operates at 10Hz for 360-degree scans. 
### Update: 10/05/2022
- SLAM method: Hector-Mapping
  - input: LaserScan
- Dependency: 
  - [ROS-noetic](http://wiki.ros.org/noetic/Installation)
  - Hector mapping: `sudo apt-get install ros-noetic-hector-mapping`
- How to use:
  - `cd $YOUR_ROS_WORKSPACE/src`
  - `git clone https://github.com/Jarvis-X/qb-SLAM/`
  - `cd ..`
  - `catkin_make`
- To run:
  - make sure the usb port the LiDAR sensor is using has writting permission
  - In separate terminals (I use [terminator](https://github.com/gnome-terminator/terminator) for window management), run
    - `roscore`
    - `roslaunch ldlidar_stl_ros ld06.launch`
    - `roslaunch hector_mapping mapping_default.launch scan_topic:=/LiDAR/LD06`
    - `rosrun rviz rviz` if you want to eye-inspect the map, add topic /map to visualize.
