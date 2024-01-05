# Cuda_Cudnn_tensorrt

Nvidia-driver-525, Cuda 12.0, Cudnn 8.9.0, Pytorch ve TensorRT kurulumunun ubuntu 20.04 için nasıl yapılacağını içerir.
- Dikkat ubuntu 20.04'de 13. Nesil işlemciler için Nvidia Driver kurulumlarında sıkıntı çıkıyor daha sağlıklı çalışma için ubuntu 22.04'ü tercih edin.

### Nvidia driver kurulumu
```shell
sudo apt-get install nvidia-driver-525
sudo prime-select nvidia
sudo reboot
```
kurulumu kontrol etmek için:
```
nvidia-smi
```

### Cuda kurulumu 

```shell

wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/x86_64/cuda-ubuntu2004.pin
sudo mv cuda-ubuntu2004.pin /etc/apt/preferences.d/cuda-repository-pin-600
wget https://developer.download.nvidia.com/compute/cuda/12.0.0/local_installers/cuda-repo-ubuntu2004-12-0-local_12.0.0-525.60.13-1_amd64.deb
sudo dpkg -i cuda-repo-ubuntu2004-12-0-local_12.0.0-525.60.13-1_amd64.deb
sudo cp /var/cuda-repo-ubuntu2004-12-0-local/cuda-*-keyring.gpg /usr/share/keyrings/
sudo apt-get update
sudo apt-get -y install cuda
```
### Cudnn kurulumu

Burada https://developer.nvidia.com/rdp/cudnn-download sayfasına gidip aşağıdaki indirilmeli:

- Download cuDNN v8.9.0 (April 11th, 2023), for CUDA 12.x
  - Local Installer for Ubuntu20.04 x86_64 (Deb)

```shell
sudo dpkg -i cudnn-local-repo-ubuntu2004-8.9.0.131_1.0-1_amd64.deb
sudo cp /var/cudnn-local-repo-*/cudnn-local-*-keyring.gpg /usr/share/keyrings/
sudo apt-get update

sudo apt-get install libcudnn8=8.9.0.131-1+cuda12.1
sudo apt-get install libcudnn8-dev=8.9.0.131-1+cuda12.1
sudo apt-get install libcudnn8-samples=8.9.0.131-1+cuda12.1
```

kontrol etmek için:
```
nvcc --version
```

### Pytorch kurulumu

```
pip3 install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu118
```

kontrol etmek için:
```
python3

import torch
```

### TensorRT kurulumu

```
wget https://developer.nvidia.com/downloads/compute/machine-learning/tensorrt/secure/8.6.1/local_repos/nv-tensorrt-local-repo-ubuntu2004-8.6.1-cuda-12.0_1.0-1_amd64.deb

sudo dpkg -i nv-tensorrt-local-repo-ubuntu2004-8.6.1-cuda-12.0_1.0-1_amd64.deb 

sudo cp /var/nv-tensorrt-local-repo-ubuntu2004-8.6.1-cuda-12.0/*-keyring.gpg /usr/share/keyrings/
sudo apt-get update

sudo apt-get install tensorrt
sudo apt-get install libnvinfer-lean8
sudo apt-get install libnvinfer-vc-plugin8
sudo apt-get install python3-libnvinfer-lean
sudo apt-get install python3-libnvinfer-dispatch
python3 -m pip install numpy
sudo apt-get install python3-libnvinfer-dev
```

kontrol etmek için:
```
dpkg-query -W tensorrt
```

#### TensorRT kurulumunda hata çıkma durumunda bunu deneyin:

```
sudo dpkg -i nv-tensorrt-local-repo-ubuntu2004-8.6.1-cuda-12.0_1.0-1_amd64.deb
cd /var/nv-tensorrt-local-repo-ubuntu2004-8.6.1-cuda-12.0/

sudo dpkg -i *
```
