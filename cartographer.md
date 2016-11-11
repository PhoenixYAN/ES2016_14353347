#Lab5 ROS and Cartographer安装实验
本次实验结合了谷歌官方和hticm博客的提示进行了尝试。
---
##1、实验流程

###1、安装ROS
####（1）获取root权限

 `su root`
####（2）设置好ROS的资源清单

	sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
####（3）配置好密钥
`sudo apt-key adv --keyserver hkp://ha.pool.sks-keyservers.net:80 --recv-key 0xB01FA116`

####（4）检查apt-get获取包的地址更新
`sudo apt update`
####（5）执行ROS-Full install
`sudo apt-get install ros-jade-desktop-full`

![lab5_1](http://i.imgur.com/3oFqgPZ.png)
####(6)初始化rosdep
`sudo rosdep init`

`rosdep update`

![lab5_2](http://i.imgur.com/I2HGJ2Q.png)
####(7)设置环境变量

![lab5_3](http://i.imgur.com/DaIfn3U.png)

####(8)安装rosinstall
`sudo apt-get install python-rosinstall`

![lab5_4](http://i.imgur.com/7lnd56a.png)

###（2）安装依赖项
sudo apt-get install -y google-mock libboost-all-dev  libeigen3-dev libgflags-dev libgoogle-glog-dev liblua5.2-dev libprotobuf-dev  libsuitesparse-dev libwebp-dev ninja-build protobuf-compiler python-sphinx  ros-indigo-tf2-eigen libatlas-base-dev libsuitesparse-dev liblapack-dev
###（3）安装ceres solver
####①从博主的github上拷贝文件
` git clone https://github.com/hitcm/ceres-solver-1.11.0.git`
####②新建ceres-bin文件夹并进入其目录下

`mkdir ceres-bin`

`cd ceres-bin`
####③执行cmake

`cmake ../ceres-solver-1.11.0`

![lab6_1](http://i.imgur.com/j0lrFiA.png)

![lab6_2](http://i.imgur.com/rYzqp7f.png)

####④进行make测试

`make -j3`

`make test`

![test_result](http://i.imgur.com/2kMAJaR.png)
###（4）安装cartographer
####①从博主的github上拷贝文件
`git clone https://github.com/hitcm/cartographer.git`

####②进入build文件夹，安装ninja
`	
	
	cd cartographer/build
	cmake .. -G Ninja
	ninja
	ninja test
	sudo ninja install
`

![ninja test](http://i.imgur.com/ANvZxtA.png)
###（4）安装cartographer ros
####①从博主的github上拷贝文件

`git clone https://github.com/hitcm/cartographer_ros.git`

![lab6_3](http://i.imgur.com/FuDlRFZ.png)
####①初始化catkin_ws文件
mkdir catkin_ws
cd catkin_ws
wstool init src

####③执行catkin_make

![build](http://i.imgur.com/PcJ0Rhw.png)

##2、运行结果

![result](http://i.imgur.com/in6DwUy.png)

##3、实验遇到的困难和解决方法
在运行demo时不断出现以下错误。
![lab6_5](http://i.imgur.com/XHXI5SM.png)
一开始我以为是设ros的catkin_ws路径问题，但后来发现是catkin_ws文件夹中，cartographer没有放在src下进行catkin_make.

重新catkin_make后，依旧不能设置路径，然后我注意到自己处于root用户状态，而设定source需要在普通用户的文件路径进行设置。

最后exit后rospack profile，大功告成


