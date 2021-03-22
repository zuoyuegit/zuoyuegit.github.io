---
title: 搭建自己的博客（Hexo + Github + Gitee）
date: 2021-03-22 11:13:46
tags: learning
---

**目录**

[toc]  


### 前言
首先要了解一下我们搭建博客要用到的框架（Hexo），Hexo是高效的静态站点生成框架，它基于Node.js。通过Hexo，我们可以直接使用Markdown语法来撰写博客。写完后只需执行两三条命令即可将生成的网页上传到你的github上。我们无需关心网页源代码的具体细节，只需要用心写好我们的博客内容就行。  



### 1. 安装Git  

* 安装Git  
```bash
# 安装Git
brew install git

# 验证Git是否安装成功
# 若提示：git version *** (Apple Git-122.3)，当前git版本为Apple自带版本
git --version
```

* 切换Git版本  
```bash
# 查看git启动路径
# 若提示：/usr/bin/git，则还是使用Apple自带版本，尝试重启iTerm2试试
which git

# 重启后若还是Apple自带版本，手动切换
vi .zshrc
# 新增配置；优先读取 /usr/local/bin 内的命令
export PATH="/usr/local/bin:$PATH"
# 刷新配置，使配置生效
source ~/.zshrc
```



### 2. 连接本地 Git 与 Github   

* 设置Git  
```bash

# 设置 Github 账号
git config --global user.name "your_git_name"
# 设置 Github 邮箱地址
git config --global user.email "your_email@example.com"

# 检查Git账号、邮箱是否设置正确
git config user.name
git config user.email
```

* 生成公私钥SSH key  
```bash
# 检查是否存在现有的 SSH 密钥
ls -al ~/.ssh

# 生成公私钥 key
ssh-keygen -t ed25519 -C "your_email@example.com"
>Enter file in which to save the key (/Users/zhangshan/.ssh/id_ed25519):
>Enter passphrase (empty for no passphrase): # 可选择输入安全密码
>Enter same passphrase again: # 再次输入安全密码

```

* 将 SSH 密钥添加到 ssh-agent  
```bash
# 启动 ssh 代理
eval "$(ssh-agent -s)"
>Agent pid 3487

# 将 SSH 私钥添加到 ssh-agent 并将密码存储在密钥链中
ssh-add -K ~/.ssh/id_ed25519
>Enter passphrase for /Users/zuoyue/.ssh/id_ed25519: # 输入安全密码

```

* 新增 SSH 密钥到 GitHub 帐户  
```bash
# 查看公钥，并复制
cat ~/.ssh/id_ed25519.pub
```

![GitHub设置](https://gitee.com/zuoyuegitee/pic/raw/master/blog/img/2021/03/21/22-17-28-1402d1.png)
![新建SSH Keys](https://gitee.com/zuoyuegitee/pic/raw/master/blog/img/2021/03/21/22-17-45-4d1b11.png)
![上传SSH Keys](https://gitee.com/zuoyuegitee/pic/raw/master/blog/img/2021/03/21/22-17-55-6f870a.png)

* 验证是否成功
```bash
# 访问连接Github
ssh -T git@github.com

# 出现以下提示，便是成功访问
>Hi your_git_name! You've successfully authenticated, but GitHub does not provide shell access.
```



### 3. 创建GitHub博客项目  

* 创建博客项目  
登录GitHub，点击右上角 + 号按钮  
![创建博客仓库](https://gitee.com/zuoyuegitee/pic/raw/master/blog/img/2021/03/21/22-18-09-0f50c2.png)

* 初始化博客项目  
博客项目名称必须以  “用户名 + .gitgub.io”  结尾
![初始化博客仓库](https://gitee.com/zuoyuegitee/pic/raw/master/blog/img/2021/03/21/22-18-16-7e22e0.png)

* 查看博客地址  
![点击设置博客](https://gitee.com/zuoyuegitee/pic/raw/master/blog/img/2021/03/21/22-18-26-decaa4.png)
![设置博客主题002](https://gitee.com/zuoyuegitee/pic/raw/master/blog/img/2021/03/21/22-18-41-74612b.png)
![设置博客主题003](https://gitee.com/zuoyuegitee/pic/raw/master/blog/img/2021/03/21/22-18-50-24539b.png)



### 4. 安装Node.js  

* 安装Node.js  
```bash
# 安装Node.js
brew install node

# 添加国内镜像源
npm config set registry https://registry.npm.taobao.org
```



### 5. 安装Hexo  

* 安装 Hexo  
```bash
# 选择合适的博客目录
mkdir ~/myblog
# 进入博客目录
cd ~/myblog

# 安装 Hexo
npm install hexo-cli -g
# 验证 Hexo 是否安装成功
hexo -v
# 初始化 Hexo 目录
hexo init
# 安装必要的软件
npm install

# 生成静态网页
hexo g
# 打开本地服务器
hexo s
# 输出提示，复制地址，打开 Hexo 网页
>INFO  Validating config
>INFO  Start processing
>INFO  Hexo is running at http://localhost:4000 . Press Ctrl+C to stop.
```

* 连接本地博客与GitHub  
```bash
# 打开博客根目录下的_config.yml文件
vi ~/myblog/_config.yml

# 修改最后一行的配置；填写你的Github博客地址
deploy:
  type: 'git'
  repository: https://your_git_name.github.io/xxxx.github.io
  branch: master # 博客发布后生成html页面的分支
  
# 进入博客根目录
cd ~/myblog
# 安装Git部署插件
npm i hexo-deployer-git
```

* 创建 hexo 分支，用于保存博客源代码  
```bash
# 初始化博客
git init
# 绑定远程仓库
git remote add origin https://your_git_name.github.io/xxxx.github.io

# 创建 hexo 分支 博客操作都是在此分支
git checkout -b hexo

# 添加需要提交的内容
git add .
# 提交备注
git commit -m "初始化博客"

# 推送至远程分支
git push origin hexo
```

* 更换电脑后如何继续写博客  
```bash
# 重新安装 Hexo ；并 clone 远程博客代码分支
git clone -b hexo https://your_git_name.github.io/xxxx.github.io ~/myblog
```



### 6. 更换主题  

* 进入 Hexo 主题网站
推荐主题：<https://shen-yu.gitee.io/2019/ayer/>
主题网站：<https://hexo.io/themes/>




### 7. 写文章、发布文章  

* 新建一篇博客  
```bash
# 新建一篇博客，title 便是博客名称
hexo n "title"

# 编写博客；推荐一款好用的MarkDown编辑工具 Typora
vi ~/myblog/source/_posts/title.md

# 生成静态网页
hexo g
# 打开本地服务器
hexo s
# 发布博客
hexo d

# 生成静态网页并发布博客（组合命令）
hexo d -g
```

* Hexo  命令详解  
参考官网：<https://hexo.io/zh-cn/docs/commands.html>  



### 7.   Gitee + PicGo + Typora 搭建图床平台  

##### 7-1. 创建 Gitee 图片仓库  
* 在gitee上创建一个仓库，用来存放图片，仓库必须是公开的。  
  ![创建图片仓库01](https://gitee.com/zuoyuegitee/pic/raw/master/blog/img/2021/03/21/22-19-10-b47d70.png)
  ![创建图片仓库02](https://gitee.com/zuoyuegitee/pic/raw/master/blog/img/2021/03/21/22-19-17-bc2834.png)

* 创建私人令牌。  
![创建私人令牌01](https://gitee.com/zuoyuegitee/pic/raw/master/blog/img/2021/03/21/22-19-24-d15a47.png)
![创建私人令牌02](https://gitee.com/zuoyuegitee/pic/raw/master/blog/img/2021/03/21/22-19-32-0e3673.png)
![创建私人令牌03](https://gitee.com/zuoyuegitee/pic/raw/master/blog/img/2021/03/21/22-19-39-4f4882.png)
![创建私人令牌04](https://gitee.com/zuoyuegitee/pic/raw/master/blog/img/2021/03/21/22-19-47-828933.png)

##### 7-2. 安装 PicGo  

* 安装 PicGo  
```bash
brew install picgo
```

* 为 PicGo 安装 Gitee图床 插件 
![安装 Gitee图床 插件01](https://gitee.com/zuoyuegitee/pic/raw/master/blog/img/2021/03/21/22-19-55-433b7b.png)

* 设置 Gitee图床插件
![安装 Gitee图床 插件02](https://gitee.com/zuoyuegitee/pic/raw/master/blog/img/2021/03/21/22-20-07-c1340a.png)



##### 7-2. 安装 Typora  

* 安装 Typora  
```bash
brew install typora
```

* 为 Typora 配置 PicGo 插件 
![为 Typora 配置 PicGo 插件01](https://gitee.com/zuoyuegitee/pic/raw/master/blog/img/2021/03/21/22-20-13-dd0852.png)  



### 8.   博客相关优化设置  

##### 8-1. PicGo 插件库  
插件库地址：https://github.com/PicGo/Awesome-PicGo  

##### 8-2. github、gitee代码同时推送  

* 修改代码仓库 .git 文件夹中的 config 文件  
```bash
vi ~/myblog/.git/config
```

* 新增仓库地址
![新增仓库地址](https://gitee.com/zuoyuegitee/pic/raw/master/blog/img/2021/03/21/22-53-43-6c0ab9.png)  


##### 8-3. 博客同时发布到 github、gitee  

* 修改 博客目录下的 _config 配置文件  
```bash
vi ~/myblog/_config
```

![新增git仓库地址](https://gitee.com/zuoyuegitee/pic/raw/master/blog/img/2021/03/21/22-58-27-9e2a74.png)  

* 执行博客发布命令  
```bash
hexo d -g
```


##### 8-4. 使用Hexo设置Gitee自动部署时需要特别配置Hexo  
配置参考地址：https://github.com/yanglbme/gitee-pages-action/issues/34  

* 新增配置文件 sync.yml；配置文件在博客仓库 source\.github\workflows\ 目录下  
```bash
# 如果 source 目录下没有 .github 目录，则需要新建
cd ~/myblog/source
# 新建 .github 目录
mkdir .github
# 新建 .github 目录下的 workflows 目录
mkdir .github/workflows
# 新增配置文件
vi .github/workflows/sync.yml
```

* 配置文件内容如下
```bash
name: Sync

on:
  push:
    branches:
      - master

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Build Gitee Pages
        uses: github账号/gitee-pages-action@main
        with:
          # 注意替换为你的 Gitee 用户名
          gitee-username: gitee用户名
          # 注意在 Settings->Secrets 配置 GITEE_PASSWORD
          gitee-password: ${{ secrets.GITEE_PASSWORD }}
          # 注意替换为你的 Gitee 仓库，仓库名严格区分大小写，请准确填写，否则会出错
          gitee-repo: gitee用户名/gitee仓库
          # 要部署的分支，默认是 master，若是其他分支，则需要指定（指定的分支必须存在）
          branch: master
```

* 在 github 仓库中设置上述配置文件中需要的参数
> 进入 github 博客仓库，点击仓库的 Settings 按钮，找到左侧菜单栏中 secrets 选项  
> GITEE_PASSWORD                   # Gitee账号的密码  
> GITEE_RSA_PRIVATE_KEY       # id_rsa私钥   vi ~/.ssh/id_ed25519  
![新增 secrets 参数](https://gitee.com/zuoyuegitee/pic/raw/master/blog/img/2021/03/21/22-59-52-827e06.png)


* 修改博客仓库下的 _config.yml 配置  
Hexo默认会忽略隐藏文件和文件夹（包括名称以下划线和 .开头的文件和文件夹，Hexo的_posts和_data等目录除外）。因此需要在后台仓库的_config.yml文件添加这样的配置才能把.github的目录也给带进来。
```bash
vi ~/myblog/_config

# 搜索到 skip_render 属性并修改
skip_render:
  - ".github/**/*"

# 搜索到 include 属性并修改
include:
  - ".github/**/*"

# 找到 deploy 属性 新增 ignore_hidden 属性
deploy:
  type: git
  ignore_hidden: false # 添加这个属性值为false
  repository:
    gitee: 你的 gitee 博客仓库地址
    github: 你的 github 博客仓库地址
  branch: master # 博客发布后生成html页面的分支
```