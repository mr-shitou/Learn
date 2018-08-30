# Android中所有的布局或者View

> 这里收集，所有的布局，包括基础布局、support库布局、design库布局。如果有其他好的布局也收集到这里。
>
> 很重要的一点：只包括目前还在使用中的布局，废弃的布局标记为@Deprecated。这里只做记录，知道这样的布局，详细内容会把好的文章链接放到下方。

[TOC]

## 基础布局

### 简介

我们可以理解Android的屏幕为一个画布，这个画布是可以延伸到屏幕外的。但是在屏幕外对于用户来说没有什么意义，所以我们的布局文件一般是为屏幕展示内容准备的。这里提到这个因为消除大家思想的局限性（我不知道这点以前，一直以为只能在屏幕里面），想具体了解的可以搜索Android窗口，还可以搜索下Android视图绘制，这里不再做介绍。只要知道，布局是一种显示规则，规定里面的子控件的空间分布。至于其中父布局和子控件互相影响的关系，记得搜索Android视图绘制。

这些布局是可以互相嵌套，所以可以展现出多种多样的界面，但是多重嵌套也导致UI绘制耗时以及资源浪费。所以Google推出了ConstraintLayout，现在请尽量使用这个布局。

另外，当实现一个界面的时候可以使用多种布局方式来实现要根据具体情况选择最好的实现方式。考虑的因素，比如上面的提到的嵌套层数，布局复杂程度以及代码编写复杂程度等等（没想到吧，写个简答的XML也这么麻烦）。所以，没有最好的，只有最合适的，这同样适用于代码编写中。

下面对基础布局做简单介绍，记录个别属性，其他的属性会在下面推荐些比较好的文章，大家去那里查看就好。

### AbsoluteLayout（@Deprecated API 3）

### FrameLayout

> 设计用来占据屏幕上一块区域，显示一个单独的控件。所有的控件默认显示在左上角，后面的控件会堆叠在上个控件上方。很简单，所以这是最轻量级的布局，轻量级简单来说就是，效率高。

| [`android:foregroundGravity`](https://developer.android.google.cn/reference/android/widget/FrameLayout.html#attr_android:foregroundGravity) | Defines the gravity to apply to the foreground drawable. （设置前景色位置，所以要设置前景色才有效，并且前景色要设置为图片） |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [`android:measureAllChildren`](https://developer.android.google.cn/reference/android/widget/FrameLayout.html#attr_android:measureAllChildren) | Determines whether to measure all children or just those in the VISIBLE or INVISIBLE state when measuring. （确定在测量时是测量所有子控件，还是仅测量处于可见状态的子控件。默认是false） |

### LinearLayout

>

## 链接

[Android 基础：常用布局 介绍 & 使用（附 属性查询）](https://www.jianshu.com/p/4fac6304d872/)

[小Demo小知识-android:foreground与android:background](https://www.jianshu.com/p/b5ecd39ed494)

[onWindowFocusChanged和measureAllChildren](https://blog.csdn.net/lintcgirl/article/details/46315645)



