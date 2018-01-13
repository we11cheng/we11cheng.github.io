---
layout:     post
title:      "Git添加空文件夹的方法"
subtitle:   ""
date:       2018-01-13 16:00:00
author:     "管维诚"
header-img: "img/gwc_sea.jpg"
---

朋友遇到这样一个问题，输入git status命令的时候Untracked files竟然没有他刚刚添加的文件夹。让我觉得匪夷所思。我第一反应是不是.gitignore文件的问题或者是文件夹已经commit。朋友笃定没有commit .gitignore也没问题，后来我也自己做了一次实验，发现竟然是空文件夹在捣鬼，因为我在文件夹添加一个文件的时候，git status状态是对的。然后Google发现确实存在这样的问题，于是把解决方案记录了下来。

参考链接<https://stackoverflow.com/questions/115983/how-can-i-add-an-empty-directory-to-a-git-repository>

简单介绍一下解决方案。

#### <font color=#E52B50 size=3>需要注意的一点就是在哪个个目录创建.gitignore文件（在你空白文件夹下面创建)</font>![](http://p2bzzkn05.bkt.clouddn.com/18-1-13/40809453.jpg)如图gwc文件夹就是我们空白的文件夹。在mac系统下.后缀表示是隐藏文件夹。创建的方式有很多，可以通过终端 touch [文件名+后缀] 或者vim [文件名+后缀]来操作。推荐大家使用vim编辑器，用久了绝对会爱上它。然后在.gitignore 输入以下内容
```
# Ignore everything in this directory
*
# Except this file
!.gitignore

```
###*表示所有都不忽略。这个时候再切换到本地工作目录的时候。再次git status你会惊奇的发现空文件夹也在untracked files列表里了。

