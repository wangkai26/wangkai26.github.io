---
title: 'Js基础'
date: 2024-10-10T20:34:02+08:00               # 创建时间
lastmod: 2024-10-10T20:34:02+08:00            # 更新时间
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

11111111


def app_bitmap_read_bit(pstr, struct_c):
    """按bit读取数据"""
    struct_dict = copy.copy(struct_c) # 浅拷贝，不修改内部数据
    bit_values = list(struct_dict.values())
    bit_keys = list(struct_dict.keys())
    index = -bit_values[0]
    del bit_values[0]
    pstr = str(bin(hex_to_int("1" + rever_bytes(pstr)))).split("0b1")[1] # "1" 无效数据
    struct_dict[bit_keys[0]] = bin_to_int(pstr[index:])
    for i in range(len(bit_values)):
        bit_result = bin_to_int(pstr[-(-index + bit_values[i]):index]) # 反向获取数据
        struct_dict[bit_keys[i+1]] = bit_result
        index += -bit_values[i]

    class struct_data(object):
        def __init__(self):
            names = self.__dict__
            for key,value in struct_dict.items(): # 动态赋值变量
                names[key] = value
    return  struct_data()