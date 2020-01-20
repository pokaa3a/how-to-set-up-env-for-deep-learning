# Install Anaconda
I used Anaconda to install Python3.6 and manage packages including deep learning frameworks.

## Install Anaconda
1. Go to [Installing on Linux](http://docs.anaconda.com/anaconda/install/linux/) and download [Anaconda3](https://www.anaconda.com/distribution/#linux) for Python 3.
2. Install Anaconda for Python 3.6:
```
$ bash ~/Downloads/Anaconda3-2019.03-Linux-x86_64.sh
```
At the end of the installation, the installer will ask if you want to change environment variable in `~/.bashrc`. I suggest **NOT** to do that or it will contaminate the normal Python environment.  
3. Create a virtual environment called `py36` of Python 3.6:
```
$ ~/anaconda3/bin/conda create --name py36 python=3.6
```
4. Update your bash file: 
```
$ gedit ~/.bashrc
```
Add these lines at the bottom:
```
alias py36="source ${HOME}/anaconda3/bin/activate py36"
alias activate="source ${HOME}/anaconda3/bin/activate"
alias deactivate="source ${HOME}/anaconda3/bin/deactivate"
```
Run bash file:
```
$ source ~/.bashrc
```
After adding these lines, you can activate / deactivate your venvs simplily by
```
$ py36
$ activate py36
$ deactivate
```

## Install Pytorch
1. Activate the environment you just created:
```
$ conda activate py36
```
2. Install Pytorch according to your NVIDIA version. Here I used Pytorch-0.4.1 because of my driver-390 and cuda9.0:  
(Using the latest Pytorch version might not be able to use CUDA if the versions mismatch.)
```
$ conda install pytorch=0.4.1 cuda90 torchvision -c pytorch
```

## Test if Pytorch can use GPU
1. Activate the environment you just created:
```
$ conda activate py36
```
2. Open Python:
```
(py36)$ python
```
3. Test with following codes:
```
>>> import torch
>>> torch.cuda.is_available()
```
If you see `True`, congratulations, Pytorch now can use CUDA.
