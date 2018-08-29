# Text各种控件

> 记录官方Text相关控件功能

[TOC]

## 总结

基本都是根据inputType的值派生出来的，没有太多的用处，inputType值用于改变键盘形态，方便输入。inputType是EditText最重要的属性，当然是在XML中。

其中最重要的是AutoCompleteTextView及其子类MultiAutoCompleteTextView，AutoCompleteTextView继承至EditText并实现Filter.FilterListener接口。主要用于类似搜索时，输入内容，提示相关展示。具体使用方法，

## 知识点记录

### lableFor标签

EditText中的labelFor属性。指定视图的id，此视图用作可访问性标签 。例如，UI中EditText之前的TextView通常指定EditText中包含的信息。因此，TextView是EditText的标签。 一般来说，不处理或者将值和id值设置为一样即可。当在一个TextView中指定值时，警告提示也会消失。

### imeOption标签

actionUnspercified    未指定。IME_NULL

actionNone            没有动作IME_ACTION_NONE

actionGo              去往。带到键入的文本目标，例如当输入URL时。

actionSearch          搜索。获得搜索已键入文本的结果。

actionSend            发送。将文本传递到目标。通常在写邮件时使用。

actionNext            下一步。使用户进入到接受文本的下一个字段。

actionDone            完成。关闭软键盘。

actionPrevious        上一步。使用户进入到接受文本的上一个字段。

flagNoFullscreen      用于请求IME从不进入全屏模式。并非所有IMAGE都遵守。

flagNavigatePrevious  向后导航。

flagNavigateNext      向前导航。

flagNoExtractUi       用于指定IME不需要显示其提取的文本ui。

flagNoAccessoryAction 与自定义结合使用。当全屏操作时，该附件不应作为附件按钮使用。

flagNoEnterAction     与自定义结合使用。操作不应作为“输入”键的替换而在线使用。

flagForceAscii        请求IME可以输入ASCII字符。

如果设置了键盘没有变化那么需要单独加一些其他的属性配合使用xml中 属性设置：

1将singleLine设置为true；2将inputType设置为text；

### inputType

none               没有内容类型。文本不可编辑。

text               只是普通的旧文本。

textCapCharacters  字母，所有字母大写。

textCapWords       字母，单词首字母大写。

textCapSentence    字母，每句首字母大写。

textAutoCorrect    对正在进行输入的文本进行自动校对。

textAutoComplete   自动输入。

textMultiLine      允许多行文本。如果没有设置，文本将被限制为一行。

textImeMultiLine   输入法提供多行。

textNoSuggestions  输入法不提示词典单词。

textUri            URI格式。

textEmailAddress   邮件格式。

textEmailSubject   邮件主题。

textShortMessage   短消息。

textLongMessage    长消息。

textPersonName     人名格式。

textPostalAddress   邮政邮寄地址。

textPassword       密码格式。

textVisiblePassword密码可见格式。

textWebEditTextweb 表单中的文本。

textFilter         文本筛选格式。过滤

textPhonetic       拼音输入格式。

textWebEmailAddressweb表单中的邮件地址

textWebPasswordweb 表单中的密码

Number             数字格式。

numberSigned       有符号数。

numberDecimal      浮点数。

numberPassword     密码数字。

phone              拨号键盘

datetime            日期和时间键盘。

date               日期键盘。

time               时间键盘。