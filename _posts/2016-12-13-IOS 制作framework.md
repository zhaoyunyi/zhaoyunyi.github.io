---
layout: post
title:  “IOS Swfit 制作framework”
date:   2016-12-13
excerpt: "IOS Swfit 制作framework"
tag:
- IOS
- Swift
---

###   IOS 制作 Swift编译构建的 framework

1. IOS 的静态库分两种一种是 后缀 *.a*   另一种是 后缀 *.framework*  。在XCode6 之苹果提供的是前面一种打包方式，从远古时代走过来的开发者在加载一些类库的是难免会碰到这种后缀的类库库。XCode6 之后苹果提供了framework 的的制作方法，能打包包括源码、图片资源、xib等。

2. 这里老的 *.a* 库的制作就不写了，有兴趣的读者自己查阅相关资料，另外Swift 不支持这种类库打包方式。framework 的好处很多，比如抽取一部分公共的代码给两个不同的工程使用，打包一个工程的代码嵌入到另外一个工程等等。如果配合 *.workspace* 来管理多个项目工程以及公共代码部分会有更好的效果   <!--（这部分公共代码待会通过编译出 framework 给多个工程使用）--> 

3. xcode -> new ->project  选中下方图片左边那个图片构建出来一个工程

   ![19304CFC-7BDB-46C6-8D60-BFB316712401]({{ site.url }}/images/post_images/19304CFC-7BDB-46C6-8D60-BFB316712401.png)

   这个工程跟正常的single project 之类的正常工程不一样没有一些必须的启动文件，比如storyboard 之类的。注意：这里如果选用Target 的话，会在当前工程目录下新建对应的Target 编译项，依赖于当前的project 而不是独立一个project。

4. 这时候管理多个工程最好就新建一个workspace 就像使用cocoapods 一样，只不过cocopods自动生成好了对应的workspace 以及对应配置项目，有就直接像下图 拖入即可，如果没有就新建一个workspace 文件同样的操作即可。至于多个工程文件的目录如何放置，看每个人自己的做法，只要注意主工程如果有对应的需要添加对应的目录索引即可。

![057AD691-0C4C-47DB-8592-D9AEF9986BAF]({{ site.url }}/images/post_images/057AD691-0C4C-47DB-8592-D9AEF9986BAF.png)

5. 在Test 工程下面有个Product 目录下 会生成一个 对应的.framework 文件，在主工程里对这个framework 进行索引即可。

6. 这个是手动管理的方式.framework的方式，可以使用cocopods 进行管理，也可以直接拿到编译出来的 .framework文件进行使用不过要注意[debug 和release 进行合并 参考喵神文章](http://swifter.tips/code-framework/)

7. 如果framework 中有资源文件，在手动加载使用的时候除了需要 在Embeded添加对应 framework，还要在 build Phases 中导入， 这样就很难避免 会导致包变大情况。除非单独通过脚本的方式将所有的xib 资源 和图片资源的bundle 都拷贝进去，这里只提供了这样的一个思路。这个思路也可以参考下面的链接。

8. 一些细节以及碰到的坑参考下面的总结




## 参考的相关链接

[制作总结](http://www.cnblogs.com/rayshen/p/5613990.html)

[使用Swift打造库的碰到的坑](http://www.cnblogs.com/rayshen/p/5613990.html)

[会需要打包xib文件资源](https://blog.cnbluebox.com/blog/2014/12/08/xib-in-frameworks/)
