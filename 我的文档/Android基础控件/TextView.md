# Text

[TOC]

## TextView

> public class TextView extends View implements ViewTreeObserver.OnPreDrawListener

- 类的继承，TextView是一个神奇的类，它的重要性就像纸张在我们现实生活中的作用

java.lang.Object
   ↳	android.view.View
 	   ↳	android.widget.TextView

Known direct subclasses 

| [Button](https://developer.android.google.cn/reference/android/widget/Button.html) | A user interface element the user can tap or click to perform an action. |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [CheckedTextView](https://developer.android.google.cn/reference/android/widget/CheckedTextView.html) | An extension to `TextView` that supports the `Checkable` interface and displays. |
| [Chronometer](https://developer.android.google.cn/reference/android/widget/Chronometer.html) | Class that implements a simple timer.                        |
| [DigitalClock](https://developer.android.google.cn/reference/android/widget/DigitalClock.html) | *This class was deprecated in API level 17. It is recommended you use TextClock instead.* |
| [EditText](https://developer.android.google.cn/reference/android/widget/EditText.html) | A user interface element for entering and modifying text.    |
| [TextClock](https://developer.android.google.cn/reference/android/widget/TextClock.html) | `TextClock` can display the current date and/or time as a formatted string. |

Known indirect subclasses 

| [AutoCompleteTextView](https://developer.android.google.cn/reference/android/widget/AutoCompleteTextView.html) | An editable text view that shows completion suggestions automatically while the user is typing. |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [CheckBox](https://developer.android.google.cn/reference/android/widget/CheckBox.html) | A checkbox is a specific type of two-states button that can be either checked or unchecked. |
| [CompoundButton](https://developer.android.google.cn/reference/android/widget/CompoundButton.html) | A button with two states, checked and unchecked.             |
| [ExtractEditText](https://developer.android.google.cn/reference/android/inputmethodservice/ExtractEditText.html) | Specialization of `EditText` for showing and interacting with the extracted text in a full-screen input method. |
| [MultiAutoCompleteTextView](https://developer.android.google.cn/reference/android/widget/MultiAutoCompleteTextView.html) | An editable text view, extending `AutoCompleteTextView`, that can show completion suggestions for the substring of the text where the user is typing instead of necessarily for the entire thing. |
| [RadioButton](https://developer.android.google.cn/reference/android/widget/RadioButton.html) | A radio button is a two-states button that can be either checked or unchecked. |
| [Switch](https://developer.android.google.cn/reference/android/widget/Switch.html) | A Switch is a two-state toggle switch widget that can select between two options. |
| [ToggleButton](https://developer.android.google.cn/reference/android/widget/ToggleButton.html) | Displays checked/unchecked states as a button with a "light" indicator and by default accompanied with the text "ON" or "OFF". |

| Nested classes | 内部嵌套类（就是内部类）                                     |
| -------------- | ------------------------------------------------------------ |
| `enum`         | `TextView.BufferType`Type of the text buffer that defines the characteristics of the text such as static, styleable, or editable. |
| `interface`    | `TextView.OnEditorActionListener`Interface definition for a callback to be invoked when an action is performed on the editor. |
| `class`        | `TextView.SavedState`User interface state that is stored by TextView for implementing `View.onSaveInstanceState()`. |

## XML属性（属性值全部都可以通过方法来设置）

| XML attributes                                               | 当设置其中一些属性时，会使Text View变成可输入，即变成"EditText"。系统会提示使用相应控件 |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [`android:autoLink`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:autoLink) | Controls whether links such as urls and email addresses are automatically found and converted to clickable links.（ 控制是否自动查找网址和电子邮件地址等链接并将其转换为可点击链接 ） |
| [`android:autoSizeMaxTextSize`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:autoSizeMaxTextSize) | The maximum text size constraint to be used when auto-sizing text.（ 自动调整文本大小时要使用的最大文本大小约束。 要同时设置[`android:autoSizeTextType`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:autoSizeTextType)属性，26新属性） |
| [`android:autoSizeMinTextSize`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:autoSizeMinTextSize) | The minimum text size constraint to be used when auto-sizing text. |
| [`android:autoSizePresetSizes`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:autoSizePresetSizes) | Resource array of dimensions to be used in conjunction with `autoSizeTextType` set to `uniform`. |
| [`android:autoSizeStepGranularity`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:autoSizeStepGranularity) | Specify the auto-size step size if `autoSizeTextType` is set to `uniform`. |
| [`android:autoSizeTextType`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:autoSizeTextType) | Specify the type of auto-size.[AutoSizing](https://developer.android.google.cn/guide/topics/ui/look-and-feel/autosizing-textview)（自适应文本，26新属性，上面的几个autosize方法都属于这个新增的特性） |
| [`android:autoText`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:autoText) | If set, specifies that this TextView has a textual input method and automatically corrects some common spelling errors.（ 如果设置，则指定此TextView具有文本输入方法并自动更正一些常见的拼写错误。默认为“false” 。应该在EditText中使用,或者使用[`android:inputType`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:inputType)代替） |
| [`android:breakStrategy`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:breakStrategy) | Break strategy (control over paragraph layout).（控制段落布局，个人感觉没什么用处，也可能自己没有尝试出应该设定的值所带来的效果。23新增） |
| [`android:bufferType`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:bufferType) | Determines the minimum type that getText() will return.（主要用来反馈getText()方法， EditText and LogTextBox 只返回Editable) |
| [`android:capitalize`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:capitalize) | If set, specifies that this TextView has a textual input method and should automatically capitalize what the user types.（ 如果设置，则指定此TextView具有文本输入方法，并应自动将用户键入的内容大写。已经弃用，使用[`android:inputType`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:inputType)。Et中设置大写 。） |
| [`android:cursorVisible`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:cursorVisible) | Makes the cursor visible (the default) or invisible.（ 使光标可见（默认）或不可见 ） |
| [`android:digits`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:digits) | If set, specifies that this TextView has a numeric input method and that these specific characters are the ones that it will accept.（设置允许输入的字符，用于密码格式字符限定等） |
| [`android:drawableBottom`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:drawableBottom) | The drawable to be drawn below the text.（底部图片，指在文字的下方而不是背景） |
| [`android:drawableEnd`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:drawableEnd) | The drawable to be drawn to the end of the text.             |
| [`android:drawableLeft`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:drawableLeft) | The drawable to be drawn to the left of the text.            |
| [`android:drawablePadding`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:drawablePadding) | The padding between the drawables and the text.（ 图案和文本之间的填充，所有的上下左右都使用这一个。可以设置为负数） |
| [`android:drawableRight`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:drawableRight) | The drawable to be drawn to the right of the text.           |
| [`android:drawableStart`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:drawableStart) | The drawable to be drawn to the start of the text.           |
| [`android:drawableTint`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:drawableTint) | Tint to apply to the compound (left, top, etc.) drawables.（给绘制图案着色） |
| [`android:drawableTintMode`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:drawableTintMode) | Blending mode used to apply the compound (left, top, etc.) drawables tint.（着色和图案的混合模式） |
| [`android:drawableTop`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:drawableTop) | The drawable to be drawn above the text.                     |
| [`android:editable`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:editable) | If set, specifies that this TextView has an input method.（是否可编辑） |
| [`android:editorExtras`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:editorExtras) | Reference to an `<input-extras>` XML resource containing additional data to supply to an input method, which is private to the implementation of the input method.（引用以一个`<input-extras>` XML文件来提供额外的输入数据） |
| [`android:elegantTextHeight`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:elegantTextHeight) | Elegant text height, especially for less compacted complex script text.（此设置选择尚未压缩的字体变体以适合基于拉丁语的垂直度量标准，并且还会增加顶部和底部边界以提供更多空间 。这个不太常用，意思也不明确，没查到，大题猜测是对拉丁语文本高度的一个设置，21增加） |
| [`android:ellipsize`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:ellipsize) | If set, causes words that are longer than the view is wide to be ellipsized instead of broken in the middle.（当文字长度超过控件时，该如何显示。经常用来在文末显示省略号， marquee 是跑马灯效果，文字横向移动。 如果setMaxLines（int）用于设置两行或多行，则只支持END和MARQUEE（其他省略类型不会执行任何操作） ） |
| [`android:ems`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:ems) | Makes the TextView be exactly this many ems wide.（ em是一个印刷排版的单位，表示字宽的单位。 em字面意思为：equal M   （和M字符一致的宽度为一个单位）简称em 。是用来设置控件宽度的，用处不大） |
| [`android:fallbackLineSpacing`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:fallbackLineSpacing) | Whether to respect the ascent and descent of the fallback fonts that are used in displaying the text.（ 需要避免连续行中的文本相互碰撞 ，也就是说避免重叠。这些适用于一些特定的语言，更高更长的文字，如藏语。28增加，这里可以看出，谷歌一直在提升对世界上小语言的更多的适配和贴合） |
| [`android:firstBaselineToTopHeight`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:firstBaselineToTopHeight) | Distance from the top of the TextView to the first text baseline.（ 从TextView顶部到第一个文本基线的距离,设置会覆盖“上内距”的值。从这点来看，和“上内距”，应该差不多，只不过是28新增 ) |
| [`android:fontFamily`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:fontFamily) | Font family (named by string or as a font resource reference) for the text.（ 设置文本字体 ，将字体文件放到资源文件夹下的font文件夹下引入） |
| [`android:fontFeatureSettings`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:fontFeatureSettings) | Font feature settings.（ 字体功能设置。格式与CSS font-feature-settings属性相同：https：//www.w3.org/TR/css-fonts-3/#font-feature-settings-prop 。21新增） |
| [`android:freezesText`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:freezesText) | If set, the text view will include its current complete text inside of its frozen icicle in addition to meta-data such as the current cursor position.(保存当前的内容和状态，EditText不管值是真还是假，都会保存) |
| [`android:gravity`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:gravity) | Specifies how to align the text by the view's x- and/or y-axis when the text is smaller than the view. |
| [`android:height`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:height) | Makes the TextView be exactly this tall.                     |
| [`android:hint`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:hint) | Hint text to display when the text is empty.（ 提示文本为空时显示的文本 ，提示内容） |
| [`android:hyphenationFrequency`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:hyphenationFrequency) | Frequency of automatic hyphenation.（自动连字的频率，默认值是从主题设置的。聊天场景可以用到，具体不太懂什么意思。23新增） |
| [`android:imeActionId`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:imeActionId) | Supply a value for `EditorInfo.actionId` used when an input method is connected to the text view.（ 为输入法连接到文本视图时使用的EditorInfo.actionId提供值 。IME(Input Method Editor)输入法编辑器 ,对软键盘按键进行监听，实现操作。比如点击回车） |
| [`android:imeActionLabel`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:imeActionLabel) | Supply a value for `EditorInfo.actionLabel` used when an input method is connected to the text view. |
| [`android:imeOptions`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:imeOptions) | Additional features you can enable in an IME associated with an editor to improve the integration with your application.（设置et的动作类型，设置singleLine为true,设置inputType为Text） |
| [`android:includeFontPadding`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:includeFontPadding) | Leave enough room for ascenders and descenders instead of using the font ascent and descent strictly.(字体底部和顶部预留出足够的空间，而不是严格按照设定的字体的padding值) |
| [`android:inputMethod`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:inputMethod) | If set, specifies that this TextView should use the specified input method (specified by fully-qualified class name).（已经废弃，使用inputType） |
| [`android:inputType`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:inputType) | The type of data being placed in a text field, used to help an input method decide how to let the user enter text.（非常重要的属性，指定输入类型） |
| [`android:justificationMode`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:justificationMode) | Mode for justification.（适应的模式，只有inter_word,拉伸字间距。26新增，没有对应方法） |
| [`android:lastBaselineToBottomHeight`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:lastBaselineToBottomHeight) | Distance from the bottom of the TextView to the last text baseline.（设置会覆盖 paddingBottom.，28新增。） |
| [`android:letterSpacing`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:letterSpacing) | Text letter-spacing.( 设置文字字母间距。该值以“EM”为单位。 轻微膨胀的典型值为约0.05。 负值收紧文本 ，21新增) |
| [`android:lineHeight`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:lineHeight) | Explicit height between lines of text.（ 为此TextView设置显式行高。这相当于TextView中后续基线之间的垂直距离 ，28新增） |
| [`android:lineSpacingExtra`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:lineSpacingExtra) | Extra spacing between lines of text.（文本行间的额外间距，不包括最后一行） |
| [`android:lineSpacingMultiplier`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:lineSpacingMultiplier) | Extra spacing between lines of text, as a multiplier.（文本行间额外间距的乘机，百分比。先百分比改变，再加额外的像素值，应用到View中） |
| [`android:lines`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:lines) | Makes the TextView be exactly this many lines tall.（设置文本的行数，使整个View是些行的高度。 显示多行时，默认的光标位置是居中显示的，如想把光标定位在最上面的左边，需要设置android:gravity=”top” ） |
| [`android:linksClickable`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:linksClickable) | If set to false, keeps the movement method from being set to the link movement method even if autoLink causes links to be found.（设置链接是否可点击） |
| [`android:marqueeRepeatLimit`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:marqueeRepeatLimit) | The number of times to repeat the marquee animation.（[`android:ellipsize`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:ellipsize)值为“marquee”时使用， marquee_forever ，实现跑马灯效果） |
| [`android:maxEms`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:maxEms) | Makes the TextView be at most this many ems wide.（设置为最大的em个数宽度） |
| [`android:maxHeight`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:maxHeight) | Makes the TextView be at most this many pixels tall.         |
| [`android:maxLength`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:maxLength) | Set an input filter to constrain the text length to the specified number.（ 限制显示的文本长度，超出部分不显示 ） |
| [`android:maxLines`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:maxLines) | Makes the TextView be at most this many lines tall.（最大行数，超出行数不显示） |
| [`android:maxWidth`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:maxWidth) | Makes the TextView be at most this many pixels wide.         |
| [`android:minEms`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:minEms) | Makes the TextView be at least this many ems wide.           |
| [`android:minHeight`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:minHeight) | Makes the TextView be at least this many pixels tall.        |
| [`android:minLines`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:minLines) | Makes the TextView be at least this many lines tall.         |
| [`android:minWidth`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:minWidth) | Makes the TextView be at least this many pixels wide.        |
| [`android:numeric`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:numeric) | If set, specifies that this TextView has a numeric input method.（数字输入内容，限定输入的数字格式。已弃用，使用inputType） |
| [`android:password`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:password) | Whether the characters of the field are displayed as password dots instead of themselves. |
| [`android:phoneNumber`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:phoneNumber) | If set, specifies that this TextView has a phone number input method. |
| [`android:privateImeOptions`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:privateImeOptions) | An addition content type description to supply to the input method attached to the text view, which is private to the implementation of the input method.（不太懂，看名字，应还是和ime有关） |
| [`android:scrollHorizontally`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:scrollHorizontally) | Whether the text is allowed to be wider than the view (and therefore can be scrolled horizontally).（设置文本超出宽度的时候，下方是否有滚动条使其横向滚动） |
| [`android:selectAllOnFocus`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:selectAllOnFocus) | If the text is selectable, select it all when the view takes focus.（如果view设置可以选择，则在view获取焦点的时候，选中全部文本内容） |
| [`android:shadowColor`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:shadowColor) | Place a blurred shadow of text underneath the text, drawn with the specified color.（ 设置文本阴影的颜色， 需要与shadowRadius一起使用 。生成的文本阴影不与View上的属性交互，这些属性负责实时阴影， elevation 和translationZ 交互） |
| [`android:shadowDx`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:shadowDx) | Horizontal offset of the text shadow.（ 设置阴影横向坐标开始位置。即阴影横坐标的偏移 ） |
| [`android:shadowDy`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:shadowDy) | Vertical offset of the text shadow.（ 设置阴影纵向坐标开始位置。即阴影纵坐标的偏移 ） |
| [`android:shadowRadius`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:shadowRadius) | Blur radius of the text shadow.（ 设置阴影的半径。设置为0.1就变成字体的颜色了，一般设置为3.0的效果比较好。即扩散范围 ） |
| [`android:singleLine`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:singleLine) | Constrains the text to a single horizontally scrolling line instead of letting it wrap onto multiple lines, and advances focus instead of inserting a newline when you press the enter key.（ 对于不可编辑的文本，默认值为false（多行换行文本模式），但如果为inputType指定任何值，则默认值为true（单行输入字段模式）全局属性singleLine在API 3被弃用，maxLines更改静态文本的布局，并使用inputType属性中的textMultiLine标志代替可编辑文本视图（如果同时提供singleLine和inputType，则inputType标志将覆盖singleLine的值）） |
| [`android:text`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:text) | Text to display.                                             |
| [`android:textAllCaps`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:textAllCaps) | Present the text in ALL CAPS.                                |
| [`android:textAppearance`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:textAppearance) | Base text color, typeface, size, and style.                  |
| [`android:textColor`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:textColor) | Text color.                                                  |
| [`android:textColorHighlight`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:textColorHighlight) | Color of the text selection highlight.（ 设置用于显示选择突出显示的颜色 ） |
| [`android:textColorHint`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:textColorHint) | Color of the hint text.                                      |
| [`android:textColorLink`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:textColorLink) | Text color for links.（链接的文字颜色）                      |
| [`android:textIsSelectable`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:textIsSelectable) | Indicates that the content of a non-editable text can be selected.（设置文本是否可以选择，用于复制、粘贴等操作。EditText始终可以，和值无关） |
| [`android:textScaleX`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:textScaleX) | Sets the horizontal scaling factor for the text.（ 设置文字之间间隔，默认为1.0f。即文本的水平缩放系数 ） |
| [`android:textSize`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:textSize) | Size of the text.                                            |
| [`android:textStyle`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:textStyle) | Style (normal, bold, italic, bold\|italic) for the text.     |
| [`android:typeface`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:typeface) | Typeface (normal, sans, serif, monospace) for the text.      |
| [`android:width`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:width) | Makes the TextView be exactly this wide.                     |

*TextView的属性值很多，另外还有继承的父类View的属性。所以能实现的效果也很多，关键是每个属性之间的配合。因为很多事情TextView都定义好了，所有EditText本身就不用做什么，自身没有一定扩展属性*

- 额外的一些属性

  自定义文本选中时出现的复制箭头

  android:  textSelectHandleLeft
  android:  textSelectHandleRight
  android:  textSelectHandle
  自定义编辑文本的样式

  android:  textEditPasteWindowLayout
  android:  textEditNoPasteWindowLayout
  android:  textEditSidePasteWindowLayout
  android:  textEditSideNoPasteWindowLayout
  android:  textEditSuggestionItemLayout
  自定义编辑文本光标的样式

  android:  textCursorDrawable

## TextView新特性

### AutoSizing TextViews

> v4包支持，14及以上，26新特性。具体内容写在另一个文档里，关于基础控件的属性研究到此为止，转而着重研究实现效果。具体的属性，用到时搜索即可。



## 样式和主题

- **样式**

  是指为 `View` 或窗口指定外观和格式的属性集合。样式可以指定高度、填充、字体颜色、字号、背景色等许多属性。 样式是在与指定布局的 XML 不同的 XML 资源中进行定义。

  Android 中的样式与网页设计中层叠样式表的原理类似 — 您可以通过它将设计与内容分离。

*css对应样式，内容对应HTML。这样，对样式相关的修改都在一个*

- **主题**

  是指对整个 `Activity` 或应用而不是对单个 `View`（如上例所示）应用的样式。 以主题形式应用样式时，Activity 或应用中的每个视图都将应用其支持的每个样式属性。 例如，您可以 Activity 主题形式应用同一 `CodeFont` 样式，之后该 Activity 内的所有文本都将具有绿色固定宽度字体。 

*主题是整体的样式，定义样式中的属性，只要整个activity或者应用内支持的属性，都会使用定义样式中的属性值*

### 定义样式

要创建一组样式，请在您的项目的 `res/values/` 目录中保存一个 XML 文件。 **可任意指定该 XML 文件的名称**，但它必须使用 `.xml` 扩展名，并且必须保存在 `res/values/` 文件夹内。

该 XML 文件的根节点必须是 `<resources>`

### 继承

您可以通过 `<style>` 元素中的 `parent` 属性指定应作为您的样式所继承属性来源的样式。您可以利用它来继承现有样式的属性，然后只定义您想要更改或添加的属性。 您可以从自行创建的样式或平台内建的样式继承属性。 （如需了解有关从 Android 平台定义的样式继承属性的信息，请参阅下文的[使用平台样式和主题](#使用平台样式和主题)。） 例如，您可以继承 Android 平台的默认文本外观，然后对其进行修改：

```xml
 <style name="GreenText" parent="@android:style/TextAppearance">
        <item name="android:textColor">#00FF00</item>
    </style>
```

如果您想从自行定义的样式继承属性，则*不*必使用 `parent` 属性， 而是只需将您想继承的样式的名称以前缀形式添加到新样式的名称之中，并以句点进行分隔。 例如，要创建一个继承上文定义的 `CodeFont` 样式的新样式，但将颜色设置为红色，您可以按如下方式创建这个新样式：

```xml
    <style name="CodeFont.Red">
        <item name="android:textColor">#FF0000</item>
    </style>
```

### 样式属性

既然您已了解了样式是如何定义的，就需要了解什么类型的样式属性（由 `<item>` 元素定义）可以使用。您多半已经熟悉了其中的一些，例如 `layout_width` 和 `textColor`。 当然，还有许多其他样式属性可供您使用。

相应的类引用最便于查找适用于特定 `View` 的属性，其中列出了所有支持的 XML 属性。 例如，[TextView XML 属性](https://developer.android.google.cn/reference/android/widget/TextView.html#lattrs)表中所列的所有属性都可在 `TextView` 元素（或其其中一个子类）的样式定义中使用。 该引用中列出的其中一个属性是 [`android:inputType`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:inputType)，因此，如果您正常情况下会在 `<EditText>` 元素中放置 [`android:inputType`](https://developer.android.google.cn/reference/android/widget/TextView.html#attr_android:inputType) 属性，如下所示

**这个简单示例可能显得工作量更大，但如果您添加更多样式属性并将能够在各种地方重复使用样式这一因素考虑在内，就会发现回报可能很丰厚。**

*更好的理解这句话，就是根据情况，来选择使用哪种方式来设置样式。这种情况，在Android的设计中有很多体现，表达的最重要的意思就是，根据具体情况选择合适的。而不是，推荐的就是最好的*

如需查看所有可用样式属性的参考资料，请参阅 `R.attr` 参考资料。 切记，不是所有 View 对象都接受样式属性或者所定义的样式属性，因此正常情况下您应该引用所支持样式属性的具体 `View` 类。 不过，如果您应用样式的 View 不支持所有样式属性，该 View 将只应用那些受支持的属性，并直接忽略其他属性。

不过，某些样式属性任何 View 元素都不提供支持，只能以主题形式应用。 这些样式属性应用于整个窗口而非任何类型的 View。例如，主题的样式属性可以隐藏应用标题、隐藏状态栏或更改窗口的背景。 这些类型的样式属性不属于任何 View 对象。要发现这些仅主题样式属性，请在 `R.attr` 参考资料中查看有关以 `window` 开头的属性的内容。 例如，`windowNoTitle` 和 `windowBackground` 是只有在样式以主题形式应用于 Activity 或应用时才起作用的样式属性。 请参阅下文有关以主题形式应用样式的信息。

## 对 UI 应用样式和主题

设置样式的方法有两种：

- 如果是对单个视图应用样式，请为布局 XML 中的 View 元素添加 `style` 属性。
- 或者，如果是对整个 Activity 或应用来应用样式，请为 Android 清单中的 `<activity>` 或 `<application>` 元素添加 `android:theme` 属性。

当您对布局中的单个 `View` 应用样式时，该样式定义的属性只应用于该 `View`。 如果对 `ViewGroup` 应用样式，子 `View`元素将**不会**继承样式属性 — 只有被您直接应用样式的元素才会应用其属性。 不过，您*可以*通过以主题形式应用样式，使所应用的样式作用于所有 `View` 元素。

要以主题形式应用样式定义，您必须在 Android 清单中将样式应用于 `Activity` 或应用。 如果您这样做，Activity 或应用内的每个 `View` 都将应用其支持的每个属性。 例如，如果您对某个 Activity 应用前面示例中的 `CodeFont` 样式，则所有支持这些文本样式属性的 View 元素也会应用这些属性。 任何不支持这些属性的 View 都会忽略这些属性。 如果某个 View 仅支持部分属性，将只应用这些属性。

### 对视图应用样式

为 XML 布局中的视图设置样式的方法如下：

```
<TextView
    style="@style/CodeFont"
    android:text="@string/hello" />
```

现在该 TextView 将按照名为 `CodeFont` 的样式的定义设置样式（请参阅上文[定义样式](https://developer.android.google.cn/guide/topics/ui/themes#DefiningStyles)中的示例）。

**注：**`style` 属性*不*使用 `android:` 命名空间前缀。

### 对 Activity 或应用应用主题

要为您的应用的所有 Activity 设置主题，请打开 `AndroidManifest.xml` 文件并编辑 `<application>` 标记，在其中加入带样式名称的 `android:theme` 属性。 例如：

```
<application android:theme="@style/CustomTheme">
```

如果您只想对应用中的一个 Activity 应用主题，则改为给 `<activity>` 标记添加 `android:theme` 属性。

正如 Android 提供了其他内建资源一样，有许多预定义主题可供您使用，可免于自行编写。 例如，您可以使用 `Dialog` 主题，为您的 Activity 赋予类似对话框的外观：

```
<activity android:theme="@android:style/Theme.Dialog">
```

或者，如果您希望背景是透明的，则可使用 Translucent 主题：

```
<activity android:theme="@android:style/Theme.Translucent">
```

如果您喜欢某个主题，但想做些调整，只需将该主题添加为您的自定义主题的 `parent`。 例如，您可以像下面这样对传统明亮主题进行修改，使用您自己的颜色：

```
<color name="custom_theme_color">#b0b0ff</color>
<style name="CustomTheme" parent="android:Theme.Light">
    <item name="android:windowBackground">@color/custom_theme_color</item>
    <item name="android:colorBackground">@color/custom_theme_color</item>
</style>
```

（请注意，此处颜色需要以单独资源形式提供，因为 `android:windowBackground` 属性仅支持对另一资源的引用；不同于 `android:colorBackground`，无法为其提供颜色字面量。）

现在，在 Android 清单内使用 `CustomTheme` 替代 `Theme.Light`：

```
<activity android:theme="@style/CustomTheme">
```

### 根据平台版本选择主题

新版本的 Android 可为应用提供更多主题，您可能希望在这些平台上运行时可以使用这些新增主题，同时仍可兼容旧版本。 您可以通过自定义主题来实现这一目的，该主题根据平台版本利用资源选择在不同父主题之间切换。

例如，以下这个声明所对应的自定义主题就是标准的平台默认明亮主题。 它位于 `res/values` 之下的一个 XML 文件（通常是 `res/values/styles.xml`）中：

```
<style name="LightThemeSelector" parent="android:Theme.Light">
    ...
</style>
```

为了让该主题在应用运行在 Android 3.0（API 级别 11）或更高版本系统上时使用更新的全息主题，您可以在 `res/values-v11` 下的 XML 文件中加入一个替代主题声明，但将父主题设置为全息主题：

```
<style name="LightThemeSelector" parent="android:Theme.Holo.Light">
    ...
</style>
```

现在像您使用任何其他主题那样使用该主题，您的应用将在其运行于 Android 3.0 或更高版本的系统上时自动切换到全息主题。

`R.styleable.Theme` 提供了可在主题中使用的标准属性的列表。

如需了解有关根据平台版本或其他设备配置提供备用资源（例如主题和布局）的详细信息，请参阅[提供资源](https://developer.android.google.cn/guide/topics/resources/providing-resources.html)文档。

## 使用平台样式和主题

Android 平台提供了庞大的样式和主题集合，供您在应用中使用。 您可以在 `R.style` 类中找到所有可用样式的参考资料。 要使用此处所列样式，请将样式名称中的所有下划线替换为句点。 例如，您可以使用 `"@android:style/Theme.NoTitleBar"` 应用 `Theme_NoTitleBar` 主题。

不过，`R.style` 参考资料并不完备，未对样式做全面说明，因此查看这些样式和主题的实际源代码可让您更清楚地了解每个样式提供的样式属性。如需查看更详实的 Android 样式和主题参考资料，请参阅以下源代码：

- [Android 样式 (styles.xml)](https://android.googlesource.com/platform/frameworks/base/+/refs/heads/master/core/res/res/values/styles.xml)
- [Android 主题 (themes.xml)](https://android.googlesource.com/platform/frameworks/base/+/refs/heads/master/core/res/res/values/themes.xml)

这些文件有助于您通过示例进行学习。例如，在 Android 主题源代码中，您可以找到 `<style name="Theme.Dialog">`的声明。 在该定义中，您可以看到用来为 Android 框架使用的对话框设置样式的所有属性。

如需了解有关 XML 中样式和主题语法的详细信息，请参阅[样式资源](https://developer.android.google.cn/guide/topics/resources/style-resource.html)文档。

如需查看您可用来定义样式或主题的可用样式属性（例如“windowBackground”或“textAppearance”）的参考资料，请参阅 `R.attr` 或您创建的样式所对应的 View 类。

## 参考网站（考虑是否给网址添加说明）

[TextView官方API](https://developer.android.google.cn/reference/android/widget/TextView)

[API 25 (Android 7.1.1 API) widget.TextView——属性分析](https://blog.csdn.net/qqicq2001/article/details/53229119)

[AutoSizing](https://developer.android.google.cn/guide/topics/ui/look-and-feel/autosizing-textview)

[样式和主题](https://developer.android.google.cn/guide/topics/ui/themes)