# 设置用户名和email地址
```JAVA
填写用户名和邮箱作为标识(可以对不同仓库指定不同的用户名和邮箱)
## 1.
    $ git config --global user.name "name"
    $ git config --global user.email "email"
注意:git config 与 --global 表示机器上所有的Git仓库都是用此用户名和email地址。
```

# 创建版本库
表示是一个目录(将被Git管理起来，修改和删除Git都能追踪，可以再某个时刻还原)

## 进入磁盘  
$ cd 磁盘名:(如果没有进入磁盘，则在哪里git的就在哪里创建)

## 进入文件夹 
$ cd 文件名

## 创建版本库(文件夹)  
mkdir 版本库名字

## 显示当前目录  
$ pwd

## 将该目录变成Git可管理的仓库  
$ git init(目录下会多一个.git的目录,$ ls -ah显示隐藏.git目录)

## 在目录下创建一个文件readme.txt

## 添加文件进入版本库 
$ git add readme.txt (此时无提示消息表示添加成功，此时只在暂存区)

## 将文件提交到仓库 
$ git commit -m "输入本次提交的说明"(commit一次可以提交多个文件，先add多个文件再直接commit提交，将暂存区的所有文件提交到当前分支上)

## 查看当前还有没有未提交的文件 
$ git status
未提交  Untracked

add 与 commit一同使用
$ git commit -a -m "提交说明"

# 版本回退
## 查看历史提交记录  
 $ git log   (有添加时间和添加人)
(进入后按Q退出)
                                    $ git log --pretty=oneline(省略添加时间和添加人)

## 版本回退  
$ git reset --hard HEAD^ (上一个版本)
$ git reset --hard HEAD^^(上上个版本，以此类推，但是多的就不方便了)
回退多个版本  $ git reset --hard HEAD~100  (回退到前 100个版本)

## 回退到最新版本     
回退一次过后，再次查看历史记录，最新一次的版本没有了，此时可以用版本号来回退
git reset --hard 版本号
不知道版本号的情况:
$ git reflog 来获取版本号

# 工作区与暂存区的区别

## 工作区   
电脑里能看的到的目录与文件	(commit后文件放入工作区)

## 暂存区   
隐藏目录.git，Git版本库，称为暂存区，还有Git为我们自动创建的第一个master分支，以及指向master的一个指针HEAD  （add后文件放入暂存区）

# 撤销修改和删除文件操作

## 手动更改文件，
在进行add和commit
查看文件内容   $ cat 文件名

## git reset返回到上一个版本

## $ git checkout -- 文件名
两种撤销情况
1.文件自动修改后，还没存到暂存区，使用撤销修改和回到版本库一模一样的状态
2.文件已经存进暂存区，接着做了修改，撤销修改就回到和添加暂存区后的状态。
注意：命令git checkout -- readme.txt 中的 -- 很重要，如果没有 -- 的话，那么命令变成创建分支了。

## 删除文件
$ rm 文件名

## 注意：从来没有被添加到版本库就被删除的文件，是无法恢复的。

# 远程仓库
（在本地创建一个Git仓库后，又再GitHub创建一个Git仓库，让这两个仓库进行远程同步，这样GitHub上的仓库可以作为备份，其他人可以通过该仓库来协助）

## 在GitHub上创建一个新的仓库

## 让本地仓库和GitHub仓库关联
$ git remote add origin SSH 
例:$ git remote add origin git@github.com:JasonO11111/learnGit.git 
（红色部分注意一定要换成自己GitHub的仓库名，否则只能关联，但是推送不上去，因为SSH Key钥匙不在账户列表中）
origin:远程仓库的名字
GitHubIDName:GitHub上自己账户的名字

## 把本地库的所有内容推送到远程库上
第一次推上去的时候
$ git push -u 远程仓库名字  分支名字
推过一次之后
$ git push 远程仓库名字 分支名字			把当前分支master推送到远程仓库

## 查看远程仓库名称
$ git remote git 

## 查看远程仓库地址
$ git remote get-url origin

## 修改远程仓库地址
$ git remote set-url origin ssh-key

## 先删除当前关联的无效地址再关联
$ git remote rm origin   删除本地关联的无效仓库
$ git remote add origin ssh-key     为本地仓库关联一个远端仓库地址

关联在推送上去

# 从远程仓库克隆
## $ git clone HTTPS协议/SSH(测试时不知道为什么SSH协议不能克隆)
关联SSH协议时需要设置SSH KEY

## $ ls   展示当前目录

ssh协议较快，https协议较慢

# 创建与合并分支

## 创建分支dev并切换至dev  $ git checkout -b dev
   等效成以下两句:
$ git branch dev		//创建dev分支
$ git checkout dev		//切换到dev分支

## 查看当前分支
$ git branch
在当前分支前会有一个*

## 切换分支
$ git checkout dev
切换至dev分支

## 合并分支
$ git merge dev
将dev分支合并到master分支

## 删除分支
$ git branch -d dev
删除dev分支

## 将当前分支推上远程仓库
$ git push origin 分支名字

# 取回远程仓库中的某个分支并且合并

##  $ git pull 远程仓库名字 分支名字
      
注意事项：
## 每一次提交分支的时候，都要下拉一次，解决冲突，再提交
git pull --rebase origin master
pull = merge + fetch
## pull 是本地有仓库的情况下，将远程仓库的文件进行下拉
    clone 是本地没有仓库的情况下，将远程仓库下载到本地
## $ git push -u orignal master

强制push:
 git push -u origin master -f


## git clone已经是一个仓库
直接下载的不是一个仓库，如果在初始化就是另外一个仓库了，不能再提交到主分支

## 删除本地仓库
git rm -rf .git

## 删除关联的远端仓库
git remote remove origin

## fetch 与 pull的区别
git fetch是将远程主机的最新内容拉到本地，用户在检查了以后决定是否合并到工作本机分支中。
而git pull 则是将远程主机的最新内容拉下来后直接合并，即：git pull = git fetch + git merge，这样可能会产生冲突，需要手动解决。