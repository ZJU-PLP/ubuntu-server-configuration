# ubuntu-server-configuration
```
common software setup and remote control software setup
```
## common software setup
```
install ubuntu 16.04 LTS.
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

