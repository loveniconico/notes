# Git基础
## 下载and安装
### Windows
 - [Windows下载和安装](https://book.git-scm.com/download/win)
### Mac OS
 - [Mac OS下载和安装](https://book.git-scm.com/download/mac)
### Linux
 - [Linux下载和安装](https://book.git-scm.com/download/linux)

## 上手配置
### 配置用户信息
#### 全局配置
```
git config --global user.name "youName"
git config --global user.email youEmail
```
> 全局配置存储在`C:\Users\userName`下的.gitconfig文件内
#### 仅为当前仓库配置
```
git config user.name "youName"
git config user.email youEmail
```
> 当前仓库配置存储在当前仓库目录下的`.git/config`文件夹里  
 我们可以使用`git config --list`命令来查看当前仓库的配置信息

## 创建仓库
创建新文件夹，打开，然后执行`git init`以创建新的 git 仓库.
## 克隆仓库
执行`git clone URL`  

