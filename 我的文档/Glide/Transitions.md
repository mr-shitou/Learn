# Transitions

> 加载图片时的过渡动画

[TOC]

### 关于过渡

在 Glide 中，[`Transitions`(直译为”过渡”)](https://muyangmin.github.io/glide-docs-cn/javadocs/400/com/bumptech/glide/request/transition/Transition.html) 允许你定义 Glide 如何从占位符到新加载的图片，或从缩略图到全尺寸图像过渡。Transition 在单一请求的上下文中工作，而不会跨多个请求。因此，[`Transitions`](https://muyangmin.github.io/glide-docs-cn/javadocs/400/com/bumptech/glide/request/transition/Transition.html) 并不能让你定义从一个请求到另一个请求的动画（比如，交叉淡入效果）。

### 默认过渡

不同于 Glide v3，Glide v4 将**不会**默认应用交叉淡入或任何其他的过渡效果。每个请求必须手动应用过渡。

### 标准行为

Glide 提供了很多的过渡效果，用户可以手动地应用于每个请求。Glide 的内置过渡以一致的方式运行，并且将根据加载图像的位置在某些情况下避免运行。

在 Glide 中，图像可能从四个地方中的任何一个位置加载出来：

1. Glide 的内存缓存
2. Glide 的磁盘缓存
3. 设备本地可用的一个源文件或 Uri
4. 仅远程可用的一个源 Url 或 Uri

如果图像从 Glide 的内存缓存中加载出来，Glide 的内置过渡将不会执行。然而，在另外三种场景下，Glide 的内置过渡都会被执行。

要改变这种行为并编写你自己的定制过渡，请阅读接下来的 [custom transitions](https://muyangmin.github.io/glide-docs-cn/transitions#custom-transitions) 章节。

### 指定过渡

你可以查看 [Options documentation](https://muyangmin.github.io/glide/doc/options.html#transitionoptions) 以获取概览和示例代码。

[`TransitionOptions`](https://muyangmin.github.io/glide-docs-cn/javadocs/400/com/bumptech/glide/TransitionOptions.html) 用于给一个特定的请求指定过渡。 每个请求可以使用 [`RequestBuilder`](https://muyangmin.github.io/glide-docs-cn/javadocs/400/com/bumptech/glide/RequestBuilder.html) 中的 [`transition()`](https://muyangmin.github.io/glide-docs-cn/javadocs/400/com/bumptech/glide/RequestBuilder.html#transition-com.bumptech.glide.TransitionOptions-) 方法来设定 [`TransitionOptions`](https://muyangmin.github.io/glide-docs-cn/javadocs/400/com/bumptech/glide/TransitionOptions.html) 。还可以通过使用 [`BitmapTransitionOptions`](https://muyangmin.github.io/glide-docs-cn/javadocs/400/com/bumptech/glide/load/resource/bitmap/BitmapTransitionOptions.html) 或 [`DrawableTransitionOptions`](https://muyangmin.github.io/glide-docs-cn/javadocs/400/com/bumptech/glide/load/resource/drawable/DrawableTransitionOptions.html) 来指定类型特定的过渡动画。对于 Bitmap 和 Drawable 之外的资源类型，可以使用 [`GenericTransitionOptions`](https://muyangmin.github.io/glide-docs-cn/javadocs/400/com/bumptech/glide/GenericTransitionOptions.html)。

### 性能提示

Android中的动画代价是比较大的，尤其是同时开始大量动画的时候。 交叉淡入和其他涉及 alpha 变化的动画显得尤其昂贵。 此外，动画通常比图片解码本身还要耗时。在列表和网格中滥用动画可能会让图像的加载显得缓慢而卡顿。为了提升性能，请在使用 Glide 向 ListView , GridView, 或 RecyclerView 加载图片时考虑避免使用动画，尤其是大多数情况下，你希望图片被尽快缓存和加载的时候。作为替代方案，请考虑预加载，这样当用户滑动到具体的 item 的时候，图片已经在内存中了。

### 常见错误

#### 对占位符和透明图片交叉淡入

Glide 的默认交叉淡入(cross fade)效果使用了 [`TransitionDrawable`](https://developer.android.com/reference/android/graphics/drawable/TransitionDrawable.html) 。它提供两种动画模式，由 [`setCrossFadeEnabled()`](https://developer.android.com/reference/android/graphics/drawable/TransitionDrawable.html#setCrossFadeEnabled(boolean)) 控制。当交叉淡入被禁用时，正在过渡的图片会在原先显示的图像上面淡入。当交叉淡入被启用时，原先显示的图片会从不透明过渡到透明，而正在过渡的图片则会从透明变为不透明。

在 Glide 中，我们默认禁用了交叉淡入，这样通常看起来要好看一些。实际的交叉淡入，如上所述对两个图片同时改变 alpha 值，通常会在过渡的中间造成一个短暂的白色闪屏，这个时候两个图片都是部分不透明的。

不幸的是，虽然禁用交叉淡入通常是一个比较好的默认行为，当待加载的图片包含透明像素时仍然可能造成问题。当占位符比实际加载的图片要大，或者图片部分为透明时，禁用交叉淡入会导致动画完成后占位符在图片后面仍然可见。如果你在加载透明图片时使用了占位符，你可以启用交叉淡入，具体办法是调整 [`DrawableCrossFadeFactory`](https://muyangmin.github.io/glide-docs-cn/javadocs/400/com/bumptech/glide/request/transition/DrawableCrossFadeFactory.html) 里的参数并将结果传到 [`transition()`](https://muyangmin.github.io/glide-docs-cn/javadocs/400/com/bumptech/glide/TransitionOptions.html#transition-com.bumptech.glide.request.transition.TransitionFactory-) 中。

### 定制过渡

如果要定义一个自定义的过渡动画，你需要完成以下两个步骤：

1. 实现 [`TransitionFactory`](https://muyangmin.github.io/glide-docs-cn/javadocs/400/com/bumptech/glide/request/transition/TransitionFactory.html) .
2. 使用 [`DrawableTransitionOptions#with`](https://muyangmin.github.io/glide-docs-cn/javadocs/400/com/bumptech/glide/load/resource/drawable/DrawableTransitionOptions.html#with-com.bumptech.glide.request.transition.TransitionFactory-) 来将你自定义的 `TransitionFactory` 应用到加载中。

如果要改变你的 transition 的默认行为，以更好地控制它在不同的加载源（内存缓存，磁盘缓存，或uri）下是否被应用，你可以检查一下你的 [`TransitionFactory`](https://muyangmin.github.io/glide-docs-cn/javadocs/400/com/bumptech/glide/request/transition/TransitionFactory.html) 中传递给 [`build()`](https://muyangmin.github.io/glide-docs-cn/javadocs/400/com/bumptech/glide/request/transition/TransitionFactory.html#build-com.bumptech.glide.load.DataSource-boolean-) 方法的那个 [`DataSource`](https://muyangmin.github.io/glide-docs-cn/javadocs/400/com/bumptech/glide/load/DataSource.html) 。

如需示例代码，请查看 [`DrawableCrossFadeFactory`](https://github.com/bumptech/glide/blob/8f22bd9b82349bf748e335b4a31e70c9383fb15a/library/src/main/java/com/bumptech/glide/request/transition/DrawableCrossFadeFactory.java#L35).