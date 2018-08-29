# RecyclerView

> ListView的时代早已经过去，RecyclerView是现在使用率最高的控件。对其熟练掌握，在界面上就满足了很大一部分日常需求。下面将把基本用法、高级用法以及一些技巧和相关开源库尽可能的记录下来。最后，可能的话还想顺便记录下ListView。

[TOC]

## 官方文档翻译

> RecyclerVIew和ListVIew一样是“列表”，是ListView的升级版。先来看看官方是如何讲解的，下面是对其概要翻译。

###概要

如果，你需要展示一个包含大量数据集合或者数据需要经常更新的可滑动列表，那么就应该尝试使用RecyclerView。

**小技巧**：通过 **File > New > Fragment > Fragment (List)** ，可以快速的创建一个包含RecyclerView的Fragment。（真的很不错，感觉这样省去了很多步骤。DummyContent类和名字一样，用来产生“假”的列表数据）

我们可以创建一个列表项为CardVIew样式的RecyclerView。 [Create a Card-based Layout](https://developer.android.google.cn/guide/topics/ui/layout/cardview.html)，其实，就是在列表项布局添加CardView即可。

一个简单的RecyclerView列子，[RecyclerView Sample App](https://github.com/googlesamples/android-RecyclerView/)。（特别简单，只是展示LinearLayoutManager、GridLayoutManager两种布局，并显示数据加载情况和Item点击情况。感觉log写的不错，可以学习下）

### 简要实现分析

要使用RecyclerView，在布局中添加RecyclerView，实现相关的类，并搭配LayoutManager（LinearLayoutManager、GridLayoutManager、StaggeredGridLayoutManager) 或者你自己自定义的LayoutManager。

个人观点：LayoutManager是用来管理RecyclerView的，也正是因为这个，才使RecyclerView这么强大。我们还可以自定义自己的LayoutManager，这个符合先进的设计理想，真的很棒。

每个列表项，都是由ViewHolder来展现的，所以，要继承“RecyclerView.ViewHolder”。（原理上，和ListView中的ViewHolder一样，这里RecyclerView已经替我们实现了。如果不了解，那就需要好好了解下了）

ViewHolder又由Adapter来管理，所以，我们需要创建一个继承RecyclerView.Adapter的Adapter。**结合上面的简单总结下**:

```java
//我们的Adapter就应该像这样，里面的具体逻辑在后面讨论
public class CustomAdapter extends RecyclerView.Adapter<CustomAdapter.ViewHolder> {}
```

RecyclerView本身做了一些优化工作:

- 预加载，比如界面显示的列表项position位置为0到9，但是10位置的数据也已经绑定到RecyclerView中了。这样，当我们向下滑动时，它就已经准备好了。
- 内部实现了ViewHolder，我们不需要自己实现（也不是不需要实现，而是实现RecyclerView提供给我们的方法）。当列表滑出屏幕又重新回到屏幕时，我们可以复用ViewHolder（简单说下，ViewHolder就是用来保存View实列，提供视图复用）。但是，那种离开屏幕较久的ViewHolder就会被释放，也可以绑定视图。
- 当展示的列表项改变时，我们可以通过RecyclerView.Adapter.notify...()形式的具体方法来通知RecyclerView数据改变了。（...表示多种形式的notify()方法，具体为[notify()相关方法](#notify()相关方法)）

**说说自己的理解**：

### 开始使用

> 代码就不贴在这里了，具体可以看官方网页，并且还有Kotlin代码。链接在下方

1. 添加支持库

   dependencies {    implementation 'com.android.support:recyclerview-v7:27.1.1'}

   （关于支持库，这里多说下，有很多坑。如果有时间，要好好看看这方面的姿势。萌新的话，就尽可能使用和所学例子相同的环境配置和支持库配置）

2. 在布局中添加RecyclerView

3. 代码中获取RecyclerView，添加“LayoutManager”、“Adapter”

4. 创建RecyclerView的Adapter

   Adapter是重点，不过也很简单，写起来。把上面总结的那行代码写完之后，根据报红的地方，快捷键Alt+Enter两次：创建一个ViewHolder类继承RecyclerView.ViewHolder；实现方法。随后就是根据官方示例改下就OK了。当然，我们也可以添加自己的方法，实现项目中需要实现的特定操作。

5. 很重要的一点是，我们需要自己在Adapter中写点击事件的回调，就写在“onBindViewHolder ”中。其实

**小技巧**：在数据发生改变时，[ListAdapter](https://developer.android.google.cn/reference/android/support/v7/recyclerview/extensions/ListAdapter.html) 对决定列表中那些列表项需要更新很有用。这个时v27新增的接口，当然，它也继承RecyclerView.Adapter，是一个抽象类。

### 自定义RecyclerView

> 一般情况下来讲，你是不需要自定义的。只需要做好视图填充和展示即可，除非你有特殊的要求

系统本身提供了三个LayoutManager（这个是管理布局的老大，Manager，经理嘛），

- [LinearLayoutManager](https://developer.android.google.cn/reference/android/support/v7/widget/LinearLayoutManager.html) （ListView)
- [GridLayoutManager](https://developer.android.google.cn/reference/android/support/v7/widget/GridLayoutManager.html)       (多个并排ListView)
- [StaggeredGridLayoutManager](https://developer.android.google.cn/reference/android/support/v7/widget/StaggeredGridLayoutManager.html)  （瀑布流）

如果，这些都不合胃口，就需要继承`RecyclerView.LayoutManager`  并重写方法。（或者，找个适合自己的库，我感觉还是后者简单些，哈哈）

###添加列表项动画

默认情况下，RecyclerView使用`DefaultItemAnimator`类来控制列表项动画。如果自定义动画，继承   `RecyclerView.ItemAnimator` 并实现方法。

### 使列表项可选择

> 敲黑板啦，这是个新库[`recyclerview-selection`](https://developer.android.google.cn/reference/androidx/recyclerview/selection/package-summary.html)  ，在androidx包下。androidx不知道的也需要了解下，我也是刚补了课。这个库先记下来，等androidx成熟并可以使用时，再来使用这个库肯定会感觉很舒服。
>
> 水平有限。下方翻译不一定准确，感觉官方写的太复杂了，看的一头雾水。

**7**步走战略：

1. 先确定使用的选择项的键值类型，然后创建[`ItemKeyProvider`](https://developer.android.google.cn/reference/androidx/recyclerview/selection/ItemKeyProvider.html)。

   三种类型，`Parcelable` (所有子类，比如`Uri`), `String`,  `Long` 。具体看 [`SelectionTracker.Builder`](https://developer.android.google.cn/reference/androidx/recyclerview/selection/SelectionTracker.Builder.html) 

2. 实现 [`ItemDetailsLookup`](https://developer.android.google.cn/reference/androidx/recyclerview/selection/ItemDetailsLookup.html)

   [`ItemDetailsLookup`](https://developer.android.google.cn/reference/androidx/recyclerview/selection/ItemDetailsLookup.html)通过RecyclerView Item的MotionEvent值来给选择库反馈当前Item信息。它其实是根据RecyclerView.ViewHolder实例的备份，从而生成 [`ItemDetails`](https://developer.android.google.cn/reference/androidx/recyclerview/selection/ItemDetailsLookup.ItemDetails.html)  的工厂类。

3. 更新Item视图来显示是否被选择

   选择库不提供默认的选择样式，所以你必须要在onBindViewHolder() 方法中提供选择样式。推荐发方式如下

   - 控件调用setActivated() 方法（注意，不是setSelected()方法）
   - 更新视图，根据是否选择展示的不同状态。推荐使用 [color state list resource](https://developer.android.google.cn/guide/topics/resources/color-list-resource.html) 来决定选择与否的展示视图（就是”selector“）。

4. 使用[ActionMode](https://developer.android.google.cn/reference/android/support/v7/view/ActionMode.html) 提供一个选择后的操作。

   注册一个 [`SelectionTracker.SelectionObserver`](https://developer.android.google.cn/reference/androidx/recyclerview/selection/SelectionTracker.SelectionObserver.html)  观测者，当选择改变时通知它。当有一个Item被选择时，启动ActionMode并提供可进行的操作（比如删除）。当操作结束时，别忘了终止ActionMode。

5. 进行次要操作时的应对

   当选择操作执行时，如果用户点击或者拖拽时要注册合适的监听器来监听这些操作。具体内容参看 [`SelectionTracker.Builder`](https://developer.android.google.cn/reference/androidx/recyclerview/selection/SelectionTracker.Builder.html) 

6. 使用 [`SelectionTracker.Builder`](https://developer.android.google.cn/reference/androidx/recyclerview/selection/SelectionTracker.Builder.html) 组装所有内容 

   使用Long类型的示例

   ```java
   SelectionTracker tracker = new SelectionTracker.Builder<>(
           "my-selection-id",
           recyclerView,
           new StableIdKeyProvider(recyclerView),
           new MyDetailsLookup(recyclerView),
           StorageStrategy.createLongStorage())
           .withOnItemActivatedListener(myItemActivatedListener)
           .build();
   ```

7. 在[activity lifecycle](https://developer.android.google.cn/guide/components/activities/activity-lifecycle.html)（activity生命周期）中包含选择事件

   为了保持选择状态在activity的生命周期中，您的应用必须在activity的onSaveInstanceState()和onRestoreInstanceState()中分别调用选择跟踪器的onSaveInstanceState（)和onRestoreInstanceState()。您的应用还必须为SelectionTracker提供唯一的选择ID ，此ID是必需的，因为活动或片段可能具有多个不同的ID， 因为activity或者fragment可能有多个不同可选择列表，并且都需要保存他们的选择状态。

**译后总结**：终于翻译完了，翻译的不好甚至有可能有很多错误的地方。大概的意思就是个可以选择的列表，可以想象下我们选择文件删除的操作。总感觉写的太复杂了，以后再研究这个，毕竟现在还用不到。

### 额外的礼物

[Sunflower](https://github.com/googlesamples/android-sunflower) ，官方的高级Demo，值得一起学习哈。（这个需要最新的Android Studio 3.2版本并且使用的Kotlin一些新的库，如果真的想尝试的话，可以[点击这里下载](https://developer.android.google.cn/studio/preview/)一个。这个是可以和现有版本一起使用的，具体方法参考官网即可）

## API

### notify()相关方法

1. notifyItemChanged(int position) 更新列表position位置上的数据可以调用
2. notifyItemInserted(int position) 列表position位置添加一条数据时可以调用，伴有动画效果 
3. notifyItemRemoved(int position) 列表position位置移除一条数据时调用，伴有动画效果 
4. notifyItemMoved(int fromPosition, int toPosition) 列表fromPosition位置的数据移到toPosition位置时调用，伴有动画效果 
5. notifyItemRangeChanged(int positionStart, int itemCount) 列表从positionStart位置到itemCount数量的列表项进行数据刷新 
6. notifyItemRangeInserted(int positionStart, int itemCount) 列表从positionStart位置到itemCount数量的列表项批量添加数据时调用，伴有动画效果 
7. notifyItemRangeRemoved(int positionStart, int itemCount) 列表从positionStart位置到itemCount数量的列表项批量删除数据时调用，伴有动画效果

### 小技巧

1.  recyclerView.setHasFixedSize(true);

   当列表Item不会因为数据内容改变其大小时（列表项多少不算），使用这个，应该会避免每次都重复计算Item大小。从而使效率更高，一般情况下，Item的大小也不会改变。所以要记得使用这个小技巧方法。

 

 

 

 









## 链接

官方使用介绍：[Create a List with RecyclerView](https://developer.android.google.cn/guide/topics/ui/layout/recyclerview)