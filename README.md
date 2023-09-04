# KBOT SERIAL MOTOR
## Description
This package using for SLAM and Save map
## Requirements
```
$ sudo apt install ros-noetic-hector-slam ros-noetic-map-server
```
## Create Package
- Create kbot_slam package
```
$ cd ~/catkin_ws/src
$ catkin_create_pkg kbot_slam std_msgs
$ cd ~/catkin_ws
$ catkin_make
$ source ~/.bashrc
```
- Create slam.launch
```
$ roscd kbot_slam
$ mkdir launch
$ cd launch
$ touch slam.launch
$ nano slam.launch
<?xml version="1.0"?>
<launch>

    <include file="$(find hector_mapping)/launch/mapping_default.launch">
        <arg name="pub_map_odom_transform" value="true"/>
        <arg name="base_frame" value="base_link"/>
        <arg name="odom_frame" value="base_link"/>
    </include>

</launch>
```
- Create savemap.launch
```
$ roscd kbot_slam
$ mkdir maps
$ cd launch
$ touch savemap.launch
$ nano savemap.launch
<?xml version="1.0"?>
<launch>

    <arg name="map_file" default="-f $(find kbot_slam)/maps/map"/>

    <node name="map_server" pkg="map_server" type="map_saver"  output="screen" args="$(arg map_file)"/>

</launch>
```
## Command
- KBOT Slam
```
$ roslaunch kbot_serial rosserial.launch
```
- KBOT Savemap
```
$ roslaunch kbot_teleop teleop.launch
```