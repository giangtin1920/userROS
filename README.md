# userROS

[1. Tạo workspace](#Taoworkspace)

[2. Lệnh ROS](#LenhROS)

[3. Đổi tên USB portname](#doitenUSB)

[4. Gazebo khi mô phỏng USV](#Gazebo)

[5. Cloud Server](#CloudServer)

[6. Các gói tin cần thiết](#goitin)

[7. Tạo public/subscribe/serial node](#Taonode)

[8. Cài SSH](#SSH)

[9. Submodule](#Submodules)

[10. usbCAN](#usbCAN)

[11. Save file log](#saved)

[12. Connect to rosmaster](#rosmaster)

<a name = "Taoworkspace"></a>
## 1. Tạo workspace

    mkdir catkin_ws
    cd catkin_ws
    mkdir src
    cd src
    catkin_init_workspace
    cd ..
    catkin_make
    
<a name = "LenhROS"></a>
## 2. Lệnh ROS
    Cấp quyền:                    sudo chmod
    Quay về thư mục home          cd 
    Xem thư mục hiện hành         ls
    Tạo thư mục                   mkdir
    Copy thư mục                  scp -r
    Copy file                     scp
    Lệnh mở trình ghi màn hình:   simplerecorder
    Remove (thư mục):             rm -r 
    Xem các cổng USB hiện tại:    ls - l /dev /ttyUSB*
    Copy sang máy tính khác       Scp -r qgroundcontrol   giangtin@[ip]
    Cấp quyền để đọc usb          Sudo chmod 777 /dev/

<a name = "doitenUSB"></a>
## 3. Đổi tên USB portname:

    1. Xem tên của cổng USB:
    
    dmesg | grep ttyUSB
    
    2. Xem thông tin cổng:
    
    udevadm info --name=/dev/ttyUSBx --attribute-walk
    
    Tìm ATTRS{idVendor}=="xxxx", ATTRS{idProduct}=="xxxx", ... đúng của cổng USB
    
    3. Thêm file rules : 
    
    sudo gedit /etc/udev/rules.d/68-usb-HgtA.rules
    
    4. Chạy lệnh `sudo nano /etc/udev/rules.d/68-usb-HgtA.rules` để thêm dòng sau vào file rules:
    
    SUBSYSTEM=="tty", ATTRS{idVendor}=="xxxx", ATTRS{idProduct}=="xxxx", SYMLINK+="your_device_name"
    
    5. Reload rules:
    
    sudo udevadm trigger
    ls -l /dev/ttyUSB*
    
<a name = "Gazebo"></a>
## 4. Gazebo khi mô phỏng USV

Update là khi cài 1 gói nào đó thì nó sẽ cập nhật lại thư viện và kiểm tra thiếu gói hay có phiên bản mới hơn không.
Upgrade là để cập nhật phiên bản mới nhất. Khi cập nhật Gazebo:

    sudo apt update
    sudo apt upgrade
    
<a name = "CloudServer"></a>
## 5. Cloud Server

[Broker Configuration - MaQiaTTo Free Online MQTT Broker](http://www.hivemq.com/demos/websocket-client/)

[MQTT Websocket Client (hivemq.com)](https://maqiatto.com/login)

<a name = "goitin"></a>
## 6. Các gói tin cần thiết

    sudo apt-get install ros-melodic-serial
    sudo apt-get install ros-melodic-socketcan-interface
    sudo apt-get install ros-melodic-socketcan-bridge
    sudo apt-get install can-utils
    sudo apt-get install ros-melodic-serial

    Nếu cần sử dụng giao tiếp CAN thì cài:
    sudo apt-get install ros-melodic-socketcan-interface 
    sudo apt-get install ros-melodic-socketcan-bridge
    sudo apt-get install can-utils

<a name = "Taonode"></a>
## 7. Tạo public/subscribe/serial node

[radar package](https://github.com/giangtin1920/radar_pkg)

<a name = "SSH"></a>
## 8. Cài SSH

https://wiki.matbao.net/ssh-la-gi-cach-dung-ssh-trao-doi-du-lieu-voi-server-linux/

    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get install openssh-server
    sudo nano /etc/ssh/sshd_config
    sudo service ssh status

<a name = "Submodules"></a>
## 9. Submodule

Thêm 1 submodules vào repo có sẵn:

    git config submodule.recurse true
    git submodule add https://github.com/giangtin1920/userROS.git
    
Clone 1 repo có sẵn 1 submodules:

    git clone https://github.com/giangtin1920/userROS.git
    git config submodule.recurse true
    git submodule update --init
 

<a name = "usbCAN"></a> 
## 10. usbCAN

[USB-CAN USB2CAN adapter](https://vi.aliexpress.com/item/4000045445478.html?spm=a2g0o.productlist.0.0.3d471aecyULEVA&algo_pvid=022b6bf8-fdf5-48ce-b676-9b29fb85163f&algo_exp_id=022b6bf8-fdf5-48ce-b676-9b29fb85163f-8&pdp_ext_f=%7B%22sku_id%22%3A%2210000000102107671%22%7D)

Cài tools cần thiết:

    sudo apt install net-tools
    sudo apt-get install can-utils

Load the kernel modules we need for CAN:

    sudo modprobe can
    sudo modprobe can_raw
    sudo modprobe slcan
    
    Automatically load the SocketCAN kernel modules on boot:
    sudo nano /etc/modules

Installing a CAN device requires loading the can_dev module and configuring the IP link to specify the CAN bus bitrate: s8 - 1000 Kbit/s

    sudo slcand -o -c -f -s8 /dev/ttyUSB1 slcan0
    sudo ifconfig slcan0 up
    
Now check that the interface has been added successfully:
 
    ip addr
        CAN identifier: 456h
        CAN data: 00h FFh AAh 55h 01h 02h 03h 04h (8 bytes)
        To send this CAN message using our can0 CAN network interface:
    cansend slcan0 456#00FFAA5501020304

<a name = "saved"></a>
## 11. Save file from terminal

    command |tee out1.txt
    
## 12. Connect to ROS master

    192.168.0.2 is ip master
    export ROS_MASTER_URI=192.168.0.2:11311
    
## 13. Git in Eclipse


