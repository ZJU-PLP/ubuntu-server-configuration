# ubuntu-server-configuration
> common software setup and remote control software setup
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

