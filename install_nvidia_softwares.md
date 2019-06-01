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
$ sudo add-apt-repository ppa:graphics-drivers
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
