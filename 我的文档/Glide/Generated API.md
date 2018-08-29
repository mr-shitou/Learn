# Generated API

> 接着家里的文档，继续写

[TOC]

### 简介

Glide v4 使用 [注解处理器 (Annotation Processor)](https://docs.oracle.com/javase/8/docs/api/javax/annotation/processing/Processor.html) 来生成出一个 API，在 Application 模块中可使用该流式 API 一次性调用到 [`RequestBuilder`](https://muyangmin.github.io/glide-docs-cn/javadocs/400/com/bumptech/glide/RequestBuilder.html)， [`RequestOptions`](https://muyangmin.github.io/glide-docs-cn/javadocs/400/com/bumptech/glide/request/RequestOptions.html) 和集成库中所有的选项。

所以，当我们在gradle中添加的时候添加了两个，另一个用于“注解”。

Generated API 模式的设计出于以下两个目的：

1. 集成库可以为 Generated API 扩展自定义选项。
2. 在 Application 模块中可将常用的选项组打包成一个选项在 Generated API 中使用

虽然以上所说的工作均可以通过手动创建 [`RequestOptions`](https://muyangmin.github.io/glide-docs-cn/javadocs/400/com/bumptech/glide/request/RequestOptions.html) 子类的方式来完成，但想将它用好更具有挑战，并且降低了 API 使用的流畅性。

### 开始使用

#### 有效使用范围

Generated API 目前仅可以在 Application 模块内使用。这一限制可以让我们仅持有一份 Generated API，而不是各个 Library 和 Application 中均有自己定义出来的 Generated API。这一做法会让 Generated API 的调用更简单，并确保 Application 模块中 Generated API 调用的选项在各处行为一致。这一限制在接下来的版本中也许会被取消（以实验性或其他的方式给出）。

**简单讲，就是写一个类如下。在使用Glide的地方，用`GlideApp` 调用方法即可，好处就和上面说的一样，不需要再手动创建相应子类等等。**

```java
//不需要实现什么方法，像这样就可以，就是这么简单
@GlideModule
public final class MyAppGlideModule extends AppGlideModule {}
```

#### Android Studio(需要记住，否则真的会出现下面说的问题)

Android Studio 在大多数时候都可以正确地处理注解处理器 (annotation processor) 和 generated API。然而，当你第一次添加你的 `AppGlideModule` 或做了某些类型的修改后，你可能需要重新构建 (rebuild) 你的项目。 无论何时，如果你发现 API 没有被 import ，或看起来已经过期，你可以通过以下方法重新构建：

1. 打开 Build 菜单；
2. 点击 Rebuild Project。

**一个很重要的点，使用KotLin时，对引入的注解，需要做特殊处理。当使用KotLin时，再去官方文档查看**

### GlideExtension

Glide Generated API 可在 Application 和 Library 中被扩展。扩展使用被注解的静态方法来添加新的选项、修改现有选项、甚至添加额外的类型支持。

[`@GlideExtension`](https://muyangmin.github.io/glide-docs-cn/javadocs/400/com/bumptech/glide/annotation/GlideExtension.html) 注解用于标识一个扩展 Glide API 的类。任何扩展 Glide API 的类都必须使用这个注解来标记，否则其中被注解的方法就会被忽略。

被 [`@GlideExtension`](https://muyangmin.github.io/glide-docs-cn/javadocs/400/com/bumptech/glide/annotation/GlideExtension.html) 注解的类应以工具类的思维编写。这种类应该有一个私有的、空的构造方法，应为 final 类型，并且仅包含静态方法。被注解的类可以含有静态变量，可以引用其他的类或对象。

**这部分，感觉最主要学的是注解类编写的思想**

在 Application 模块中可以根据需求实现任意多个被 [`@GlideExtension`](https://muyangmin.github.io/glide-docs-cn/javadocs/400/com/bumptech/glide/annotation/GlideExtension.html) 注解的类，在 Library 模块中同样如此。当 [`AppGlideModule`](https://muyangmin.github.io/glide-docs-cn/javadocs/400/com/bumptech/glide/module/AppGlideModule.html) 被发现时，所有有效的 [Glide 扩展类](https://muyangmin.github.io/glide-docs-cn/javadocs/400/com/bumptech/glide/annotation/GlideExtension.html) 会被合并，所有的选项在 API 中均可以被调用。合并冲突会导致 Glide 的 Annotation Processor 抛出编译错误。

被 `@GlideExtention` 注解的类有两种扩展方式：

1. [`GlideOption`](https://muyangmin.github.io/glide-docs-cn/javadocs/400/com/bumptech/glide/annotation/GlideOption.html) - 为 [`RequestOptions`](https://muyangmin.github.io/glide-docs-cn/javadocs/400/com/bumptech/glide/request/RequestOptions.html) 添加一个自定义的选项。
2. [`GlideType`](https://muyangmin.github.io/glide-docs-cn/javadocs/400/com/bumptech/glide/annotation/GlideType.html) - 添加对新的资源类型的支持(GIF，SVG 等等)。

#### GlideOption

用 [`@GlideOption`](https://muyangmin.github.io/glide-docs-cn/javadocs/400/com/bumptech/glide/annotation/GlideOption.html) 注解的静态方法用于扩展 [`RequestOptions`](https://muyangmin.github.io/glide-docs-cn/javadocs/400/com/bumptech/glide/request/RequestOptions.html) 。`GlideOption` 可以：

1. 定义一个在 Application 模块中频繁使用的选项集合。
2. 创建新的选项，通常与 Glide 的 [`Option`](https://muyangmin.github.io/glide-docs-cn/javadocs/400/com/bumptech/glide/load/Option.html) 类一起使用。

要定义一个选项集合，你可以这么写：

```java
@GlideExtension
public class MyAppExtension {
  // Size of mini thumb in pixels.
  private static final int MINI_THUMB_SIZE = 100;

  private MyAppExtension() { } // utility class

  @GlideOption
  public static void miniThumb(RequestOptions options) {
    options
      .fitCenter()
      .override(MINI_THUMB_SIZE);
  }
```

这将会在 [`RequestOptions`](https://muyangmin.github.io/glide-docs-cn/javadocs/400/com/bumptech/glide/request/RequestOptions.html) 的子类中生成一个方法，类似这样：

```java
public class GlideOptions extends RequestOptions {

  public GlideOptions miniThumb() {
    MyAppExtension.miniThumb(this);
  }

  ...
}
```

你可以为方法任意添加参数，但要保证第一个参数为 [`RequestOptions`](https://muyangmin.github.io/glide-docs-cn/javadocs/400/com/bumptech/glide/request/RequestOptions.html)。

```java
@GlideOption
public static void miniThumb(RequestOptions options, int size) {
  options
    .fitCenter()
    .override(size);
}
```

在自动生成的方法中新添的参数同样被加了进来：

```java
public GlideOptions miniThumb(int size) {
  MyAppExtension.miniThumb(this);
}
```

之后你就可以使用生成的 `GlideApp` 类调用你的自定义方法：

```java
GlideApp.with(fragment)
   .load(url)
   .miniThumb(thumbnailSize)
   .into(imageView);
```

使用 `@GlideOption` 标记的方法应该为静态方法，并且返回值为空。请注意，这些生成的方法在一般的 `Glide` 和 `RequestOptions` 类里不可用。（也就是说，如果不使用注解生成GlideApp，而是使用Glide来调用是不会调用自定义的扩展内容）

#### GlideType（和上面的GlideOption差不多）

被 [`@GlideType`](https://muyangmin.github.io/glide-docs-cn/javadocs/400/com/bumptech/glide/annotation/GlideType.html) 注解的静态方法用于扩展 [`RequestManager`](https://muyangmin.github.io/glide-docs-cn/javadocs/400/com/bumptech/glide/RequestManager.html) 。被 `@GlideType` 注解的方法允许你添加对新的资源类型的支持，包括指定默认选项。

例如，为添加对 GIF 的支持，你可以添加一个被 `@GlideType` 注解的方法：

```java
@GlideExtension
public class MyAppExtension {
  private static final RequestOptions DECODE_TYPE_GIF = decodeTypeOf(GifDrawable.class).lock();

  @GlideType(GifDrawable.class)
  public static void asGif(RequestBuilder<GifDrawable> requestBuilder) {
    requestBuilder
      .transition(new DrawableTransitionOptions())
      .apply(DECODE_TYPE_GIF);
  }
}
```

这样会生成一个包含对应方法的 [`RequestManager`](https://muyangmin.github.io/glide-docs-cn/javadocs/400/com/bumptech/glide/RequestManager.html) ：

```java
public class GlideRequests extends RequesetManager {

  public RequestBuilder<GifDrawable> asGif() {
    RequestBuilder<GifDrawable> builder = as(GifDrawable.class);
    MyAppExtension.asGif(builder);
    return builder;
  }

  ...
}
```

之后你可以使用生成的 `GlideApp` 类调用你的自定义类型：

```java
GlideApp.with(fragment)
  .asGif()
  .load(url)
  .into(imageView);
```

被 `@GlideType` 标记的方法必须使用 [`RequestBuilder`](https://muyangmin.github.io/glide-docs-cn/javadocs/400/com/bumptech/glide/RequestBuilder.html) 作为其第一个参数，这里的泛型 `<T>` 对应 [`@GlideType`](https://muyangmin.github.io/glide-docs-cn/javadocs/400/com/bumptech/glide/annotation/GlideType.html) 注解中传入的类。该方法应为静态方法，且返回值为空。方法必须定义在一个被 [`@GlideExtension`](https://muyangmin.github.io/glide-docs-cn/javadocs/400/com/bumptech/glide/annotation/GlideExtension.html) 注解标记的类中。

##连接
[官方文档](https://muyangmin.github.io/glide-docs-cn/doc/generatedapi.html)
