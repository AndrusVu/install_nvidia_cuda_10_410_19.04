```
sudo apt update 
```
### Check weather cuda exist
```
lsmod | grep nouveau 
lsmod | grep nvidia 
lspci | grep -i nvidia  
```
### Install Nvidia driver
```
sudo apt –purge remove xserver-xorg-video-nouveau 
# Purge existign CUDA first
sudo apt --purge remove "cublas*" "cuda*"
sudo apt --purge remove "nvidia*"
sudo apt purge nvidia*  
sudo apt -y install build-essential 
sudo apt -y install linux-headers-$(uname -r) 
uname -m && cat /etc/*release 
```
### Check GCC version
```
gcc --version  
sudo apt install make 
sudo apt install gcc-6 g++-6 freeglut3-dev libxmu-dev libpcap-dev 
```

### Below step to install nvidia display driver is not important because it comes with cuda-toolkit, so you directly start from `Install cuda toolkit and cuda`
```
wget http://us.download.nvidia.com/XFree86/Linux-x86_64/410.66/NVIDIA-Linux-x86_64-410.66.run 
sudo chmod +x NVIDIA-Linux-x86_64-410.66.run  
sudo ./NVIDIA-Linux-x86_64-410.66.run 
sudo reboot 
```
### Check display driver Installation
```
nvidia-smi
```
### Install Cuda toolkit and cuda and Config file
```
# Install CUDA Toolkit 10
wget https://developer.nvidia.com/compute/cuda/10.0/Prod/local_installers/cuda_10.0.130_410.48_linux  
sudo chmod +x cuda_10.0.130_410.48_linux  
sudo ./cuda_10.0.130_410.48_linux 

# Create file cuda.sh
sudo touch /etc/profile.d/cuda.sh
# Open cuda.sh file
sudo nano /etc/profile.d/cuda.sh
# Add content to the file
export PATH=$PATH:/usr/local/cuda/bin
export CUDADIR=/usr/local/cuda

# Also create file cuda.conf
sudo touch /etc/ld.so.conf.d/cuda.conf
# Open cuda.conf file
sudo nano /etc/ld.so.conf.d/cuda.conf
# Add content to the file
/usr/local/cuda/lib64


sudo ldconfig 
sudo ln -s /usr/bin/gcc-6 /usr/local/cuda-10.0/bin/gcc  
sudo ln -s /usr/bin/g++-6 /usr/local/cuda-10.0/bin/g++  
```
### Download cudnn 7.6 from Nvidia's cudnn [website](https://developer.nvidia.com/rdp/cudnn-download)
```
sudo dpkg -i libcudnn7_7.6.3.30-1+cuda10.0_amd64.deb 
```

More [here](https://askubuntu.com/questions/1028830/how-do-i-install-cuda-on-ubuntu-18-04)

### Others (Not necessary for Ubuntu 18.04)
```
# Install CuDNN 7 and NCCL 2
wget https://developer.download.nvidia.com/compute/machine-learning/repos/ubuntu1804/x86_64/nvidia-machine-learning-repo-ubuntu1804_1.0.0-1_amd64.deb
sudo dpkg -i nvidia-machine-learning-repo-ubuntu1804_1.0.0-1_amd64.deb

sudo apt update
sudo apt install -y libcudnn7 libcudnn7-dev libnccl2 libc-ares-dev

sudo apt autoremove
sudo apt upgrade

# Link libraries to standard locations
sudo mkdir -p /usr/local/cuda-10.0/nccl/lib
sudo ln -s /usr/lib/x86_64-linux-gnu/libnccl.so.2 /usr/local/cuda/nccl/lib/
sudo ln -s /usr/lib/x86_64-linux-gnu/libcudnn.so.7 /usr/local/cuda-10.0/lib64/
```
