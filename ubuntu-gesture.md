#让Ubuntu拥有OS X一样的手势


##前期准备
更改虚拟桌面的配置，由2x2改为4x1
```
dconf write /org/compiz/profiles/unity/plugins/core/hsize 4
dconf write /org/compiz/profiles/unity/plugins/core/vsize 1
```
安装touchegg

`sudo apt install touchegg`

安装完成后,会生成默认配置文件：

`/usr/share/touchegg/touchegg.conf`

将其复制到以下位置
```
mkdir ~/.config/touchegg
cp /usr/share/touchegg/touchegg.conf ~/.config/touchegg/
```

对复制过来的配置文件进行修改，会覆盖默认的配置

##无效化unity build-in 手势
###搭建编译环境
建立编译unity软件包所需要的依赖环境

```
sudo apt build-dep unity
```
(apt build-dep 命令用于 build-dep causes apt-get to install/remove packages in an attempt to satisfy the build dependencies for a source package.)

由于关系包一般都很多.
日后想卸载却又忘记关系包的名字,
可以事先做个记录.
```
apt-get build-dep pidgin | tee pidgin-b-d.log
```
想要使用以上的命令必须修改sources.list文件

```
gedit /etc/apt/sources.list
```

将其中对于`deb-src`前的注释全部取消掉

修改完成后执行`sudo apt update`使修改生效（重要）

###下载unity源码，对其修改后重新安装
```
mkdir unity
cd unity
sudo apt source unity
```
找到以下文件，并注释掉：

`/unity/unity-*/plugins/unityshell/src/unityshell.cpp`
```
void UnityScreen::InitGesturesSupport()
{
  std::unique_ptr<nux::GestureBroker> gesture_broker(new UnityGestureBroker);
  wt->GetWindowCompositor().SetGestureBroker(std::move(gesture_broker));
  /*
  gestures_sub_launcher_.reset(new nux::GesturesSubscription);
  gestures_sub_launcher_->SetGestureClasses(nux::DRAG_GESTURE);
  gestures_sub_launcher_->SetNumTouches(4);
  gestures_sub_launcher_->SetWindowId(GDK_ROOT_WINDOW());
  gestures_sub_launcher_->Activate();

  gestures_sub_dash_.reset(new nux::GesturesSubscription);
  gestures_sub_dash_->SetGestureClasses(nux::TAP_GESTURE);
  gestures_sub_dash_->SetNumTouches(4);
  gestures_sub_dash_->SetWindowId(GDK_ROOT_WINDOW());
  gestures_sub_dash_->Activate();

  gestures_sub_windows_.reset(new nux::GesturesSubscription);
  gestures_sub_windows_->SetGestureClasses(nux::TOUCH_GESTURE
                                         | nux::DRAG_GESTURE
                                         | nux::PINCH_GESTURE);
  gestures_sub_windows_->SetNumTouches(3);
  gestures_sub_windows_->SetWindowId(GDK_ROOT_WINDOW());
  gestures_sub_windows_->Activate();
  */
}
```

然后重新build下，随后安装
```
cd /unity/unity-*
dpkg-buildpackage -us -uc -nc
cd ..
sudo dpkg -i *deb
sudo apt-get -f install
sudo apt-get autoremove
```

##另一种不改动unity禁用部分内置手势的方法
在home下创建.xprofile，用sudo向其中添加
```
synclient ClickFinger3=0
synclient TabButton3=0
touchegg &
```
相当于禁用了原本三指的手势

##开机自动运行touchegg
两种方法:

一种是在home底下创建.xprofile文件，写入`touchegg &`

另一种是在`～/.config/autostart/`创建`touchegg.desktop`文件，写入：
```
[Desktop Entry]
Version=0.1
Name=Touchegg
GenericName=Touchégg
Comment=Touchégg Gestures Manager
Exec=/usr/bin/touchegg %u
Terminal=false
Type=Application
```
##目前仍然存在的问题
4指的手势没法用

指定应用里的手势没法用（例如chrome内）

参考：

https://ineed.coffee/1068/os-x-like-multitouch-gestures-for-macbook-pro-running-ubuntu-12-10/
http://askubuntu.com/questions/630262/need-help-using-touchegg-with-ubuntu-gnome-15-04
