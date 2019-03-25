# usb转can的驱动
# 参考：https://autonomoustuff.atlassian.net/wiki/spaces/RW/pages/17473096/Fix+linuxcan+Kvaser+SDK+Install
$ sudo apt-add-repository ppa:jwhitleyastuff/linuxcan-dkms
$ sudo apt update && sudo apt install -y linuxcan-dkms

$ mkdir -p ~/radar_ws/src
$ cd ~/radar_ws/src
$ git clone https://github.com/astuff/kvaser_interface.git
$ cd ~/radar_ws/
$ catkin_make
----------------error--------------
CMake Error at /opt/ros/melodic/share/catkin/cmake/catkinConfig.cmake:83 (find_package):
  Could not find a package configuration file provided by "can_msgs" with any of the following names
解决：
$ sudo apt install ros-melodic-can-msgs
---------------error--------------
$ roslaunch kvaser_interface kvaser_can_bridge.launch
---------------error--------------
RLException: [kvaser_can_bridge.launch] is neither a launch file in package [kvaser_interface] nor is [kvaser_interface] a launch file name
The traceback for the exception was written to the log file
解决：
$ roscore
$ source devel/setup.bash
---------------error--------------
[ERROR] [1551582008.357215420]: Kvaser CAN Interface - Error opening reader: -2 - A bad parameter was provided to the CAN interface during initalization.
解决：
修改launch文件中的"can_hardware_id"="55257"
---------------error--------------
$ sudo apt install ros-melodic-delphi-esr-msgs

$ sudo apt update && sudo apt install apt-transport-https
$ sudo sh -c 'echo "deb [trusted=yes] https://s3.amazonaws.com/autonomoustuff-repo/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/autonomoustuff-public.list'
$ sudo apt update
---------------error--------------
E: Malformed entry 1 in list file /etc/apt/sources.list.d/autonomoustuff-public.list (Component)
E: The list of sources could not be read.
解决：
更新地址写错了
---------------error--------------
$ sudo apt install ros-melodic-delphi-esr
$ rosrun delphi_esr delphi_esr_can

============rviz============
添加Marker，改Global Options为esr_driver，改Marker Topic为/as_tx/radar_markers，可以显示绿色小方条

--------------------------------------
参考：[https://autonomoustuff.atlassian.net/wiki/spaces/RW/pages/17509820/Delphi+ESR]
delphi_esr_msgs/EsrTrack | parsed_tx/radartrack | All tracks (unfiltered) produced by the ESR.	


$ rostopic type /parsed_tx/radartrack | rosmsg show
std_msgs/Header header
  uint32 seq
  time stamp
  string frame_id
string canmsg
uint8 track_ID
float32 track_lat_rate
bool track_group_changed
uint8 track_status
float32 track_angle
float32 track_range
bool track_bridge_object
bool track_rolling_count
float32 track_width
float32 track_range_accel
uint8 track_med_range_mode
float32 track_range_rate

