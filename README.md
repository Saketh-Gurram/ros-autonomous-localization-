# ros-autonomous-localization

The objective of this project was to implement a Sanitizer Robot to autonomously map, localize, navigate.

The project included 2 stages as depicted below: 

The project utilizes the ROS2 package [explore_lite](https://github.com/robo-friends/m-explore-ros2) for autonomous mapping of the environment.

## Requirements
The package requires the following to run successfully:
1. ROS2 Humble
2. House simulation Environment
The package was developed on Ubuntu 22.04 

## Building the package
In order to build the package, put the **explore** and **amr_project** folders into your ROS2 workspace and build using the following commands:
```
colcon build --packages-select explore_lite
colcon build --packages-select amr_project  
```
And then install by using:
```
. install/setup.bash
```

## Running the tasks
The House simulation environment can be launched by using:
```
ros2 launch turtlebot3_gazebo turtlebot3_house.launch.py
```

### Autonomous mapping

The autonomous mapping can be done by running the following commands in three different terminals:
1. Launch Gazebo in the first terminals:
   ```
   ros2 launch turtlebot3_gazebo turtlebot3_dqn_stage4.launch.py 
   ```
2. Launch RVIZ2 in order to visualize the mapping the process and to launch the NAV2 stack:
   ```
   ros2 launch turtlebot3_navigation2 navigation2.launch.py use_sim_time:=True params_file:=/$HOME/ros2_ws/src/amr_project/config/nav2_params.yaml slam:=True
   ```
   Make sure that the **params_file** argument contains the correct path to the parameters file while launching.
3. Launch the explore lite package in order to start the mapping:
   ```
   ros2 launch explore_lite explore.launch.py
   ```
In order to visualize the frontiers, go to RVIZ, then click on MarkerArray, select topic: /explore/frontiers

### Localization and Navigation

This task allows the robot to localize autonomously by using the /global_localization topic.

1. Launch the bighouse environment in the first terminal:
   ```
   ros2 launch turtlebot3_gazebo turtlebot3_house.launch.py
   ```
2. Launch RVIZ and NAV2 stack in a separate terminal:
   ```
   ros2 launch turtlebot3_navigation2 navigation2.launch.py use_sim_time:=True map:=$HOME/ros2_ws/src/amr_project/maps/house_map.yaml params_file:=/$HOME/ros2_ws/src/amr_project/config/nav2_params.yaml
   ```
   Ensure that the path for params_file and map are consistent with the location of the package and configuration files.
3. In a separate terminal, launch the localization and navigation nodes:
   ```
   ros2 launch amr_project task3.launch.py
   ```



