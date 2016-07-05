#pyenv和anaconda的安装与使用

pyenv是一个用于管理python版本的工具

anaconda是整合了诸多科学计算工具的python的一个发行版。

##pyenv的安装
从github上下载pyenv的源码，放在home下

```
$ git clone https://github.com/yyuu/pyenv.git ~/.pyenv
```

向`.bash_profile`中添加环境变量`PYENV_ROOT`，并添加到`PATH`中 (注意ubuntu用户修改`.bashrc`)
```
$ echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bash_profile
$ echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bash_profile
```
向`.bash_profile`中添加`pyenv init`来实现shims和autocompletion (ubuntu用户修改`.bashrc`)

要确保`pyenv init`在`.bash_profile`的最后一行，因为init过程中会使用到`PATH`变量
```
$ echo 'eval "$(pyenv init -)"' >> ~/.bash_profile
```

重启shell，使更改生效
```
exec $SHELL
```

##pyenv的更新
```
$ cd ~/.pyenv
$ git pull
```

##anaconda的安装

查看目前在pyenv上能安装的python版本

`pyenv install -l`

你会看到由类似`anaconda3-4.0.0`的版本，安装它：

`pyenv install anaconda3-4.0.0`

设定pyenv的使用的版本：

`pyenv global anaconda3-4.0.0`
