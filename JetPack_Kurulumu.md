# Jetson Cihaza JetPack 5.x Kurulumu

Bu doküman, **Ubuntu işletim sistemine sahip bir host bilgisayar**
üzerinden **Jetson cihazına JetPack 5.1.x kurulumu** için adımları
açıklar. Kurulumlar **NVIDIA SDK Manager** ile gerçekleştirilir.

https://www.forecr.io/blogs/installation/jetpack-5-x-installation-for-dsboard-ornx-lan sitesi takip edilerek kurulum yapılmıştır. Flashlama işlemi terminal komutları ile yapıldığında shell hatası alınmıştır o nedenle flashlama işlemi siteden farklı olarak terminal kodu ile değil SDK manager ile yapılmıştır.

------------------------------------------------------------------------

## 1. NVIDIA SDK Manager Kurulumu
Host bilgisayar içerisinde sdk manager yüklü mü kontrol edilir yüklü değilse aşağıdaki adımlar izlenerek kurulumu yapılır.

1.  [NVIDIA SDK Manager](https://developer.nvidia.com/sdk-manager)
    adresinden `.deb` uzantılı Ubuntu paketini indirin.

2.  Terminalde şu komutları çalıştırın:

    ``` bash
    sudo apt update
    sudo apt install ./sdkmanager_[sürüm].deb
    sdkmanager
    ```

3.  İlk açılışta **NVIDIA Developer** hesabı ile giriş yapın.

------------------------------------------------------------------------

## 2. Jetson Linux İmajını İndirme

1.  SDK Manager'ı açın ve Jetson cihazınızı host bilgisayara bağlayın.

2.  **Target Hardware** otomatik görünmelidir.

3.  "Host Machine" seçeneğini seçmenize gerek yok.

4.  **JetPack sürümünü** (5.1.3, 5.1.4, 5.1.5) seçin ve STEP2 'e geçin.

5.  Sadece **Jetson Linux** seçeneğini işaretleyin, şartları kabul edin,
    adım 3'e geçin.

6.  SDK Manager, kullanıcı adınızın şifresini soracaktır. Şifreyi girin ve devam edin.

7.  Jetson OS oluşturulduktan sonra SDK Manager, Jetson modülünün flashlama stilini sorar. Bu adımı skip butonuna tıklayarak atlayın. SDK Manager' ı kapatmayın.
8.  **Target HW image folder** yoluna gidin:

        ~/nvidia/nvidia_sdk/JetPack_5.x.x_Linux_JETSON_ORIN_[NX/NANO]_TARGETS/
JetPack-5.1.1 için:  
          Orin NX: ~/nvidia/nvidia_sdk/JetPack_5.1.1_Linux_JETSON_ORIN_NX_TARGETS/  
          Orin Nano: ~/nvidia/nvidia_sdk/JetPack_5.1.1_Linux_JETSON_ORIN_NANO_TARGETS/  
 JetPack-5.1.2 için:  
          Orin NX: ~/nvidia/nvidia_sdk/JetPack_5.1.2_Linux_JETSON_ORIN_NX_TARGETS/  
          Orin Nano: ~/nvidia/nvidia_sdk/JetPack_5.1.2_Linux_JETSON_ORIN_NANO_TARGETS/  
 JetPack-5.1.3 için:  
          Orin NX: ~/nvidia/nvidia_sdk/JetPack_5.1.3_Linux_JETSON_ORIN_NX_TARGETS/  
          Orin Nano: ~/nvidia/nvidia_sdk/JetPack_5.1.3_Linux_JETSON_ORIN_NANO_TARGETS/  
 JetPack-5.1.4 için:  
          Orin NX: ~/nvidia/nvidia_sdk/JetPack_5.1.4_Linux_JETSON_ORIN_NX_TARGETS/  
          Orin Nano: ~/nvidia/nvidia_sdk/JetPack_5.1.4_Linux_JETSON_ORIN_NANO_TARGETS/  


------------------------------------------------------------------------

## 3. BSP Dosyalarının Kurulumu

1.  GitHub'dan uygun BSP dosyasını indirin ve zipten çıkarın:

-JetPack-5.1.1 için:   
Orin NX: (https://github.com/forecr/dsboard_ornx_lan_orin_bsp/raw/master/dsboard_ornx_lan_orin_nx_JP5_1_1_bsp.tar.xz)  
Orin Nano: (https://github.com/forecr/dsboard_ornx_lan_orin_bsp/raw/master/dsboard_ornx_lan_orin_nano_JP5_1_1_bsp.tar.xz)  
JetPack-5.1.2 için:   
Orin NX: (https://github.com/forecr/dsboard_ornx_lan_orin_bsp/raw/master/dsboard_ornx_lan_orin_nx_JP5_1_2_bsp.tar.xz)  
Orin Nano: (https://github.com/forecr/dsboard_ornx_lan_orin_bsp/raw/master/dsboard_ornx_lan_orin_nano_JP5_1_2_bsp.tar.xz)  
JetPack-5.1.3 için:  
Orin NX: (https://github.com/forecr/dsboard_ornx_lan_orin_bsp/raw/master/dsboard_ornx_lan_orin_nx_JP5_1_3_bsp.tar.xz)  
Orin Nano: (https://github.com/forecr/dsboard_ornx_lan_orin_bsp/raw/master/dsboard_ornx_lan_orin_nano_JP5_1_3_bsp.tar.xz)  
JetPack-5.1.4 için:  
Orin NX: (https://github.com/forecr/dsboard_ornx_lan_orin_bsp/raw/master/dsboard_ornx_lan_orin_nx_JP5_1_4_bsp.tar.xz)  
Orin Nano: (https://github.com/forecr/dsboard_ornx_lan_orin_bsp/raw/master/dsboard_ornx_lan_orin_nano_JP5_1_4_bsp.tar.xz)  

NOT: Aşağıdaki adımlar Orin NX için yapılmıştır, diğer Jetson modül tipleri için de aynıdır, sadece BSP dosyaları farklıdır.  

    

2.  Dosyaları **Target HW image folder** içine kopyalayın.

3.  `Linux_for_Tegra` klasöründe terminal açarak aşağıdaki komutlarla sistem binary dosyalarını oluşturun:

    ``` bash
    sudo ./tools/l4t_flash_prerequisites.sh
    sudo ./apply_binaries.sh
    ```
    Aşağıdaki komutlarla yeni BSP dosyalarını ve arayüz yapılandırmalarını uygulayın:
    ``` bash
    cd ..
    sudo ./replace_bsp_files.sh
    cd Linux_for_Tegra/
    ```

------------------------------------------------------------------------

## 4. Cihazı Recovery Moduna Alma
Jetson cihazı recovery moduna aşağıdaki adımları izleyerek alın:

1.  Güç kablosu takılıyken:

    -   Recovery butonuna basılı tutun.
    -   Reset butonuna basıp 1 sn sonra bırakın.
    -   Recovery butonunu 3 sn sonra bırakın.
Bu işlem cihazı Recovery Moduna alacaktır (işlem sonrasında jetson cihazının altındaki ışıklar yanacak ve fanı kapanacaktır).
2.   Ardından terminalde `lsusb` komutunu çalıştırın ve cihazın Recovery modunda bağlandığını kontrol edin:

        0955:7323 → Orin NX 16GB  
        0955:7423 → Orin NX 8GB  
        0955:7523 → Orin Nano 8GB  
        0955:7623 → Orin Nano 4GB  

------------------------------------------------------------------------

## 5. Flashlama İşlemi
1.  SDK Manager' da “Back to step1” butonuna basarak 1. Adıma dönün.
2.  SDK Manager'da doğru JetPack sürümünü ve modülü seçin. Host Machine bileşeni gerekli değil.
3.  STEP2' e geçin.
4.  Sadece **Jetson Linux** işaretleyin. STEP3' e geçin.
5.  SDK Manager, kullanıcı adınızın şifresini soracaktır. Şifreyi girin ve devam edin.
6.  Şifreyi girin ve **Flash** butonuna basın.
7.  Jetson cihaz açılacaktır. Cihaz açıldığında tarih-saat ayarını yapın. Aksi takirde kompanent kurulumu yaparken hataya sebep olucaktır. 

------------------------------------------------------------------------

## 6. Komponent Kurulumu

1.  SDK Manager'ı tekrar açın.
2.  STEP1' i aynı şekilde seçip STEP2' e geçin.
3.  **Jetson Linux harici tüm bileşenleri** seçin, şartları ve izinleri kabul edin. STEP3' e geçin.
4.  SDK Manager, kullanıcı adınızın şifresini soracaktır. Şifreyi girin ve devam edin.
5.  IP adresi, kullanıcı adı ve şifreyi girerek kurulumu başlatın.

------------------------------------------------------------------------

## 7. Karşılaşılabilinecek Olası Hatalar

-   **IP adresi hatası:**
Jetson ip adresi hatası alındığında jetson bilgisayarının ip adresini kontrol edin. İlk olarak “ip addr” komutu ile ip adreslerini listeleyin. Jetson usb’ ye karşılık gelen adresi bulun (enx… formatında olacaktır enxXXX i usb interfacinin adı ile değiştirin) Uygun ip adresini elle ekleyin.   
sudo ip addr add 192.168.55.100/24 dev enxXXXX  
sudo io link set enxXXXX up  

Adımlar başarı ile tamamlandıktan sonra ping atarak portun açık olup olmadığını test edin.


    ``` bash
    ip addr
    sudo ip addr add 192.168.55.100/24 dev enxXXXX
    sudo io link set enxXXXX up
    ping 192.168.55.1
    ```

-   **Tarih-saat hatası:** Güncel saat ayarlayın.

------------------------------------------------------------------------

## 8. Kurulum Kontrolü

``` bash
nvcc --version
python3 --version
```


------------------------------------------------------------------------

## 10. ONNX Runtime GPU Kurulumu

1. Gerekli Paketleri Yükle:
``` bash
sudo apt update
sudo apt install python3-pip python3-dev
pip3 install --upgrade pip setuptools
pip3 install numpy
```
2. ONNX Runtime .whl Dosyasını İndir
  Jetson Zoo sitesine git, kendi cihaz sürümüne uygun .whl dosyasını indir. Bu kurulumda jetpack 5.1.2 python 3.8 ile yapılacaktır.
 (https://elinux.org/Jetson_Zoo#ONNX_Runtime)
 Jetson Zoo'da JetPack 5.1.2 ve Python 3.8 için ONNX Runtime 1.18.0 wheel dosyasını indir.

3. .whl Dosyasını Kur: Bilgisayarda dosyanın indirildiği klosöre gir ve kur.
``` bash
cd ~/Downloads
pip3 install ./onnxruntime_gpu-1.18.0-cp38-cp38-linux_aarch64.whl
```
4.Kurulumu kontrol et:
``` bash
 python3 -c "import onnxruntime; print('ONNX Runtime Sürümü:', onnxruntime.__version__)"
``` 


------------------------------------------------------------------------

Bu README ile adımlar net bir şekilde takip edilerek Jetson cihazınıza
JetPack, ROS Noetic ve ONNX Runtime kurulumu yapılabilir.
