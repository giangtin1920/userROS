# userROS

## 1. Tạo workspace

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
    
## 4. Gazebo khi mô phỏng USV

Update là khi cài 1 gói nào đó thì nó sẽ cập nhật lại thư viện và kiểm tra thiếu gói hay có phiên bản mới hơn không.
Upgrade là để cập nhật phiên bản mới nhất. Khi cập nhật Gazebo:

    sudo apt update
    sudo apt upgrade
    
## 5. Cloud Server

[Broker Configuration - MaQiaTTo Free Online MQTT Broker](http://www.hivemq.com/demos/websocket-client/)

[MQTT Websocket Client (hivemq.com)](https://maqiatto.com/login)

## 6. 

