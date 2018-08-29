# Glide分析和总结

> 借鉴别人的博客和自己的理解，尽可能的把Glide吃透。参考原文链接地址在最下方
>
> 在这之前，应该明白一个问题，那就是Glide分v3和v4版本。如何从v3到v4也把官方文档的链接贴到下方

[TOC]

## 如何使用

Glide的最大目标就是使App快速、高效、流畅的加载图片，并使应用“glide”。不得不说，这个名字起的太契合了。我个人认为这是在Android平台上最好的图片加载框架。这么说就想表达一个意思，如果可以的话，再项目组能用Glide就用Glide。不要再去对比其他的框架，或者纠结其他的什么细节，因为这是Google爸爸推荐的，用Glide并且用好它，就足够了。

1. 添加依赖，注意版本选择，推荐最新。参考官方文档，可能特殊情况要做一些处理。
2. 添加GlideAppModel;
3. GlideAppModel.whit().load().into();一行代码搞定

## 主要功能

> 对于平常使用，其实不需要“大动干戈”，作为一个好的开源库，Glide里面已经做了很多处理。我们需要做的就是往里面添加我们的参数设置即可。

- 占位图（三种）
- 指定图片格式（例如，GIF，Picasso不支持）
- 缩略图
- 过渡动画
- 指定图片大小
- 图像变换（Glide会拿ImageView的ScaleType值）
- 缓存
- 图像质量
- 预加载

## ImageView的ScaleType

1. android:scaleType=“center”  保持原图的大小，显示在ImageView的中心。当原图的size大于ImageView的size时，多出来的部分被截掉。  
2. android:scaleType=“center_inside”  以原图正常显示为目的，如果原图大小大于ImageView的size，就按照比例缩小原图的宽高，居中显示在ImageView中。如果原图size小于ImageView的size，则不做处理居中显示图片。  
3. android:scaleType=“center_crop”  以原图填满ImageView为目的，如果原图size大于ImageView的size，则与center_inside一样，按比例缩小，居中显示在ImageView上。如果原图size小于ImageView的size，则按比例拉升原图的宽和高，填充ImageView居中显示。 
4. android:scaleType=“matrix”  不改变原图的大小，从ImageView的左上角开始绘制，超出部分做剪切处理。 
5.  androd:scaleType=“fit_xy”  把图片按照指定的大小在ImageView中显示，拉伸显示图片，不保持原比例，填满ImageView.  
6. android:scaleType=“fit_start”  把原图按照比例放大缩小到ImageView的高度，显示在ImageView的start（前部/上部）。  
7. android:sacleType=“fit_center”  把原图按照比例放大缩小到ImageView的高度，显示在ImageView的center（中部/居中显示）。
8. android:scaleType=“fit_end”  把原图按照比例放大缩小到ImageView的高度，显示在ImageVIew的end（后部/尾部/底部）

## 一些乱的理解

Glide设置了两种，一个是默认的情况，这种情况下我们使用起来也比比较简单，并且不需要设置太多的参数。比如在RecyclerView中展示的图片

另一种情况，当默认不再满足我们的情况时，Glide允许我们设置高端的操作，比如缓存，图片质量等。再甚者，我们可以定制参数，展开来说，就是，我们可以往Glide中添加方法，然后我们就可以调用。这点上，有点类似于“继承”了Glide并且添加了方法，这种设计思想和实现真的太厉害了，不过原理上其实是在Glide中引用了我们写的方法，通过GlideAppModel。

更厉害的，就是我们可以定制ModelLoader。具体的细节不去探究，简单说，就是我们定制我们的资源，通过Glide处理来显示。显示和资源的获取和处理分开了。

## 链接

[Gldie的Github主页](https://github.com/bumptech/glide)

[从v3迁移到v4](https://muyangmin.github.io/glide-docs-cn/doc/migrating.html) 

[Google推荐——Glide使用详解](https://www.jianshu.com/p/7ce7b02988a4)

郭霖的[Android图片加载框架最全解析（一），Glide的基本用法](https://blog.csdn.net/guolin_blog/article/details/53759439)

[ImageView的scaleType的属性理解](https://blog.csdn.net/qq_34902522/article/details/76682293)

[Android ImageView 的scaleType 属性图解](https://www.jianshu.com/p/32e335d5b842)

[图形变换库-glide-transformations](https://github.com/wasabeef/glide-transformations)