### 初始化git项目

git init 

会下载一个默认的  .git 目录



### 推送数据

git add 从工作区 推送到 暂存区

git commit 从工作区推送到 本地仓库

git push 从本地仓库 推送到远程仓库

git clone 从远程仓库 clone 一个项目 并建立本地仓库

### 设置签名

git cofig 用户名 邮箱

git config -global 用户名 邮箱 设置全局的签名

eg：

git config user.name WangNing

git config user.email WangNingJava@163.com



### 查看签名

cat .git/config

查看 git 签名保存的地方

### 查看状态

git status



### 如果 二次提交的是修改的操作

二次提交修改的操作 直接可以使用命令

git commit -a good.txt （这个方法 不能被撤销）

而不用再次 git add good.txt

不用再次加入缓冲区了

## 提交的简单写法

git commit -m "备注" good.txt 不用进入vim 直接可以提交



# 版本的前进和后退

### 查看版本

git log

### 指定版本

head -》 指向 就是那个版本

```linux
$ git log
commit 795df723c27375761ddd66b43ee0c14766c4b8b9 (HEAD -> master)
Author: WangNing <WangNingJava@163.com>
Date:   Sun Jun 7 14:27:35 2020 +0800

    my sen e

commit d56f70230db9e3903c86577e61fb580bc7168168
Author: WangNing <WangNingJava@163.com>
Date:   Sun Jun 7 12:07:29 2020 +0800

    my first commit exe

```

### 漂亮（简洁的日志打印）

git log --pretty=oneline

git log --oneline

git reflog   (显示移动步数)

```
$ git reflog
5dc260b (HEAD -> master) HEAD@{0}: commit: five commit exe
8a50d78 HEAD@{1}: commit: fir commit exe
c7b16a1 HEAD@{2}: commit: three commit exe
795df72 HEAD@{3}: commit: my sen e
d56f702 HEAD@{4}: commit (initial): my first commit exe

```

### 回到之前版本

git reset --hard 索引值

### 找回删除的文件

回退版本 回到没有别删除的那个状态

git reset --hard 版本号

回退到没有别删除的状态 即可找回被删除的文件

必要条件就是

能找回删除文件 必须要存在的时候进行了提交

### 查看不同

git diff good.txt

如果没有参数 就和暂存区进行比较

git diff HEAD apple。txt

给本地库里面的某个版本进行比较

不带 文件名 可以比较多个文件

### 查看分支

git branch -v 查看分支

git branch hot_fix 新建分支

git checkout hot_fix 切换分支

### 合并分支

合并分支的第一步·

  切换到被合并的分支上 master

  执行 merge 命令

```
ssssssssssssd
aaaaaaaaaaaaaaaaaaaaaaaaaassssssssss
sa
<<<<<<< HEAD
master edit
=======
hot_fix edit
>>>>>>> hot_fix
会出现冲突

```

解决冲突

```
删除特殊符号 
编辑成自己满意的的程度（商讨）

```

```
On branch master
All conflicts fixed but you are still merging.
  (use "git commit" to conclude merge)

提示 虽然所有的冲突都已经解决了 但是依然还是没有用合并的状态
修复标记 
不能使用 git commit -m  " " 文件名 的方式
只能使用 git commit -m  " " 不加文件名称
```



### 推送到github上面

git remote -v  查看远程仓库地址



git remote add 别名 https://github.com/wangningjava/CodeStu.git

别名 可以随便取



CodeStu https://github.com/wangningjava/CodeStu.git (fetch)
CodeStu https://github.com/wangningjava/CodeStu.git (push)



区别 fetch  用来取回的地址

push 用来推送的地址



### git的push操作

git push 别名（github地址） 分支 



### clone克隆的效果

git clone 

完整的 把远程库下载到本地

初始化本地库

克隆他的别名



### 拉取到本地库pull

pull = fetch（拉取操作 和 push 相反） + merge（合并分支 命令）

pull = fetch + merge

git fetch[远程库地址别名]

### 合并 远程仓库地址

git merge  连接（CodeStu）/master

合并远程的 master 到本地库的master



git pull [远程地址别名] master



### 管理凭据

控制面板 --> 所有控制面板项 --> 凭据管理器

下次想再次登录 需要删除



### 合并

```
git remote add origin github地址
git push -u origin master
连接起来 本地仓库和远程仓库
```

