---
title: 'Basic'
date: 2024-09-17T15:31:08+08:00 #创建时间
lastmod: 2024-09-17T15:31:08+08:00 #更新时间
author: ["kai"] #作者
draft: false
searchHidden: false
tags: 
- hugo
---


---
date: 2024-02-02T04:14:54-08:00
draft: false
params:
  author: kai
title: hugo使用title
weight: 10

---



验证是否安装完成：

输入 `hguo version`，检查是否有如下打印信息

```
D:\github-kai\kai_blog>hugo version
hugo v0.131.0-bfbee17932ff24009008aa94cdd75c0c41f59279 windows/amd64 BuildDate=2024-08-02T09:03:48Z VendorInfo=gohugoio
```



快速运行流程：

1. 在 quickstart 目录中为您的项目创建 目录结构 `hugo new site quickstart`
2. 将当前目录更改为项目的根目录。`cd quickstart`
3. 进入 themes 目录，下载主题，如 papermod，`git clone https://github.com/adityatelange/hugo-PaperMod.git`


4. 回到主目录启动 Hugo 启动本地服务器并生成站点内容，`hugo server -D`





重要链接：

1. [Features · adityatelange/hugo-PaperMod Wiki (github.com)](https://github.com/adityatelange/hugo-PaperMod/wiki/Features#edit-link-for-posts)
2. [[置顶\] hugo博客搭建 | PaperMod主题 | Sulv's Blog (sulvblog.cn)](https://www.sulvblog.cn/posts/blog/build_hugo/)



[[golang\][hugo]使用Hugo搭建静态站点-腾讯云开发者社区-腾讯云 (tencent.com)](https://cloud.tencent.com/developer/article/1546275)

[Hugo | 一起动手搭建个人博客吧 | 小球飞鱼 (mantyke.icu)](https://mantyke.icu/posts/2021/hugo-build-blog/)

https://blog.csdn.net/p_function/article/details/103842298


https://www.emojiall.com/zh-hans/all-emojis

https://bore.vip/archives/ca21a352/index.html
https://www.shaohanyun.top/posts/env/blog_build2/
https://dvel.me/posts/hugo-papermod-config/#markdown-%e6%b8%b2%e6%9f%93%e9%a3%8e%e6%a0%bc

Hugo 与 github page 关联
https://ratmomo.github.io/p/2024/06/%E4%BD%BF%E7%94%A8-hugo--github-pages-%E9%83%A8%E7%BD%B2%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2/

1. 安装hugo


创建项目

Hugo new
PS D:\github-kai> hugo new site kai-blog
Congratulations! Your new Hugo site was created in D:\github-kai\kai-blog.

Just a few more steps...

1. Change the current directory to D:\github-kai\kai-blog.
2. Create or install a theme:

  - Create a new theme with the command "hugo new theme <THEMENAME>"
  - Or, install a theme from https://themes.gohugo.io/

3. Edit hugo.toml, setting the "theme" property to the theme name.
4. Create new content with the command "hugo new content <SECTIONNAME>\<FILENAME>.<FORMAT>".
5. Start the embedded web server with the command "hugo server --buildDrafts".

See documentation at https://gohugo.io/.

建好后，有以下内容：

1. Archetypes   有 default.md
2. Assets          空
3. Content         空
4. Data         空
5. i18n         空
6. Layouts         空
7. Static         空
8. Themes         空
9. hugo.toml     1kb

参考教程：

1. https://www.sulvblog.cn/
2. https://www.sulvblog.cn/posts/blog/build_hugo/#6%e5%90%af%e5%8a%a8%e5%8d%9a%e5%ae%a2
3. 















## 配置文件 - 基本

注意：没有配置 theme 时，本地运行，页面会是：Page Not Found

默认的配置文件为根目录下 hugo.toml 文件

默认内容：

```toml
baseURL = 'https://example.org/'
languageCode = 'en-us'
title = 'ABC Widgets, Inc.'
[params]
  subtitle = 'The Best Widgets on Earth'
  [params.contact]
    email = 'info@example.org'
    phone = '+1 202-555-1212'
```



**查看默认加载路径**： Hugo会按优先级顺序尝试加载以下配置文件，你可以根据这些默认路径检查配置文件：

- `config.yaml`
- `config.toml`
- `config.json`

如果你有多个配置文件（例如`hugo.yaml`和`hugo.toml`），Hugo会根据文件类型加载默认的`config.yaml`、`config.toml`或`config.json`。确保你命名的配置文件是`config.yaml`而不是`hugo.yaml`。



因为不习惯 toml 的语法，所以我删除了原先的 hugo.toml，新建了文件 config.yaml 

```yaml
baseURL: https://example.org/
languageCode: en-us
title: My New Hugo Site.
theme: hugo-PaperMod # 主题名字，和themes文件夹下的一致
```



## 配置文件 - 进阶





### 站点导航菜单 menu





在 Hugo 中，`menu`配置项用于定义站点导航菜单，`identifier`是每个菜单条目的一个唯一标识符。



# PaperMod

[Features · adityatelange/hugo-PaperMod Wiki (github.com)](https://github.com/adityatelange/hugo-PaperMod/wiki/Features#profile-mode)









时间轴设置

archives，注意设置 layout: "archives" ，这是最核心的









## 文件头部规范



```
+++
Categories =["github"]
Tags = ["github", "开发者", "go"]
date = "2019-12-12T18:20:42+08:00"
title = "hugo搭建github博客过程"
description = "landv"
+++
```

- 1.title 文章名称
- 2.description 文章详细介绍
- 3.tag 标签
- 4.categories 文章分类





## _index 作用



如果在文件夹下不生成 _index.md 文件

那进入主页的 posts 可以直接看到文章标题

但在主页点击按钮会进入 404 界面，因为无法找到 url

```yaml
    buttons:
      - name: 👨🏻‍💻技术
        url: posts/tech
      - name: 📕阅读
        url: posts/read
      - name: 🏖生活
        url: posts/life
```



只要创建了 _index.md 文件，甚至不需要任何内容，再点击按钮就可以到文章界面



## 常用命令



```shell
#使用方法:
  hugo
  hugo [flags]
  hugo [command]
  hugo [command] [flags]

#查看版本
hugo version

#版本和环境详细信息
hugo env

#创建新站点
hugo new site "$mysite"

#创建文章
hugo new index.md  

在content/文件夹可以看到，此时多了一个markdown格式的文件index.md，打开文件可以看到时间和文件名等信息已经自动加到文件开头，包括创建时间，页面名，是否为草稿等。

#编译生成静态文件，Hugo将编译所有文件并输出到public目录  
hugo
   

#编译生成静态文件并启动web服务
hugo server
```

常用参数：

```shell
 --bind="127.0.0.1"    服务监听IP地址；
  -p, --port=1313       服务监听端口；
  -w, --watch[=true]      监听站点目录，发现文件变更自动编译；
  -D, --buildDrafts     包括被标记为draft的文章；
  -E, --buildExpired    包括已过期的文章；
  -F, --buildFuture     包括将在未来发布的文章；
  -b, --baseURL="www.datals.com"  服务监听域名；
  --log[=false]:           开启日志；
  --logFile="/var/log/hugo.log":          log输出路径；
  -t, --theme=""          指定主题；
  -v, --verbose[=false]: 输出详细信息
```







# 一些小问题：

hugo server 和 hugo server -D 的区别：

1. **`hugo server -D`**： 这个命令会启动本地服务器并生成站点内容，同时包括所有标记为草稿的文章。也就是说，即使文章还在草稿状态（`draft: true`），它们也会在本地预览时显示出来。这对于开发和调试非常有用：

总结起来，`-D`参数的作用是确保包含草稿文章，以便在本地环境中可以预览和测试这些内容。如果你在开发过程中需要查看所有文章（包括草稿），推荐使用`hugo server -D`。而如果你只关心那些已经不是草稿的内容，可以仅使用`hugo server`。



2.profileMode 不生效

2. profileMode 不生效：

解决办法：将其放在 params 内部，

为什么使用 `params` 能够解决问题

1. **约定俗成**：Hugo 的设计理念中，把自定义的站点参数统一放在 `params` 下，是一种约定俗成的做法。这样不仅代码更加清晰，而且也避免了可能的命名冲突。
2. **模板访问**：将自定义参数放在 `params` 下，可以确保 Hugo 能够正确地将这些参数包含在其上下文中，使得它们能够被模板正确访问和渲染。
3. **一致性**：统一将所有自定义参数放在 `params` 下，保证了配置的结构和访问的一致性，使得管理配置更加方便。



### 报错：

defaultContentLanguage: "zh" # # 设置默认语言为中文

hugo new a.md 

panic: lang not set

解决办法，

将 `defaultContentLanguage: "zh"` 对应语言设置为和 `languageCode` 一样，我之前是因为 `defaultContentLanguage` 为空



生成文章不展示



可能是因为 draft 状态为 True，将其修改为 False 就可以啦。