# Widget

> 话说，现在我还没搞清楚Google对这个词的定义，什么才属于Widget的范畴。现将Android Studio上的这个分类控件记录如下

[TOC]

- ToggleButton

  ToggleButton < CompoundButton  < Button

  源码中介绍，CompoundButton有两种状态，当点击或者按下的时候会自动发生变化。所以很多选择性的控件都继承于CompoundButton。

- CheckBox（继承于CompoundButton）

- RadioButton（继承于CompoundButton）

- CheckedTextView（继承与TextView实现Checkable接口，所有既能选择又能展示Text）

  基本上，等同于，TextView和CheckBox的组合。但是明显应该使用这个控件。源码中介绍，在具有选择功能的ListView中使用会非常有用。注意，要使文字居中需要“textAlignment”属性，这是View的属性。点击选择的事件要我们自己去获取。

  相关文章链接：

  [CheckedTextView使用Demo](https://blog.csdn.net/zouchengxufei/article/details/51029489)

  [CheckedTextView 使用](https://blog.csdn.net/vae260772/article/details/77089759?locationNum=1&fps=1)

  [原来还有这货----CheckedTextView ](http://blog.sina.com.cn/s/blog_495c8c720101asjj.html)

  [Android开发-CheckedTextView复选框居左文字居中-AndroidStudio](https://blog.csdn.net/iwanghang/article/details/69568317)

  [CheckedTextView 注意事项](https://www.jianshu.com/p/0266e851982f)

- Spinner（继承至AbsSpinner  <  AdapterView<SpinnerAdapter>）

  看到这个AdapterView，肯定都知道这个是列表型的控件，其实他就是个下拉菜单。比较简单，不作过多介绍

  [android Spinner控件详解](https://blog.csdn.net/qq_32059827/article/details/53106821)

  [Android--UI之Spinner](https://www.cnblogs.com/plokmju/p/android_Spinner.html)

- ProgressBar（直接继承View，使用的方法直接搜索即可）

- SeekBar（继承至AbsSeekBar <  ProgressBar。）

  源码讲，AbsSeekBar就是添加了一个可以自由拖拽thumb的ProgressBar

- QuickContactBadge（继承ImageView并实现OnClickListener接口）

  从实现OnClickListener接口来看，就是用来点击的，其实这个是用来关联联系人，然后实现点击效果——这里的点击效果是指发送短信或者打电话。

  [Android QuickContactBadge](https://blog.csdn.net/kinglearnjava/article/details/46237733)

- RatingBar（继承至AbsSeekBar）

  [Ratingbar UseGuide](https://www.jianshu.com/p/06c321b7f19b)

- Switch（继承至CompoundButton，不用想都知道了。。）

- Space（轻量级View，直接继承View，为两个组件之间添加间距）

  [学Android Space控件，只看这篇文章就行了](https://blog.csdn.net/dajian35/article/details/74842681)

  

