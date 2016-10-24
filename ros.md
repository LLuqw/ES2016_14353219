# ROS安装  



---
## Installation  
### 1.1 配置ubuntu仓库  
配置ubuntu仓库允许"restricted","universe"以及"multiverse"，我们可以参考[https://help.ubuntu.com/community/Repositories/Ubuntu](https://help.ubuntu.com/community/Repositories/Ubuntu),这里说明很详细。  
### 1.2 配置源列表  
配置你的电脑去接收来自packages.ros.org. ROS Jade的软件，下面命令只适合ubuntu14.04  
`sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'`  
### 1.3 安装密钥  
`sudo apt-key adv --keyserver hkp://ha.pool.sks-keyservers.net:80 --recv-key 0xB01FA116`  
### 1.4 安装  
先检查下软件更新 `sudo apt-get update`  
安装Desktop-Full Install，包括： ROS, rqt, rviz, robot-generic libraries, 2D/3D simulators, navigation and 2D/3D perception  
`sudo apt-get install ros-jade-desktop-full`  
要找到可用的包可以使用 `apt-cache search ros-jade`  
### 1.5 初始化rosdep  
在使用ROS之前，我们需要初始化rosdep。rosdep使得你能更简单地安装你想要编译的源代码的相关系统，有些核心组件必须跑在ROS上  
`sudo rosdep init`  
`rosdep update`  
### 1.6 配置环境  
每次当你的程序运行时如果ROS环境变量能自动加入bash session，那么将会很方便  
``echo "source /opt/ros/jade/setup.bash" >> ~/.bashrc``  
`source ~/.bashrc`  
### 1.7 获取 rosinstall  
rosinstall是在ROS上频繁使用的命令行工具，我们能用一个命令就去轻松下载源代码  
`sudo apt-get install python-rosinstall`  
### 1.8 建立farm status  
我们安装的包的来源是[ROS build fram](http://build.ros.org/),我们可以检查包的状态[http://repositories.ros.org/status_page/ros_jade_default.html](http://repositories.ros.org/status_page/ros_jade_default.html)  
## Tutorials 
想要测试我们的安装，可以去看[http://wiki.ros.org/ROS/Tutorials](http://wiki.ros.org/ROS/Tutorials)






