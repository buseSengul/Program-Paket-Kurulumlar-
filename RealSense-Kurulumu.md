# realsense2_camera Paketi Kurulumu

1. Öncelikle APT deposunda var mı kontrol et:
 ``` bash
sudo apt update
apt search ros-noetic-realsense2-camera
 ``` 
2. Gözüküyorsa:
 ``` bash
sudo apt install ros-noetic-realsense2-camera
 ``` 
3.Bulunmazsa (Jetson’da sıkça olur, çünkü ARM64 depolarında olmayabilir) → kaynak koddan kur:
 ``` bash
# workspace yoksa oluştur
mkdir -p ~/catkin_ws/src
cd ~/catkin_ws/src
# realsense ROS wrapper
git clone https://github.com/IntelRealSense/realsense-ros.git -b ros1-legacy
cd ~/catkin_ws
catkin_make
source devel/setup.bash
 ``` 
4. Kamerayı çalıştır:

Kurulumdan sonra:
 ``` bash
roscore
roslaunch realsense2_camera rs_camera.launch enable_color:=true
 ``` 

Başarılıysa /camera/color/image_raw gibi ROS topic’leri yayınlanmaya başlar.
5. Topic’leri listele:

Yeni bir terminalde:
 ``` bash
rostopic list
 ``` 

6. rqt_image_view ile görüntü aç:
``` bash
rqt_image_view
 ```

--------------------------------------------------------------------------------------------

