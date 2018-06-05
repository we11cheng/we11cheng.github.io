---
layout:     post
title:      "iOS证书相关知识点汇总"
subtitle:   "iOS证书"
date:       2018-06-05 13:00:00
author:     "管维诚"
header-img: "img/gwc_sea.jpg"
---

## iOS开发中证书相关
- 苹果跟证书Apple Root Certificate： 安装xcode时自动安装。手动更新[AppleWWDRCA.cer](https://developer.apple.com/certificationauthority/AppleWWDRCA.cer)
- 开发证书Development：用来开发和调试应用程序。
- 发布证书Production：用来分发应用程序。
- 配置文件：包含（调试者证书，授权调试设备清单，应用ID）。真机运行相关的配置文件。参考链接<http://ryantang.me/blog/2013/11/28/apple-account-3/>。
- 如何申请这两种证书，参考<https://www.jianshu.com/p/d1a93a689a14> 写的很详细。

## 需要注意的问题
- 打包app证书和私钥缺一不可。
- 发布证书创建的时候一定要妥善保存证书信息。 证书(.cer)是通过当前电脑CSR(.certSigningRequest)文件生成的，CSR文件通过keychain工具来制作，生成之后会在keychain里保存私钥，苹果通过CSR生成的证书文件则包含公钥信息。Xcode打包生成ipa包的时候会用到这个私钥签名。
- 私钥最初只有一份，想要在其他电脑打包的话，需要共享私钥p12文件，参考<http://www.cnblogs.com/mnstar/p/6274712.html>
- 私钥参考图（有私钥才能导出p12文件）![](http://p2bzzkn05.bkt.clouddn.com/18-5-31/84967138.jpg)

## 证书失效/过期问题
- Apple Worldwide Developer Relations Certification Authority) 证书过期，参考<https://developer.apple.com/certificationauthority/AppleWWDRCA.cer> 更新证书即可。
- 登录苹果开发者<https://developer.apple.com/> 登录账号。查看左侧Membership信息。检查开发者账号是否到期。

## 什么时候移除证书操作
- 一般不推荐移除证书操作。这是下下策，什么情况下执行移除操作：1.旧机器找不到证书和私钥2.重新打包提示找不到私钥文件，打包失败。（旧机器指的的第一次生成证书的那台机器）。
- 移除证书也是分了权限的。登录开发者中心。查看左侧People查看团队所有成员信息。只有Agent和Admin账户下才能执行证书的移除操作。相对安全，普通成员是无法执行证书移除操作。


