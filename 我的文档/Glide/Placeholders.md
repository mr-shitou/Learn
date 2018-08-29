# Placeholders

> 图片使用中的占位符，比如默认图片，错误图片等

[TOC]

### 类型

Glide允许用户指定三种不同类型的占位符，分别在三种不同场景使用：

- [placeholder](https://muyangmin.github.io/glide-docs-cn/javadocs/400/com/bumptech/glide/request/RequestOptions.html#placeholder-int-)
- [error](https://muyangmin.github.io/glide-docs-cn/javadocs/400/com/bumptech/glide/request/RequestOptions.html#error-int-)
- [fallback](https://muyangmin.github.io/glide-docs-cn/javadocs/400/com/bumptech/glide/request/RequestOptions.html#fallback-int-)

#### 占位符(Placeholder)

占位符是当请求正在执行时被展示的 Drawable （比如网易云正在加载时，显示的图片，即默认图片）。当请求成功完成时，占位符会被请求到的资源替换。如果被请求的资源是从内存中加载出来的，那么占位符可能根本不会被显示。如果请求失败并且没有设置 `error Drawable` ，则占位符将被持续展示。类似地，如果请求的url/model为 `null` ，并且 `error Drawable` 和 `fallback` 都没有设置，那么占位符也会继续显示。

使用 [generated API](https://muyangmin.github.io/glide-docs-cn/doc/generatedapi.html) ：

```java
//使用GlideApp需要先知道上面的 “generated API”
GlideApp.with(fragment)
  .load(url)
  .placeholder(R.drawable.placeholder) //默认图片
  .error(R.drawable.error)  //错误显示图片
  .fallback(R.drawable.fallback)  //当数据为空，而不认为时错误时，显示的图片
  .into(view);
```

或者，使用颜色

```java
GlideApp.with(fragment)
  .load(url)
  .placeholder(new ColorDrawable(Color.BLACK))
  .into(view);
```

#### 错误符(Error)

`error Drawable` 在请求永久性失败时展示。`error Drawable` 同样也在请求的url/model为 `null` ，且并没有设置 `fallback Drawable` 时展示。

使用方法在上方的代码示例中已经展示出来。

#### 后备回调符(Fallback)

`fallback Drawable` 在请求的url/model为 `null` 时展示。设计 `fallback Drawable` 的主要目的是允许用户指示 `null` 是否为可接受的正常情况。例如，一个 `null` 的个人资料 url 可能暗示这个用户没有设置头像，因此应该使用默认头像。然而，`null` 也可能表明这个元数据根本就是不合法的，或者取不到。 默认情况下Glide将 `null` 作为错误处理，所以可以接受 `null` 的应用应当显式地设置一个 `fallback Drawable` 。

使用方法在上方的代码示例中已经展示出来。

这个理解起来，就是，当为null是正常时，要提供一个默认的图片。很重要的一点时，假如，设置了错误占位图的话。如果不设置回调图，那么将显示错误占位图，设置则显示回调占位图。

个人认为这个不太常用。

### FAQ

##### 占位符是异步加载的吗？

No。占位符是在主线程从Android Resources加载的。我们通常希望占位符比较小且容易被系统资源缓存机制缓存起来。

##### 变换是否会被应用到占位符上？

No。Transformation仅被应用于被请求的资源，而不会对任何占位符使用。例如你正在加载圆形图片，你可能希望在你的应用中包含圆形的占位符。但是你也可以考虑自定义一个View来剪裁(clip)你的占位符，达到你的transformation的效果。

##### 在多个不同的View上使用相同的Drawable可行么？

通常可以，但不是绝对的。任何无状态(`non-stateful`)的 Drawable（例如 `BitmapDrawable` ）通常都是ok的。但是有状态的 Drawable 不一样，在同一时间多个 View 上展示它们通常不是很安全，因为多个View会立刻修改(`mutate`) Drawable 。对于有状态的 Drawable ，建议传入一个资源ID，或者使用 `newDrawable()` 来给每个请求传入一个新的拷贝。

**这个不是很理解，什么是有状态和无状态的图片，以后再理解**

## 链接

[官方文档](https://muyangmin.github.io/glide-docs-cn/doc/placeholders.html)