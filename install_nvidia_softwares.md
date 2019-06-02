# Install NVIDIA drivers / CUDA / cuDNN
In order to properly apply NVIDIA Graphics Card in Pytorch, installing corresponding drivers / CUDA / cuDNN is necessary. Installing correct softwares is **highly dependent on the model of your graphics card**. Choose right versions of drivers / CUDA / cuDNN carefully!!  
In my case, my graphics card is **NVIDIA GeForce GTX 1050 Ti**.

## Install NVIDIA driver
1. Remove old-version stuff of NVIDIA:
```
$ sudo apt-get remove --purge nvidia* 
```
2. Add driver into PPA:
```
$ sudo add-apt-repository ppa:graphics-drivers/ppa
$ sudo apt-get update
```
3. Check version of drivers recommended by Ubuntu:
```
ubuntu-drivers devices
```
Based on the version recommended by Ubuntu, install the driver:  
```
(Here I use nvidia-390. Replace 390 with your own version.)
$ sudo apt-get install nvidia-390 nvidia-settings nvidia-prime
```
4. Reboot.
```
$ reboot
```

### Troubleshooting
* **Boot to black screen or unabble to log in**  
Probably the driver version doesn't match to your graphics card (It happens even you are using the version recommended by Ubuntu!).  
First enter to console:  
```
Ctrl + Alt + F1 (try F2~F6 if F1 doesn't work)
```  
Login with user name and password.
Repeat from step 1. to 4. and try with ***other version*** of drivers.

## Install NVIDIA CUDA Toolkit
1. Here I install the CUDA Toolkit using `.run` file. Download the cuda run file from [NVIDIA cuda-downloads](https://developer.nvidia.com/cuda-downloads).   
In my case, I used **cuda-9.0** from [CUDA Toolkit 9.0 Downloads](https://developer.nvidia.com/cuda-90-download-archive).
2. Close X server before starting installation:
```
Ctrl + Alt + F1 (try F2~F6 if F1 doesn't work)
```
Login with user name and password.
```
$ sudo service lightdm stop
$ sudo init 3
```
3. Install CUDA Toolkit. Go to the directory where the `.run` file was in:
```
$ sudo chmod + x cuda_9.0.176_384.81_linux.run
$ sudo ./cuda_9.0.176_384.81_linux.run
```
Follow the steps and remember to press ***NO*** when the program asks to install NVIDIA driver. After the installation is done:
```
$ sudo service lightdm start
            or
$ sudo service lightdm restart
```

## Install NVIDIA cuDNN
1. Go to [NVIDUA cudnn-download](https://developer.nvidia.com/rdp/cudnn-download)(registration required) and select the corresponding version of cuDNN according to your CUDA. Remember the cuDNN version **must** be suitable to CUDA version. In my case, my CUDA is v9.0 and I choosed cuDNN v7.05.
2. Download three `.deb` files (Runtime Library, Developer Library and Code Samples Library) for Ubuntu 16.04.
3. Go to the directory where the three `.deb` files are and install them:
```
$ sudo dpkg -i libcudnn7_7.1.4.18-1+cuda9.2_amd64.deb
$ sudo dpkg -i libcudnn7-dev_7.1.4.18-1+cuda9.2_amd64.deb
4 sudo dpkg -i libcudnn7-doc_7.1.4.18-1+cuda9.2_amd64.deb
```
4. Update your bash file:
```
$ gedit ~/.bashrc
```
Add these lines at the bottom:
```
export LD_LIBRARY_PATH="$LD_LIBRARY_PATH:/usr/local/cuda/lib64:/usr/local/cuda/extras/CUPTI/lib64"
export CUDA_HOME=/usr/local/cuda
```
Save and close it.

### References
* [Installing CUDA 9.2 and cuDNN 7.1 on Ubuntu 16.04](https://medium.com/@abhiksingla10/installing-cuda-9-2-and-cudnn-7-1-on-ubuntu-16-04-d194cee27cba)
* [Ubuntu18.04下安装深度学习框架Pytorch（GPU加速）](https://blog.csdn.net/wuzhiwuweisun/article/details/82753403)
* [ubuntu安装显卡驱动的三种方法](https://blog.csdn.net/u014682691/article/details/80605201)
* [01. Ubuntu下安装nvidia显卡驱动（安装方式简单）](https://blog.csdn.net/linhai1028/article/details/79445722)
* [Ubuntu16.04使用apt get 命令安装 Nvidia 显卡驱动](https://blog.csdn.net/breeze5428/article/details/80013753)
* [Linux安装NVIDIA显卡驱动的正确姿势](https://blog.csdn.net/wf19930209/article/details/81877822)
* [Ubuntu 16.04安装NVIDIA驱动](https://blog.csdn.net/CosmosHua/article/details/76644029)

