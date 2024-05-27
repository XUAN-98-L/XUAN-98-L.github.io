---
title: 基于hexo和github page搭建博客
date: 2023-05-17 15:47:13
categories: 
- 软件算法
- 生信无关
tags: ['技术','个人成长']
hide: false
---
本文是基于hexo和github page搭建博客的安装指南，主要介绍了基于Scoop对win10系统的软件进行管理，hexo的安装与Hexo Fluid主题配置。

<!-- more -->
# 使用github page搭建blog

## 1 基于Windows10系统，使用Scoop进行软件安装与管理 [Scoop][1]

在 PowerShell 中输入下面内容，保证允许本地脚本的执行：

    set-executionpolicy remotesigned -scope currentuser

然后执行下面的命令安装 Scoop：

    iex (new-object net.webclient).downloadstring('https://get.scoop.sh')

静待脚本执行完成就可以了，安装成功后，让我们尝试一下：

    scoop help

整体搭建流程基于[教程][2]

    # 安装Git
    scoop install git 
    # 安装 nvm
    scoop install nvm 
    # 查看可用的 NodeJS 版本，这里建议使用 LTS 版本
    nvm list available 
    # 安装 NodeJS，我这里安装的是最新 LTS 版本 18.16.0
    nvm install 18.16.0 
    #先使用 scoop 安装 sudo 这个工具
    scoop install sudo
    # NodeJS 版本使用 18.16.0，注意这里需要管理员权限
    sudo nvm use 18.16.0 

## 2. 安装[Hexo][3]

    #一键安装Hexo
     npm install -g hexo-cli

    #创建项目并初始化
    hexo init my_blog
    cd my_blog
    npm install

    #3. 生成网页文件 &本地启动
    hexo generate # 生成页面，此命令可以简写为 `hexo g`
    hexo server # 本地启动，可简写为 `hexo s`

## 3.修改Hexo主题为[fluid][4]
    #在博客根路径下（C:\Users\liu\my_blog）将git上的_config.yml文件复制过去并重命名为_config.fluid.yml
    #对根目录的_config.yml文件进行如下修改：
    heme: fluid  # 指定主题

    language: zh-CN  # 指定语言，会影响主题显示的语言，按需修改

## 4.创建【关于页】
hexo的[用户手册][5]

    hexo new page about

创建成功后修改 /source/about/index.md，添加 layout 属性。修改后的文件示例如下：
    ---
    title: 标题
    layout: about
    ---
    这里写关于页的正文，支持 Markdown, HTML

**注意**：在对关于页进行修改后，需要重新启动hexo

    hexo clean
    hexo g
    hexo s

## 5.创建文章
修改 _config.yml 文件。这项配置是为了在生成文章的同时，生成一个同名的资源目录用于存放图片等资源文件。

    #将第43行的false改为true
    post_asset_folder: true

创建文件名为 blog_build_remark 文章。
    hexo new post blog_build_remark



# 发布 GitHub Pages
安装 hexo-deployer-git
   
    npm install hexo-deployer-git --save

修改站点配置

    deploy:
        type: git
        repo: https://github.com/XUAN-98-L/XUAN-98-L.github.io

默认会将数据推送到github的master branch,可以直接通过链接进行访问 https://xuan-98-l.github.io/

设置完成后使用命令进行推送(使用cmd)
    hexo clean
    hexo deploy


[1]: https://sspai.com/post/52496
[2]: https://xie.infoq.cn/article/ac51ce1f6e9434779c35cbb6c
[3]: https://hexo.io/zh-cn/docs/#%E5%AE%89%E8%A3%85-Hexo
[4]: https://github.com/fluid-dev/hexo-theme-fluid
[5]: https://fluid-dev.github.io/hexo-fluid-docs/guide/#%E5%BD%92%E6%A1%A3%E9%A1%B5