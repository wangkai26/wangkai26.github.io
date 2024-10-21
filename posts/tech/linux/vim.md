---
title: 'Vim'
date: 2024-09-22T13:21:29+08:00               # 创建时间
lastmod: 2024-09-22T13:21:29+08:00            # 更新时间
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







报错：

> E325: ATTENTION
> Found a swap file by the name "/var/tmp/hello.sh.swp"
>           owned by: ubuntu   dated: Fri Oct 04 12:15:26 2024
>          file name: /data/exer_sh/hello.sh
>           modified: no
>          user name: ubuntu   host name: VM-12-2-ubuntu
>         process ID: 3404503 (STILL RUNNING)
> While opening file "hello.sh"
>       CANNOT BE FOUND
> (1) Another program may be editing the same file.  If this is the case,
>     be careful not to end up with two different instances of the same
>     file when making changes.  Quit, or continue with caution.
> (2) An edit session for this file crashed.
>     If this is the case, use ":recover" or "vim -r hello.sh"
>     to recover the changes (see ":help recovery").
>     If you did this already, delete the swap file "/var/tmp/hello.sh.swp"
>     to avoid this message.





第一个 shell 脚本

```shell
vim hello.sh
```

第一行井号开头的内容代表 使用 zsh 执行命令

```shell
#!/bin/zsh
echo "hello,world!"
date
pwd
whoami
echo "end"
```

写完之后，使用 chmod 命令给文件添加执行权限，否则执行时会遇到报错：zsh: permission denied

```shell
chmod a+x hello.sh
```

切换根用户执行脚本文件，sudo su



执行结果：

```shell
VM-12-2-ubuntu# ./hello.sh 
hello,world!
Sat Oct  5 01:35:58 PM CST 2024
/data/exer_sh
root
end
```

符合预期

这就是一个最简单的脚本的执行过程



shell 脚本支持分支、条件判断 和 循环等编程语言中才有的特性，也可以定义函数和变量，可以调用系统命令以及其他程序，还可以进行文件读写等操作，是非常强大的工具。

