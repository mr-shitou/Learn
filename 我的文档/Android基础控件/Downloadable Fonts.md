# Downloadable Fonts

> 本文结合官方文档以及相关搜索内容和个人观点，相关链接在文末列出

[TOC]

## 简介

手机上有很多应用，而每个应用在产品经理和美工小姐姐的爱护下，为了保持自己独特的魅力都会想要使用好看的字体。所以，程序里会有相应的字体文件，导致应用包变大，以前好的处理方式则是安装的时候再下载字体。但是不管怎样，加入很多软件使用的字体都一样，但是每个应用都保持一个字体文件，显然对手机资源是浪费的。所以，谷歌在8.0(26)提供了“Downloadable Fonts”新特性，使用支持库26版本以上即可在4.0（14）以上版本使用。现在，就让我们在网上下载字体，然后大家分享使用吧。

### 谷歌官方示例

[Downloadable Fonts sample app](https://github.com/googlesamples/android-DownloadableFonts)

## 工作流程

> 字体提供程序是一种检索字体并在本地缓存它们的应用程序，以便其他应用程序可以请求和共享字体。下图说明了该过程 

![Main components in Emoji compat process](https://developer.android.google.cn/guide/topics/ui/images/look-and-feel/downloadable-fonts/downloadable-fonts-process.png) 

### 三种使用方式

- [通过Android Studio和Google Play服务](#通过Android Studio和Google Play服务)
- [通过编程](#通过编程)
- [通过支持库](#通过支持库)

### 通过Android Studio和Google Play服务

> 你可以在Android Studio 3.0以及更高的版本通过Google Play服务来使用这个特性
>
> 注意：手机设备必须具有11或更高版本的Google Play服务才能使用Google字体提供

1. 打开布局编辑器，选择TextView,在属性面版中找到fontFamily属性（可以直接在上面的搜索框中搜索），在下拉框中选择More Fonts

   ![Layout Editor](https://developer.android.google.cn/guide/topics/ui/images/look-and-feel/downloadable-fonts/layout-editor.png) 

2. 在打开的界面（如下图）右上方Source下拉框选择**Google Fonts** （默认应该就是这个）

3. 在字体选择框中选择一个合适的字体

4. 选择**Create downloadable font** and click **OK** （这里选择**Add font to project**，会将字体文件捆绑到项目中）

   ![Layout editor](https://developer.android.google.cn/guide/topics/ui/images/look-and-feel/downloadable-fonts/resources-window.png) 

这样，Android Studio会自动生成在应用中正确呈现字体所需的相关XML文件 ，res目录下会生成font文件夹，以及在values目录下会生成响应字体部署文件。

### 通过编程

要以编程方式使用可下载字体功能，您需要与两个关键类进行交互 

- **android.graphics.fonts.FontRequest**：这个类允许创建一个字体请求 
- **FontsContract**：此类允许根据字体请求创建新的Typeface对象 

### 通过支持库





## 参考了解及推荐链接

[官方链接](https://developer.android.google.cn/guide/topics/ui/look-and-feel/downloadable-fonts)