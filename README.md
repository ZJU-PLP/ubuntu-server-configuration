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

