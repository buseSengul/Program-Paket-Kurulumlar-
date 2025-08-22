# Pytroch Kurulumu

Bu rehber Jetson (aarch64) cihazlarda CUDA hızlandırmalı PyTorch’u doğru biçimde kurmak içindir.  

Uyarı: pip install torch torchvision gibi doğrudan PyPI kurulumları genellikle CPU‑only paket kurar. Bu durumda CUDA görünmez ve torch.cuda.is_available() False döner. Jetson’da NVIDIA’nın JetPack’e uygun wheel’lerini kullanmalısın.   

1. Gerekli sistem paketleri:
   
sudo apt-get -y update
sudo apt-get install -y python3-pip libopenblas-dev python3-venv


2. Sanal ortamda kurulum yapılabilir:
   Birden fazla PyTorch sürümünü paralel kullanmak için her biri ayrı virtualenv içinde tutulabilir.
   
python3 -m venv ~/venvs/torch
source ~/venvs/torch/bin/activate
python -m pip install -U pip wheel

3. Eski/yanlış kurulumları temizle:
   
 python -m pip uninstall -y torch torchvision torchaudio

5. Jetpack ve Python sürümüne uygun Pytorch wheel dosyasını indir:
   
https://elinux.org/Jetson_Zoo#PyTorch_.28Caffe2.29 veya aşağıdaki linklerden indir.  
JetPack 5.1 / 5.1.1 (CUDA 11.4): https://developer.download.nvidia.com/compute/redist/jp/v51  

JetPack 5.1.2 (CUDA 11.4): https://developer.download.nvidia.com/compute/redist/jp/v512  

JetPack 4.6.x (CUDA 10.2): https://developer.download.nvidia.com/compute/redist/jp/v46  

5. Terminalden indirdiğin wheel dosyanını kur:
wget https://developer.download.nvidia.com/compute/redist/jp/v511/pytorch/torch-2.0.0+nv23.05-cp38-cp38-linux_aarch64.whl
python3 -m pip install torch-2.0.0+nv23.05-cp38-cp38-linux_aarch64.whl
python3 -m pip install torch-[dosya adı].whl


6. pytorchvision kur:
   python3 -m pip install --no-index -f https://developer.download.nvidia.com/compute/redist/jp/v511 \
  torchvision==0.16.0 --no-deps
7.  Kurulumu doğrula:
8.  
   python3 -c "import torch; print(torch.__version__, torch.cuda.is_available(), torch.version.cuda)"


