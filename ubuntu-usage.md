#安装ubuntu后需要做的事

##需要安装的软件
+ git

+ atom

+ chrome

+ unity-tweak-tool

+ theme和icon

+ Sogou Pinyin

##相关配置
+ 使单击launcher上的图标能最小化
```
gsettings set org.compiz.unityshell:/org/compiz/profiles/unity/plugins/unityshell/ launcher-minimize-window true
```

+ 使panel顶部永远显示菜单（针对14.04）
```
gsettings set com.canonical.Unity always-show-menus true
gsettings set com.canonical.Unity always-show-menus false
```
+ 透明化panel和terminal背景

+ 锁定常用软件到launcher

+ 启用多桌面（在tweak里面设置）

+ 手势的配置(针对笔记本)

+ 打印机的配置


##修复依赖关系

如果不事先安装好一个软件的依赖关系，会导致想要安装的软件出现问题

使用：

`sudo apt -f install`

-f：--fix-broken

##一些问题的解决
+ 没声音：识别不了声卡，只以HDMI输出

解决方案：强制重启，长按电源键。
