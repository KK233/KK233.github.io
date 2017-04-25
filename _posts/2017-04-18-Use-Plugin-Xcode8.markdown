--- 
layout: post 
title:  "Xcode8使用插件"
date:   2017-04-18 13:35:36 +0800

categories: iOS
---

Apple在Xcode升级到8.0以后, 因为插件造成的漏洞, 不允许直接加载第三方插件了, 换成了一种extension的方式, 但是给的权限非常少

我们可以通过给Xcode自签名的方式实现加载插件, 但是注意:**尽可能不要使用自签名的Xcode进行打包上传, 在上传时最好使用Mac App Store的官方版本**


1. 关闭Xcode
2. 制作一个签名
- 打开钥匙串管理
- 点击 `钥匙串访问` -> `证书助理` -> `创建证书`
- 名称可自选, 比如此时使用名称:`XcodeSign`
- 整数类型选择`代码签名`
3. 在terminal中输入以下命令完成Xcode的重签名

```
sudo codesign -f -s XcodeSign (XcodeSign是你前面代码签名的名称) /Applications/Xcode.app (地址是你的Xcode绝对路径)
```

4. 其他无法加载等问题可以查阅[这篇博客](http://kk233.github.io/ios/2015/12/03/Xcode-plugin-skip-reload.html)
