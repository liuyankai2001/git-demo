# git常用命令

```bash
git config --global user.name 用户名 #设置全局签名
git config --global user.email 邮箱 #设置全局签名
# 存储位置：C:\Users\28329\.gitconfig

git init #git初始化
git status #查看git状态
git add 文件名 #添加暂存区
git add . #添加所有未添加的文件到暂存区
git rm --cached 文件名 #删除暂存区追踪的文件

git commit -m "日志信息" 文件名

git reflog #查看历史版本信息
git log #查看详细日志
git log --graph #以图的形式显示出提交日志
git log --graph --pretty=format:"%h %s" #以格式化图的形式显示出提交日志

git reset --hard 版本号 #版本穿梭
#当前版本信息存储位置：C:\Users\28329\Desktop\git-demo\.git\refs\heads\master


git checkout -- 文件名 #撤销修改的文件 
git reset HEAD 文件名 #暂存区文件->工作区 （绿变红）
```

# git分支操作

```bash
git branch #查看当前所处分支
git branch -v #查看分支
git branch 分支名 #创建分支
git branch -d 分支名 #删除分支
git checkout 分支名 #切换分支
git checkout -b 分支名 #创建分支并切换到分支
git merge 分支名 #合并分支(正常合并)
#注意：如果将B合并入A，则要切换到A，才使用命令git merge B
```

冲突合并：

产生冲突的原因：合并分支时，两个分支在同一个文件的同一个位置有两套完全不同的修改，git无法替代我们决定使用哪一个。必须人为决定新代码内容

手动修改，修改后，bug分支并没有随之更新

修改后，用add将其添加到暂存区后commit，此时不要加文件名。

# github使用

```bash
git remote -v #查看当前所有远程地址别名
git remote add 别名 远程地址 #添加远程仓库地址
git push 别名 分支 #推送，将本地端的【分支】推送到远程端【别名】
git push origin A:B#推送，将本地端的【A分支】推送到远程端【别名】的【B分支】
git pull 别名 分支 #拉取更新代码，将远程端【别名】的【分支】分支拉取到本地更新
git pull origin A:B#拉取更新代码，将远程端【别名】的【A分支】分支拉取到本地的【B分支】

git pull 别名 分支 #等价于
git fetch 别名 分支
git log master..origin/master --oneline 查看本地代码和远程代码差异
git merge 别名/分支

git clone 地址 #第一次从github中下载代码，公共代码库克隆不需要登陆
$ ssh-keygen -t rsa -C 邮箱

git pull -u 别名 分支 #设置默认推送目的地

git pull origin dev

git fectch origin dev
git merge origin/dev

git rebase -i HEAD~3
git rebase -i 版本号

git tag -a v1 -m '描述' #打标签
git push 别名 分支 --tags #推送tag到远程代码仓库
 
#review
git fetch origin
git checkout -b ddz origin/ddz
git merge dev
git checkout dev
git merge --no-ff ddz
git push origin dev
```

# git rebase三种场景

```bash
#第一种场景：本分支进行版本合并
git rebase -i HEAD~3
git rebase -i 版本号

#第二种场景：master和dev分支之间进行版本合并
git rebase master #在dev分支上
git merge dev #在master分支上

#第三种场景：在github和本地master上进行版本合并
git fetch origin dev
git rebase origin/dev
D:\Program Files\Beyond Compare 4
```

注意：如果git rebase产生冲突，则按照指令解决冲突后，使用`git rebase --continue`后继续往下走



# git配置文件

* 项目配置文件：项目/.git/config

  ```bash
  git config --local user.name 用户名 #设置全局签名
  git config --local user.email 邮箱 #设置全局签名
  ```

* 全局配置文件：~/.gitconfig

  ```bash
  git config --global user.name 用户名 #设置全局签名
  git config --global user.email 邮箱 #设置全局签名

* 系统配置文件：/etc/.gitconfig

  ```bash
  git config --system user.name 用户名 #设置全局签名
  git config --system user.email 邮箱 #设置全局签名
  ```

# git免密登录

* 在URL中体现

  ```
  原来的地址：https://github.com/liuyankai01/git-demo.git
  修改后的地址：https://用户名:密码@github.com/liuyankai01/git-demo.git
  
  git remote add origin https://用户名:密码@github.com/liuyankai01/git-demo.git
  git push origin master
  ```

* SSH实现

  ```
  1.生成公钥和私钥(默认放在~/.ssh目录下，id_rsa.pub公钥、id_rsa私钥)
  ssh-keygen -t rsa -C liuyankai23@mails.ucas.ac.cn
  
  2.拷贝公钥的内容，并设置到github中
  
  3.在git本地配置中设置ssh地址
  	git remote add origin git@github.com:liuyankai01/git-demo.git
  	
  4. 以后使用git push时就不用再输入密码了
  ```

* git自动管理凭证



# git忽略文件

创建`.gitignore`文件

`https://github.com/github/gitignore`各种语言的`.gitignore`文件模板

在用户目录下创建文件`git.ignore`写入以下内容

```java
# Compiled class file
*.class

# Log file
*.log

# BlueJ files
*.ctxt

# Mobile Tools for Java (J2ME)
.mtj.tmp/# Package Files #
*.jar
*.war
*.nar
*.ear
*.zip
*.tar.gz
*.rar

hs_err_pid*

.classpath
.project
.settings
target
.idea
*.iml
```

之后打开`.gitconfig`文件写入以下`[core]`内容:

```
[user]
	name = liuyankai
	email = liuyankai23@mails.ucas.ac.cn
[core]
	excludesfile = C:/Users/28329/git.ignore
```



# gitlab

gitlab下载地址：https://mirrors.tuna.tsinghua.edu.cn/gitlab-ce/yum/el7/

```bash
# 关闭防火墙
systemctl stop firewalld
systemctl disable firewalld
# 安装依赖
yum install curl openssh-server postfix cronie -y
service postfix start
chkconfig postfix on
```

```bash
# 使用清华大学的镜像源安装GitLab，相关配置及安装参照：https://mirror.tuna.tsinghua.edu.cn/help/gitlab-ce/
# vim /etc/yum.repos.d/gitlab-ce.repo
[gitlab-ce]
name=Gitlab CE Repository
baseurl=https://mirrors.tuna.tsinghua.edu.cn/gitlab-ce/yum/el$releasever/
gpgcheck=0
enabled=1
```

```
yum makecache
yum install gitlab-ce #自动安装最新版
```

```bash
# 修改gitlab运行外部URL默认的访问地址
# vim /etc/gitlab/gitlab.rb
external_url 'http://IP地址:端口号'
```



```bash
gitlab-ctl start    # 启动所有 gitlab 组件
gitlab-ctl stop        # 停止所有 gitlab 组件
gitlab-ctl restart        # 重启所有 gitlab 组件
gitlab-ctl status        # 查看服务状态
gitlab-ctl reconfigure        # 启动服务
vim /etc/gitlab/gitlab.rb        # 修改默认的配置文件
gitlab-rake gitlab:check SANITIZE=true --trace    # 检查gitlab
sudo gitlab-ctl tail        # 查看日志
gitlab-ctl --help #查看更多命令
```

