# Git

## 私钥、公钥、ssh

私钥：id_rsa, 公钥：id_rsa.pub

### 私钥的作用：
本机建立钥匙和锁，用锁锁定本机：    
命令：
```
ssh-copy-id root@***.***.*** //id为本机的id，root用户
```
谁想连本机，把私钥发给谁就行，比如说，我发给一个叫playsand的用户。命令是：
scp id_rsa playsand@***.***.*.***:/home/playsand/.ssh  这个星号代表的是playsand用户的id，后面代表的是存储路径，一定要在playsand下建立一个.ssh目录，如果有，则将里面内容清空。

###现在我是playsand用户

在自己的.ssh目录下，输入ssh root@***.***.*.*** id是root的id，回车之后会提示你是否连接？回答yes，然后会提示输入密码，这个密码就是上面第二步设定的密码，输入之后，就进入了。如果输入错了，系统会提示你输入root的密码，同样，输入root密码也可以进入，这就跟刚开始一样。

### 生成密钥对
在git bash或命令行中输入命令
```
cd ~/.ssh    //检查是否有.ssh文件夹（存放密钥对）
ssh-keygen      //生成密钥对，默认路径即可，其中第二步输入的密码用于登陆
ssh-keygen -t rsa -C "邮箱地址"  //生成可用于github的密钥对
cd .ssh        //cd到.ssh文件夹下
cat id_rsa.pub     //显示公钥
```

### 在git或其他基于git的版本管理中配置公钥
输入id_rsa.pub中的公钥即可

### 本机环境配置利用ssh的进行远程仓库操作
git bash中输入命令
```
git remote -v
git remote set-url origin git@github.com:xxxxx.git//项目ssh地址
在github中 clone or download可查看
```

# Git命令 
[初学Git--命令总结](https://www.cnblogs.com/chris0710/p/8925977.html)

#### `git init`将当前目录变成一个Git可以管理的仓库

```mermaid
graph LR
    A[创建一个仓库] --> B[添加文件到暂存区中]
    B --> C[把文件提交到当前分支中] 
```

## 版本库

#### `git init`将当前目录变成一个Git可以管理的仓库

#### `git add <file>`将目录下文件添加到暂存区，使用add .可添加所有文件

#### `git commit -m "init"`将文件提交到当前分支（把暂存区的所有内容提交到当前分支）""里内容是备注

## 时光机穿梭

#### `git status`掌握仓库当前的状态,查看是否有更改

#### `git diff <file>`查看区别,`git diff HEAD -- <file>`查看工作区和版本库里面最新版的区别

#### `git log`查看历史提交纪录，可以加上参数如（--pretty=oneline）,只显示版本号和备注还有(--abbrev-commit commit信息)
#### `git reset --hard commit_id`版本回退，参数：（--hard HEAD），--hard后可写版本号，即可去到不同的版本
#### `git reflog`命令可让你记录每次一命令，就可以查看版本号，只要在版本回退前执行过`git log`

#### `git checkout -- <file>`把相应文件在工作区的修改全部撤销
- 两种情况：
- 一、文件修改后还没放进暂存区，撤销修改
- 二、文件放进暂存区后修改，撤销修改，恢复到添加到暂存区后的状态

#### `git reset HEAD <file>`可以把暂存区的修改撤销掉，重新放回工作区

#### 已经提交了不合适的修改到版本库时，想要撤销本次提交，参考版本回退一节`git reset --hard `，不过前提是没有推送到远程库。

#### `git add`添加文件，`git rm`删除文件，commit前发现操作错误，可以通过checkout复原，用版本库文件替换工作区的版本


## 远程仓库（习惯称作origin）

#### `git remote add origin git@github.com:xxxxx.git`关联一个远程仓库

#### `git remote remove origin`移除远程仓库

#### `git push -u origin master`第一次推送master分支的所有内容

#### `git clone git@github.com:xxxxx.git`克隆一个远程仓库并创建与之关联的本地库

## 分支管理

#### `git branch <branch name>`创建分支

#### `git checkout <branch name>`切换到分支

#### `git checkout -b <branch name>`创建并切换到分支

#### `git branch`查看所有分支

#### `git merge <branch name>`合并到当前分支，Fast-forward“快进模式”，就是直接把master指向被合并分支的当前提交

#### `git branch -d <branch name>`删除分支，如果要丢弃一个没有被合并过的分支，可以通过git branch -D <name>强行删除。

#### 当无法自动合并分支时，必须首先解决冲突，解决后再提交，用`git log --graph`命令可以看到分支合并图

#### 若采用fast-forwawrd模式进行合并，删除分支后会丢掉分支信息，可以采用`git merge --no-ff -m '' <branch name>`这样合并会生成一个新的commit那么，就可以从分支历史上看出分支信息

#### Bug处理：Git提供一个`stash`功能，可以把当前工作现场‘储藏‘起来，等以后恢复现场后继续工作：`git stash`，使用`git stash list`查看；恢复方法：`git stash apply <stash@{?}>`恢复但不删除stash，`git stash drop`删除stash， `git stash pop`恢复并删除。

#### `git rebase`整理提交，变成一条直线，缺点是本地的分叉提交已经被修改过了，原理是变基，改变master的位置为分叉前

## 标签管理
采用标签的目的是：标记！用标签和commit对应起来，实际上是指向某个commit的指针，那么想取那个打标签的时刻的历史版本出来就很方便。

#### 首先切换到想打标签的分支,使用`git tag v1.0`就可以打一个名为`v1.0`的标签，采用命令`git tag`查看所有标签，可以加上参数（commit id:通过`git log --pretty=oneline --abbrev-commit`查看），`git tag <tag name> <commit id>`

#### 采用`git show <tag name>`查看标签信息，注意标签不是按时间顺序列出而是字母顺序

#### 还可以创建有说明的标签,`git tag -a <tag name> -m "information" <commit id>`

#### 删除标签`git tag -d <tag name>`,删除远程标签有点麻烦，现在本地删除`git tag -d <tag name>`，再用push`git push origin :refs/tags/<tag name>`

#### 推送某个标签到远程`git push origin <tag name>`,推送所有尚未推送的标签到远程`git push origin --tags`

[Git网站](https://git-scm.com/)

[Git Cheat Sheet](https://gitee.com/liaoxuefeng/learn-java/raw/master/teach/git-cheatsheet.pdf)