---
layout:     post
title:      "搬瓦工VPS上搭建WordPress博客"
subtitle:   "WordPress"
date:       2018-02-06 17:00:00
author:     "管维诚"
header-img: "img/13884744.jpg"
---

## 记录下搬瓦工搭建WordPress方法
* 第一种方法是在服务器上安装LNMP一键安装包，然后在linux环境下直接装WordPress。它的好处是系统资源占用率低，有的人用这种方法在64兆内存的vps都能装上WordPress并正常运行，但是由于它全程都在Linux环境下设置，对新手来说太难，安装容易失败，而且建站以后，想在服务器上设置一些东西也麻烦。所以，我不推荐新手用这种方法，感兴趣的话可以去百度下。

* 第二种方法是先在服务器上装管理面板，然后在面板上安装服务器必要套件，最后安装WordPress。这样虽然系统资源占用高一些，但是方便了很多，就像在使用虚拟主机一样，不用什么操作都得输命令。而且还有个好处，新建一个WordPress网站几分钟就能搞定，比第一种方法有效率多。非常推荐使用面板。

## 记录下第二种方法（mac环境）
* 1 购买搬瓦工VPS。地址<https://bwh1.net/index.php>
* 2 获取服务器IP和端口号。![](http://p2bzzkn05.bkt.clouddn.com/18-2-6/82357460.jpg)
* 3 利用Mac自带应用Terminal SSH 登录远端VPS（购买VPS的时候SSH登录密码会以邮件的方式的给你，当然然kiWiVM面板也能修改Root密码）。![](http://p2bzzkn05.bkt.clouddn.com/18-2-6/55737477.jpg)如图所以表示已经登录成功。
* 4 在[root@localhost ~]#后面复制粘贴下面命令，并按回车后，就开始自动下载并安装面板了。
`
yum install -y wget && wget -O install.sh http://download.bt.cn/install/install.sh && sh install.sh
`   
* 5 安装过程一路continue。安装完成以后。**Bt-Panel** **username** **password** 需要记录一下。
* 6 在浏览器打开我们的VPS地址。输入刚刚的用户名和密码，进入宝塔管理面板。
