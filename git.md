### git

#### 什么叫git  为什么用   有何优点  

分布式管理系统     在多人项目开发的时候使用    快 无需联网

#### 安装

#### 常用的命令

##### 创建一个版本库

+ git init   创建一个版本库  多了一个git文件   文件夹下及其子目录会受到 git的管理   无论是修改删除还是添加 都会被记录

##### 查看修改状态和添加暂存区并提交

+ git status  查看修改状态   无论是删除修改 添加  都在掌握之中
+ git add file。。。  把一个文件或者多个用空格隔开 添加到暂存区   git关注的是修改 
+ git commit -m "提交说明"

##### 版本的回退

+ git reset --hard  HEAD^ 回退上个版本
+ git reset --hard  HEAD^^回退上上个版本
+ git resset --hard HEAD ~100 回退一百个版本
+ git reset --hard HEAD commitid  回退到指定的版本

##### 管理修改

+ git diff HEAD -- 文件名   查看版本库最新和工作区的区别

##### 撤销修改

+ git checkout -- file  放弃工作区的修改   恢复到暂存区  或者恢复到和版本库一样的内容

+ git reset HEAD file   放弃提交的暂存区

+ git checkout -- file 替换为版本库最新版本

##### 远程仓库

+ ssh-keygen -t rsa -C "1246430195@qq.com" 创建ssh key
+ git remote add origin(给远程仓库起的名字)   //添加空仓库
+ git push -u origin master   第一次提交本地的仓库  -u参数是把本地和远程建立关系   下面的提交都可以省略-u这个参数
+ git clone   从远程clone一个仓库  默认关联master   
+ git clone -b dev 路径名称    //clone远程的dev分支
+ git checkout -b dev  origin/dev   //用本地的dev关联远程的dev
+ git checkout -b dev  origin/dev  建立和远程dev的关系   首先要确保远程有dev分支
+ git branch --set-upstream-to=origin/dev dev  建立和远程 dev的关系

##### 查看分支

+ git log --graph --pretty=oneline --abbrev-commit  查看分支包括和并的情况

##### 分支管理(HEAD指针是指向分支  master指针是指向当前分支的提交)

+ git branch dev  创建dev分支
+ git checkout dev  切换到dev分支 
+ git checkout -b dev   创建并切换到dev分支
+ git branch 查看当前的分支
+ git merge dev  合并指定dev分支到当前所在的分支
+ deleted branch dev
+ git branch -d dev  删除dev分支    只能在别的分支上删除   
+ git merge --no--ff -m "说明" dev   取消快速合并 

##### 存储修改的现场  切换到其他分支

+ git stash  储存当前的未提交的修改和暂存区   变成干净的分支
+ git stash list 列出所存储的零时存储
+ git stash apply ..使用哪一个stash
+ git stash drop  ..
+ git stach pop   使用当前的保存并删除(建议使用 ， 用一个删除一个   不要保存很多 不然很乱)

##### 创建future分支

+ 如果没有合并就要删除  就需要  git branch -D  分支  -D强行删除这个分支

##### 查看远程仓库

+ git remote
+ git remote  -v  查看详细信息

##### 获取远程的dev分支建立连接



##### git rebase 了解一下把







##### 设置标签

+ git log --pretty=oneline --abbrev-commit  查看提交的id

+ $ git tag -a v0.1 -m "version 0.1 released" 1094adb 为某个版本打标签（推荐）

+ git  tag  v1.0    默认打到当前版本（不推荐）

+  $ git tag -d v0.1 删除标签

+ git show tagname

+ git tag   查看当前的标签

+ git checkout tagname  到达某个标签点

+  命令git push origin <tagname>可以推送一个本地标签；

  命令git push origin --tags可以推送全部未推送过的本地标签；

  命令git tag -d <tagname>可以删除一个本地标签；

  命令git push origin :refs/tags/<tagname>可以删除一个远程标签。 

##### 起别名   在用户主目录 gitconfig文件中配置

+ git config --global alias.ci commit

### 搭建git服务器

