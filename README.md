# agricultural_vehicles

## chmod
    sudo chmod 777 /dev/ttyUSB0

## start command
    cd ~/ros/agricultural_vehicles
    
    roscore
    
    . devel/setup.bash
    
    rosrun JoyStick joystick /dev/input/js0
    
    rosrun microsoft_rfid rfid_py.py /dev/agricultural_rfid 38400
    
    rosrun magnetic_rail mr_position_py.py /dev/agricultural_magnetic_rail 115200

    rosrun kevin_tcp tcp_server_py.py

    rosrun GPS_pkg GPS_ /dev/ttyUSB2 38400

    rosrun GPS_pkg IMU_ /dev/ttyACM0 115200

    rosrun rviz rviz -d ~/ros/agricultural_vehicles/src/agricultural_vehicles_rviz.rviz

    rosrun move_robot move_robot /dev/agricultural_arduino_nano 115200

    rosrun AnhungControl AnhungControl "192.168.0.11" 9930

    roslaunch hector_slam_launch tutorial.launch
    
    rosrun sick_tim sick_tim551_2050001 "192.168.0.10"
    

## RTK導航啟動步驟
- open rviz
- 按搖桿back -> load map 
- 按 rviz 2d pose estimate -> 往前拉 heading
- 按 y -> send mission
- 按 LB 進 auto

## button
- back -> load map
- Y -> send mission
- LB -> auto/mannal
- A -> joystick mode
- RT -> 油門
- LT -> 煞車

## ros debug
    rostopic echo /mr_msg

    rostopic echo /Send_Pose

    rostopic pub -r 5 Send_Pose geometry_msgs/PoseStamped // tab

    rostopic pub /Command std_msgs/String "data: 'Create Map'"
    rostopic pub /Command std_msgs/String "data: 'Save Map'"

## usb 固定
    lsusb
    udevadm info --attribute-walk --name=/dev/ttyUSB0

    sudo vim /etc/udev/rules.d/usb.rules

    sudo service udev reload
    sudo service udev restart

    cd /dev/
    ls

### 原始資料

    nano Bus 001 Device 008: ID 0403:6001 Future Technology Devices International, Ltd FT232 USB-Serial (UART)
    mag KERNELS=="1-1.1:1.0"
    rfid KERNELS=="1-1.2:1.0"

### 寫入資料
    KERNEL=="ttyUSB*", ATTRS{idVendor}=="0403", ATTRS{idProduct}=="6001", MODE:="0777", SYMLINK+="agricultural_arduino_nano"
    KERNELS=="1-1.1:1.0", SYMLINK+="agricultural_magnetic_rail"
    KERNELS=="1-1.2:1.0", SYMLINK+="agricultural_rfid"



## 問題
- IMU 校正