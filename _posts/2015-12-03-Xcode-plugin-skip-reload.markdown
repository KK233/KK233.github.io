--- 
layout: post 
title:  "Xcodeload插件不小心点了skip" 
date:   2015-12-03-14:03:33 +0800 

categories: iOS
---

terminal中使用`defaults delete com.apple.dt.Xcode DVTPlugInManagerNonApplePlugIns-Xcode-7.1.1(最后是Xcode版本号)`就可以重新load所有插件


顺便如果Xcode更新后UUID插件时效的问题,可以在terminal中使用`find ~/Library/Application\ Support/Developer/Shared/Xcode/Plug-ins -name Info.plist -maxdepth 3 | xargs -I{} defaults write {} DVTPlugInCompatibilityUUIDs -array-add 当前Xcode的UUID`的方法来给插件添加当前版本的UUID

当前版本的UUID可以在terminal中使用`defaults read /Applications/Xcode.app/Contents/Info DVTPlugInCompatibilityUUID`命令获取
