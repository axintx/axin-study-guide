# 	Git 版本控制工具

## Ⅰ. 介绍

> 版本控制 (Version control) 是一种软件工程技巧,在软件开发过程中, 确保不同开发人员编辑的同一程序文件都得到同步

## Ⅱ. 集中式和分布式区别

### 1. 集中式版本控制

- 集中式版本控制工具 ( Centralzed Version Control Systems 简称: CVCS) , 如 **CVS 和 SVN**
  - 单一的集中管理服务器, 保存所有文件的修订版本
  - 协同开发人员通过客户端连接到这台服务器, 取出最新的文件或者提交更新
- 中央服务器不能出现故障
  - 否则无法提交更新,无法协同工作
  - 当中心数据库磁盘损坏, 又没有备份,则数据丢失

### 2.分布式版本控制

- 分布式管本控制系统 ( Distributed Version Control System 简称: DVCS), 如 **GIT**
  - 客户端把 代码仓库完整的镜像下载,包括完成的历史记录
  - 每次克隆,实际上都是一次对代码仓库的完成备份

## Ⅲ. Git 环境安装搭建

### 1. 安装

- [Git 官网: https://git-scm.com/](https://git-scm.com) 
- 默认安装就可以了

### 2. Bash - CMD  - GUI 区别

- **Git Bash**, Unix shell 的一种, Linux 和 Mac OS X 都将它作为默认的 shell
  - Git Bash 就是一个 shell , 是 Windows 下的命令行工具, 可以执行 Linux 命令
  - Git Bash 基于 CMD, 在 CMD 的基础上添加一些新的命令与功能
- **Git CMD**
  - 命令行提示符 (CMD) 是 Windows 操作系统上的命令行解释程序
- **Git GUI**
  - 提供一个 图形用户界面 来运行 git 命令

### 3. Git 配置

#### (1) Git 通过 git config 设置 git 外观和行为的配置变量

- /etc/gitconfig 文件: 系统上每一个用户以及所属仓库的通用配置
  - git config --system 命令读写该文件中的配置变量
  - 需用(超级)管理员权限修改
- ~/.gitconfig 或 C://用户/wlswang/.gitconfig 文件 (当前用户)
  - 可以传递 --global 选项让 Git 读写此文件, 对系统上所有仓库生效
- 使用仓库的 Git 目录中的 config 文件 (.git/config) 当前仓库有效

#### (2) Git 配置选项

- 设置用户名和邮箱地址

  - git 提交都会使用这些信息,会写入到每次提交中,不可更改
  - 使用 --gloabl 选项, 该命令只需要运行一次

  ```shell
  git config --global user.name "wlswang"
  git config --global user.email "eniac10@163.com"
  ```

- 查看当前配置信息

  ```shell
  git config --list
  ```

- Git 别名 (alias)

  ```shell
  git config --global alias.co commit
  # 相当于
  git commit -m '配置别名'
  git co -m '配置别名'
  ```

## Ⅳ. Git 初始化本地仓库

### 1. 获取 Git 仓库

- 初始化 Git 仓库

  ```shell
  git init 
  # 创建一个 .git 的子目录,包含初始化 git 仓库中所有的必须文件
  ```

- 从其他服务器远程克隆仓库

  ```shell
  git clone https://github.com/XXX/XXX.git
  ```

## Ⅴ. Git 记录更新变化过程

### 1. 检测文件状态

```shell
git status
git status -s
git status --short
```

### 2. git 忽略文件

- 一些文件不需要 Git 管理,

  - 通常是自动生成的文件
  - 也可自己创建 .gitignore 文件, 在文件中列出要忽略的文件模式

- 比如 Vue 项目自动创建的忽略文件

  - 可以去 Github 上搜索 gitignore 项目, 复制里面的文件

  ```shell
  # .gitignore
  
  .DS_Store
  node_modules
  /dist
  
  # local env files
  .env.local
  .env.*.local
  
  # log files
  npm-debug.log*
  yarn-debug.log*
  yarn-error.log*
  pnpm-debug.log*
  
  # Editor directories and files
  .idea
  .vscode
  *.suo
  *.ntvs
  *.njsproj
  *.sln
  *.sw?
  ```

### 3. Git 命令

```shell
# 初始化仓库
git init 

# 添加文件
git add .

# 查看状态
git status

# 提交到暂存区
git commit -m 'commit info'  # 提交后会有一个 校验和(commit id)
git commit -a -m 'commit info' # git add . 和 git commit -m 组合体

# 查看历史
git log # 查看提交的历史
git log --pretty=oneline # 在一行显示提交历史
git log --pretty=oneline --graph # 多分支形成的图形提交历史
git reflog # 记录每一次操作历史

# 版本回退
git reset --hard HEAD^ # HEAD^回退到上一个版本, HEAD^^回退到上上个版本
git reset --hard HEAD~1000 # 回退到上 1000 个版本
git reset --hard commitID # 回退到指定版本

# 克隆
git clong http://xxx/xxx/xxx.git

# 拉取
git pull = git fetch + git merge
git fetch # 从远程仓库中(默认origin)获取最新的代码, 默认没合并到本地仓库
git fetch origin master 
git merge # 通过 merge 合并代码, 如果报以下错误,这使用下个命令解决
# fatal: refusing to merge unrelated histories
git merge --allow-unrelated-histories # 使用这个命令解决上面错误
	

# 将本地仓库的代码推送到远程仓库中
git push # 默认 push 到 origin 远程仓库中
git push origin master
```

## Ⅵ. Git 远程仓库和验证

### 1. 远程仓库

- 远程仓库通常是在某个服务器上
- 第三方 git 服务器
  - [GitHub: https://github.com/ ](https://github.com/) (常用)
  - [Gitee: https://gitee.com/](https://gitee.com) (常用)
  - Gitlab
- 自己在服务器中搭建一个 Git 服务 (常用)

### 2. Git 服务器验证方式

#### (1) 方式一: 基于 HTTP 的凭证存储

- HTTP 协议是无状态的连接, 每次连接都需要用户名和密码

- Git 凭证系统 Git Crediential 选项

  - 选项一: 默认所有都不缓存, 每次连接都会询问用户名和密码

  - 选项二: "cache" 模式将凭证存放在内存中一段时间, 密码不会被存储在磁盘中, 15分钟后从内存中清除

  - 选项三: "store" 将凭证用明文的形式存放在磁盘中, 永不过期

  - 选项四: Mac 中 git 有 "osxkeychain" 模式, 将凭证以加密形式缓存到系统用户的钥匙串

  - 选项五: windows 可以安装 "Git Credential Manage for Windows" 辅助工具,一般情况下安装 git 时就自动安装此工具了

    ```shell
    # 执行此命令验证是否安装成功
    git config credential.helper
    # manager-core 显示此结果 安装成功,否则失败
    ```

#### (2) 方式二: 基于 SSH 的密钥

- Secure Shell (安全外壳协议, 简称 SSH) 是一种加密的网络传输协议, 可在不安全的网络中为网络服务提供安全的传输环境

- SSH 以非对称加密实现身份验证

  - 自动生成公钥私钥进行简单的加密网络连接, 然后使用密码认证登录
  - 手动生成公钥私钥,通过生成密钥进行认证,不输入密码就可登录
    - 公钥放在待访问的电脑中,私钥由用户自行保管

- 生成公钥和私钥, 然后配置到 Git 仓库中

  ```shell
  ssh-keygen -t ed25519 -C "your email"
  ssh-keygen -t rsa -b 2048 -C "your email"
  ```

### 3. 管理远程服务器

```shell
# 查看远程地址
git remote
git remote -v 
git remote --verbose

# 添加远程地址
git remote add <shortname> <url>
git remote add gitlab http://xxx/xxx/xxx.git

# 重命名远程地址
git remote rename gitlab glab

# 移除远程地址
git remote remove gitlab
```

### 4. 远程交互

```shell
# 情况一: 已有远程项目
git clone XXX
git add .
git commit -m 'info'
git pull
git push

# 情况二: 一个全新的项目
# 创建一个远程仓库
# 方案一:
git clone XXX
git add .
git commit -m 'info'
git push

# 方案二
# 创建一个本地仓库并且搭建本地项目
git remote add origin http://XX/XX.git
git branch --set-upstream-to=origin/master # 将本地分支跟踪上有分支master
git fetch
git merge --allow-unrelated-histories # 
git config push.default upstream # 默认使用上游分支
git push
```

## Ⅶ. Git 标签 tag 用法

```sh
# 删除本地 tag
git tag -d <tagname>

# 删除远程tag
git push <remote> -delete <tagname>
git push origin --delete v1.2

# 检出 tag ,查看标签所指向的文件版本
git checkout v1.2
```

## Ⅷ. Git 分支的使用过程

```shell
# 查看分支
git branch # 查当前所有的分支
git branch -v # 同时查看最后一次提交
git branch --merged # 查看所有合并当当前分支的分支
git branch --no-merged # 查看所有没有合并到当前分支的分支

# 创建分支
git branch test

# 切换分支 
git checkout test

# 创建分支并且切换分支
git checkout -b test

# 切换分支后在推到远程仓库
git push -u origin/test

# 删除分支
git branch -d test
git branch -D test # 强制删除某个分支
```

## Ⅸ. 工作流 (GIT Flow)

XXX

## Ⅹ. GIT远程分支的管理

```shell
# 推送分支到远程
git push origin <branch>

# 跟踪远程分支
	# 克隆仓库默认跟踪 origin/master 的 master 分支
	# 通过 --track 跟踪其他分支
git checkout --track <remote>/<branck>
git checkout <branch> # 简写

# 删除远程分支
git push origin --delete <branch>
```

## Ⅺ. Git rebase 的使用

- 在 git 中整合来自不同分支的修改主要有两种方法: merge 和 rebase (变基)
- 可以理解为改变当前分支的 base
- 比如在分支 test 上执行 rebase master ,可以改变 test 的 base 为 master 



### 1. rebase 和 merge 的选择

- rebase 和 merge 是对 Git 历史的不同处理方法:
  - merge 用于记录 git 的所有历史, 其分支的历史错综复杂, 也全部记录下来
  - rebase 用于简化历史记录, 将两个分支的历史简化, 整个历史就更加简介
- 根据场景自行选择
- **rebase 的黄金法则: 永远不要在主分支上使用rebase**
  - 如果在 main 上使用 rebase, 会造成大量的提交历史在 main 分支中不同

## Ⅻ. Git 常见命令速查表

### 1. 创建版本

```shell
 # 克隆远程版本库
git clone <url>

# 初始化本地版本库
git init
```

### 2. 修改和提交

```shell
# 查看状态
git status

# 查看变更内容
git diff

# 跟踪所有改动过的文件
git add .

# 跟踪指定的文件
git add <file>

# 文件改名
git mv <old> <new>

# 删除文件
git rm <file>

# 停止跟踪文件但不删除
git rm --cached <file>

# 提交所有更新过的文件
git commit -m 'commit message'

# 修改最后一次提交
git commit --amend
```

### 3. 查看提交历史

```shell
# 查看提交历史
git log 

# 查看指定文件的提交历史
git log -p <file>

# 以列表方式查看指定文件的提交历史
git blame <file>
```



### 4. 撤销

```shell
# 撤消工作目录中所有未提交文件的修改内容
git reset --hard HEAD

# 撤消指定的未提交文件的修改内容
git checkout HEAD <file>

# 撤消指定的提交
git revert <commit>
```



### 5. 分支与标签

```shell
# 显示所有本地分支
git branch

# 切换到指定分支或标签
git checkout <branch/tag>

# 创建新分支
git branch <new branch>

# 删除本地分支
git branch -d <branch>

# 列出所有本地标签
git tag

# 基于最新提交创建标签
git tag <tagname>

# 删除标签
git tag -d <tagname>
```



### 6. 合并

```shell
# 合并指定分支到当前分支
git merge <branch>

# 指定分支到当前分支
git rebase <branch>
```



### 7. 远程操作

```shell
# 查看远程版本库信息
git remote -v

# 查看指定远程版本库信息
git remote show <remote>

# 添加远程版本库
git remote add <remote> <url>

# 从远程库获取代码
git fetch <remote>

# 下载代码及快速合并
git pull <remote> <branch>

# 上传代码及快速合并
git push <remote> <branch>

# 删除远程分支或标签
git push <remote> :<branch/tag-name>

# 上传所有标签
git push --tags
```

[GIT工具](../../Ⅴ_杂项-打怪指南/01_武器(工具)指南/01_GIT工具/README.md)