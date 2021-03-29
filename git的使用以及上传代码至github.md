# 初始化git仓储

git init  

此命令会在当前命令下创建一个git文件对我们的代码备份

# 配置使用者的用户名和邮

配置用户名   git config --global user.name "tiankai"

配置邮箱       git config --global user.email "893998552@qq.com"  (邮箱不要求是真实的)

# 把代码存储在git中

## 1将代码放在git的门口

git  add  ./文件名     

git  add  ./                  

第一条命令只能将此文件放在备份在git中，第二条命令是将当前目录下的所有文件备份在git中

## 2将代码放在git中

git commit -m “对此次提交的描述”

## 3一次性将代码放入git中 

git commit --all -m "对此次提交的描述"   

# 命令查看放在git门口的代码

git  status

# git查看日志

## 1全部显示

git log        

## 2在一行显示

git log --oneline

## 3更多信息的查看

git reflog

可以查看你的提交记录以及以及回退的记录

# 版本的回退

## 正常的回退

git reset --hard HEAD ~0

## 非常灵活的回退

git reset --hard 版本号

正常的回退之后并不会将之前的记录删除只是将head指向了回退点，如果在正常的回退之前执行了 git lof --oneline 知道之前的记录号，如果你反悔回退了那么依然可以找到之前的版本。或者利用git reflog 查看提交和回退记录来寻找记录号以达到任意回退的目的

# git分支操作

## 1分支的理解

## 2查看分支

git branch

此命令显示所有的分支

## 3创建分支

git branch 分支名 （例如：git branch dev）

此命令将会创建一个新的分支

## 4切换分支

git checkout 分支名 (例如：git checkout dev)

此命令将会进行分支的切换成功则会将在master位置显示分支名字

## 5删除分支

git branch -d 分支名 （例如git branch -d dev）

此命令会将以创建的一个分支进行删除 **自己不能删除自己**

## 6合并分支

### （1）自动合并分支

git merge dev

此命令会将dev中编写的代码合并到master中，把当前分支与指定分支合并，当前分支指的是前面又*的分支

### （2）手动合并分支

如果出现冲突则与要手动处理，例如：在分支dev中提交了代码，返回master分支之后忘记合并，此时在master中提交了一次代码，将master分支和dev分支进行合并，那么系统将会提示自动和兵冲突。 手动处理之后和还需要提交一次才可以。至于保留哪一部分那是自己的事情。

# 将本地的代码上传到git hub

## 1git hub网址

www.github.com

## 2在git hub上创建一个仓库（https）

### （1）Repository name

仓库名称，如果失败则更改其他名字即可

### （2）属性选择

 public 开源

 private 收费

### （3）上传

git push **网址** 分支 （例如：git push https://github.com/15191742310/text12121.git master）**远程的分支和本地的分支要保持一致**

这里的网址指的是在github创建一个仓库时选择https系统给出的一个连接

###  （4）删除github上的仓库

setting 然后下拉点击 Delete this repository

## 3在git hub上创建一个仓库（ssh）

当上传一段代码时如果是hppts上传时需要将自己的账号密码给其他人这就分非常的离谱。  创建仓储的方式与**https**的方式一致

### （1）code ssh

这种的地址格式  git@github.com:15191742310/text12121.git

### （2）公钥私钥

####     （1）生成公钥和私钥

ssh-keygen -t rsa  -C “任意邮箱”  （例如：$ ssh-keygen -t rsa -C "893998552@qq.com"）

ssh上传代码不需要输入用户密码就能验证上传者的身份。但是地址不能时所有人都能上传，只能时自己人才可以传。这里就有**公钥和私钥**的概念。公钥和私钥之间有关联。私钥自己保留，公钥给github网站。

####     （2）验证

打开用户目录找到用户名 或者 win+r   cmd  回车 查看用户名点开 会发现一个 .ssh目录中就有公钥和密钥

####     （4）设置

找到密钥的位置打开git bash 输入 clip < ~/.ssh/id_rsa.pub 让后在github上右上角setting  ssh将自己的密钥复制命名添加就可以了

**直接设置会破坏ras的结构会出错**

### （3）上传

   git  push [地址] 分支

 （例如：’git push git@github.com:15191742310/test1198.git master‘）

ssh上传代码不需要输入用户密码就能验证上传者的身份。但是地址不能时所有人都能上传，只能时自己人才可以传。这里就有**公钥和私钥**的概念。公钥和私钥之间有关联。私钥自己保留，公钥给github网站。



## 4在git hub上获取一个项目

### （1）直接下载

git pull [网址] 分支 （例如：' git pull https://github.com/15191742310/text12121 master'） 

**这里成功的关键是创建一个本地的存储git，这里一般会进行合并**

### （3）clone

git pull [网址] 分支 （例如：' git clone https://github.com/15191742310/text12121 '） 

**这里需要注意的是clone不需要创建一个本地的git，多次clone会将本地的文件进行覆盖**

# 模拟两个用户

## （1）小明和小红的问题

 当小明上传自己的代码小红下载代码。此时小明更改的代码，并且上传。小红修改自己代码但是只是在本地保存但是没有上传。当小红从github获取代码的时候系统会提示有可能会将自己本地的代码覆盖。

conflict 冲突

总的来说要 push之前先要在本地保存（git commit --all -m "对此次提交的描述"   ）然后pull在本地把冲突解决，才可以提交到服务器。服务器无法处理冲突。