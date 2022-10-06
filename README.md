# qb-SLAM
This repository serves as the SLAM module of the quadrotor-blimp project. We are using the LiDAR sensor product LD06 of [ldrobot](https://www.ldrobot.com/en) that operates at 10Hz for 360-degree scans. 
### Update: 10/05/2022
- SLAM method: Hector-Mapping
  - input: LaserScan
- Dependency: 
  - [ROS-noetic](http://wiki.ros.org/noetic/Installation)
  - Hector mapping: `sudo apt-get install ros-noetic-hector-mapping`
- Clone and prepare the src:
  - `cd $YOUR_ROS_WORKSPACE/src`
  - `git clone https://github.com/Jarvis-X/qb-SLAM/`
  - `cd ..`
  - `catkin_make`
  - `roscd hector-mapping/launch`
  - We need to change something in the launch file `sudo $YOUR_FAV_TEXT_EDITOR mapping_default.launch`
    - Change the default argument "base_frame" into `<arg name="base_frame" default="base_link"/> <!-- was "base_footprint" -->`
    - Change the default argument "odom_frame" into `<arg name="odom_frame" default="base_link"/> <!-- was "nav" -->`
    - Go to the last line before `</launch>`: it is commented out. Change that into `<node pkg="tf" type="static_transform_publisher" name="map_nav_broadcaster" args="0 0 0 0 0 0 base_link lidar_frame 100"/>`
- To run:
  - make sure the usb port the LiDAR sensor is using has writting permission. If any problems encountered, check [README_LiDAR.md](https://github.com/Jarvis-X/qb-SLAM/blob/main/README_LiDAR.md)
  - In separate terminals (I use [terminator](https://github.com/gnome-terminator/terminator) for window management), run
    - `roscore`
    - `roslaunch ldlidar_stl_ros ld06.launch`
    - `roslaunch hector_mapping mapping_default.launch scan_topic:=/qb-SLAM/LD06`
    - `rosrun rviz rviz` if you want to eye-inspect the map, add topic /map to visualize.
