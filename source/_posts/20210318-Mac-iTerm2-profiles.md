---
title: Mac iTerm2 终端利器
date: 2021-03-18 14:57:56
tags: MacBook
---

**目录**

[toc]

## 前言  
iTerm2是Terminal的替代品，是iTerm的后继产品。它适用于MacOS 10.14或更高版本的Mac。 
官网地址：<https://iterm2.com/>  
最终效果图如下：  
![iTerm2效果图](https://gitee.com/zuoyuegitee/pic/raw/master/blog/img/2021/03/19/17-26-27-99b2b1.png)  


### 一、安装  

* 通过 Homebrew 安装  
```bash
# 搜索 iTerm2 软件包信息
brew search iterm2

# 安装 iTerm2
brew install iterm2
```



### 二、优化  

##### 1. 安装 Oh my zsh：  
Oh my zsh 开源地址：<https://github.com/ohmyzsh/ohmyzsh>  

* 开始安装  
```bash
# curl 安装方式
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

* 安装命令和安装完成后的截图：  
![Oh my zsh 安装](https://gitee.com/zuoyuegitee/pic/raw/master/blog/img/2021/03/19/17-26-51-8c288a.png)  


##### 2. 安装 PowerLine  

PowerLine 官网地址：<http://powerline.readthedocs.io/en/latest/installation.html>  

* 开始安装  
```bash
# curl 安装方式
pip install powerline-status --user
```

* 如果提示：zsh: command not found: pip。则需要先安装 pip；再安装 PowerLine  
```bash
# curl 安装方式
sudo easy_install pip
```


##### 3. 安装 PowerFonts 字体  
PowerFonts 开源地址：<https://github.com/powerline/fonts.git>  

* 开始安装  
安装字体库需要首先将项目git clone至本地，然后执行源码中的install.sh。  
新建 MacConfig 文件夹（后续软件相关的配置都可以放到这个目录中）再新建 iTerm2 配置目录  
```bash
# 新建配置文件目录
mkdir ~/MacConfig/iTerm2
# 进入配置目录
cd ~/MacConfig/iTerm2

# 克隆 PowerFonts 字体
git clone https://github.com/powerline/fonts.git
# 安装 PowerFonts 字体
sh ~/MacConfig/iTerm2/fonts/install.sh
```

* 设置 iTerm2 的字体
iTerm2 -> Preferences -> Profiles -> Text，在Font区域选中Change Font，然后找到Meslo LG字体。有L、M、S可选，看个人喜好：
![设置 iTerm2 的字体](https://gitee.com/zuoyuegitee/pic/raw/master/blog/img/2021/03/19/17-27-15-ee3c76.png)  


##### 4. 安装 agnoster 主题  

agnoster 主题开源地址：<https://github.com/fcamblor/oh-my-zsh-agnoster-fcamblor>  

* 开始安装  
安装主题需要首先将项目git clone至本地，然后执行源码中的install.sh。  
```bash
# 进入配置目录
cd ~/MacConfig/iTerm2

# 克隆 PowerFonts 字体
git clone https://github.com/fcamblor/oh-my-zsh-agnoster-fcamblor.git
# 安装 PowerFonts 字体
sh ~/MacConfig/iTerm2/oh-my-zsh-agnoster-fcamblor/install.sh
```

* 安装过程如图（执行上面的命令会将主题拷贝到oh my zsh的themes中）：  
![主题安装过程](https://gitee.com/zuoyuegitee/pic/raw/master/blog/img/2021/03/19/17-27-25-0dfcec.png)  

* 更改主题配置（执行命令打开zshrc配置文件，将ZSH_THEME后面的字段改为agnoster）  
```bash
vi ~/.zshrc
```

![修改主题配置](https://gitee.com/zuoyuegitee/pic/raw/master/blog/img/2021/03/19/17-27-40-13aa16.png)  

* 刷新配置（保存 .zshrc 配置退出、退出 vi 模式）:  
```bash
source ~/.zshrc
```

![主题效果图](https://gitee.com/zuoyuegitee/pic/raw/master/blog/img/2021/03/19/17-28-05-001959.png)  


##### 5. 命令补全、安装高亮插件  
命令补全插件开源地址：<https://github.com/zsh-users/zsh-autosuggestions.git>  
高亮插件开源地址：<https://github.com/zsh-users/zsh-syntax-highlighting.git>  

* 开始安装  
安装插件需要将项目git clone至插件目录，然后修改配置。  
```bash
# 进入插件目录
cd ~/.oh-my-zsh/custom/plugins/

# 克隆命令补全插件
git clone https://github.com/zsh-users/zsh-autosuggestions.git

# 克隆高亮插件至本地
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git

# 修改配置
vi ~/.zshrc
```

* 请务必保证插件顺序，zsh-syntax-highlighting必须在最后一个；保存、退出、刷新配置  
![高亮插件修改](https://gitee.com/zuoyuegitee/pic/raw/master/blog/img/2021/03/19/17-29-53-8df24b.png)  


##### 6. 设置 iTerm2 配色及背景图  

背景图地址：<https://pan.baidu.com/s/15-ps2TQbox48Xxn63iGUog>  密码：id9l  

* 新建 Profile，并设置为默认 （修改之前先备份 Profile ）
![新建Profile](https://gitee.com/zuoyuegitee/pic/raw/master/blog/img/2021/03/19/17-30-10-b141b4.png)  

* iTerm2 配色
![iTerm2 配色](https://gitee.com/zuoyuegitee/pic/raw/master/blog/img/2021/03/19/17-33-35-f36ae0.png)  

* iTerm2 背景图
![iTerm2 背景图](https://gitee.com/zuoyuegitee/pic/raw/master/blog/img/2021/03/19/17-33-52-fbcb55.png)

* iTerm2 光标
![iTerm2 光标修改](https://gitee.com/zuoyuegitee/pic/raw/master/blog/img/2021/03/19/17-34-13-4b8190.png)  

* iTerm2 标签页名称
![iTerm2 标签页名称](https://gitee.com/zuoyuegitee/pic/raw/master/blog/img/2021/03/19/17-34-22-c937e0.png)  


##### 7. 设置悬浮窗口：
使用场景：你正在全屏浏览器浏览网页，或者正在全屏编辑器写代码写文章之类的，突然想到了什么，或发现了什么，想快速打开终端，执行一两条命令（诸如打开文件、启动服务等），然后关闭。  

* 创建新的 Profile 取名：HotKey Window  
背景与窗口风格设置  
![iTerm2 标签页名称](https://gitee.com/zuoyuegitee/pic/raw/master/blog/img/2021/03/19/17-34-32-c7bd24.png)

> Full-Width Top of Screen：让终端显示在屏幕顶部，并占满整个宽度。  
> 
> Screen width Cursor : 这个和上面的参数搭配，用来判定哪个屏幕属于当前的工作空间，表示你的鼠标在哪，哪里就是当前的工作空间。
> 
> Current Spce : 只显示在当前的工作空间，举个例子吧，假设你在当前屏幕打开了终端，你切换到下一个屏幕时它就不会跟到下一个屏幕。  

* 设置 HotKey
![iTerm2 标签页名称](https://gitee.com/zuoyuegitee/pic/raw/master/blog/img/2021/03/19/17-34-42-bfd01a.png)


更多设置参考：
<https://zhuanlan.zhihu.com/p/112383265?from_voters_page=true>

