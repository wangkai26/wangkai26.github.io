---
title: 'Vscode'
date: 2024-10-05T14:06:41+08:00               # 创建时间
lastmod: 2024-10-05T14:06:41+08:00            # 更新时间
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


# VScode



## 常用插件

一、普适

Chinese (Simplified) (简体中文) Language Pack for Visu

为 VS Code提供本地化界面

二、Python相关

Python

三、前端开发

https://blog.csdn.net/weixin_43248785/article/details/105095440

open in browser

这允许您在默认浏览器或应用程序中打开当前文件。

## 各种快捷键

https://zhuanlan.zhihu.com/p/44044896

- 新建窗口：ctrl + shift + n
- 回到顶部：ctrl + home



better comment 

Better Comments 可在注释标识后插入特殊符号，从而更改注释颜色，不同符号对应的颜色如下

- ! red
- ? Blue
- *Green
- ^Yellow
- &Pink
- ~Purple
- todo Muscl



设置自动保存代码

问题：运行代码时，发现运行的还是修改前的代码，解决可以通过 ctrl+s 手动保存，但有点麻烦

解决：VSCode 左下角齿轮 设置 -> 搜索 Auto Save

四个选项

1. off 关闭
2. afterDelay  多少毫秒后自动保存
3. onFocusChange 编辑器失去焦点时自动保存。也就是鼠标在编辑器之外的区域按下左键才会保存
4. onWindowsChange 窗口失去焦点时，自动保存。即鼠标在 VScode 软件之外的界面按下左键才会保存。

一般使用 afterDelay，选用 100 ms 即可，相当于输入代码实时保存了。



vue 与 前端三件套 的区别：

1. Vue 是一个框架，而前端三件套是一组技术，由 HTML、CSS 和 JavaScript 组成。

2. Vue 是一个用于构建用户界面的 JavaScript 框架，它提供了一组可重用的组件，可以帮助开发者更快地构建 Web 应用程序。而前端三件套则是一组技术，分别用于构建网页的样式、结构和行为。

3. Vue 具有更强大的模板功能，可以帮助开发者更好地管理数据，而前端三件套则没有这样的功能。

vue的自动化构建工具是[node](https://so.csdn.net/so/search?q=node&spm=1001.2101.3001.7020).js帮我们做的，这就是我们为什么要下载node的原因。

# vue 安装及其环境配置

- https://blog.csdn.net/dream_summer/article/details/108867317
- https://blog.csdn.net/weixin_44431812/article/details/122270467?utm_medium=distribute.pc_relevant.none-task-blog-2~default~baidujs_baidulandingword~default-0-122270467-blog-103855188.235^v38^pc_relevant_default_base&spm=1001.2101.3001.4242.1&utm_relevant_index=3

## 安装 Node.js

一、安装 node.js， https://nodejs.org/en/download。由于 Node.js 中默认安装了 npm，所以无需额外配置即可在全局命令中使用 npm，测试是否安装成功，输入 node -v 与 npm -v 查看版本信息。

> C:\Users\wangkai1>node -v
> v18.17.1
>
> C:\Users\wangkai1>npm -v
> 9.6.7

二、配置默认安装目录和缓存目录

说明：这里的环境配置主要配置的是npm安装的全局模块所在的路径，以及缓存cache的路径，之所以要配置，是因为以后在执行类似：npm install express [-g] （后面的可选参数-g，g代表global全局安装的意思）的安装语句时，会将安装的模块安装到【C:\Users\用户名\AppData\Roaming\npm】路径中，占C盘空间。


> C:\Users\wangkai1>npm list -global
> npm ERR! code ENOENT
> npm ERR! syscall lstat
> npm ERR! path C:\Users\wangkai1\AppData\Roaming\npm
> npm ERR! errno -4058
> npm ERR! enoent ENOENT: no such file or directory, lstat 'C:\Users\wangkai1\AppData\Roaming\npm'
> npm ERR! enoent This is related to npm not being able to find a file.
> npm ERR! enoent
>
> npm ERR! A complete log of this run can be found in: C:\Users\wangkai1\AppData\Local\npm-cache\_logs\2023-09-03T09_13_25_845Z-debug-0.log

原因未知。

在安装目录下，新建文件夹 node_cache 和 node_global，然后执行命令，将npm的全局模块目录和缓存目录配置到我们刚才创建的那两个目录：

> C:\Users\wangkai1>npm config set prefix "D:\install_location\node_wk\node_global"
>
> C:\Users\wangkai1>npm config set cache "D:\install_location\node_wk\node_cache"

`npm config get prefix`查看npm全局安装包保存路径
`npm config get cache`查看npm装包缓存路径

现在再输入 npm list -global 就正常了

> C:\Users\wangkai1>npm list -global
> D:\install_location\node_wk\node_global
> `-- (empty)

`npm config list`查看所有npm 配置

> C:\Users\wangkai1>npm config list
> ; "builtin" config from D:\install_location\node_wk\node_modules\npm\npmrc
>
> ; prefix = "C:\\Users\\wangkai1\\AppData\\Roaming\\npm" ; overridden by user
>
> ; "user" config from C:\Users\wangkai1\.npmrc
>
> cache = "D:\\install_location\\node_wk\\node_cache"
> prefix = "D:\\install_location\\node_wk\\node_global"
>
> ; node bin location = D:\install_location\node_wk\node.exe
> ; node version = v18.17.1
> ; npm local prefix = C:\Users\wangkai1
> ; npm version = 9.6.7
> ; cwd = C:\Users\wangkai1
> ; HOME = C:\Users\wangkai1
> ; Run `npm config ls -l` to show all defaults.

三、Node.js 环境配置

首先，我的安装路径是：D:\install_location\node_wk

1. 系统变量新增，变量名：NODE_PATH，变量值：D:\install_location\node_wk\node_global\node_modules
2. 系统变量的 path 下，新建 node 的路径，（我打开查看已经有了，可能是我的 node 版本较新）
3. 设置了全局安装目录后，将用户变量 -> path 下的 npm 修改为 D:\Program Files\nodejs\node_global，我这里具体是 将 “C:\Users\wangkai1\AppData\Roaming\npm” 修改为 “D:\install_location\node_wk\node_global”

四、配置淘宝镜像源

先查看当前的下载源，registry 是注册表的意思

> C:\Users\wangkai1>npm config get registry
> https://registry.npmjs.org/

目前是国外站点，将npm的模块下载仓库从默认的国外站点改为国内的站点，这样下载模块的速度才能比较快，现在用的都是淘宝镜像源（https://registry.npm.taobao.org），使用淘宝镜像源有两种方式：临时使用和永久使用

临时使用：

```
npm --registry https://registry.npm.taobao.org install cluster
```

这个代码就是只在安装cluster的使用淘宝镜像下载，每次安装一个模块都用挺长的代码，比较繁琐，所以推荐第二种方式。

永久使用：

两种配置选择，一是直接修改npm命令的仓库地址为淘宝镜像源，另一种是安装cnpm命令。

第一种:直接修改npm的默认配置

```
npm config set registry https://registry.npm.taobao.org 
```

然后用 get 进行验证

```
C:\Users\wangkai1>npm config get registry
https://registry.npm.taobao.org
```

配置成功

第二种是 安装 cnpm，跳过

npm 结束

## 安装 vue 及 脚手架

一、安装 vue.js

```
npm install vue -g`或者`cnpm install vue -g
```

其中-g是全局安装，指安装到global全局目录去

遇到报错：

> C:\Users\wangkai1>npm install vue -g
> npm ERR! code EPERM
> npm ERR! syscall mkdir
> npm ERR! path D:\install_location\node_wk\node_cache\_cacache
> npm ERR! errno -4048
> npm ERR! Error: EPERM: operation not permitted, mkdir 'D:\install_location\node_wk\node_cache\_cacache'
> npm ERR!  [Error: EPERM: operation not permitted, mkdir 'D:\install_location\node_wk\node_cache\_cacache'] {
> npm ERR!   errno: -4048,
> npm ERR!   code: 'EPERM',
> npm ERR!   syscall: 'mkdir',
> npm ERR!   path: 'D:\\install_location\\node_wk\\node_cache\\_cacache',
> npm ERR!   requiredBy: '.'
> npm ERR! }
> npm ERR!
> npm ERR! The operation was rejected by your operating system.
> npm ERR! It's possible that the file was already in use (by a text editor or antivirus),
> npm ERR! or that you lack permissions to access it.
> npm ERR!
> npm ERR! If you believe this might be a permissions issue, please double-check the
> npm ERR! permissions of the file and its containing directories, or try running
> npm ERR! the command again as root/Administrator.
>
> npm ERR! Log files were not written due to an error writing to the directory: D:\install_location\node_wk\node_cache\_logs
> npm ERR! You can rerun the command with `--loglevel=verbose` to see the logs in your terminal

[npm安装报错（npm ERR! code EPERM npm ERR! syscall mkdir npm ERR! path C:\Program Files\nodejs\node_ca...）_婷婷心慌的博客-CSDN博客](https://blog.csdn.net/qq_42780155/article/details/119025638)

评论区说是权限问题，管理员身份运行cmd即可

删除 用户\wangkai1 下的 .npmrc 文件（隐藏）

可以了。

```
C:\Users\wangkai1>npm install vue -g

added 20 packages in 42s

2 packages are looking for funding
  run `npm fund` for details
npm notice
npm notice New major version of npm available! 9.6.7 -> 10.0.0
npm notice Changelog: https://github.com/npm/cli/releases/tag/v10.0.0
npm notice Run npm install -g npm@10.0.0 to update!
npm notice
```

查看安装的vue信息：`npm info vue` 或者`cnpm info vue`

```
C:\Users\wangkai1>npm info vue

vue@3.3.4 | MIT | deps: 5 | versions: 445
The progressive JavaScript framework for building modern web UI.
https://github.com/vuejs/core/tree/main/packages/vue#readme

keywords: vue

dist
.tarball: https://registry.npmjs.org/vue/-/vue-3.3.4.tgz
.shasum: 8ed945d3873667df1d0fcf3b2463ada028f88bd6
.integrity: sha512-VTyEYn3yvIeY1Py0WaYGZsXnz3y5UnGi62GjVEqvEGPl6nxbOrCXbVOTQWBEJUqAyTUk2uJ5JLVnYJ6ZzGbrSw==
.unpackedSize: 2.0 MB

dependencies:
@vue/compiler-dom: 3.3.4    @vue/runtime-dom: 3.3.4     @vue/shared: 3.3.4
@vue/compiler-sfc: 3.3.4    @vue/server-renderer: 3.3.4

maintainers:

- yyx990803 <yyx990803@gmail.com>
- posva <posva13@gmail.com>

dist-tags:
alpha: 3.3.0-alpha.13     latest: 3.3.4             v2-alpha: 2.7.0-alpha.12
beta: 3.3.0-beta.5        legacy: 2.6.14            v2-beta: 2.7.0-beta.8
csp: 1.0.28-csp           next: 3.2.36              v2-latest: 2.7.14

published 3 months ago by yyx990803 <yyx990803@gmail.com>
```

查看 vue 版本

```
C:\Users\wangkai1>npm list vue
C:\Users\wangkai1
`-- (empty)


C:\Users\wangkai1>npm list vue -g
C:\Users\wangkai1\AppData\Roaming\npm
`-- vue@3.3.4
  `-- @vue/server-renderer@3.3.4
    `-- vue@3.3.4 deduped
```

二、安装 webpack 模板

`npm install webpack -g`

```
C:\Users\wangkai1>npm install webpack -g

added 77 packages in 1m

9 packages are looking for funding
  run `npm fund` for details
```

webpack 4x以上，webpack将命令相关的内容都放到了webpack-cli，
所以还需要安装webpack-cli：`npm install --global webpack-cli`，
安装成功后可使用`webpack -v`查看版本号。

```
C:\Users\wangkai1>npm install --global webpack-cli

added 117 packages in 51s

15 packages are looking for funding
  run `npm fund` for details
```

不行，

```
C:\Users\wangkai1>webpack -v
'webpack' 不是内部或外部命令，也不是可运行的程序
或批处理文件。
```

找到 下载 npm 根路径

```
C:\Users\wangkai1>npm root -g
C:\Users\wangkai1\AppData\Roaming\npm\node_modules
```

哎呀，都下载都 c 盘里面了，什么情况。

先不管了，

https://blog.csdn.net/qq_39742704/article/details/120251085

解决方案：将根路径 去掉 node_module，添加到系统变量的 path。

```
C:\Users\wangkai1>webpack -v

  System:
    OS: Windows 10 10.0.19045
    CPU: (16) x64 AMD Ryzen 7 6800H with Radeon Graphics
    Memory: 7.56 GB / 13.69 GB
  Binaries:
    Node: 18.17.1 - D:\install_location\node_wk\node.EXE
    npm: 9.6.7 - D:\install_location\node_wk\npm.CMD
  Browsers:
    Edge: Spartan (44.19041.1266.0), Chromium (116.0.1938.69)
    Internet Explorer: 11.0.19041.1566
```

三、安装脚手架 vue-cli

`npm install vue-cli -g`

使用 `vue --version` 检查版本是否正确，也可以 `vue -V`，但 `vue -v` 不可以

```
C:\Users\wangkai1>vue --version
2.9.6
```

然后顺手安上 vue-router，`npm install -g vue-router`

哎，这里和教程不一样了，教程是安装在了D盘，我全安装在了C盘，不知道是哪里出了问题。

四、vue-cli 创建 vue 项目

1、创建项目（最好在cd到D盘的某个位置，即项目的路径，否则项目会新建在C:\Users\Administrator\，也可以直接在想要的项目路径下输入cmd）`vue init webpack 项目名`



```
D:\study_front>vue init webpack vue_demo
? Project name vue_demo
? Project description A Vue.js project
? Vue build standalone
? Install vue-router? Yes
? Use ESLint to lint your code? No
? Set up unit tests No
? Setup e2e tests with Nightwatch? No
? Should we run `npm install` for you after the project has been created? (recommended) npm

   vue-cli · Generated "vue_demo".


# Installing project dependencies ...
# ========================

npm WARN deprecated consolidate@0.14.5: Please upgrade to consolidate v1.0.0+ as it has been modernized with several long-awaited fixes implemented. Maintenance is supported by Forward Email at https://forwardemail.net ; follow/watch https://github.com/ladjs/consolidate for updates and release changelog
npm WARN deprecated stable@0.1.8: Modern JS already guarantees Array#sort() is a stable sort, so this library is deprecated. See the compatibility table on MDN: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort#browser_compatibility
npm WARN deprecated uuid@3.4.0: Please upgrade  to version 7 or higher.  Older versions may use Math.random() in certain circumstances, which is known to be problematic.  See https://v8.dev/blog/math-random for details.
npm WARN deprecated source-map-url@0.4.1: See https://github.com/lydell/source-map-url#deprecated
npm WARN deprecated urix@0.1.0: Please see https://github.com/lydell/urix#deprecated
npm WARN deprecated resolve-url@0.2.1: https://github.com/lydell/resolve-url#deprecated
npm WARN deprecated source-map-resolve@0.5.3: See https://github.com/lydell/source-map-resolve#deprecated
npm WARN deprecated bfj-node4@5.3.1: Switch to the `bfj` package for fixes and new features!
npm WARN deprecated acorn-dynamic-import@2.0.2: This is probably built in to whatever tool you're using. If you still need it... idk
npm WARN deprecated flatten@1.0.3: flatten is deprecated in favor of utility frameworks such as lodash.
npm WARN deprecated svgo@0.7.2: This SVGO version is no longer supported. Upgrade to v2.x.x.
npm WARN deprecated uglify-es@3.3.9: support for ECMAScript is superseded by `uglify-js` as of v3.13.0
npm WARN deprecated browserslist@2.11.3: Browserslist 2 could fail on reading Browserslist >3.0 config used in other tools.
npm WARN deprecated html-webpack-plugin@2.30.1: out of support
npm WARN deprecated core-js@2.6.12: core-js@<3.23.3 is no longer maintained and not recommended for usage due to the number of issues. Because of the V8 engine whims, feature detection in old core-js versions could cause a slowdown up to 100x even if nothing is polyfilled. Some versions have web compatibility issues. Please, upgrade your dependencies to the actual version of core-js.
npm WARN deprecated extract-text-webpack-plugin@3.0.2: Deprecated. Please use https://github.com/webpack-contrib/mini-css-extract-plugin
npm WARN deprecated svgo@1.3.2: This SVGO version is no longer supported. Upgrade to v2.x.x.
npm WARN deprecated chokidar@2.1.8: Chokidar 2 does not receive security updates since 2019. Upgrade to chokidar 3 with 15x fewer dependencies
npm WARN deprecated browserslist@1.7.7: Browserslist 2 could fail on reading Browserslist >3.0 config used in other tools.
npm WARN deprecated browserslist@1.7.7: Browserslist 2 could fail on reading Browserslist >3.0 config used in other tools.
npm WARN deprecated browserslist@1.7.7: Browserslist 2 could fail on reading Browserslist >3.0 config used in other tools.
npm WARN deprecated chokidar@2.1.8: Chokidar 2 does not receive security updates since 2019. Upgrade to chokidar 3 with 15x fewer dependencies

added 1313 packages, and audited 1314 packages in 4m

90 packages are looking for funding
  run `npm fund` for details

86 vulnerabilities (1 low, 49 moderate, 29 high, 7 critical)

To address issues that do not require attention, run:
  npm audit fix

To address all issues (including breaking changes), run:
  npm audit fix --force

Run `npm audit` for details.

# Project initialization finished!
# ========================

To get started:

  cd vue_demo
  npm run dev

Documentation can be found at https://vuejs-templates.github.io/webpack
```



进入到项目目录下，执行 `npm run dev`

```
D:\study_front\vue_demo>npm run dev

> vue_demo@1.0.0 dev
> webpack-dev-server --inline --progress --config build/webpack.dev.conf.js

(node:10000) [DEP0111] DeprecationWarning: Access to process.binding('http_parser') is deprecated.
(Use `node --trace-deprecation ...` to show where the warning was created)
 12% building modules 22/27 modules 5 active ...0!D:\study_front\vue_demo\src\App.vue{ parser: "babylon" } is deprecated; we now treat it as { parser: "babel" }.
 95% emitting

 DONE  Compiled successfully in 17440ms                                                                         19:20:25

 I  Your application is running here: http://localhost:8080
```

访问这个地址：http://localhost:8080/#/ 即可

成功啦！

npm run dev 和 npm run server https://blog.csdn.net/weixin_44152565/article/details/111355262

# cd

cmd

`cd /d D:` 可以切换到D盘





## 每次只能打开一个编辑窗口

[成功解决VScode每次只能打开一个文件，即只能打开一个编辑窗口。_旋转的油纸伞的博客-CSDN博客](https://blog.csdn.net/qq_45934285/article/details/131737203?spm=1001.2101.3001.6650.3&utm_medium=distribute.pc_relevant.none-task-blog-2~default~YuanLiJiHua~Position-3-131737203-blog-108622110.235^v38^pc_relevant_default_base&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2~default~YuanLiJiHua~Position-3-131737203-blog-108622110.235^v38^pc_relevant_default_base&utm_relevant_index=4)

文件 --> [首选项](https://so.csdn.net/so/search?q=首选项&spm=1001.2101.3001.7020) --> 设置 --> 工作台 --> 编辑管理 --> `取消勾选Enable Preview`





后端：

