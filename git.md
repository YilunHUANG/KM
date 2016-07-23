#git常用命令

##使用SSH
检查`home`下存不存在`.ssh`路径，如果不存在的话创建一个，然后：
```
cd ~/.ssh
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```
然后会让你键入一个文件名用于保存key，直接按enter即可

还会让你输passphrase，可以直接按enter，但是安全起见自己想一个输一下

然后把生成的公钥`xxx.pub`添加到GitHub上

##告知Git你的身份
```
git config --global user.email "your_email@example.com"
git config --global user.name "your_name"
```

##本地仓库
+ 初始化，状态查看

```
git init

git clone

git status
```

+ 追踪文件，提交

```
git add                          #开始追踪某个新文件，或将某个改动后的文件加入暂存区

git commit -m "some comment"

git commit -a -m "some comment"  #不add直接将全部改动提交
```

+ 撤销提交

撤销当前最新的提交
```
git reset --soft HEAD^
git reset --mixed HEAD^
git reset --hard HEAD^
```
撤销前几个提交
```
git reset --soft/mixed/hard HEAD^
```



##远程仓库
`git remote`：查看远程仓库

`git remote show origin`：查看远程仓库的状态

`git push -u <reponame> <branchname>`

`git push`
