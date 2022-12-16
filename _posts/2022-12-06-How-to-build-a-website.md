---
layout: post
title: 如何自建一个网站
date: 2022-12-16 16:04:28 +0800
categories: [网站]
tags: [site]
---
### 1. 准备工作
- 往树莓派中烧写系统
- 可以选择换成[清华的源](https://mirrors.tuna.tsinghua.edu.cn/)

### 2. 安装 Ruby 和 Ruby-dev
```bash
sudo apt install ruby -y
sudo apt install ruby-dev -y
```

### 3. 接着安装 gem 包
先换 gem 源
```bash
gem sources --add https://mirrors.tuna.tsinghua.edu.cn/rubygems/ --remove https://rubygems.org/
gem sources -l
```
然后安装 bundler, jekyll 两个包
```bash
# 安装bundler
sudo gem install bundler
# 换 bundler 源：
bundle config mirror.https://rubygems.org https://mirrors.tuna.tsinghua.edu.cn/rubygems
# 安装jekyll
sudo gem install jekyll
```

### 4. 切换到你想创建网页的目录，创建网站
```bash
cd ./...
```
接着新建网站
```bash
jekyll new my awesome-website
```

### 5. 像本篇一样弄好头信息
```liquid
---
layout: post
title: 如何自建一个网站
date: 2022-12-16 16:04:28 +0800
categories: [网站]
tags: [site]
---
```
使用 markdown↓ 写好文章内容，然后就可以

### 6. 运行
```bash
bundle exec jekyll s
```
Done!

<script src="https://utteranc.es/client.js"
        repo="laipuran/laipuran.github.io"
        issue-term="title"
        label="💬Comment"
        theme="github-dark"
        crossorigin="anonymous"
        async>
</script>