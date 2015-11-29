--- 
layout: post 
title:  "Core Foundation对象转换Objective-C对象" 
date:   2015-11-29-16:09:46 +0800 

categories: iOS
---

####简述
在Core Foundation和Foundation框架之间，有许多数据类型可以互相转换，数据类型的转换使用的时两个框架之间的 ["Toll-Free Bridging"机制](https://developer.apple.com/library/ios/documentation/CoreFoundation/Conceptual/CFDesignConcepts/Articles/tollFreeBridgedTypes.html) ，例如NSLocale和CFLocale之间的转换。

然而并不是所有的CFXxx和NSXxx之间都存在转换关系，比如NSRunLoop和CFRunLoop，NSBundle和CFBundle，NSDateFormatter和CFDateFormatter都不行。

####可以用以下三个方法来进行转换
- `__bridge` 转移Objective-C和Core Foundation的指针但是并不转移它们的所有权，不增加引用计数。例如当OC对象被释放的时候，CF对象也不能被使用。
- `__bridge_retained` 或者 `CFBridgingRetain` 使一个Objective-C指针指向Core Foundation指针，并且转移所有权，使它们的引用计数+1（需要CFRelease）
- `__bridge_transfer`或者`CFBridgingRelease` 把一个非Objective-C的指针指向Objective-C，把它的所有权交给ARC管理，这种情况在CF对象向OC对象转换的时候，经常使用。

####可以进行TFB机制转换的对象对应（[官网](https://developer.apple.com/library/ios/documentation/CoreFoundation/Conceptual/CFDesignConcepts/Articles/tollFreeBridgedTypes.html)）
![Alt text](kramdow://github.com/KK233/KK233.github.io/blob/master/_posts/1448808794538.png)

