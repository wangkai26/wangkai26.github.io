---
title: 'VSCode连接linux,配置zsh+p10k终端,踩坑经验'
date: 2024-09-17T15:36:43+08:00 #创建时间
lastmod: 2024-09-17T15:36:43+08:00 #更新时间
author: ["kai"] #作者
draft: false
searchHidden: false
tags: 
- linux
- zsh
---





本地环境：win10 + VSCode，使用 database 插件，ssh 连接服务器

为了配置这个网上看起来比较漂亮的终端，踩了一些坑，来来回回搞了快 5 个小时才搞好，这里分享下经验。

主要流程：

1. 安装zsh
2. 安装 p10k
3. 安装 Oh-My-Zsh
4. 安装 Nerd 字体
5. 配置文件 zshrc
6. 配置 p10k

## 一、安装zsh

可以输入 echo $SHELL 查看当前使用的 shell

```bash
ubuntu@VM-12-2-ubuntu:~$ echo $SHELL
/bin/bash
```

cat /etc/shells 查看支持的shell

```bash
ubuntu@VM-12-2-ubuntu:~$ cat /etc/shells
# /etc/shells: valid login shells
/bin/sh
/bin/bash
/usr/bin/bash
/bin/rbash
/usr/bin/rbash
/usr/bin/sh
/bin/dash
/usr/bin/dash
/usr/bin/tmux
/usr/bin/screen
/bin/zsh
/usr/bin/zsh
```

因为我已经安装了 zsh，所以已经有了 zsh

zsh 的安装

```bash
sudo apt install wget git curl vim -y
```

安装后，会有系统内核升级的提示，一路按回车

安装好后后再使用 cat 查看系统支持的shell，会看到比刚才多了 zsh，这样 zsh 的安装就完成了

然后，将系统默认shell 切换为 zsh

```bash
chsh -s $(which zsh)
```

### 二、安装 p10k

```text
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ~/powerlevel10k
```

国内用户可以放心使用下面 [http://gitee.com](https://link.zhihu.com/?target=http%3A//gitee.com) 上的官方镜像加速下载.

```text
git clone --depth=1 https://gitee.com/romkatv/powerlevel10k.git ~/powerlevel10k
```

推荐同时下载另外两个插件

```text
# zsh-autosuggestions自动提示插件
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
# zsh-syntax-highlighting语法高亮插件
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```

### 三、安装 Oh-My-Zsh

执行语句；

```text
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
```

中国用户可以使用 [http://gitee.com](https://link.zhihu.com/?target=http%3A//gitee.com) 上的官方镜像加速下载.

```text
git clone --depth=1 https://gitee.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
```

### 四、安装 Nerd 字体

由于我是在 win10 系统下，使用 VSCode 连接服务器的，我在电脑安装并在 VSCode 配置字体就可以了

如果不安装，会类似下图，有未知符号

> Powerlevel10k不需要自定义字体，但如果有的话可以利用它们。它可以很好地与Nerd Fonts, Source Code Pro, Font Awesome, Powerline，甚至默认的系统字体配合使用。只有在使用Nerd字体时，才能使用完整的样式选项。推荐字体:为Powerlevel10k修补的Meslo Nerd字体。



直接点击下面四个链接下载 ttf 文件并安装，官方链接

- - [MesloLGS NF Regular.ttf](https://link.zhihu.com/?target=https%3A//github.com/romkatv/powerlevel10k-media/raw/master/MesloLGS%20NF%20Regular.ttf)
  - [MesloLGS NF Bold.ttf](https://link.zhihu.com/?target=https%3A//github.com/romkatv/powerlevel10k-media/raw/master/MesloLGS%20NF%20Bold.ttf)
  - [MesloLGS NF Italic.ttf](https://link.zhihu.com/?target=https%3A//github.com/romkatv/powerlevel10k-media/raw/master/MesloLGS%20NF%20Italic.ttf)
  - [MesloLGS NF Bold Italic.ttf](https://link.zhihu.com/?target=https%3A//github.com/romkatv/powerlevel10k-media/raw/master/MesloLGS%20NF%20Bold%20Italic.ttf)

安装好后，在 VSCode 设置中输入 editor.font 找到 Font Family，设置为 MesloLGS NF 即可。

2024/9/24 更新，修改 Font Family 会一起修改编辑器中代码的字体，可以在设置中输入 terminal.integrated.font，设为 MesloLGS NF，同样会生效

### 五、配置文件 zshrc

修改以下两点即可，启动插件和主题，git 是默认启用的，主要添加后面两个

```text
# 修改主题
ZSH_THEME="powerlevel10k/powerlevel10k"

# 启用插件
plugins=(
  git
  zsh-autosuggestions
  zsh-syntax-highlighting
)
```

### 六、配置 p10k

输入以下命令即可配置 p10k，

```text
p10k configure
```

这里有一个很大的坑，我配置过程中，总是跳过最关键的 prompt style 这一步，导致我无法设置我最想要的 rainbow 效果

![img](https://pic2.zhimg.com/80/v2-a094a5aa153534a4269cecadd514a383_1440w.webp)

**需要终端输入以下命令，将终端配置支持 24 位[真彩色](https://zhida.zhihu.com/search?q=真彩色&zhida_source=entity&is_preview=1)**（这里我浪费了很多时间）

```text
export TERM="xterm-256color"
```

然后再执行 p10k configure，就会有 prompt style 选项了。

如果想重新配置，再次输入下面命令即可

```text
p10k configure
```

到此为止终于完成了！





参考链接：

1. [romkatv/powerlevel10k: A Zsh theme (github.com)](https://link.zhihu.com/?target=https%3A//github.com/romkatv/powerlevel10k%3Ftab%3Dreadme-ov-file%23oh-my-zsh)
2. [在windows中ohmyzsh 的powerlevel10k主题及插件推荐_powerlevel10k 字体下载-CSDN博客](https://link.zhihu.com/?target=https%3A//blog.csdn.net/KeyBordkiller/article/details/109537610)
3. [利用zsh+oh-my-zsh+powerlevel10k为Linux终端配置一个漂亮的shell_zsh powerlevel10k-CSDN博客](https://link.zhihu.com/?target=https%3A//blog.csdn.net/m0_72357534/article/details/135453423)
