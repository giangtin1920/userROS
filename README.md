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
    
    3. Thêm file rules : 
    
    sudo gedit /etc/udev/rules.d/68-usb-HgtA.rules
    
    4. Thêm dòng sau vào file rules:
    
    SUBSYSTEM=="tty", ATTRS{idVendor}=="1234", ATTRS{idProduct}=="5678", SYMLINK+="your_device_name"
    
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
   



