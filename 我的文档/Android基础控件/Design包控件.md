# Design包控件

> design支持库中这几个新增的控件，每个都应该拿出些时间好篇幅好好讲讲。但是这里只是作简单的介绍，具体的都放到相关的链接中（都是搜索文章的链接，并非本人缩写）。并且，很重要的一点是，这个包的控件讲究组合性，所以通常组合起来使用。

[TOC]

## CoordinatorLayout

> Disign库，需要单独的添加依赖，最好使用最新版本。另外，对于依赖的添加，最好一个统一配置文件。这就延伸出来，要好好学习gradle，学习下groovy。传送门[Groovy 使用完全解析](https://blog.csdn.net/zhaoyanjun6/article/details/70313790/)CoordinatorLayout相关联的控件比较多，所以其余不再记录。小技巧，可以直接试试将AppBarLayout拖入到界面。

**注意，现在不再使用"compile"，请使用“implementation”或者“api"。**

[CoordinatorLayout使用全解析](https://blog.csdn.net/u012124438/article/details/56701641)

[CoordinatorLayout 你不得不了解一下](https://www.jianshu.com/p/ed569a44225a)

[CoordinatorLayout 上的一些布局技巧](https://www.jianshu.com/p/e9df8c501f92)

[使用CoordinatorLayout打造各种炫酷的效果](https://www.jianshu.com/p/f09723b7e887/)

## NestedScrollView 

> 看名字就知道，嵌套的Scrollview。内部可以嵌套列表，如ListView和RecyclerView。下面记录下使用和出现的一些问题。	

[使用NestedScrollView代替ScrollView解决滑动冲突](https://blog.csdn.net/haoyuegongzi/article/details/79353775)

[一点见解: Android嵌套滑动和NestedScrollView](https://www.jianshu.com/p/1806ed9737f6/)

[NestedScrollView 在特定情况下，部分内容不显示的问题](https://blog.csdn.net/hjf_huangjinfu/article/details/79145507)

[具有NestedScrollView并且内嵌套RecyclerView，打开页面时不显示在顶部的解决方法](https://blog.csdn.net/qq_38013013/article/details/78040728)

[nestedScrollview 嵌套使用recyclerview判断滑动到底部 （嵌套滑动导致 不能使用recyclerview的onscrolled监听）](https://www.cnblogs.com/qianyukun/p/6489161.html)

## TextInputLayout

> 就是用来登录用的，说白了就是在我们输入的时候，不让提示文字消失。使用场景比较单一。

[TextInputlayout入门讲解](https://www.jianshu.com/p/c06b2a41f611)

[android新特性：TextInputLayout使用方法](https://blog.csdn.net/huangxiaoguo1/article/details/54906650)

[Android原生控件之--TextInputLayout、TextInputEditText](https://www.jianshu.com/p/de9c19d73450)

