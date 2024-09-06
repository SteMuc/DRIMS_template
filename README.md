# DRIMS2 Simulation Environment

## Gazebo Simulation

In order to run the simulation:

1. Load Gazebo environment and robot simulation:
```bash
roslaunch drims_dice_demo arm_gazebo.launch robot:=yumi # or robot:=gofa
```

2. Launch low level ROS Services Server for robot planning and control:
```bash
roslaunch abb_wrapper_control launchControlServer.launch robot:=yumi # or robot:=gofa
```

3. Launch high level ROS Services Server for robot planning and control:
```bash
roslaunch abb_wrapper_control launchTaskServer.launch
```

4. Spawn the dice in simulation:
```bash
roslaunch drims_dice_demo spawn_dice.launch
```

**NOTE:** Each command should run in its own terminal

## Example nodes

Two example nodes are provided in both Python and C++ to perform a simple grasp of the dice:

For the **Python** version, launch the following ROS node:

```bash
rosrun drims_template take_the_dice_example.py
```

Instead, for the **C++** version:

```bash
roslaunch drims_template test_example.launch
```

Both of the example programs present a basic use of the services to move the robot:
- `/plan_and_execute_pose`: plan a collision-free joint trajectory to a given goal Cartesian pose and execute it.
- `/plan_and_execute_slerp`: plan a collision-free joint trajectory by usign SLERP interpolation to a given a goal Cartesian pose and execute it.
- `/plan_and_execute_joint`: plan a collision-free joint trajectory to a given a Joint goal and execute it.
- `/open_gripper`: open the gripper.
- `/close_gripper`: close the gripper.

In the following description are repored the ROS service definition, located in the `abb_wrapper_msgs` folder:

**Service structure `abb_wrapper_msgs/plan_and_execute_pose`**
```
# == Request ==
geometry_msgs/Pose goal_pose
bool is_relative
---
# == Response ==
bool success
string message
```

- `/plan_and_execute_joint`: plan a collision-free joint trajectory and to a given goal joints configuration and execute it.

**Service structure `abb_wrapper_msgs/plan_and_execute_joint`**
```
# == Request ==
float64[] joint_goal
---
# == Response ==
bool success
string message
```

- `/plan_and_execute_slerp`: plan a collision-free cartesian trajectory and to a given goal  and execute it.

**Service structure `abb_wrapper_msgs/plan_and_execute_slerp`**
```
# == Request ==
geometry_msgs/Pose goal_pose
bool is_relative
---
# == Response ==
bool success
string message
```

- `/open_gripper` and `/close_gripper`

**Service structure `abb_wrapper_msgs/open_gripper` and `abb_wrapper_msgs/open_gripper`**
```
bool in_flag
---
bool out_flag
string message
```


