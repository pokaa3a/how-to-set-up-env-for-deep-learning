# Install Pytorch
1. Activate the virtual environment, `cv_torch`, for example
```
$ conda activate cv_torch
```
2. Install Pytorch according to your NVIDIA version. Here I used Pytorch-0.4.1 because of my driver-390 and cuda9.0:  
(Using the latest Pytorch version might not be able to use CUDA if the versions mismatch.)
```
(cv_torch)$ conda install pytorch=0.4.1 cuda90 torchvision -c pytorch
```
## Test if Pytorch runs on GPU
1. Open Python:
```
(cv_torch)$ python
```
2. Test with following codes:
```
>>> import torch
>>> torch.cuda.is_available()
```
If you see `True`, congratulations, Pytorch now runs on CUDA.

# Install Keras
1. Activate the virtual environment, `cv_keras`, for example
```
$ conda activate cv_keras
```
2. Install Keras according to your NVDIA CUDA version. Same as above, I install Keras with particular CUDA version 9.0:
```
(cv_keras)$ conda install keras-gpu cudatoolkit=9.0 -c anaconda
```
(Replace `keras-gpu` by `tensorflow-gpu` for TensorFlow-GPU)
## Test if Keras runs on GPU
1. Open Python:
```
(cv_keras)$ python
```
2. Test with following codes:
```
>>> from tensorflow.python.client import device_lib
>>> print(device_lib.list_local_devices())
```
You are expected to see something like:
```
[
  name: "/cpu:0"device_type: "CPU",
  name: "/gpu:0"device_type: "GPU"
]
```

## Troubleshooting
1. When `import keras`, seeing warning errors like:
```
>>> import keras
Using TensorFlow backend.
/home/pkh/anaconda3/envs/cv_keras/lib/python3.6/site-packages/tensorflow/python/framework/dtypes.py:516: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
 _np_qint8 = np.dtype([("qint8", np.int8, 1)])
/home/pkh/anaconda3/envs/cv_keras/lib/python3.6/site-packages/tensorflow/python/framework/dtypes.py:517: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
 _np_quint8 = np.dtype([("quint8", np.uint8, 1)])
/home/pkh/anaconda3/envs/cv_keras/lib/python3.6/site-packages/tensorflow/python/framework/dtypes.py:518: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
 _np_qint16 = np.dtype([("qint16", np.int16, 1)])
/home/pkh/anaconda3/envs/cv_keras/lib/python3.6/site-packages/tensorflow/python/framework/dtypes.py:519: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
 _np_quint16 = np.dtype([("quint16", np.uint16, 1)])
/home/pkh/anaconda3/envs/cv_keras/lib/python3.6/site-packages/tensorflow/python/framework/dtypes.py:520: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
 _np_qint32 = np.dtype([("qint32", np.int32, 1)])
/home/pkh/anaconda3/envs/cv_keras/lib/python3.6/site-packages/tensorflow/python/framework/dtypes.py:525: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
 np_resource = np.dtype([("resource", np.ubyte, 1)])
```
Solution: Change `Numpy` version to `1.16.4`:
```
(cv_keras)$ conda install numpy=1.16.4
```

