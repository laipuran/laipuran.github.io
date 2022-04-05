---
layout: post
title: WPF开发中出现的问题
date: 2021-01-03 08:19:02 +0800
categories: [C#, 桌面]
tags: [wpf]
---
###  1. 导航界面
写法
```c#
FrameOfMainWindow.NavigationService.Navigate(new Uri("YourPage.xaml", UriKind.Relative));
```

### 2. Resource Dictionary
新建一个 Resource Dictionary 如果想在全局应用，在 App.xaml 中加入 **Merged Dictionaries** 项，位置使用 Relative Uri 即可。
本文持续更新中

<script src="https://utteranc.es/client.js"
        repo="laipuran/laipuran.github.io"
        issue-term="title"
        label="💬Comment"
        theme="github-dark"
        crossorigin="anonymous"
        async>
</script>
