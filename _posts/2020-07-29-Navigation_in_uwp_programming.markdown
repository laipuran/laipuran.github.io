---
layout: post
title: UWP中的页面导航
date: 2020-07-29 15:46:23 +0800
categories: [C#, 桌面]
tags: [uwp]
---
**本人编程“小白”一个。**

在阅读这一篇文章时，如果您没有安装UWP，请参照我写的
[开始学习UWP]({% post_url 2020-05-21-Start_to_learn_uwp %})

OK, let's start working.

首先，创建一个空白应用（我用的是C#），进入后，在左上角项目中新建项目
![UWP加入新页面](https://laipuran.github.io/blog-img/UWP%E5%8A%A0%E5%85%A5%E6%96%B0%E9%A1%B5%E9%9D%A2.png)

在新建的页面加入内容，如
```xaml
    <TextBlock FontSize="48">Another Page!<\TextBlock>
```

在MainPage.xaml的 **grid** 内加入
```xaml
    <Button Name="NavigationButton" Click="NavigationButton_Click">Go to next page<\Button>
    <Frame x:Name""MyFrame><\Frame>
```

将输入位置点到 **NavigationButton_Click** ，按F12导航到MainPage.xaml.cs函数处，加入
```cs
    MyFrame.Navigate(typeof(你新建页面的名字));
```
这可以在你设置的Frame位置转移到另外一个页面。

按 **Ctrl** + **F5** 运行代码，查看结果。

[下载实例](https://laipuran.github.io/blog-img/Navigate.rar)

<script src="https://utteranc.es/client.js"
        repo="laipuran/laipuran.github.io"
        issue-term="title"
        label="💬Comment"
        theme="github-dark"
        crossorigin="anonymous"
        async>
</script>
