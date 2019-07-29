# GPSParse_Projection

# README

## 引言

本实验为差分导航数据解析及单路径地图采集实验，重点是要掌握差分导航定位系统的基本原理和串口数据解析的方法。实验中，首先要选择正确的串口和波特率，然后依据所选导航设备的串口协议依次解析出各项导航数据，包括经度、纬度、高度、航向角、搜星数、RTK状态、车速等信息。还可利用解析后的位姿数据将车辆行驶过的路径保存为地图文件，供导航路径规划模块使用。本实验包含1个ROS包和1个.py文件：xfgps_parse和main.py。其中，xfgps_parse的ROS包为差分导航驱动模块，负责读取导航串口数据并解析，将解析后的实时经纬度、高度、航向角、RTK状态、车速等信息在UI界面依次显示，同时发送给其他模块；在接收到UI界面发送的采集地图信号后，可将车辆行驶过的路径信息存储为地图文件。main.py为UI控制界面，负责导航设备串口、波特率的选择，解析后各项导航数据的显示和开始程序、采集地图等使能信号的发送。各节点之间的消息通信如下图所示：

![node](https://raw.githubusercontent.com/GuoXiaoxiao1/GPS_Parse/master/GPS/Node.png)

## 依赖

- ros kinect(Ubuntu 16.04)
- pyqt5

## 编译

```
% cd GPSParse_Projection/src
% sudo chmod -R 777 *
% cd ..
% catkin_make
    
```

## 运行

！！！开始本实验前请使用Cutecom串口软件测试导航设备的端口号，并在UI控制界面上选择正确的串口和波特率后开始程序！！！

```
% cd GPSParse_Projection
% source devel/setup.bash
% roslaunch xfgps_parse gps_parse.launch

```

- 在UI界面中，点击“Start”按钮开始程序。若选择的串口和波特率不正确，则会弹出相应的提示框，需要在正确选择串口和波特率之后才能启动程序。程序启动后，即开始实时解析车辆当前位置信息并显示，包括：时间、经度、纬度、高度、RTK状态、搜星数、差分延时、车速、航向角。
- 可以解析后导航数据的格式将车辆行驶过的路径信息存储为地图文件。点击“Collect”按钮开始采集地图；通过选择“Road attribute”下拉框实现不同道路属性值的切换，点击“Switch attribute”根据不同道路特征切换相应的属性值。地图采集完成后，点击“Pause”按钮暂停采集。点击“Save”按钮将采集的路径存储为地图文件，并显示文件的存储路径。地图文件的存储路径默认为.py文件所在目录的map文件夹下，默认文件名为map.txt。
- 若需要多次操作采集地图，应先删除上次保存的地图，否则新保存的地图点会以追加的方式补充在原地图文件中。
- 更多UI界面操作信息与显示信息可参考本实验的实验指导书中示例软件展示部分。

## 示例demo

![demo](https://raw.githubusercontent.com/GuoXiaoxiao1/GPS_Parse/master/GPS/UI.png) 

## 联系我们

如果您有相关实验课件的其他需要，或向我们反馈一些本实验存在的bug,或想向我们提供一些特殊场景的实验数据，请联系我们：

```
Email: lemonxiaoxiao9@163.com

```

注：反馈数据的格式应为rosbag包
