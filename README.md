# Gazebo-Sim
Be used for simulation of UAV and UGV in Gazebo


## 文件描述
### ackerman_sim

该功能包是 ackerman 车的 gazebo 仿真环境


## 使用方法

将 models 中的  放入 ~/.gazebo/models中。

其中 kinect 这个 模型原本的包里应该有，但是没有传感器插件，所以把官方的替换掉

### ackerman_sim 依赖

```
sudo apt install ros-${ROS_DISTRO}-controller-manager ros-${ROS_DISTRO}-controller-manager-dbgsym \
                 ros-${ROS_DISTRO}-joint-state-controller ros-${ROS_DISTRO}-joint-state-controller-dbgsym \
                 ros-${ROS_DISTRO}-effort-controllers-dbgsym ros-${ROS_DISTRO}-effort-controllers ros-${ROS_DISTRO}-ros-control \
                 ros-${ROS_DISTRO}-ros-controllers
```

### ackerman_sim 使用流程：

#### 启动仿真场景

```
roslaunch ackerman_sim_gazebo ackerman_sim.launch       // 文件中可以更换场景，以及选择时候使用系统的 里程计
```

#### 使用键盘控制
```
rosrun ackerman_sim_gazebo keyboard_controll
```

#### 查看当前传感器话题

```
rostopic list
```


## Debug
Q: ackerman_sim 功能包中如果 roslaunch ackerman_sim_gazebo ackerman_sim.launch 显示控制器有问题
A: 应该是 python 的 yaml 文件太新了 需要改源码
```
sudo gedit /opt/ros/noetic/lib/controller_manager/spawner
```
181 行  name_yaml = yaml.load(open(name))  替换为

name_yaml = yaml.load(open(name), Loader=yaml.FullLoader)