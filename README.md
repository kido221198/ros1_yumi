# How to run different programs

## Position Control, ABB Driver
1. Set /industrial_core/simple_message/include/simple_message/joint_data.h -> MAX_NUM_JOINT = 10
2. Uncomment left_arm/right_arm in /yumi/yumi_moveit_config/config/controllers.yaml and comment the others
3. Open RobotStudio backup ROS_ABB_Driver
4. rosbuild
5. roslaunch yumi_support robot_interface.launch 
6. roslaunch yumi_moveit_config demo_online.launch


## Position Control, RWS
1. Set /industrial_core/simple_message/include/simple_message/joint_data.h -> MAX_NUM_JOINT = 20
2. Uncomment yumi/joint_traj_pos_controller_l/yumi/joint_traj_pos_controller_r in /yumi/yumi_moveit_config/config/controllers.yaml and comment the others
3. Open RobotStudio backup ROS_RWS
4. rosbuild
5. roslaunch yumi_moveit_config yumi_movegroup.launch 
6. roslaunch yumi_moveit_config demo_online.launch
