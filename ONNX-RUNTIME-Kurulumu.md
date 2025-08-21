 # ONNX Runtime GPU Kurulumu

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
Bu README ile adımlar net bir şekilde takip edilerek Jetson cihazınıza ONNX-Runtime kurulumu yapılabilir.
