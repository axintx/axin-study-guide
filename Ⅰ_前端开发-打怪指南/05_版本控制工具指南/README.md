# 版本控制

## 介绍

>版本控制 (Version control) 是维护工程蓝图的标准做法, 能追踪工程蓝图从诞生一直到定案的过程
>
>版本控制 (Version control) 是一种软件工程技巧,在软件开发过程中, 确保不同开发人员编辑的同一程序文件都得到同步

## 版本控制功能

- 存储管理多版本的项目
- 备份管理重大版本
- 恢复之前的项目版本
- 记录项目的各种信息
  - 功能修改, bug 修复, 添加新需求
- 合并多开发者的代码

## 版本控制历史

### 1. 无版本控制

- 通过文件备份进行管理, 在通过 diff 命令对比文件差异

### 2. CVS 

- CVS (Concurrent Versions System) 诞生于 1985年, 是第一个被大规模使用的版本控制工具
- Dick Grune 教授发明, SVN 的前身

### 3. SVN

- SVN (Subversion) 由 CollabNet 公司 2000 年资助开发, 对 CVS 进行很多优化
- SVN 和 CVS 都是 **集中式版本控制工具**

### 4. Git

- Linus 用大概一周时间,开发 Git  用来取代 Biteeper (linux 社区早期使用的版本控制工具, 后期对Linux不免费使用)
- Linus 设计Git的核心, 后期将 Git 交 Junio C Hamano 来维护



## 集中式版本控制

- 集中式版本控制工具 ( Centralzed Version Control Systems 简称: CVCS) , 如 **CVS 和 SVN**
  - 单一的集中管理服务器, 保存所有文件的修订版本
  - 协同开发人员通过客户端连接到这台服务器, 取出最新的文件或者提交更新
- 中央服务器不能出现故障
  - 否则无法提交更新,无法协同工作
  - 当中心数据库磁盘损坏, 又没有备份,则数据丢失

## 分布式版本控制

- 分布式管本控制系统 ( Distributed Version Control System 简称: DVCS), 如 **GIT**
  - 客户端把 代码仓库完整的镜像下载,包括完成的历史记录
  - 每次克隆,实际上都是一次对代码仓库的完成备份





