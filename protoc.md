卸载

```shell
sudo apt-get remove libprotobuf-dev 
sudo apt-get remove protobuf-compiler 
sudo apt-get remove python-protobuf 
sudo rm -rf /usr/local/bin/protoc 
sudo rm -rf /usr/bin/protoc
sudo rm -rf /usr/local/include/google
sudo rm -rf /usr/local/include/protobuf*
sudo rm -rf /usr/include/google
sudo rm -rf /usr/include/protobuf*
```

下列软件包将被【卸载】：

```shell
libgazebo9-dev libignition-msgs-dev libignition-transport4-dev
libprotobuf-dev libprotoc-dev ros-melodic-drone-wrapper
ros-melodic-gazebo-dev ros-melodic-gazebo-plugins ros-melodic-gazebo-ros
ros-melodic-gazebo-ros-control ros-melodic-gazebo-ros-pkgs
ros-melodic-hector-gazebo-plugins ros-melodic-rqt-drone-teleop
```



Protobuff 安装方式 

```shell
apt-get install libprotobuf-dev protobuf-compiler  #安装在系统
pip install protobuf==3.0.0 #安装在python
conda install libprotobuf=3.0.0 #安装在anaconda#
```


