---
title: 'Principles'
date: 2024-09-16T21:37:21+08:00 #创建时间
lastmod: 2024-09-16T21:37:21+08:00 #更新时间
author: ["kai"] #作者
draft: false
searchHidden: false
tags: 
- regex
---


正则表达式(Regular Expression)是一种文本模式，包括普通字符（例如，a 到 z 之间的字母）和特殊字符（称为"元字符"），可以用来描述和匹配字符串的特定模式。





## 正则表达式 

简介：正则表达式(Regular Expression)其实就是一门工具，**目的**是为了字符串模式匹配，从而实现搜索和替换功能。它是一种**用来描述规则的表达式**。而它的底层原理也十分简单，就是使用状态机的思想进行模式匹配。大家可以利用[regexper.com](https://link.juejin.cn/?target=https%3A%2F%2Fregexper.com%2F)这个工具很好地可视化自己写的正则表达式:





## 修饰符

正则表达式一般被两个斜线包裹起来，后面跟上一些修饰符，如，修饰符含义：

1. g 表示 global，即 全局匹配

2. i 表示 ignore case，即 忽略大小写

3. m 表示 multiline，即 多行匹配

   

## 基本语法-单个和多个字符



\ 代表转义字符，.、*、[、] 等，如果想要匹配它们本身的话，就需要在前面加一个反斜线来转义一下



匹配单个字符

. 在正则表达式中 表示出了换行符之外的任意一个字符



方括号表示字符的集合，方括号内部可以放 字符、数字 或 其他字符，

- 单个字符，如 abc123

- 可以使用一个中杠来表示范围。比如 a-z 表示从 a 到 z 的所有小写字母，1-3 代表 1 到 3 的所有数字。
- 尖括号表示取反，如：^a-z 代表除了小写字母之外的任意字符，^A-Za-z 代表除了字母之外的任意字符

notice：尖角号^只有在方括号内部才表示取反，在方括号外面表示匹配每一行的开头。



在正则表达式中，经常遇到匹配 数字、字母 或 空白字符这样的场景，如果每次都写方括号，再写一堆字符，会非常繁琐。

所以，正则表达式提供了一些预定义的字符类，用来匹配常见的字符，如 

- \d 代表数字，作用与 [0-9] 完全一致
- \D 代表非数字，等价于 [^0-9\]
- \w 代表 数字、字母 或 下划线，等价于
- \W 代表 \w 取反，数字、字母 或 下划线 之外的任意字符，比如 空白字符 或 一些特殊字符
- \s 代表 空白字符，代表 空格 或者 tab，
- \S 代表 \s 取反，非空白字符





## 位置和边界匹配 Anchors

常用 ^ 和 $，匹配每行的开头和结尾

\b 单词边界，boundary，比如，要找到文本中以 in 开头的字符，可以用 \bin，那 in 在单词中间 或 结尾，就不会被匹配到，想独立匹配 in 这个单词的话，就在前后都加上 \b，

\b 非单词边界，如 \bin\b，只有在单词中间的 in 会被匹配到，而开头、结尾 和 中间的 in 都不会被匹配到



## 量词 Quantifiers

量词，顾名思义，就是表示重复次数的

\+ 代表前面的字符 重复了一次或者 多次

\. 代表前面的字符重复了 零次 或者 多次

? 代表前面的字符重复了 零次 或者 一次

花括号表示指定的重复次数，比匹配 a 后面有 三个 t 这样的字符串的话，使用 at{3}，花括号中除了使用一个数字表示精确的重复次数外，还可以使用逗号分隔开的两个数字表示一个范围。如 3~5 个 t 的话，使用 at{3,5}。{3,} 表示至少重复了 3 次，

notice：正则表达式默认是贪婪匹配的，也就是会匹配尽可能多的字符。（默认情况下，尽可能多地匹配，直到不再满足匹配条件为止）

与贪婪模式相对的是 非贪婪模式，有时候不需要匹配尽可能多的字符，只需要满足最小的匹配条件就可以了，这时可以在量词后面加一个?，如 at{3,}? 匹配到三个 ? 后就会停止匹配



## 分组和引用 Groups

 分组可以将多个字符作为一个整体来处理

最简单的分组用法：比如，想要匹配多个 at，直接使用 at*，会匹配到 attt，使用 (at)\* 才会匹配到多个at，如 atatatat，表示 at 出现了多次，只想匹配 at 重复三次，可以使用 (at){3}

例子2：匹配 pattern 和 Pattern

可以使用方括号匹配 p 或 P，[pP]attern，还可以使用竖线，代表逻辑或：pattern|Pattern，如果使用 P|pattern，会匹配到 P 或则 pattern，匹配不到 Pattern，不符合需求，这时可以使用分组，将 P 和 p 括起来作为一个分组，然后再加上单词剩余的部分，(P|p)attern 即可。



使用小括号创建一个分组后，可以捕获这个分组的内容，在后续的处理中也可以引用或者提取这部分内容。如：



例子3：时间匹配和替换

要求：将以下时间均修改为 mm-dd-yyyy 的格式

> 2024-10-04
> 2024-10-05
> 2024-10-078
> 20240302
> 2021/54/26

首先匹配这三种时间格式， 表达式：`(\d{4})[-/.]?(\d{2})[-/.]?(\d{2})`，三个分组，分别为 年月日

替换的话，在 VSCode 和 regrex 中使用 $2-$3-$1 即可，其他编程语言也是类似的



有时，我们只是想要一个分组的功能，但是并不需要捕获这个分组，可以使用问号加一个冒号来表示非捕获分组，如：`(\d{4})[-/.]?(?:\d{2})[-/.]?(\d{2})`，只有两个分组，分别是 年 和 日



re.compile 将正则表达式转化为正则对象，生成正则对象，需要和 match、search、findall 搭配使用



分组另一个常用用法是 引用。

例子1：想要匹配一些单词，这些单词的第一个字母和最后一个字母必须相同，alibaba 和 tencent 满足该条件，google 不满足。

可使用分组和引用来实现，把第一个字母用分组包含起来，

我自己实现是这样子的，使用了非贪婪模式`([a-z]).*?\1`，

存在一个问题，会将 google 中，goog 匹配到，是因为没有限制单词的边界，可在结尾处使用 \b 进行限制。

最终结果：`([a-z]).*？\1\b`，



## 前瞻和后顾 Lookahead & Lookbehind



前瞻是匹配到某些字符前面的内容，后顾就是匹配到某些字符后面的内容。



前瞻和后顾是一种特殊的匹配方式，按照是否匹配还可以分为 正向前瞻、负向前瞻、正向后顾 和 负向后顾。

简单说，就是匹配到某些字符前面或者后面的内容，但不包括这些字符本身



1. positive lookahead. Matches a group after the main expression without including it in the result。正向前瞻，匹配主表达式后的组，但不将其包含在结果中
2. Negative lookahead.  Specifies a group that can not match after the main expression(if it matches, the result is discarded). 负向前瞻，指定主表达式后不能匹配的组(如果匹配，则丢弃结果)
3. Positive lookbehind. Matches a group before the main expression without including it in the result. 正向后顾，匹配主表达式之前的组，但不将其包含在结果中。
4. Negative lookbehind.
   Specifies a group that can not match before the main expression(if it matches, the result is discarded). 负向后顾，指定一个不能在主表达式之前匹配的组(如果匹配，则丢弃结果)



例子1：匹配数字前方的$，如下，要匹配第一个和第四个 $

> $100
> $dasdf
> $f2fda
> $2dfas

对应正则表达式：`\$(?=\d+)`，？= 代表正向前瞻，只有数字前方的 $ 被匹配到了，这就是正向前瞻

如果将 ？= 替换为 ？！，代表 负向前瞻，就是 ？= 的取反，也就是 当后面内部不是数字的时候，匹配前方的 $，对应正则表达式 `\$(?!\d+)`，对应第二个和第三个。

还是上面的例子，如果想匹配到以 $ 开头的数字，需要给前面的 $ 加上一个分组，括号里面再加上一个 ?<=，这个符号代表正向后顾，`(?<=\$)\d+` 可以匹配到 100 和 2，

将 = 替换为 ！，表示负向后顾





# 其他



版本

正则表达式的不同版本

- POSIX 基本 - Baisc Regular Expression（BRE）
- POSIX 扩展 - Extended Regular Expression (ERE)
- Perl 兼容正则表达式（PCRE）
- 其他版本（Python、Java 等）

不同版本之间，可能会有一些不同的特性和差异

比如，前瞻和后顾，在 js 中，直到 SE2018 之后采开始支持

Linux 中，grep、sed 和 awk 等工具，都是基于 POSIX 标准的 BRE 或者 ERE，对于一些现代的正则表达式中的特性也是不支持的。

如果 正则表达式没有匹配到想要的结果，可能是版本不支持，这时候就需要查一下对应版本的文档，查看支持的特性和语法，再做相应调整。



# 总结

1. 字符匹配
2. 位置匹配
3. 量词
4. 分组和引用
5. 前瞻和后顾



# Python 特性

分组命名

这是我工作中用到的一个正则表达式：

```python
start_time_p_3 = re.compile(
            r'start_time\s*:\s*(?P<time>\d+.*?\d+.*?\d+\s*\d+.*?\d+.*?\d+).*status\s*=\s*(?P<status>\d+)'
        )
```

在Python的`re`模块中，确实可以通过`(?P<name>...)`这样的语法来为正则表达式中的分组命名。这种方式相比于传统的数字索引方式（如group(1)）更加直观和方便，特别是当你的正则表达式中有多个分组，并且这些分组并不是按照顺序使用的时候。

当你使用这个编译后的正则表达式对象去搜索或匹配文本时，可以通过分组的名字来提取信息，例如：

```python
pythonmatch = start_time_p_3.search(some_text)
if match:
    print(match.group('time'))  # 输出匹配到的时间部分
    print(match.group('status'))  # 输出匹配到的状态部分
```

这种方式使得提取特定部分的信息变得更加容易管理，尤其是在处理复杂的字符串解析任务时。





正则表达式命名分组确实是Python `re` 模块的一个特性。这种语法 `(?P<name>...)` 是Python特有的，并不是所有正则表达式引擎都支持这种语法。以下

### Python 中的命名分组

在Python中，`re` 模块支持命名分组，这使得提取信息更加直观和方便。具体来说：

- `(?P<name>...)` 用于定义一个名为 `name` 的分组。
- 可以通过 `match.group('name')` 来访问命名分组的内容。



在其他环境中，如JavaScript、Java、.NET 或者一些在线正则表达式测试工具，通常不支持这种命名分组的语法。它们通常使用不同的方法来实现类似的功能。





group方法返回一个或者多个匹配的子组。如果只有一个参数，结果就是一个字符串，如果有多个参数，结果就是一个元组（每个参数对应一个项），如果没有参数，整个匹配都被返回。 如果一个参数值为 0，即是group(0)，相应的返回值就是整个匹配字符串；如果它是一个范围 [1..99]，结果就是相应的括号组字符串。如果一个组号是负数，或者大于样式中定义的组数，一个 IndexError 索引错误就 raise。如果一个组包含在样式的一部分，并被匹配多次，就返回最后一个匹配。
————————————————

                            版权声明：本文为博主原创文章，遵循 CC 4.0 BY-SA 版权协议，转载请附上原文出处链接和本声明。

原文链接：https://blog.csdn.net/a66666_/article/details/103412774





#### JavaScript

在JavaScript中，可以使用命名捕获组，但是语法略有不同：

```
javascriptconst regex = /start_time\s*:\s*(?<time>\d+.*?\d+.*?\d+\s*\d+.*?\d+.*?\d+).*status\s*=\s*(?<status>\d+)/;
const match = regex.exec(someText);
if (match) {
    console.log(match.groups.time);  // 输出匹配到的时间部分
    console.log(match.groups.status);  // 输出匹配到的状态部分
}
```



# VSCode

在 vscode 中，可以用 正则模式，快速在每一行的开头或结尾 替换数据。开启正则模式。输入 ^ 或 $ ，



正则表达式



## re模块

re模块中，常用 re.match、re.serach、re.findall


 linux 和 mac系统中，可以通过 grep 和 sed 等命令使用正则表达式进行文本处理

视频中的正则表达式在线工具网站：https://regexr.com

左边是导航栏，可以切换设置或者查看帮助文档

python 的 re模块

1. 



### group

group方法返回一个或者多个匹配的子组。如果只有一个参数，结果就是一个字符串，如果有多个参数，结果就是一个元组（每个参数对应一个项），如果没有参数，整个匹配都被返回。 如果一个参数值为 0，即是group(0)，相应的返回值就是整个匹配字符串；如果它是一个范围 [1..99]，结果就是相应的括号组字符串。如果一个组号是负数，或者大于样式中定义的组数，一个 IndexError 索引错误就 raise。如果一个组包含在样式的一部分，并被匹配多次，就返回最后一个匹配。

使用了 `(?P<name>…)` 语法， group(n)中，参数n就也可能是命名组合的名字。如果一个字符串参数在样式中未定义为组合名，一个 [`IndexError`](https://docs.python.org/zh-cn/3.7/library/exceptions.html#IndexError) 就 `raise`。

```python
a = r'start_time\s*:\s*(?P<time>\d+.*?\d+.*?\d+\s*\d+.*?\d+.*?\d+).*status\s*=\s*(?P<status>\d+)'
y = re.search(a,"IMU:start_time:2023-07-19 15:47:28 status=1")
print(y.group('time'))
print(y.group('status'))

2023-07-19 15:47:28
1
```

字符串：IMU:start_time:2023-07-19 15:47:28 status=1



参考教材：

1. [30分钟正则表达式教程_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1fm411C7fq/?spm_id_from=333.999.0.0&vd_source=626bc1cfeb9a64da3cae7f833674f3d6)
2. [正则表达式不要背正则表达式一直是困扰很多程序员的一门技术，当然也包括曾经的我。大多数时候我们在开发过程中要用到某些正则表 - 掘金 (juejin.cn)](https://juejin.cn/post/6844903845227659271?searchId=20241005143828A0BEB34E963E966A8888#heading-0)

贪婪匹配：https://blog.csdn.net/lekusun9671/article/details/105066676

文档：https://docs.python.org/zh-cn/3/howto/regex.html

re.group：https://blog.csdn.net/a66666_/article/details/103412774

正则表达式不要背：https://juejin.cn/post/6844903845227659271