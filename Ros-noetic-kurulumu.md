# ROS Noetic Kurulumu

Bu dosya, ROS Noetic’in desktop-full sürümünü adım adım kurmanız için hazırlanmıştır.  
1. ROS deposunu ekle
ROS paketlerini indirebilmek için resmi depoyu APT kaynaklarına ekleyin:

``` bash
sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
```
2. GPG anahtarını ekle  
Depoyu imzalayan anahtarı ekleyin:

``` bash
sudo apt install curl # if you haven't already installed curl
curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | sudo apt-key add –
```
3. Paket indeksini güncelle
``` bash
sudo apt update
```
4. ROS Noetic Desktop-Full kur
Tüm araçlar, RViz, rqt ve 2D/3D simülatörler dahil:

``` bash
sudo apt install ros-noetic-desktop-full
```
5. (Opsiyonel) Paketleri listele/ara
Kurulumun geldiğini görmek veya başka paketlere bakmak için:

``` bash
apt search ros-noetic
```
6. Ortam değişkenlerini kalıcı yap
Yeni açılan her terminalde ROS’un otomatik yüklenmesi için:

``` bash
echo "source /opt/ros/noetic/setup.bash" >> ~/.bashrc
source ~/.bashrc
```
7. Geliştirme araçları
Kaynaktan paket derlemek ve yönetmek için gerekli araçlar:

``` bash
sudo apt install python3-rosdep python3-rosinstall python3-rosinstall-generator python3-wstool build-essential
```
8. rosdep
Çoğu sistemde bir önceki adımda kurulur; yoksa aşağıyı çalıştırın.

``` bash
sudo apt install python3-rosdep
```
9. rosdep’i başlat
Bağımlılıkların otomatik çözümü için:

``` bash
sudo rosdep init
rosdep update
```

------------------------------------------------------------------------
Bu README ile adımlar net bir şekilde takip edilerek Jetson cihazınıza JetPack kurulumu yapılabilir.
