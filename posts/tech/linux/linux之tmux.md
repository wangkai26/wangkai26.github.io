---
title: 'Linux之tmux'
date: 2024-09-20T21:15:39+08:00               # 创建时间
lastmod: 2024-09-20T21:15:39+08:00            # 更新时间
author: ["kai"]                 # 作者
draft: false                    # 是否为草稿
searchHidden: false
categories: 
- 分类1
tags: 
- 标签1
description: ""                 # 描述
weight:                         # 输入1可以顶置文章，用来给文章展示排序，不填就默认按时间排序
slug: ""
draft: false 
comments: true                  # 是否展示评论
showToc: true                   # 显示目录
TocOpen: true                   # 自动展开目录
hidemeta: false                 # 是否隐藏文章的元信息，如发布日期、作者等
disableShare: true              # 底部不显示分享栏
showbreadcrumbs: true           # 顶部显示当前路径
cover:
    image: ""                   # 图片路径：posts/tech/文章1/picture.png
    caption: ""                 # 图片底部描述
    alt: ""
    relative: false
---





# tmux

cd # 可快速切换到当前用户根目录下

tmux



## 安装 tmux

```bash
sudo apt-get install tmux
```



## 新建 tmux 终端

```

```



## tmux 常用命令





```bash
#列出创建的 tmux 进程
tmux list-sessions

# 创建新的 session,创建后会自动进入该 tmux 的 session 下
tmux new -s session_name 
# 等价于
tmux new-session -s session_name

# 回到之前某个会话
tmux a -t session_name
 
# 退出到主界面
tmux det

```



## ctrl + b



若创建了多个会话

```
先按ctrl+b ，再按s，然后就可以在会话间选择其中一个，按enter进入。
```

查看会话里的历史[信息记录](https://so.csdn.net/so/search?q=信息记录&spm=1001.2101.3001.7020)

```
先按ctrl+b，然后按Page Up ，Page Down
#  按 q 退出历史信息查看模式
```



按 c

切换到不同的 tmux session



tmux 终端下，按下 ctrl + b，然后再按 d，会将该终端和 ssh 会话分离，回到







回到某个 session

tmux a -t session_name

可以先关掉终端，过一会儿再回来看 ouput 是否有对应文件，



删除 session

tmux kill-session -t session_name



使用tmux时，有一个问题，我在普通ssh终端，上下划动鼠标滚轮时，能够看到之前的数据，但在 tmux 内，我划动滚轮时，会在命令行切换之前输入过的命令，我该如何恢复

> 在 tmux 中，滚动鼠标滚轮时默认情况下是用于滚动 tmux 的缓冲区而不是终端的滚动。如果您想在 tmux 中恢复使用滚轮滚动终端的功能，您可以进行以下配置：
>
> 1. 打开 tmux 配置文件（通常是 ~/.tmux.conf）：
>
> ```Shell
> vi ~/.tmux.conf
> ```
>
> 1. 在配置文件中添加以下行：
>
> ```Shell
> set -g mouse on
> ```
>
> 1. 保存并关闭文件。
> 2. 重新加载 tmux 配置：
>
> ```Shell
> tmux source-file ~/.tmux.conf
> ```
>
> 现在，您应该能够在 tmux 中使用鼠标滚轮来滚动终端，并查看之前的输出。
>
> 
>
> 请注意，某些终端模拟器可能需要额外的配置才能支持鼠标滚轮功能。如果上述配置不起作用，请确保您的终端模拟器已启用了鼠标滚轮支持，并查阅相应终端模拟器的文档以获取更多信息。





参考链接：

tmux：https://blog.csdn.net/m0_65266030/article/details/135510327



https://www.cnblogs.com/wanglouxiaozi/p/14813284.html

终端复用器Tmux（一个让你彻底放弃 nohup/& 命令的工具）

https://blog.csdn.net/m0_65266030/article/details/135510327

https://blog.csdn.net/qq_18677445/article/details/139146070

终端复用器：https://www.cnblogs.com/wanglouxiaozi/p/14813284.html

还有一个可以让命令在后台持续运行，nohup

https://www.ruanyifeng.com/blog/2019/10/tmux.html
