---
title: Hexo常用命令
date: 2023-05-19 12:44:47
categories: 
- 软件算法
- 生信无关
tags: ['个人成长','技术']
hide: false
---
本文保存常用的hexo配置与命令。

<!-- more -->
# 常用命令
### 创建新的文章页面（名称为Hexo_personal_design）
    hexo new post Hexo_personal_design

### 在_config.yml中进行如下配置，可在

    post_asset_folder: true
    marked:
        prependRoot: true
        postAsset: true

    #在/source/_posts/Hexo_personal_design文件夹中存放background.jpg文件夹并通过如下命令进行调用。
    ![](backgroud.jpg)

### 在文章修改完成后使用命令进行推送到git(使用cmd)
    hexo clean
    hexo deploy

### 存放全局image的位置（主页背景等）
    C:\Users\liu\my_blog\public\img

### 将Hexo从C盘迁移到D盘
    d:
    cd D:\my_blog

### 如果遇到问题, 可通过查询[Hexo官网][1]以及[Hexo Fluid][2]进行查找。

### 上标下标书写方式
~~~
H<sub>2</sub>O  CO<sub>2</sub>
爆米<sup>TM</sup>
~~~

H<sub>2</sub>O  CO<sub>2</sub>
爆米<sup>TM</sup>

[1]: https://hexo.io/zh-cn/docs/
[2]: https://fluid-dev.github.io/hexo-fluid-docs/guide/#%E5%85%B3%E4%BA%8E%E6%8C%87%E5%8D%97