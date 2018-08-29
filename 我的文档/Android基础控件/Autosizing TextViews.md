# Autosizing TextViews

> 结合官方文档以及别人的文章以及自己的一些看法。用到的文章，具体链接在下方列出

[TOC]

## 简介

这是Android8.0（26）的新增特性，可以使文字**大小**在不同的屏幕上自适应。v4支持库从26版本开始提供对低版本的支持，最低支持4.0（14）。支持包中，类名是`TextViewCompat`  。注意这里是说文字大小，不是控件大小。**只支持静态文本及其子类，如TextView和Button等，不支持EditText**

## 设置自适应的TextView

> 注意，不推荐使用“wrap_content”确定宽高值，可能会有不确定的错误出现。

可以设置的三个值,可以在XML文件和代码中设置

- [Default](#Default)  
- [Granularity](#Granularity)
- [Preset Size](#Preset Size)

### Default

> 默认设置允许TextView的自动调整在水平轴和垂直轴上均匀缩放 ，两个值，"none"和“uniform”

- 代码中调用

  setAutoSizeTextTypeWithDefaults(int autoSizeTextType)  

- XML中使用

  添加“android:autoSizeTextType”属性

- 使用支持库

  - 代码中直接引用

    ```java
    //直接使用支持类，引用定义好的TextView
    textView = findViewById(R.id.text);
    TextViewCompat.setAutoSizeTextTypeWithDefaults(textView, TextViewCompat.AUTO_SIZE_TEXT_TYPE_UNIFORM);
    ```

  - 在XML中使用

    使用app:autoSizeTextType="uniform"。命名空间前缀是“app”，并且添加app命名空间定义。但是我在使用过程中不可以使用，使用“android”又会显示版本限制。在代码中就可以实现效果，所以，假如你也出现这种情况，还是在代码中设置吧，千万别纠结这个问题。

**注意：**Default中的`minTextSize = 12sp`, `maxTextSize = 112sp`,`granularity = 1px` 。即最小，最大以及变化值，用于和下面的属性对应。

### Granularity

> 通过这个属性值可以定义最小和最大文本大小的范围以及指定每个步骤大小的维度 。TextView在最小和最大尺寸范围内均匀缩放，每个增量按“粒度”属性中设置的值进行。 

使用方法和[Default](Default)相似，只不过需要额外添加三个参数，最大，最下以及增减变量

只列出在XML中的使用

```xml
<?xml version="1.0" encoding="utf-8"?>
<TextView
    android:layout_width="match_parent"
    android:layout_height="200dp"
    android:autoSizeTextType="uniform"
    android:autoSizeMinTextSize="12sp"
    android:autoSizeMaxTextSize="100sp"
    android:autoSizeStepGranularity="2sp" />
```

### Preset Size

> 预设大小允许我们指定TextView在自动调整文本大小时选择的所有值 ，也就是说，指定可以选择的值，当更改大小时对比选择一个我们预先设定好的合适值。

使用方法和上面相似，这里只列出在XML中的使用方法

首先，在res/values/arrays.xml 文件下编写好我们的预设值

```xml
<resources>
  <array name="autosize_text_sizes">
    <item>10sp</item>
    <item>12sp</item>
    <item>20sp</item>
    <item>40sp</item>
    <item>100sp</item>
  </array>
</resources>
```

然后在我们的布局中引入

```xml
<?xml version="1.0" encoding="utf-8"?>
<TextView
    android:layout_width="match_parent"
    android:layout_height="200dp"
    android:autoSizeTextType="uniform"
    android:autoSizePresetSizes="@array/autosize_text_sizes" />
```

这里说明下，我们的TextView在调整大小的时候，理想情况下是这样的。假如系统觉得文字大小应该38sp合适，那么就会对比我们上面的预设值，选择40sp。但是还会有很多复制的情况，就不具体讨论，简而言之就是文字大小会选择你预设值里面的一个，但是选择哪一个还是要系统去判断。说实话，我不太推荐这个方式。

## 参考链接或推荐链接

https://developer.android.google.cn/guide/topics/ui/look-and-feel/autosizing-textview

https://www.cnblogs.com/plokmju/p/8268005.html