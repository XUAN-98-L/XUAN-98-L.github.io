---
title: hexo迁移(win2mac)
date: 2024-05-27 13:43:13
tags:
  - 生活
---
hexo迁移到mac电脑
<!-- more -->

# 使用[安装教程](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-homebrew-on-macos)为mac安装homebrew：

注意添加brew到系统路径

```bash

(echo; echo 'eval "$(/opt/homebrew/bin/brew shellenv)"') >> /Users/gloria/.zprofile

eval "$(/opt/homebrew/bin/brew shellenv)

```

# 安装node.js和git

```shell

brew install node.js

brew install git

```

# 安装hexo

```shell

npm install -g hexo-cli

#安装 hexo-deployer-git
npm install hexo-deployer-git --save

```

# 从git上将过往博客clone到本地
- 在原来的电脑上创建hexo分支，并将全部文件夹都上传上去

- 在新电脑上配置[git ssh](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/checking-for-existing-ssh-keys)

```shell
#将hexo分支克隆到本地（注意克隆的时候一定要选择ssh而不是https）
git clone -b hexo git@github.com:XUAN-98-L/XUAN-98-L.github.io.git hexo
```

# hexo初始化
```
#需要进入到hexo文件夹内
npm install hexo --save

#修改_config.yml中deploy的部分，将其从https改为ssh
deploy:
  type: git
  repo: git@github.com:XUAN-98-L/XUAN-98-L.github.io.git
```

# obsidian 和hexo连用
https://itreefly.com/posts/e5113722.html

obsidian将“文件与链接”中“使用wiki链接“关闭

使用obsidian打开_posts作为仓库，并安装Custom Attachment Location插件
设置Location for new attachment为：
./${filename}
并将rename attachment files打开

# 将修改后的文件推送到git
```
git add .
git commit -m “提交消息”
git push
```