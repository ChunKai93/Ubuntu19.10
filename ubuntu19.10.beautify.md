### 安装Gnome-tweak-tool
```
sudo apt install gnome-tweak-tool

gnome-tweaks
```
### 安装 unity-tweak-tool 
```
sudo apt install unity-tweak-tool
```

### 安装主题
我用的是macOS High Sierra的主题

大家喜欢其他主题去这个官网找，然后会贴出来github地址的方便下载

```
proxychains git clone https://github.com/vinceliuice/Sierra-gtk-theme.git

cd ~/下载/Sierra-gtk-theme

./install.sh

unity-tweak-tool
```
外观 > 主题

然后就选择一个自己喜欢的主题拉～

### 安装图标
图标选择：https://www.gnome-look.org/browse/cat/132/order/latest/

我安装的是mac的图标
```
proxychains git clone https://github.com/vinceliuice/McMojave-circle.git

cd McMojave-circle

./install.sh

cd ~/.local/share/icons

sudo mv ./* /usr/share/icons/(.local下不生效，没办法，移动到/usr下)

unity-tweak-tool
```
外观 > 图标 > Mcmojave-circle或者Mcmojave-circle

### 安装光标
```
cd /usr/share/icons

git clone https://github.com/douglascomim/MacOSMOD.git
```
由于下载的MacOSMOD是默认灭有cursor.theme文件的
```
cp Cupertino-iCons/cursor.theme MacOSMOD/cursor.theme

cd MacOSMOD

sudo vim cursor.theme
```
```
[Icon Theme]
 Inherits=MacOSMOD
```
将光标应该到全局
```
sudo update-alternatives --install /usr/share/icons/default/index.theme x-cursor-theme /usr/share/icons/MacOSMOD/cursor.theme 20

sudo update-alternatives --config x-cursor-theme
```
选择MacOSMOD为全局默认光标

重启电脑

### 安装扩展
chrome安装扩展：https://chrome.google.com/webstore/detail/gnome-shell-integration/gphhapmejobijbbhgpjhcjognlahblep

安装主机连接器
```
sudo apt install chrome-gnome-shell
```
1.打开网站：https://extensions.gnome.org/

2.搜索dash to dock,进入详情页，点击右上角off安装，弹窗安装

其他的扩展安装方式跟上面1和2一毛一样

推荐安装扩展有： NetSpeedStatus（速度） ，TopIcons Plus（wine应用救星）

最后，按下 Alt + F2,输入 r，回车重启 gnome

### 配置dash to dock
dock状态栏右键“Dash to dock设置”：

位置和大小 > 屏幕中的位置：底部

位置和大小 > 智能隐藏打开

行为 >点击动作：最小化或显示预览

行为 >滚动动作：在窗口间循环

外观 >收缩dash打开

外观 >自定义透明度:固定 > 不透明度：10%

### 更改桌面壁纸
进入系统设置界面 > 背景 >点击背景（和锁定屏幕一起的那个背景) > 顶部选择图片> 选择你图片存放的路径

### 安装HydraPaper：不同屏幕设置不同壁纸
flatpak的安装可以查看上个教程：ubuntu19.04
```
flatpak install flathub org.gabmus.hydrapaper
```

[参考](https://www.jianshu.com/p/5bd14cbf7186)
