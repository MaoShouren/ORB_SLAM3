## 0、安装ORB-SLAM3 ROS的步骤：
https://blog.csdn.net/zardforever123/article/details/125044004
reference: https://github.com/UZ-SLAMLab/ORB_SLAM3/issues/442 (可以de很多bug)


## 1、rosbag运行命令：

```bash
# terminator1
roscore

# terminator2
# located: ~/code/ORB_SLAM3
rosrun ORB_SLAM3 Stereo_Inertial Vocabulary/ORBvoc.txt Examples/Stereo-Inertial/EuRoC.yaml false

# terminator3
# located: ~/code/ORB_SLAM3/Examples/ROS/ORB_SLAM3/bag
rosbag play --pause V1_02_medium.bag /cam0/image_raw:=/camera/left/image_raw /cam1/image_raw:=/camera/right/image_raw /imu0:=/imu

# PS: rostopic list:
  /camera/left/image_raw
  /camera/right/image_raw
  /clock
  /fcu/imu
  /fcu/motor_speed
  /imu
  /rosout
  /rosout_agg
  /vicon/firefly_sbx/firefly_sbx
```

## 2、使用gazebo中的仿真数据来跑ORB-SLAM3

话题修改（参考）
https://blog.csdn.net/qq_41861406/article/details/124362545

修改ros_rgbd.cc文件中的 message_filters中订阅的话题（一个为rgb相机，一个为深度相机）

``` bash
# 编译代码
/build_ros.sh

# 运行代码
# 单目惯性
cd ~/code/ORB_SLAM3
rosrun ORB_SLAM3 Mono_Inertial Vocabulary/ORBvoc.txt Examples/Monocular-Inertial/my_RealSense_D435i.yaml

# 纯单目
rosrun ORB_SLAM3 Mono Vocabulary/ORBvoc.txt Examples/Monocular/RealSense_D435i.yaml
```
