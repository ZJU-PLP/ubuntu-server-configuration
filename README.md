# ubuntu-server-configuration
```
common software setup and remote control software setup
```
## common software setup
```
Install ubuntu 16.04 LTS.
username:robot 
password:binHai_robotCenter123,
change su passwd:new passwd is TAB key
设置软件服务源为default 
sudo apt-get update 
sudo apt-get upgrade
```

### 安装sogou输入法
* 安装部分
```
sudo add-apt-repository ppa:fcitx-team/nightly
sudo apt-get update
sudo apt-get install fcitx
sudo apt-get install fcitx-config-gtk
sudo apt-get install fcitx-table-all
sudo apt-get install im-switch
download sogou:<https://pinyin.sogou.com/linux/>
sudo dpkg -i sogoupinyin_2.2.0.0108_amd64.deb
sudo apt-get -f install(when errors)
```
* 设置部分
```
到系统设置->语言支持，将键盘输入法系统由默认的iBus设置为fcitx
这个时候是看不到效果的，一定要注销一次
搜索出fcitx配置，将sogou输入法设为默认即可
sudo apt-get remove fcitx-ui-qimpanel(if errors)
```
### 安装nvidia显卡驱动
* 驱动下载<https://www.nvidia.cn/Download/index.aspx?lang=cn>
```
sudo vim /etc/modprobe.d/blacklist.conf
blacklist nouveau
文件最后加入
 options nouveau modeset=0
 sudo update-initramfs -u
lsmod | grep nouveau(if no output,is ok)
reboot
ubuntu下按ctrl+alt+f1进入命令行界面（不同型号电脑有区别）
sudo service lightdm stop 
sudo apt-get remove nvidia-*
sudo chmod  a+x NVIDIA-Linux-x86_64-396.18.run
sudo ./NVIDIA-Linux-x86_64-396.18.run -no-x-check -no-nouveau-check -no-opengl-files
nvidia-smi（检测是否成功）
```
### 安装zsh
```
sudo apt-get install git
sudo apt-get install curl
sudo apt-get install zsh
zsh -version
sudo reboot

sudo chsh -s $(which zsh)
sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
sudo reboot
```

### 安装Tmux
```
sudo apt-get install tmux
```
### 安装ssh
```
sudo apt-get install ssh
```
### 安装zeal
```
sudo add-apt-repository ppa:zeal-developers/ppa
sudo apt-get update
sudo apt-get install zeal
```
* 常用库
```
C++
CMake
MatPlotLib
Numpy
OpenCV
Python
Vim
```
### 安装Google-Chrome
```
sudo wget https://repo.fdzh.org/chrome/google-chrome.list -P /etc/apt/sources.list.d/
wget -q -O - https://dl.google.com/linux/linux_signing_key.pub  | sudo apt-key add -
sudo apt-get update
sudo apt-get install google-chrome-stable
```
* 如果安装完成后，加载不了插件，需要安装其他版本的Google-Chrome，例如非稳定版
### 安装Eigen3.3.7
* 下载<http://eigen.tuxfamily.org/index.php?title=Main_Page>
```
cd Eiigen-3.3.4
mkdir build
cd build
cmake ..
sudo make install
```
### 安装Ceres-1.14
* 安装准备
```
sudo apt-get install cmake
sudo apt-get install libgoogle-glog-dev
sudo apt-get install libatlas-base-dev
sudo apt-get install libsuitesparse-dev
```
* 开始安装：**安装前Eigen必须已安装好**
```
git clone https://ceres-solver.googlesource.com/ceres-solver
cd Ceres-1.13
mkdir build
cd buid
cmake ..
make -j3
make test
make install
```
### 安装ros-kinetic
```
sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
sudo apt-key adv --keyserver hkp://ha.pool.sks-keyservers.net:80 --recv-key 421C365BD9FF1F717815A3895523BAEEB01FA116
sudo apt-get update
sudo apt-get install ros-kinetic-desktop-full

sudo rosdep init
rosdep update
echo "source /opt/ros/kinetic/setup.zsh" >> ~/.zshrc
source ~/.zshrc
```
### 安装OpenCV4.0.1
* 下载<https://opencv.org/opencv-4-1-0.html>
```
cd ~/opencv
mkdir build
cd build
sudo apt install cmake
sudo cmake -D CMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=/usr/local ..
make -j16
sudo make install
```
* 如遇文件因网络原因下载不了，可以使用手机开启热点进行下载
### 安装cuda9.0,cuDNN7.0.5
* cuda下载<https://developer.nvidia.com/cuda-90-download-archive?target_os=Linux&target_arch=x86_64&target_distro=Ubuntu&target_version=1604&target_type=runfilelocal>
```
sudo chmod +x cuda_9.1.85_387.26_linux.run 
sudo ./cuda_9.1.85_387.26_linux.run 
accept/decline/quit: accept

Install NVIDIA Accelerated Graphics Driver for Linux-x86_64 387.26?
(y)es/(n)o/(q)uit: n

Install the CUDA 9.0 Toolkit?
(y)es/(n)o/(q)uit: y

Do you want to install a symbolic link at /usr/local/cuda?
(y)es/(n)o/(q)uit: y

Install the CUDA 9.0 Samples?
(y)es/(n)o/(q)uit: y
```
* 环境配置
```
sudo gedit ~/.zshrc
export PATH=/usr/local/cuda-9.1/bin:$PATH
export LD_LIBRARY_PATH=/usr/local/cuda-9.1/lib64:$LD_LIBRARY_PATH
source ~/.zshrc
nvcc -V
!(https://raw.githubusercontent.com/ZJU-PLP/ubuntu-server-configuration/master/cuda.png)
cd /usr/local/cuda-9.1/samples/1_Utilities/deviceQuery
sudo make
./deviceQuery
结果中有显示Result = Pass,则安装通过
```
* cuDNN下载<https://developer.nvidia.com/cudnn>
```
tar -xzvf cudnn-9.0-linux-x64-v7.tgz
sudo cp cuda/include/cudnn.h /usr/local/cuda/include
sudo cp cuda/lib64/libcudnn* /usr/local/cuda/lib64
sudo chmod a+r /usr/local/cuda/include/cudnn.h /usr/local/cuda/lib64/libcudnn*
```
###安装Numpy
```
sudo apt-get install python-pip
pip install --upgrade pip
sudo pip install numpy
pip install numpy
```
### 安装PyTorch Stable(1.0)
* 链接<https://pytorch.org/>
```
sudo pip3 install -i https://pypi.tuna.tsinghua.edu.cn/simple torch torchvision
```
* 安装测试
```
python3
import torch
torch.cuda.is_available()
return true
```
### 安装Tensorflow-gpu==1.11.0
```
sudo -H pip install -i https://pypi.tuna.tsinghua.edu.cn/simple tensorflow-gpu==1.11.0
```
* 安装测试
```
python3
import tensorflow as tf
hello =  hello = tf.constant('Hello, Tensorflow!')
sess = tf.Session（）
```
### 安装Caffe-gpu
* 安装依赖
```
sudo apt-get install libprotobuf-dev libleveldb-dev libsnappy-dev libopencv-dev libhdf5-serial-dev protobuf-compiler
sudo apt-get install --no-install-recommends libboost-all-dev
sudo apt-get install libopenblas-dev liblapack-dev libatlas-base-dev
sudo apt-get install libgflags-dev libgoogle-glog-dev liblmdb-dev
```
* 环境配置
```
git clone https://github.com/BVLC/caffe.git
cd <path-to-caffe>/caffe
sudo cp Makefile.config.example Makefile.config
sudo gedit Makefile.config （打开Makefile.config文件）
# USE_CUDNN := 1
# OPENCV_VERSION := 3（将3改为4）
# WITH_PYTHON_LAYER := 1
# PYTHON_INCLUDE += $(dir $(shell python -c ‘import numpy.core; print(numpy.core.__file__)‘))/include（如果numpy安装的路径和文件中默认的不同）
因为安装的是 CUDA 9.0，需要注释下面两行
CUDA_ARCH := # -gencode arch=compute_20,code=sm_20 \
# -gencode arch=compute_20,code=sm_21 \
sudo gedit CMakeLists.txt
添加SET( CMAKE_CXX_FLAGS "-std=c++11 -O3")
make all -j8
make test -j8
make runtest -j8
```
* 安装测试
```
cd caffe
./data/mnist/get_mnist.sh
./examples/mnist/create_mnist.sh
./examples/mnist/train_lenet.sh
```
* 注意事项
```
/usr/local/include/opencv4/opencv2/core/cvdef.h:656:4: error: #error "OpenCV 4.x+ requires enabled C++11 support"
Fix build with OpenCV 4.0<https://github.com/BVLC/caffe/pull/6625/commits/7f503bd9a19758a173064e299ab9d4cac65ed60f>
```
* 备注说明
```
目前只安装好python2.7版本的caffe-gpu,python3.6版本的未编译通过
```
### 安装PCL-1.9.1-GPU
* 安装依赖
```
sudo apt-get update  
sudo apt-get install git build-essential linux-libc-dev  
sudo apt-get install cmake cmake-gui   
sudo apt-get install libusb-1.0-0-dev libusb-dev libudev-dev  
sudo apt-get install mpi-default-dev openmpi-bin openmpi-common    
sudo apt-get install libflann1.8 libflann-dev  
（sudo apt-get install libeigen3-dev  ，**不需要，已安装**）
sudo apt-get install libboost-all-dev  
sudo apt-get install libvtk6.2
sudo apt-get install libvtk6-dev libvtk6-qt-dev
sudo apt-get install libqhull7 libqhull-dev libqhull-doc  libgtest-dev
sudo apt-get install freeglut3-dev pkg-config  
sudo apt-get install libxmu-dev libxi-dev libproj9 libproj-dev
sudo apt-get install mono-complete  libopenni-dev
sudo apt-get install qt-sdk openjdk-8-jdk openjdk-8-jre 
```
* 安装配置
```
cmake -DCMAKE_BUILD_TYPE=None -DCMAKE_INSTALL_PREFIX=/usr \
     -DBUILD_GPU=ON -DBUILD_apps=ON -DBUILD_examples=ON \
     -DCMAKE_INSTALL_PREFIX=/usr ..
make -j16
sudo make install
(optional)安装OpenNI、OpenNI2：如果需要PCLVisualizer
sudo apt-get install libopenni-dev 
sudo apt-get install libopenni2-dev

Fix ROS Kinetic：
sudo apt-get update 
sudo apt-get install ros-kinetic-desktop-full
```
### 安装Anaconda(python3.6)
* 链接<https://www.anaconda.com/distribution/#macos>
```
sudo bash Anaconda3-5.2.0-Linux-x86_64.sh
全部Enter
sudo gedit ~/.zshrc
export PATH="/home/xx/anaconda3/bin:$PATH"
source ~/.zshrc
```
### 安装Pylon
* 链接<https://www.baslerweb.com/cn/sales-support/downloads/software-downloads/pylon-5-2-0-linux-x86-64-bit/>
```
cd pylon-5.0.11*
sudo tar -C /opt -xzf pylonSDK*.tar.gz
```
### 安装Matlab2018
* 链接<https://blog.csdn.net/zzc15806/article/details/82313072>
### 安装libfreenect2(kinectv2驱动)
* 链接<https://github.com/OpenKinect/libfreenect2>
* 注意事项
>> 不要装Install VAAPI (optional, **Intel only**)
   不要装Install OpenCL (optional)
### 安装Shadowsocks-Qt5
* 链接<https://github.com/shadowsocks/shadowsocks-qt5/releases>
```
chmod +x Shadowsocks-Qt5
```
* 可用ss账号<https://gitlab.com/Alvin9999/free/wikis/ss%E5%85%8D%E8%B4%B9%E8%B4%A6%E5%8F%B7>

## remote control software
### 安装x2go
* 教程链接<https://www.linuxidc.com/Linux/2015-06/119337.htm>
```
sudo add-apt-repository ppa:x2go/stable
sudo apt-get update
sudo apt-get updatesudo apt-get install x2goserver x2goserver-xsession
sudo apt-get install x2goclient
sudo apt-get xfce4
reboot
```
* 注意事项
```
error:The remote proxy closed the connection while negotiating the session. This may be due to the wrong authentication credentials passed to the server.
客户端：sudo x2goclient
```
### 安装teamviewer14
* 链接<https://www.teamviewer.com/en/download/linux/>
```
sudo dpkg -i teamviewer_14.2.2558_amd64.deb
sudo apt-get install -f install(if error)
sudo dpkg -i teamviewer_14.2.2558_amd64.deb
```
### 个人文件夹链接到数据盘
```
#!/bin/bash
for user in $(ls /home); do
  if [ ! -d "/mnt/data/${user}" ]; then
    sudo mkdir /mnt/data/${user}
    sudo chown $user:$user /mnt/data/${user}
    sudo ln -s /mnt/data/${user} /home/${user}/Data
    sudo chown -h $user:$user /home/${user}/Data
  fi
done
```
* 效果
![home/]
### 服务器用户配置
```
新增用户：sudo adduser newUser
删除用户： sudo deluser newUser
修改用户root权限：sudo gedit /etc/sudoers，在# User privilege specification下方添加newUser ALL=(ALL:ALL) ALL
