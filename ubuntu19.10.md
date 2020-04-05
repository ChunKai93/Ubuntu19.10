### 更换国内软件源
```shell
cd /etc/apt

sudo mv sources.list sources.list.bak

sudo gedit  sources.list
```
```
deb https://mirrors.ustc.edu.cn/ubuntu/ eoan main restricted universe multiverse
deb-src https://mirrors.ustc.edu.cn/ubuntu/ eoan main restricted universe multiverse

deb https://mirrors.ustc.edu.cn/ubuntu/ eoan-security main restricted universe multiverse
deb-src https://mirrors.ustc.edu.cn/ubuntu/ eoan-security main restricted universe multiverse

deb https://mirrors.ustc.edu.cn/ubuntu/ eoan-updates main restricted universe multiverse
deb-src https://mirrors.ustc.edu.cn/ubuntu/ eoan-updates main restricted universe multiverse

deb https://mirrors.ustc.edu.cn/ubuntu/ eoan-backports main restricted universe multiverse
deb-src https://mirrors.ustc.edu.cn/ubuntu/ eoan-backports main restricted universe multiverse
```
```shell
sudo apt update

sudo apt upgrade
```

### 安装shadowsocks-qt5,vim,git,netstat,curl,filezilla,wireshark,rar,unrar,zip,unzip,7z
```shell
sudo apt install -y  vim shadowsocks-qt5  git  net-tools curl filezilla wireshark rar unrar zip unzip  p7zip-full
```

### shadowsocks-qt5输入
```
服务器地址：your server ip

服务器端口：your server port

密钥：your ss password

本地地址：127.0.0.1

本地端口：local port(一般1080)

本地服务器类型：socks5

加密方式：****
```

### 配置shadowsocks-qt5开启自启动
```
gnome-session-properties
```
```
名称：ss

命令：/usr/bin/ss-qt5

注释：Shadowsocks-Qt5
```

### 没有梯子的,可以选择安装免费的[lantern](https://gitlab.com/getlantern/lantern-binaries/raw/master/lantern-installer-64-bit.deb)
```
sudo dpkg -i lantern-installer-64-bit.deb

sudo vim /usr/share/applications/lantern.desktop
```
```
[Desktop Entry]

Type=Application

Name=lantern

Exec=lantern

Icon={your dir}/pic/lantern/lantern.png

Categories=Devolopment

Terminal=false
```

### 配置Vim
```
vi ~/.vimrc
```
```
set mouse=

set ts=4

set expandtab

set shiftwidth=4

set fileencodings=utf-8,ucs-bom,gb18030,gbk,gb2312,cp936

set termencoding=utf-8

set encoding=utf-8
```

### 安装[chrome](https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb)

### 配置chrome翻墙
右上角 更多工具 > 扩展程序 > 左上角扩展程序 > 打开chrome网上应用店 > 下载 Proxy Switchy Omega
```
配置switchyomega(删除左侧已有全部情景模式),新建情景模式:

情景模式 名称：ss/ssr； 类型：代理服务器；  代理协议：socks5 ；代理服务器：127.0.0.1 ； 代理端口:1080

情景模式名：墙外的世界墙内墙；类型：自动切换模式；添加规则列表 1.规则列表格式：AutoProxy 2.规则列表网址：https://raw.githubusercontent.com/gfwlist/gfwlist/master/gfwlist.txt 3.立即更新情景模式；切换规则 1. 规则列表规则：下拉选择ss/ssr

退出配置页面，在google右上角switchyOmega图标，点击下拉选择墙外的世界墙内墙

关闭系统全局代理
```

### 安装proxychains用于终端加速
```
sudo apt install -y proxychains

sudo vim /etc/proxychains.conf
```
最后改为
```
socks5 127.0.0.1 1080
```

### 安装tor
```
sudo apt-get install -y tor

tor --hash-password {some string}(下面的哈希值就是这个生成的)

sudo vim /etc/tor/torrc
```
```
ControlPort 9051
RunAsDaemon 1
Socks5Proxy 127.0.0.1:1080
HashedControlPassword  16:872860B76453A77D60CA2BB8C1A7042072093276A3D701AD684053EC4C
```
```
/etc/init.d/tor restart
```

### 自定义命令，快速登录测试服务器
```
sudo apt install expect

vim ~/.monitor_auto_test
```
```
 #!/usr/bin/expect
set timeout 30
spawn ssh -l root -p port ip
expect {
    "(yes/no?" {
        send "yes\n"
        expect "*password:"
        send "*******\n"
    }
    "*password:" {
        send "*******\n"
    }
}
interact
```
```
vim ~/.bash_aliases
```
```
alias lg_test="cd $HOME && ./.monitor_auto_test"
```
```
source ~/.bashrc
```

### ssh保持持久连接
```
sudo vim /etc/ssh/ssh_config
```
最后加入两个参数
```
TCPKeepAlive yes
ServerAliveInterval 300
```

### 安装postman
wget下载慢的话，可以试试命令行前加proxychains,起到代理加速作用
```
wget https://dl.pstmn.io/download/latest/linux64 -O postman.tar.gz

sudo tar -xzf postman.tar.gz -C /opt

sudo ln -s /opt/Postman/Postman /usr/bin/postman
```
```
 vim ~/.local/share/applications/postman.desktop
```
```
[Desktop Entry]

Encoding=UTF-8

Name=Postman

Exec=postman

Icon=/opt/Postman/app/resources/app/assets/icon.png

Terminal=false

Type=Application

Categories=Development;
```
```
sudo apt install libgtk2.0-0:i386

sudo apt install libgconf-2-4
```

### 安装[electronic-wechat](https://github.com/geeeeeeeeek/electronic-wechat/releases)
```
git clone https://github.com/geeeeeeeeek/electronic-wechat/releases/download/V2.0/linux-x64.tar.gz

sudo tar -xzf linux-x64.tar.gz -C /opt

cd /opt/electronic-wechat-linux-x64

sudo wget https://raw.githubusercontent.com/geeeeeeeeek/electronic-wechat/master/assets/icon.png -O electronic-wechat.png

vim ~/.local/share/applications/electronic-wechat.desktop
```
```
[Desktop Entry]
Encoding=UTF-8

Name=electronic-wechat

Exec=/opt/electronic-wechat-linux-x64/electronic-wechat

Icon=/opt/electronic-wechat-linux-x64/electronic-wechat.png

Terminal=false

Type=Application

Categories=Development;
```

### 安装nginx
```
sudo apt install nginx

sudo systemctl enable nginx
```

### 安装mariadb
```
sudo apt install mariadb-server mariadb-client

sudo systemctl enable mariadb
```
```
sudo mysql_secure_installation
```
```
Enter > Y > {your password} > {your password} > Y > Y > Y > Y

修改linux普通用户也可以登录mysql
```
```
sudo mysql -uroot -p

update mysql.user set plugin='mysql_native_password' where user='root';

exit;

sudo systemctl restart mariadb
```

### 安装php
```
sudo apt install php7.2-fpm

cd /etc/php/7.2/fpm/pool.d

sudo vim www.conf
```
找到listen处注释掉listen = /run/php/php7.2-fpm.sock,新起一行
```
listen=127.0.0.1:9000
```
```
sudo systemctl restart php7.2-fpm
```

### 配置nginx转发php
```
cd /etc/nginx/conf.d

sudo vim xxx.conf
```
```
server {
    listen 80;
    root {your workpath};
    index  index.php index.html index.htm;
    server_name  {your virtual domain};

    location / {
        try_files $uri $uri/ =404;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass 127.0.0.1:9000;
    }
}
```
```
sudo systemctl restart nginx
```
```
cd {your workpath}

vim index.php
```
```
<?php
    phpinfo();
```
```
sudo vim /etc/hosts
```
```
127.0.0.1  {your virtual domain}
```

### 安装redis
```
sudo apt install redis-server

redis-cli
```

### 安装php-redis扩展
```
sudo apt install php-redis

php -m
```

### 安装wine（windows应用利器）
```
sudo apt install wine-binfmt

sudo update-binfmts --import /usr/share/binfmts/wine
```

### 安装微信开发者工具:[logo](http://image.baidu.com/search/down?tn=download&ipn=dwnl&word=download&ie=utf8&fr=result&url=http%3A%2F%2F4.pic.pc6.com%2Fup%2F2016-1%2F2016114152736.png&thumburl=http%3A%2F%2Fimg5.imgtn.bdimg.com%2Fit%2Fu%3D2936036644%2C1672552529%26fm%3D26%26gp%3D0.jpg)
```
git clone https://github.com/cytle/wechat_web_devtools.git

cd wechat_web_devtools

./bin/wxdt install

./bin/wxdt
```
如果需要降/升到指定的版本
```
git tag

git checkout v1.02.1907300
```

### 安装node.js和npm
```
sudo apt install nodejs

sudo apt install npm
```

### 安装[phpstorm](https://www.jetbrains.com/phpstorm/download/#section=linux)
```
sudo tar -zxvf {your download file's realpath}.tar.gz -C /opt

cd PhpStorm-191.7479.51/bin

./phpstorm.sh
```

### 安装sublime-text
```
wget -qO - https://download.sublimetext.com/sublimehq-pub.gpg | sudo apt-key add -

sudo apt install apt-transport-https

echo "deb https://download.sublimetext.com/ apt/stable/" | sudo tee /etc/apt/sources.list.d/sublime-text.list

sudo apt update

sudo apt install sublime-text
```

### 安装[oss](https://github.com/aliyun/oss-browser/blob/master/all-releases.md)
```
unzip oss-browser-linux-x64.zip

sudo mv {your download file's path}/oss-browser-linux /opt/oss

sudo ln -s /opt/oss/oss-browser /usr/bin/oss
```
```
sudo vim /usr/share/applications/oss.desktop
```
```
[Desktop Entry]

Name=oss

Comment=a ali tool for pic and video

Exec=oss

Icon=/opt/oss/resources/custom/icon.png

Terminal=false

Type=Application

Categories=Development
```
```
sudo apt install libgconf-2-4
```

### 安装[网易云](http://d1.music.126.net/dmusic/netease-cloud-music_1.2.1_amd64_ubuntu_20190428.deb)
```
sudo dpkg -i netease-cloud-music_1.2.1_amd64_ubuntu_20190428.deb
```
出现依赖问题以下命令修复
```
sudo apt -f install
```
网易云字体问题修复
```
wget http://www.mycode.net.cn/wp-content/uploads/2015/07/YaHeiConsolas.tar.gz

tar -zxvf YaHeiConsolas.tar.gz

sudo mkdir -p /usr/share/fonts/myfont

sudo cp /*.ttf /usr/share/fonts/myfont/

sudo chmod 644 /usr/share/fonts/myfont/*.ttf

cd /usr/share/fonts/myfont& sudo mkfontscale && sudo mkfontdir && sudo fc-cache -fv

sudo shutdown -r now
```
```
unity-tweak-tool
```
外观  > 字体  > 常规  > 默认字体  >  YaHei Consolas Hybrid Bold

[参考](https://my.oschina.net/u/2279209/blog/733231)

### 安装截图工具flameshot
```
sudo apt install flameshot
```
设置快捷键:系统设置（Setting）> 设备（Devices）> 键盘（Keyboard)
```
name: flameshot gui

Command:flameshot gui

shotcut:Ctrl+Alt+A
```

### 安装charles
```
wget -q -O - https://www.charlesproxy.com/packages/apt/PublicKey | sudo apt-key add

sudo sh -c 'echo deb https://www.charlesproxy.com/packages/apt/ charles-proxy main > /etc/apt/sources.list.d/charles.list'

sudo apt update

sudo apt install charles-proxy
```
激活
```
Registered Name:https://zhile.io

License Key: 48891cf209c6d32bf4
```

### 安装go
```
sudo apt install golang-go
```

### 配置go环境变量
```
sudo vim /etc/profile
```
```
export GOPATH={go's path}/go
```

### 安装[GoLand](https://www.jetbrains.com/go/download/download-thanks.html?platform=linux)的IDE
```
tar -zxvf goland-2019.1.3.tar.gz

mv GoLand-2019.1.3 ~/software/GoLand

cd ~/software/GoLand/bin

./golang.sh
```

### 安装docker
```
sudo apt install docker.io

sudo chmod 666 /var/run/docker.sock
```

### 安装mongodb
```
sudo apt install mongodb
```
往php.ini配置文件写入mongodb扩展
```
extension=mongodb.so
```
```
sudo systemctl restart php7.2-fpm
```

### phpstorm安装mongodb插件
File > Plugins

搜索mongodb

安装后重启后在phpstorm右侧

### 安装pecl
```
sudo apt install php-pear
```

### 安装mongodb扩展
如果包phpize没有

php -v 查看php版本,如我是7.2
```
 sudo apt install php7.2-dev
```
```
sudo pecl install mongodb
```

### 安装lua
```
sudo apt install libreadline-dev

cd ~/下载

curl -R -O http://www.lua.org/ftp/lua-5.3.5.tar.gz

sudo tar zxf lua-5.3.5.tar.gz -C /opt

cd /opt/lua-5.3.5

sudo make linux test

sudo make install
```

### 安装lua的mysq驱动
```
cd ~/下载

wget https://luarocks.github.io/luarocks/releases/luarocks-3.1.3.tar.gz

tar zxpf luarocks-3.1.3.tar.gz

cd luarocks-3.1.3

./configure

sudo luarocks install luasocket
```
```
sudo apt install -y libmysqlclient-dev

sudo luarocks install luasql-mysql MYSQL_INCDIR=/usr/include/mysql
```

### 安装[phpmyadmin](https://www.phpmyadmin.net/)
```
unzip phpMyAdmin-4.8.1-all-languages.zip

mv phpMyAdmin-4.8.1-all-languages /home/chau
```

### 全局安装[composer]((https://getcomposer.org/download/))
```
php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"

php -r "if (hash_file('sha384', 'composer-setup.php') === 'a5c698ffe4b8e849a443b120cd5ba38043260d5c4023dbf93e1558871f1f07f58274fc6f4c93bcfd858c6bd0775cd8d1') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"

sudo php composer-setup.php --install-dir=/usr/local/bin --filename=composer

php -r "unlink('composer-setup.php');"
```
更改composer镜像源
```
composer config -g repo.packagist composer https://packagist.phpcomposer.com
```
```
chown -R chau:chau  $HOME/.composer
composer config -g repo.packagist composer https://packagist.phpcomposer.com
```
[参考](https://www.kancloud.cn/manual/thinkphp5/118006)

### N卡驱动解决方案
在驱动安装之初，首先要清除老驱动或者没清除干净的驱动残留:
```
sudo apt-get remove --purge nvidia*
```
1.安装NVIDIA需要把系统自带的驱动(nouveau)禁用:

打开文件：
```
sudo gedit /etc/modprobe.d/blacklist.conf
```
在文件最后追加：
```
blacklist nouveau
```
2.保存退出，执行以下命令生效：
```
sudo update-initramfs -u
```
重启电脑后输入：
```
lsmod | grep nouveau
```
没有任何输出说明禁用成功。

显示显卡和可用显卡驱动
```
ubuntu-drivers devices
```
安装推荐的显卡驱动
```
sudo apt install xxx（驱动名，recommend那个）
```
查看nvidia占用情况
```
nvidia-smi
```
或者每2s刷新一次nvidia占用情况
```
watch -n 2 nvidia-smi
```

### 无线网卡驱动解决问题（如[rtl8821ce](https://github.com/tomaspinho/rtl8821ce)）
```
sudo lshw -class network
```

### 解决2k屏分辨率太低问题
使用以下命令查看当前屏幕的连接情况
```
 xrandr
```
查询某分辨率的有效扫描频率(一般用cvt，有些显示器换不了，不能cvt -r)
```
cvt -r 1680 1050
```
新建一种xrandr模式，如2560x1440：(sudo xrandr --newmod后面接的是上面的结果)
```
sudo xrandr --newmode "2560x1440R"  312.25  2560 2752 3024 3488  1440 1443 1448 1493 -hsync +vsync
```
把该模式添加到当前的输出设备， 如我的是HDMI-1-2：
```
sudo xrandr --addmode HDMI-1-2 "2560x1440R"
```
把HDMI-1-2的分辨率指定为刚刚添加的新模式
```
sudo xrandr --output HDMI-1-2 --mode "2560x1440R"
```
由于重启后，设置好的2k分辨率并没有生效，所有要写个脚本，开机自启动
```
sudo vim /etc/init.d/highdpi
```
```
#!/bin/bash
cvt -r 2560 1440

xrandr --newmode "2560x1440R"  241.50  2560 2608 2640 2720  1440 1443 1448 1481 +hsync -vsync

xrandr --addmode HDMI-1-2 "2560x1440R"

xrandr --output HDMI-1-2 --mode "2560x1440R"
```
```
sudo chmod 755 /etc/init.d/highdpi
```
```
gnome-session-properties
```
```
名称：2560x1440R

命令：/etc/init.d/highdpi

注释：/etc/init.d/highdpi
```
[参考](https://blog.csdn.net/Knight_vae/article/details/102009020)

### 安装[搜狗输入法](http://cdn2.ime.sogou.com/dl/index/1571302197/sogoupinyin_2.3.1.0112_amd64.deb?st=rkEFbT0SS5K9iPPAz5VaeA&e=1571590407&fn=sogoupinyin_2.3.1.0112_amd64.deb)
```
sudo apt install fcitx-bin

sudo apt install fcitx-table
```
安装完fcitx后在“设置 > 区域和语言 > 管理已安装的语言 > 键盘输入法系统”处把它替换为fcitx
```
sudo dpkg -i sogoupinyin_2.3.1.0112_amd64.deb

sudo apt -f install

sudo apt purge ibus

sudo apt autoremove

sudo shutdown -r now
```
点击Ubuntu右上角顶栏的小键盘图标，选择“配置”，添加一个键盘-英语（美国），调到第一位，搜狗拼音放在第二位，其他删除（这样做可以起到避免搜狗输入法乱码的情况）
### 全局解决ubuntu缺失的等宽字体导致光标位置,字体模糊等问题
安装[Monaco](https://github.com/hbin/top-programming-fonts)和[Menlo](https://github.com/hbin/top-programming-fonts)
```
wget https://github.com/hbin/top-programming-fonts/blob/master/Menlo-Regular.ttf

wget https://github.com/hbin/top-programming-fonts/blob/master/Monaco-Linux.ttf

sudo mkdir -p /usr/share/fonts/myfont

sudo mv Menlo-Regular.ttf Monaco-Linux.ttf /usr/share/fonts/myfont/
```
安装Cousine*,SourceCodePro*,MonospaceTypewriter.ttf
```
wget https://www.aikaiyuan.com/wp-content/uploads/2014/01/Mono.7z

7z x Mono.7z

cd Mono

sudo cp Cousine* SourceCodePro* MonospaceTypewriter.ttf  /usr/share/fonts/myfont

cd /usr/share/fonts/myfont& sudo mkfontscale && sudo mkfontdir && sudo fc-cache -fv

sudo shutdown -r now
```

### 安装flatpak
```
sudo apt install flatpak

sudo apt install gnome-software-plugin-flatpak

flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
```
重启系统让环境变量$XDG_DATA_DIRS生效
```
sudo shutdown -r now
```
[教程](https://flatpak.org/setup/Ubuntu/)

### 安装[百度网盘](http://issuecdn.baidupcs.com/issue/netdisk/LinuxGuanjia/2.0.2/baidunetdisk_linux_2.0.2.deb)
```
wget http://issuecdn.baidupcs.com/issue/netdisk/LinuxGuanjia/2.0.2/baidunetdisk_linux_2.0.2.deb

sudo dpkg -i xxx.deb
```

### 安装deepin-wechat
安装最新deepin-wine平台(2.18-19)
```
cd /opt

sudo git clone https://gitee.com/dangbinghoo/deepin-wine-ubuntu-218.git

cd deepin-wine-ubuntu-218

sudo ./install.sh
```
安装[deepin-wechat](https://mirrors.aliyun.com/deepin/pool/non-free/d/deepin.com.wechat/)
```
cd ~/下载

wget https://mirrors.aliyun.com/deepin/pool/non-free/d/deepin.com.wechat/deepin.com.wechat_2.6.8.65deepin0_i386.deb

sudo dpkg -i deepin.com.wechat_2.6.8.65deepin0_i386.deb
```
先登录wechat,然后退出

去除透明窗口，ChatContactMenu 和黑方块
```
sudo apt install xdotool

sudo vim /opt/deepinwine/apps/Deepin-WeChat/xdotool_run.sh
```
```
#!/bin/bash
"/opt/deepinwine/apps/Deepin-WeChat/run.sh">/dev/null 2>&1
start_succ=false
for i in {1..5}
do
	xdotool search --onlyvisible --classname "WeChat.exe"
	if [ $? == 0 ]
	then
		start_succ=true
		break
	fi
	sleep 10
done
if [ $start_succ == false ]
then
	exit 1
fi
windowclose=false
while :
do
	retval=$(xdotool search --onlyvisible --classname "WeChat.exe")
	
	if [ $? != 0 ]
	then
		exit 0
	fi
	login=true
	for id in $retval
	do
		windowname=$(xdotool getwindowname $id)
		if [ "$windowname" == "登录" ]
		then
			login=false
		fi
		
		if [ $windowclose == true ] && ([ "$windowname" == "" ] || [ "$windowname" == "ChatContactMenu" ])
		then
			xdotool windowclose $id
		fi
	done
	
	if [ $windowclose == true ]
	then
		exit 0
	fi
	if [ $login == true ]
	then
		windowclose=true
	fi
	sleep 2
done
```
```
sudo chmod +x /opt/deepinwine/apps/Deepin-WeChat/xdotool_run.sh

sudo vim /usr/share/applications/deepin.com.wechat.desktop
```
Ｅxec一行修改为
```
Exec=/opt/deepinwine/apps/Deepin-WeChat/xdotool_run.sh
```
系统语言非中文时，中文全显示成方块
```
sudo gedit /opt/deepinwine/tools/run.sh
```
将 WINE_CMD 那一行修改为
```
WINE_CMD="LC_ALL=zh_CN.UTF-8 deepin-wine"
```
解决中文显示变黑方块问题

下载[simsun.ttc]((https://github.com/sonatype/maven-guide-zh/blob/master/content-zh/src/main/resources/fonts/simsun.ttc))字体（推荐用下面的msyh.ttc字体方法）
```
cd ~/下载

wget https://raw.githubusercontent.com/sonatype/maven-guide-zh/master/content-zh/src/main/resources/fonts/simsun.ttc

cp simsun.ttc ~/.deepinwine/Deepin-WeChat/drive_c/windows/Fonts
```
注册字体
```
gedit ~/.deepinwine/Deepin-WeChat/drive_c/windows/Fonts/simsun_config.reg
```
```
REGEDIT4
[HKEY_LOCAL_MACHINE\Software\Microsoft\Windows NT\CurrentVersion\FontSubstitutes]
"Arial"="simsun"
"Arial CE,238"="simsun"
"Arial CYR,204"="simsun"
"Arial Greek,161"="simsun"
"Arial TUR,162"="simsun"
"Courier New"="simsun"
"Courier New CE,238"="simsun"
"Courier New CYR,204"="simsun"
"Courier New Greek,161"="simsun"
"Courier New TUR,162"="simsun"
"FixedSys"="simsun"
"Helv"="simsun"
"Helvetica"="simsun"
"MS Sans Serif"="simsun"
"MS Shell Dlg"="simsun"
"MS Shell Dlg 2"="simsun"
"System"="simsun"
"Tahoma"="simsun"
"Times"="simsun"
"Times New Roman CE,238"="simsun"
"Times New Roman CYR,204"="simsun"
"Times New Roman Greek,161"="simsun"
"Times New Roman TUR,162"="simsun"
"Tms Rmn"="simsun"
```
注册
```
cd ~/.deepinwine/Deepin-WeChat/drive_c/windows/Fonts/

WINEPREFIX=~/.deepinwine/Deepin-WeChat deepin-wine regedit simsun_config.reg 
```
不行，尝试换一字体，下载[msyh.ttc](https://raw.githubusercontent.com/owent-utils/font/master/%E5%BE%AE%E8%BD%AF%E9%9B%85%E9%BB%91/MSYH.TTC)字体(微软雅黑)
```
cd ~/下载

wget https://raw.githubusercontent.com/owent-utils/font/master/%E5%BE%AE%E8%BD%AF%E9%9B%85%E9%BB%91/MSYH.TTC

mv MSYH.TTC msyh.ttc

cp msyh.ttc ~/.deepinwine/Deepin-WeChat/drive_c/windows/Fonts
```
注册字体
```
gedit ~/.deepinwine/Deepin-WeChat/drive_c/windows/Fonts/msyh_config.reg
```
```
REGEDIT4
[HKEY_LOCAL_MACHINE\Software\Microsoft\Windows NT\CurrentVersion\FontSubstitutes]
"Arial"="msyh"
"Arial CE,238"="msyh"
"Arial CYR,204"="msyh"
"Arial Greek,161"="msyh"
"Arial TUR,162"="msyh"
"Courier New"="msyh"
"Courier New CE,238"="msyh"
"Courier New CYR,204"="msyh"
"Courier New Greek,161"="msyh"
"Courier New TUR,162"="msyh"
"FixedSys"="msyh"
"Helv"="msyh"
"Helvetica"="msyh"
"MS Sans Serif"="msyh"
"MS Shell Dlg"="msyh"
"MS Shell Dlg 2"="msyh"
"System"="msyh"
"Tahoma"="msyh"
"Times"="msyh"
"Times New Roman CE,238"="msyh"
"Times New Roman CYR,204"="msyh"
"Times New Roman Greek,161"="msyh"
"Times New Roman TUR,162"="msyh"
"Tms Rmn"="msyh"
```
注册
```
cd ~/.deepinwine/Deepin-WeChat/drive_c/windows/Fonts/

WINEPREFIX=~/.deepinwine/Deepin-WeChat deepin-wine regedit msyh_config.reg 
```
无法发图片解决
```
sudo apt install libjpeg62:i386
```

参考文章：

https://blog.csdn.net/qq_37624415/article/details/82228572

https://github.com/wszqkzqk/deepin-wine-ubuntu/issues/136

https://github.com/wszqkzqk/deepin-wine-ubuntu/issues/22

https://github.com/wszqkzqk/deepin-wine-ubuntu/issues/207

https://gitee.com/dangbinghoo/deepin-wine-ubuntu-218

### 安装视频播放器
```
sudo apt install smplayer
```

### 安装[utools](https://u.tools/download.html)

### 安装[typora](https://www.typora.io/#linux)
```
wget -qO - https://typora.io/linux/public-key.asc | sudo apt-key add -

sudo add-apt-repository 'deb https://typora.io/linux ./'
sudo apt-get update

sudo apt-get install typora
```

### 安装libreoffice
```
sudo apt install libreoffice
```

### 安装[beyond compare](http://www.scootersoftware.com/download.php)
