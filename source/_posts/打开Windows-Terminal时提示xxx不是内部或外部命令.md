---
title: 打开Windows-Terminal时提示xxx不是内部或外部命令
abbrlink: 6418
date: 2023-06-16 21:01:04
tags:
---


## 前言

之前在Windows本机上安装了`hexo-cli`包，卸载后，hexo命令就无法找到了，虽然我也不明白为什么每次打开cmd都会运行`hexo`命令。所以每次打开都会提示

```bash
'hexo' 不是内部或外部命令，也不是可运行的程序
或批处理文件。
```

## 解决方法

1. {% label win  blue %} + {% label s  blue %}，搜索`注册表编辑器`打开
2. 在`注册表编辑器窗口`的`地址栏`输入`计算机\HKEY_CURRENT_USER\Software\Microsoft\Command Processor`
3. 查看右侧的主窗口中是否有`AutoRun`字段，然后根据这个字段的值进行排查即可
{% note info simple %}
我的`AutoRun`字段值是`%USERPROFILE%\alias_key.bat`，看到`alias_key.bat`我就想起来我之前设置过hexo命令的别名脚本，把这个脚本删除就可以了吧，然后把注册表这个字段值删除，就解决这个问题了。不过我也没有设置过注册表来着，不过后面想要这种功能倒是可以这样实现，打开cmd就运行脚本文件
{% note no-icon simple %}
`%USERPROFILE%`表示用户主目录，即`C:\Users\<username>`
{% endnote %}
{% endnote %}

4. 如果第3步已排查出结果下面可跳过，在`注册表编辑器窗口`的`地址栏`输入`计算机\HKEY_LOCAL_MACHINE\Software\Microsoft\Command Processor`
5. 查看右侧的主窗口中是否有`AutoRun`字段，然后根据这个字段的值进行排查即可
