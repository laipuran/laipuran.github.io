---
layout: post
title: WPF 开发中出现的问题
date: 2021-01-03 08:19:02 +0800
---
###  1. 导航界面
导航的写法：
```c#
Frame.NavigationService.Navigate(new Uri("YourPage.xaml", UriKind.Relative));
```

### 2. Resource Dictionary
新建一个 Resource Dictionary 如果想在全局应用，在 App.xaml 中加入 **Merged Dictionaries** 项，位置使用 Relative Uri 即可。

### 3. 资源管理器(ResourceManager)
快捷键 Ctrl + Shift + A 添加新项，搜索“资源”：

![资源文件](https://laipuran.github.io/blog-img/资源文件.png)

将资源拖拽到 *.resx 中，就可以通过
```c#
ResourceManager Loader = OverTop.Resources.ResourcesFile.ResourceManager;
Bitmap icon = new((System.Drawing.Image)Loader.GetObject(name));
return Imaging.CreateBitmapSourceFromHBitmap(icon.GetHbitmap(), IntPtr.Zero, Int32Rect.Empty, BitmapSizeOptions.FromEmptyOptions());
```
来获取图片资源了。

本文持续更新中

<script src="https://utteranc.es/client.js"
        repo="laipuran/laipuran.github.io"
        issue-term="title"
        label="💬Comment"
        theme="github-dark"
        crossorigin="anonymous"
        async>
</script>
