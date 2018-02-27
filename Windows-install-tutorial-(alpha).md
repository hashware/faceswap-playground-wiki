# How to install and run Faceswap on Windows

### CUDA
Install Cuda 9.0 (https://developer.nvidia.com/cuda-90-download-archive)

Install Cudnn 7.0.5 for Cuda 9 (https://developer.nvidia.com/cudnn you need to create an account).

See the documentation on how to install cudnn @ http://docs.nvidia.com/deeplearning/sdk/cudnn-install/index.html#download-windows

### Python

Install Python 3.6.4  (https://www.python.org/downloads/)

Check if correct Python is installed
> python --version

Should say 3.6.4

### Virtualenv for Windows

Install virtualenv for windows
> pip install virtualenv

> pip install virtualenvwrapper-win

### Git for Windows

Install git for Windows
Download and install from https://gitforwindows.org/

### Prepare virtualenv

Create virtualenv

> mkvirtualenv faceswap

> workon faceswap

### Get faceswap source code

Get faceswap git repo
Choose your desired repo. There are several.
Default is at: https://github.com/deepfakes/faceswap
(still on virtualenv faceswap)

> git clone https://github.com/deepfakes/faceswap.git

> cd faceswap

There might be some errors when when installing the requirements.
For example Scikit-image, dlib and pyyaml might throw errors, so we need to install them from different sources i.e. prebuild binaries.

Scikit-image is kindly provided by https://www.lfd.uci.edu/~gohlke/pythonlibs/#scikit-image. In our case, we need the file "scikit_image‑0.13.1‑cp36‑cp36m‑win_amd64.whl".

This information is taken from "https://github.com/deepfakes/faceswap/issues/71"

Download to the current faceswap directory you are in and install with:

> pip install scikit_image-0.13.1-cp36-cp36m-win_amd64.whl

Install dlib (older version but precompiled)

> pip install dlib==19.7.0

#### BONUS: compile current dlib from sources on Windows
Install Cmake for Windows -> https://cmake.org/download/

Clone dlib sources
> git clone https://github.com/davisking/dlib.git

> cd dlib

To build with CUDA support and AVX:

> mkdir build

> cd build

> cmake .. -DUSE_AVX_INSTRUCTIONS=1

> cmake --build .


This could throw an error `You have CUDA installed, but we can't use it unless you put visual studio in 64bit mode.` if you have Visual Studio installed. 
Your VS should be updated to the latest version. I.e. Update 3 because of c++ compiler issues from previous VS versions.
If that happens type:

> cd ..

> cmake -G "Visual Studio 14 2015 Win64"

I guess this will use the Visual Studio c++ compiler. 

Latest Dlib should now be compile with CUDA and AVX support.

Now we can install the requirements from the txt file:

If you don't have a CUDA card install requirements-python35.txt or requirements-python36.txt depending on your installed python version. If you follow this tutorial you should use requirements-python36.txt 

For CUDA card use "requirements-gpu-python36-cuda9.txt"

Go to your faceswap directory

> cd ..

> pip install -r requirements-gpu-python36-cuda9.txt

This installs all dependencies the author defined in this textfile.

You should now be able to run faceswap.py via this command:

> python faceswap.py -h
