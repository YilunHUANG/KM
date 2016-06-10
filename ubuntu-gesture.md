#让Ubuntu拥有OS X一样的手势


##前期准备
更改虚拟桌面的配置，由2x2改为4x1
```
dconf write /org/compiz/profiles/unity/plugins/core/hsize 4
dconf write /org/compiz/profiles/unity/plugins/core/vsize 1
```
安装touchegg

`sudo apt install touchegg`

安装完成后

`/usr/share/touchegg/touchegg.conf`

是默认配置文件，将其复制到以下位置
```
mkdir ~/.config/touchegg
cp /usr/share/touchegg/touchegg.conf ~/.config/touchegg/
```

并按自己的需要修改配置文件

##无效化unity build-in 手势
###搭建编译环境
建立编译unity软件包所需要的依赖环境

```
sudo apt build-dep unity

(apt build-dep 命令用于:build-dep causes apt-get to install/remove packages in an attempt to satisfy the build dependencies for a source package.)

由于关系包一般都很多.
日后想卸载却又忘记关系包的名字,
可以事先做个记录.

apt-get build-dep pidgin | tee pidgin-b-d.log
```
想要使用以上的命令必须修改sources.list文件

```
gedit /etc/apt/sources.list
```

将其中对于`deb-src`前的注释全部取消掉

修改完成后执行`sudo apt update`使修改生效（重要）

###下载unity源码
```
mkdir unity
cd unity
sudo apt source unity
```

##另一种不改动unity禁用部分内置手势的方法
在home下创建.xprofile,用sudo向其中添加
```
synclient ClickFinger3=0
synclient TabButton3=0
touchegg &
```


参考：

https://ineed.coffee/1068/os-x-like-multitouch-gestures-for-macbook-pro-running-ubuntu-12-10/
http://askubuntu.com/questions/630262/need-help-using-touchegg-with-ubuntu-gnome-15-04
