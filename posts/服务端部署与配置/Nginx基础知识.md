---
title: 'Nginx基础知识'
date: 2024-10-19T16:27:44+08:00               # 创建时间
lastmod: 2024-10-19T16:27:44+08:00            # 更新时间
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

Nginx\kai

Nginx 是目前最流行的web服务器软件，也是目前互联网公司和网站的首选

快速入门和上手使用 Nginx

主要内容：

1. 基本概念
2. 安装配置
3. 常用命令
4. 反向代理
5. 负载均衡
6. 虚拟主机



最开始是由⼀个叫做igor的俄罗斯的程序员开发的，目的是为了解决 C10K 问题（C10K = 10000 concurrent connection，同时处理10000个并发连接），这个问题在当时是非常严重的，因为当时的服务器软件都是单线程的，所以在高并发的情况下，服务器的性能会变得非常差，Nginx 的出现很好地解决了这个问题，在官方的测试结果中，Nginx 可以支持5万个并发连接，在后来的发展中，Nginx 也逐渐成为了最流行的 Web 服务器软件

> 除了 Nginx，还有 Apache、Cloudflare、OpenResty 等服务器软件

2019年3⽉11⽇被美国的F5公司以6.7亿美元的价格收购，现在已经有了商业版本 Nginx Plus。一般使用开源版本的 Nginx 即可。



2019年3⽉11⽇被美国的F5公司以6.7亿美元的价格收购



## 安装Nginx

方式一：包管理器

我用的 Ubuntu，使用 apt 来安装

```
sudo apt update
sudo apt install nginx
```

输入一条install命令就可以了，比较推荐

方式二：编译安装

Nginx 是 C语言开发的，可以像其他C语言项目一样，下载Nginx源码到自己的服务器上，然后执行预编译、编译和安装的过程，这种方式比较灵活，可以自定义配置各种参数，适用于一些特殊场景，比如想要安装一些特殊的模块，想要修改一些源码来自定义一些功能。

可能会遇到一些问题，需要有一定排查和解决问题的能力

方式三：使用 Docker 安装

直接使用 Docker 镜像来安装和于小宁 Nginx

docker pull nginx

如果只是想学习和体验一下 Nginx 的话，这种方式也是够用的。



## 服务启停

直接在命令行终端输入 nginx 就可以了，回车之后没有任何提示消息的话，就表示启动成功了，这也是 Linux系统的一个设计思想，没有消息就是最好的消息，如果启动失败的话会有提示。

启动之后，打开浏览器，输入 localhost，可以看到 Nginx 的欢迎页面，表示服务器已经启动成功了。

Nginx 服务启动成功后，会作为一个后台进程一直运行，可以输入 ps -ef|grep nginx 来查看 Nginx 的进程

```
❯ ps -ef|grep nginx
root     2024851       1  0 Sep12 ?        00:00:00 nginx: master process /usr/sbin/nginx -g daemon on; master_process on;
www-data 2243671 2024851  0 Sep12 ?        00:00:01 nginx: worker process
www-data 2243672 2024851  0 Sep12 ?        00:00:00 nginx: worker process
ubuntu   2260361 2260131  0 21:13 pts/0    00:00:00 grep --color=auto --exclude-dir=.bzr --exclude-dir=CVS --exclude-dir=.git --exclude-dir=.hg --exclude-dir=.svn --exclude-dir=.idea --exclude-dir=.tox nginx
```

> **输出的每一列代表的含义**：
>
> - `UID`：进程所有者的用户名，例如 `root` 或 `www-data`。
> - `PID`：进程ID，是操作系统分配给每个进程的一个唯一标识符，例如 `2024851`。
> - `PPID`：父进程ID，即创建当前进程的进程的ID，例如 `1` (这是 `init` 进程的PID)。
> - `C`：CPU使用百分比，这里显示为0。
> - `STIME`：进程启动时间。
> - `TTY`：与进程关联的终端。
> - `TIME`：进程运行的总时间。
> - `CMD`：启动进程的命令。
>
> 根据你的输出，`nginx` 进程由 `root` 用户启动，主进程ID为 `2024851`，其工作进程由 `www-data` 用户运行。这些进程都有相同的父进程ID，即 `2024851`。

可以看到有一个 master 进程和两个 worker 进程（默认是只有一个的，我修改过配置，所以有两个）

了解 Nginx 的进程模型

master 进程就是 Nginx 的主进程，主要负责读取和验证配置文件，以及管理 worker 进程

worker 进程，就是 Nginx 的工作进程，负责处理实际的请求，

master进程只有一个，而 worker进程可以有多个，它们之间的关系就像老板和员工，worker进程的数量可以通过配置文件来调整，

在上面ps命令中，还可以看到它们的 PID，即进程ID，PID 是Linux系统中每个进程的唯一标识



还可以使用 lsof 命令查看端口占用情况，加 -i:80，表示只查看 80 端口，可以看到 80 端口正在被 nginx 的进程所占用，进程的 PID 就是刚才 ps 命令查看到的 PID，表示 Nginx 正在监听 80 端口。

```shell
❯ sudo lsof -i:80
COMMAND     PID     USER   FD   TYPE    DEVICE SIZE/OFF NODE NAME
nginx   2024851     root    6u  IPv4 411200955      0t0  TCP *:http (LISTEN)
nginx   2024851     root    7u  IPv6 411200956      0t0  TCP *:http (LISTEN)
nginx   2243671 www-data    6u  IPv4 411200955      0t0  TCP *:http (LISTEN)
nginx   2243671 www-data    7u  IPv6 411200956      0t0  TCP *:http (LISTEN)
nginx   2243672 www-data    6u  IPv4 411200955      0t0  TCP *:http (LISTEN)
nginx   2243672 www-data    7u  IPv6 411200956      0t0  TCP *:http (LISTEN)
```



这就是 Nginx 启动后，在系统中的一个情况



服务启动后，可以通过 nginx -s，后面加上一个 signal 来控制 Nginx 的停止或者重启，signal 可以是 stop、quit、reload 或者 reopen 中的一个。



nginx -s signal 

- quit：优雅停止
- stop：立即停止
- reload：重新配置文件
- reopen：重新打开日志文件



## 静态站点部署

- 服务启动后的默认页面是如何展示出来的？
- 如何从头开始搭建和部署一个属于自己的个人博客网站呢？

这节内容解决这两个问题



终端输入 nginx -V，可以查看 Nginx 的安装目录、编译参数 以及配置文件和日志文件的位置等各种信息，尤其是 Nginx 的配置文件的位置（nginx.conf），其位置与使用的操作系统 以及 安装 Nginx 的方式有关

```
❯ nginx -V
nginx version: nginx/1.18.0 (Ubuntu)
built with OpenSSL 3.0.2 15 Mar 2022
TLS SNI support enabled
configure arguments: --with-cc-opt='-g -O2 -ffile-prefix-map=/build/nginx-zctdR4/nginx-1.18.0=. -flto=auto -ffat-lto-objects -flto=auto -ffat-lto-objects -fstack-protector-strong -Wformat -Werror=format-security -fPIC -Wdate-time -D_FORTIFY_SOURCE=2' --with-ld-opt='-Wl,-Bsymbolic-functions -flto=auto -ffat-lto-objects -flto=auto -Wl,-z,relro -Wl,-z,now -fPIC' --prefix=/usr/share/nginx --conf-path=/etc/nginx/nginx.conf --http-log-path=/var/log/nginx/access.log --error-log-path=/var/log/nginx/error.log --lock-path=/var/lock/nginx.lock --pid-path=/run/nginx.pid --modules-path=/usr/lib/nginx/modules --http-client-body-temp-path=/var/lib/nginx/body --http-fastcgi-temp-path=/var/lib/nginx/fastcgi --http-proxy-temp-path=/var/lib/nginx/proxy --http-scgi-temp-path=/var/lib/nginx/scgi --http-uwsgi-temp-path=/var/lib/nginx/uwsgi --with-compat --with-debug --with-pcre-jit --with-http_ssl_module --with-http_stub_status_module --with-http_realip_module --with-http_auth_request_module --with-http_v2_module --with-http_dav_module --with-http_slice_module --with-threads --add-dynamic-module=/build/nginx-zctdR4/nginx-1.18.0/debian/modules/http-geoip2 --with-http_addition_module --with-http_gunzip_module --with-http_gzip_static_module --with-http_sub_module
```

不同的操作系统和不同的安装方式会导致这个配置文件的位置完全不同，可以使用 nginx -V 快速定位自己服务器上配置文件的准确位置，找到输入结果中的 --conf-path，等号后面的就是配置文件的位置

> Tips：也可以使用 nginx -t 查看
>
> 常见位置：
>
> - /etc/nginx/conf
> - /usr/local/etc/nginx
> - /opt/homebrew/etc/nginx

使用 VSCode 查看文件内容，文件结构下节再详细介绍，先找下默认页面的位置 

先找到 server.server.location （教程对应 nginx.conf 文件，但在我的 Ubuntu 服务器上，对应 sites-available/default 文件）

这个 location 会匹配我们在浏览器中输入的 URL，比如斜杠表示根目录，也就是当我们只输入一个 localhost 时，就会匹配到这个 location 中的内容，然后就会到它的指定目录下去找一个 index.html 文件，即在浏览器中看到的默认页面，root 对应的 html 就是目录所对应的文件夹，是一个相对路径，也就是相对 Nginx安装目录来说的，



## 配置文件

