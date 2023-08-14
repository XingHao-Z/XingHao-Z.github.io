---
title: （五）Markdown语法使用
date: 2023-08-04 21:20:28
tags:
 - markdown语法
categories:
 - hexo+NexT博客搭建
---

记录hexo+NexT特殊的语法。官方说明：[Tag Plugins](https://theme-next.js.org/docs/tag-plugins/)

<!--more-->

# 按钮 Button

**使用方法：**

```html
{% button url, text, icon [class], [title] %}
```

或者

```html
{% btn url, text, icon [class], [title] %}
```

- `url` : URL 的绝对或相对路径。
- `text` : 按钮文本。如果未指定图标`icon`，则为必填项。
- `icon` : Font Awesome 图标名称。如果未指定文本`text`，则为必填项。
- `[class]` : *可选参数。* Font Awesome 类： `fa-fw` | `fa-lg` | `fa-2x` | `fa-3x` | `fa-4x` | `fa-5x`
- `[title]` : *可选参数。*鼠标悬停时的工具提示。

**示例**

```
{% button #, 文本 %}
```

{% button #, 文本 %}

&emsp;

带text和title的按钮

```
{% btn #, 文本 %}{% btn #, Text & a,, 鼠标悬停显示内容 %}
```

{% btn #, 文本 %}{% btn #, Text & a,, 鼠标悬停显示内容 %}

```
{% btn #, 文本 %}     {% btn #, Text & b,, 注意这里两个逗号 %}
```

{% btn #, 文本 %}     {% btn #, Text & b,, 注意这里两个逗号 %}

```
{% btn #, 文本 %}
{% btn #, Text & c,, Title %}
```

{% btn #, 文本 %}
{% btn #, Text & c,, Title %}

&emsp;

带icon的按钮

```
{% btn #,, home fa-5x %}
{% btn #,, home fa-4x %}
{% btn #,, home fa-3x %}
{% btn #,, home fa-2x %}
{% btn #,, home fa-lg %}
{% btn #,, home fa-fw %}
{% btn #,, home %}
```

{% btn #,, home fa-5x %}
{% btn #,, home fa-4x %}
{% btn #,, home fa-3x %}
{% btn #,, home fa-2x %}
{% btn #,, home fa-lg %}
{% btn #,, home %}

```
{% btn #,, heading %}
{% btn #,, circle-notch %}
{% btn #,, times %}
{% btn #,, italic %}
{% btn #,, fab fa-scribd %}
{% btn #,, fab fa-edge %}
{% btn #,, fab fa-google %}
{% btn #,, fab fa-chrome %}
{% btn #,, fab fa-opera %}
{% btn #,, gem fa-rotate-270 %}
{% btn #,, arrow-left %}
{% btn #,, arrow-right %}
```

{% btn #,, heading %}
{% btn #,, circle-notch %}
{% btn #,, times %}
{% btn #,, italic %}
{% btn #,, fab fa-scribd %}
{% btn #,, fab fa-edge %}
{% btn #,, fab fa-google %}
{% btn #,, fab fa-chrome %}
{% btn #,, fab fa-opera %}
{% btn #,, gem fa-rotate-270 %}

&emsp;

带text和icon的按钮

```
{% btn #, 文本 & 图标 (buggy), home %}
{% btn #, 文本 & 图标 (fixed width), home fa-fw %}
```

{% btn #, 文本 & 图标 (buggy), home %}
{% btn #, 文本 & 图标 (fixed width), home fa-fw %}

```
{% btn #, Text & 大图标, home fa-fw fa-lg %}
{% btn #, Text & 大图标 & Title, home fa-fw fa-lg, Title %}
```

{% btn #, Text & 大图标, home fa-fw fa-lg %}
{% btn #, Text & 大图标 & Title, home fa-fw fa-lg, Title %}

&emsp;

段内的按钮

```
这是一个按钮 {% btn #, Lorem, home fa-fw fa-lg %} 被放到了文字中间
```

这是一个按钮 {% btn #, Lorem, home fa-fw fa-lg %} 被放到了文字中间

&emsp;

在其他tag内的按钮

```
{% note info %}
{% btn #, 在note内的按钮(note在下面介绍), home fa-fw %}

{% btn #,, home, Title %}{% btn #note, 点击转到note介绍 %}

[Link](#)
{% endnote %}
```

{% note info %}
{% btn #, 在note内的按钮(note在下面介绍), home fa-fw %}

{% btn #,, home, Title %}{% btn #note, 点击转到note介绍 %}

[Link](#)
{% endnote %}

&emsp;

按钮边距

```
<div class="text-center"><div>{% btn #,, heading %}{% btn #,, fab fa-edge %}{% btn #,, times %}{% btn #,, circle-notch %}</div>
<div>{% btn #,, italic %}{% btn #,, fab fa-scribd %}</div>
<div>{% btn #,, fab fa-google %}{% btn #,, fab fa-chrome %}{% btn #,, fab fa-opera %}{% btn #,, gem fa-rotate-270 %}</div></div>
```

上面这个官网给的示例不起作用（没有让按钮居中）

可以使用以下语法

```
<center>{% btn #,, heading %}{% btn #,, fab fa-edge %}{% btn #,, times %}{% btn #,, circle-notch %}</center>
<center>{% btn #,, italic %}{% btn #,, fab fa-scribd %}</center>
<center>{% btn #,, fab fa-google %}{% btn #,, fab fa-chrome %}{% btn #,, fab fa-opera %}{% btn #,, gem fa-rotate-270 %}</center>
```

<center>{% btn #,, heading %}{% btn #,, fab fa-edge %}{% btn #,, times %}{% btn #,, circle-notch %}</center>
<center>{% btn #,, italic %}{% btn #,, fab fa-scribd %}</center>
<center>{% btn #,, fab fa-google %}{% btn #,, fab fa-chrome %}{% btn #,, fab fa-opera %}{% btn #,, gem fa-rotate-270 %}</center>



&emsp;

带相对路径的按钮

```
{% btn /2023/07/27/hexo+NexT博客搭建/（四）插件安装和其他设置, 转到另一篇博客：（四）插件安装和其他设置, arrow-left fa-fw fa-lg %}
{% btn #label, 转到目录：Label, arrow-right fa-fw fa-lg, Label %}
```


{% btn /2023/07/27/hexo+NexT博客搭建/（四）插件安装和其他设置, 转到另一篇博客：（四）插件安装和其他设置, arrow-left fa-fw fa-lg %}

{% btn #label, 转到目录：Label, arrow-right fa-fw fa-lg, Label %}

&emsp;

带绝对路径的按钮

```
<center>{% btn https://github.com, GitHub, fab fa-github fa-fw fa-lg, GitHub %}</center>
```

<center>{% btn https://github.com, GitHub, fab fa-github fa-fw fa-lg, GitHub %}</center>



# 一组图片 Group Pictures

**使用方法：**

```
{% grouppicture [number]-[layout] %}
{% endgrouppicture %}
```

或

```
{% gp [number]-[layout] %}
{% endgp %}
```

- `[number]` : *可选参数。*要添加到组图片中的图片总数。

- `[layout]` : *可选参数。*布局的索引，可根据下图获得。例如，如果要将第二个布局应用于 4 张图片，请使用：

  ```
  {% grouppicture 4-2 %}
  {% endgrouppicture %}
  ```

  ![group-picture-1](group-picture-1.png)

**示例**

```
{% grouppicture 4-2 %}
![1](1.png)
![2](2.png)
![3](3.png)
![4](4.png)
{% endgrouppicture %}
```

{% grouppicture 4-2 %}

![1](1.png)

![2](2.png)

![3](3.png)

![4](4.png)

{% endgrouppicture %}

```
{% grouppicture 3-3 %}
![1](1.png)
![2](2.png)
![3](3.png)
{% endgrouppicture %}
```

{% grouppicture 3-3 %}

![1](1.png)
![2](2.png)
![3](3.png)

{% endgrouppicture %}



# 标签 Label

**使用方法：**

```
{% label [class]@text %}
```

- `[class]` :  *可选参数。* 支持的值：`default` | `primary` | `success` | `info` | `warning` | `danger`.
  如果未指定，将使用浏览器的默认样式，不同浏览器的默认样式可能不同。
- `text` : `@text` 可以指定带或不带空格
  E.g. `success @text` 和 `success@text`是一样的。

**示例**

```
Lorem {% label @标签1 %} {% label primary@标签 2 %} amet, consectetur {% label success@标签3 3, %} sed {% label info@标签4 4 %} tempor incididunt ut labore et dolore magna aliqua.

 *{% label warning @斜体 %}* 
 
 **{% label danger@加粗 %}** 
 
 ~~{% label default @划掉 %}~~ <mark>esse</mark> 
```

Lorem {% label @标签1 %} {% label primary@标签 2 %} amet, consectetur {% label success@标签3 3, %} sed {% label info@标签4 4 %} tempor incididunt ut labore et dolore magna aliqua.

 *{% label warning @斜体 %}* 

 **{% label danger@加粗 %}** 

 ~~{% label default @划掉 %}~~ <mark>esse</mark> 

# 链接网格 Link Grid

**使用方法**

```
{% linkgrid [image] [delimiter] [comment] %}
{% endlinkgrid %}
```

或

```
{% lg [image] [delimiter] [comment] %}
{% endlg %}
```

- `[image]` : *可选参数。* 默认图像 URL。
- `[delimiter]` : *可选参数。* 如果给出了可选的分隔符参数delimiter，它将被解释为每行中项目的分隔符。
- `[comment]` : *可选参数。* 如果给出了可选的注释参数comment，它将被解释为注释掉一行的符号。

**示例**

```
{% linkgrid %}
链接1 | https://xinghao-z.github.io/ | 星颢Z的博客 | /images/HeadPortrait.png
Theme NexT | https://theme-next.js.org/ | Stay Simple. Stay NexT. | /images/apple-touch-icon-next.png
链接2 | https://theme-next.js.org/ | Stay Simple. Stay NexT. | /images/apple-touch-icon-next.png
Theme NexT | https://theme-next.js.org/ | Stay Simple. Stay NexT. | /images/apple-touch-icon-next.png
% Theme NexT | https://theme-next.js.org/ | Stay Simple. Stay NexT. | /images/apple-touch-icon-next.png  这一行被注释了
{% endlinkgrid %}
```

{% linkgrid %}
链接1 | https://xinghao-z.github.io/ | 星颢Z的博客 | /images/HeadPortrait.png
Theme NexT | https://theme-next.js.org/ | Stay Simple. Stay NexT. | /images/apple-touch-icon-next.png
链接2 | https://theme-next.js.org/ | Stay Simple. Stay NexT. | /images/apple-touch-icon-next.png
Theme NexT | https://theme-next.js.org/ | Stay Simple. Stay NexT. | /images/apple-touch-icon-next.png
% Theme NexT | https://theme-next.js.org/ | Stay Simple. Stay NexT. | /images/apple-touch-icon-next.png  这一行被注释了
{% endlinkgrid %}



```
{% lg /images/apple-touch-icon-next.png , %}
Theme NexT , https://theme-next.js.org/ , Stay Simple. Stay NexT. , /images/apple-touch-icon-next.png
Theme NexT , https://theme-next.js.org/ , Stay Simple. Stay NexT. , /images/apple-touch-icon-next.png
Theme NexT , https://theme-next.js.org/ , Stay Simple. Stay NexT. , /images/apple-touch-icon-next.png
% Theme NexT , https://theme-next.js.org/ , Stay Simple. Stay NexT. , /images/apple-touch-icon-next.png
{% endlg %}
```

{% lg /images/apple-touch-icon-next.png , %}
Theme NexT , https://theme-next.js.org/ , Stay Simple. Stay NexT. , /images/apple-touch-icon-next.png
Theme NexT , https://theme-next.js.org/ , Stay Simple. Stay NexT. , /images/apple-touch-icon-next.png
Theme NexT , https://theme-next.js.org/ , Stay Simple. Stay NexT. , /images/apple-touch-icon-next.png
% Theme NexT , https://theme-next.js.org/ , Stay Simple. Stay NexT. , /images/apple-touch-icon-next.png
{% endlg %}



我不喜欢鼠标放上去抖动的效果，在自定义配置文件`styles.styl`中加了：

```stylus
//链接网格取消动画
.link-grid .link-grid-container {
  transform: none !important;
}
```

# 注释 note

**设置**

```yaml
#主题配置文件
note:
  # Note tag style values:
  #  - simple    bs-callout old alert style. Default.
  #  - modern    bs-callout new (v2-v3) alert style.
  #  - flat      flat callout style with background, like on Mozilla or StackOverflow.
  #  - disabled  disable all CSS styles import of note tag.
  style: flat
  icons: true
  # Offset lighter of background in % for modern and flat styles (modern: -12 | 12; flat: -18 | 6).
  # Offset also applied to label tag variables. This option can work with disabled note tag.
  light_bg_offset: 0
```

使用

```
{% note [class] [no-icon] [summary] %}
Any content (support inline tags too).
{% endnote %}
```

- `[class]` : *可选参数。* 支持的选项： default | primary | success | info | warning | danger.
- `[no-icon]` : *可选参数。* 在注释中进制图标
- `[summary]` : *可选参数。* 可选的注释摘要。

**示例**

```
{% note %}
## Header
(没有定义class样式)
{% endnote %}
```

{% note %}

## Header

(没有定义class样式)
{% endnote %}

```
{% note default %}
默认class参数
Welcome to [Hexo!](https://hexo.io)
{% endnote %}
```

{% note default %}
默认class参数

Welcome to [Hexo!](https://hexo.io)https://hexo.io)
{% endnote %}

```
{% note primary %}
Primary Header
**Welcome** to [Hexo!](https://hexo.io)
{% endnote %}
```

{% note primary %}
Primary Header

**Welcome** to [Hexo!](https://hexo.io)https://hexo.io)
{% endnote %}

```
{% note info %}
Info Header
**Welcome** to [Hexo!](https://hexo.io)
{% endnote %}
```

{% note info %}
Info Header

**Welcome** to [Hexo!](https://hexo.io)
{% endnote %}

```
{% note success %}
Success Header
**Welcome** to [Hexo!](https://hexo.io)
{% endnote %}
```

{% note success %}
Success Header

**Welcome** to [Hexo!](https://hexo.io)
{% endnote %}

```
{% note warning %}
Warning Header
**Welcome** to [Hexo!](https://hexo.io)
{% endnote %}
```

{% note warning %}
Warning Header

**Welcome** to [Hexo!](https://hexo.io)
{% endnote %}

```
{% note danger %}
Danger Header
**Welcome** to [Hexo!](https://hexo.io)
{% endnote %}
```

{% note danger %}

Danger Header

**Welcome** to [Hexo!](https://hexo.io)
{% endnote %}

```
{% note info no-icon %}
No icon note
Note **without** icon: `note info no-icon`
{% endnote %}
```

{% note info no-icon %}

No icon note
Note **without** icon: `note info no-icon`
{% endnote %}

```
{% note primary This is a summary %}
Details and summary
Note with summary: `note primary This is a summary`
{% endnote %}
```

{% note primary This is a summary %}
Details and summary
Note with summary: `note primary This is a summary`
{% endnote %}

```
{% note info no-icon This is a summary %}
Details and summary (No icon)
Note with summary: `note info no-icon This is a summary`
{% endnote %}
```

{% note info no-icon This is a summary %}
Details and summary (No icon)
Note with summary: `note info no-icon This is a summary`
{% endnote %}

````
{% note success %}
Codeblock in note

```
code block in note tag
code block in note tag
code block in note tag
```
{% endnote %}
````

{% note success %}

Codeblock in note

```
code block in note tag
code block in note tag
code block in note tag
```
{% endnote %}



# 选项卡 Tabs

**设置**

```yaml
#主题配置文件
tabs:
  # Make the nav bar of tabs with long content stick to the top.
  sticky: false
  transition:
    tabs: false
    labels: true
```

**使用**

```
{% tabs Unique name, [index] %}
<!-- tab [Tab caption] [@icon] -->
Any content (support inline tags too).
<!-- endtab -->
{% endtabs %}
```

- `Unique name` : 标签块标签的唯一名称，不含逗号。该名称将在 #id 中使用，作为每个标签页的前缀和索引号。如果名称中有空格，生成 #id 时将用破折号替换所有空格。Only for current url of post/page must be unique!
- `[index]` : *可选参数。*活动选项卡的索引号。如果未指定，将选择第一个选项卡（1）。如果索引为-1，则不会选择任何标签页。它将类似于spoiler。
- `[Tab caption]` : *可选参数。*当前选项卡的标题。如果未指定标题，带有标签页索引后缀的唯一名称将用作标签页的标题。如果未指定标题，但指定了图标，标题将为空。
- `[@icon]` : *可选参数。*Font Awesome 图标名称。可指定有空格或无空格；例如，"Tab caption @icon "与 "Tab caption@icon "相同。

**示例**

```
{% tabs First unique name %}
<!-- tab -->
**This is Tab 1.**
<!-- endtab -->

<!-- tab -->
**This is Tab 2.**
<!-- endtab -->

<!-- tab -->
**This is Tab 3.**
<!-- endtab -->
{% endtabs %}
```

{% tabs First unique name %}

<!-- tab -->

**This is Tab 1.**

<!-- endtab -->

<!-- tab -->

**This is Tab 2.**

<!-- endtab -->

<!-- tab -->

**This is Tab 3.**

<!-- endtab -->

{% endtabs %}



默认展示第三个选项卡

```
{% tabs Second unique name, 3 %}
<!-- tab -->
**This is Tab 1.**
<!-- endtab -->

<!-- tab -->
**This is Tab 2.**
<!-- endtab -->

<!-- tab -->
**This is Tab 3.**
<!-- endtab -->
{% endtabs %}
```

{% tabs Second unique name, 3 %}
<!-- tab -->
**This is Tab 1.**
<!-- endtab -->

<!-- tab -->
**This is Tab 2.**
<!-- endtab -->

<!-- tab -->
**This is Tab 3.**
<!-- endtab -->
{% endtabs %}

带有自定义标签的选项卡

```
{% tabs Fourth unique name %}
<!-- tab Solution 1 -->
**This is Tab 1.**
<!-- endtab -->

<!-- tab Solution 2 -->
**This is Tab 2.**
<!-- endtab -->

<!-- tab Solution 3 -->
**This is Tab 3.**
<!-- endtab -->
{% endtabs %}
```

{% tabs Fourth unique name %}
<!-- tab Solution 1 -->
**This is Tab 1.**
<!-- endtab -->

<!-- tab 解决 2 -->
**This is Tab 2.**
<!-- endtab -->

<!-- tab 方法 3 -->
**This is Tab 3.**
<!-- endtab -->
{% endtabs %}

仅带有图标的选项卡

```
{% tabs Fifth unique name %}
<!-- tab @text-width -->
**This is Tab 1.**
<!-- endtab -->

<!-- tab @font -->
**This is Tab 2.**
<!-- endtab -->

<!-- tab @bold -->
**This is Tab 3.**
<!-- endtab -->
{% endtabs %}
```

{% tabs Fifth unique name %}
<!-- tab @text-width -->
**This is Tab 1.**
<!-- endtab -->

<!-- tab @font -->
**This is Tab 2.**
<!-- endtab -->

<!-- tab @bold -->
**This is Tab 3.**
<!-- endtab -->
{% endtabs %}

选项卡里能嵌套选项卡。也能嵌套其他内容，如注释、标签等

```
{% tabs Tags %}
<!-- tab -->
**This is Tab 1.**

1. One
2. Two
3. Three

Indented code block:

    nano /etc

Tagged code block:

{% code %}
code tag
code tag
code tag
{% endcode %}

{% note default %}
Note default tag.
{% endnote %}
<!-- endtab -->

<!-- tab -->
**This is Tab 2.**

* Five
* Six
* Seven

{% note primary %}
{% youtube Kt7u5kr_P5o %}
{% endnote %}
<!-- endtab -->

<!-- tab -->
**This is Tab 3.**

{% subtabs Sub Tabs %}
<!-- tab -->
**This is Sub Tab 1.**
{% note success %}
Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Phasellus hendrerit. Pellentesque aliquet nibh nec urna. In nisi neque, aliquet vel, dapibus id, mattis vel, nisi. Sed pretium, ligula sollicitudin laoreet viverra, tortor libero sodales leo, eget blandit nunc tortor eu nibh. Nullam mollis. Ut justo. Suspendisse potenti. Pellentesque fermentum dolor. Aliquam quam lectus, facilisis auctor, ultrices ut, elementum vulputate, nunc.

{% note warning %}
Sed egestas, ante et vulputate volutpat, eros pede semper est, vitae luctus metus libero eu augue. Morbi purus libero, faucibus adipiscing, commodo quis, gravida id, est. Sed lectus. Praesent elementum hendrerit tortor. Sed semper lorem at felis. Vestibulum volutpat, lacus a ultrices sagittis, mi neque euismod dui, eu pulvinar nunc sapien ornare nisl. Phasellus pede arcu, dapibus eu, fermentum et, dapibus sed, urna.
{% endnote %}

Morbi interdum mollis sapien. Sed ac risus. Phasellus lacinia, magna a ullamcorper laoreet, lectus arcu pulvinar risus, vitae facilisis libero dolor a purus. Sed vel lacus. Mauris nibh felis, adipiscing varius, adipiscing in, lacinia vel, tellus. Suspendisse ac urna. Etiam pellentesque mauris ut lectus. Nunc tellus ante, mattis eget, gravida vitae, ultricies ac, leo. Integer leo pede, ornare a, lacinia eu, vulputate vel, nisl.
{% endnote %}
<!-- endtab -->

<!-- tab -->
**This is Sub Tab 2.**
{% note success %}
Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Phasellus hendrerit. Pellentesque aliquet nibh nec urna. In nisi neque, aliquet vel, dapibus id, mattis vel, nisi. Sed pretium, ligula sollicitudin laoreet viverra, tortor libero sodales leo, eget blandit nunc tortor eu nibh. Nullam mollis. Ut justo. Suspendisse potenti. Pellentesque fermentum dolor. Aliquam quam lectus, facilisis auctor, ultrices ut, elementum vulputate, nunc.

Sed egestas, ante et vulputate volutpat, eros pede semper est, vitae luctus metus libero eu augue. Morbi purus libero, faucibus adipiscing, commodo quis, gravida id, est. Sed lectus. Praesent elementum hendrerit tortor. Sed semper lorem at felis. Vestibulum volutpat, lacus a ultrices sagittis, mi neque euismod dui, eu pulvinar nunc sapien ornare nisl. Phasellus pede arcu, dapibus eu, fermentum et, dapibus sed, urna.

{% note danger %}
Morbi interdum mollis sapien. Sed ac risus. Phasellus lacinia, magna a ullamcorper laoreet, lectus arcu pulvinar risus, vitae facilisis libero dolor a purus. Sed vel lacus. Mauris nibh felis, adipiscing varius, adipiscing in, lacinia vel, tellus. Suspendisse ac urna. Etiam pellentesque mauris ut lectus. Nunc tellus ante, mattis eget, gravida vitae, ultricies ac, leo. Integer leo pede, ornare a, lacinia eu, vulputate vel, nisl.
{% endnote %}
{% endnote %}
<!-- endtab -->

<!-- tab -->
**This is Sub Tab 3.**

{% subtabs Sub-Sub Tabs %}
<!-- tab -->
**This is Sub-Sub Tab 1 of Sub Tab 3.**
{% note success %}
Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Phasellus hendrerit. Pellentesque aliquet nibh nec urna. In nisi neque, aliquet vel, dapibus id, mattis vel, nisi. Sed pretium, ligula sollicitudin laoreet viverra, tortor libero sodales leo, eget blandit nunc tortor eu nibh. Nullam mollis. Ut justo. Suspendisse potenti. Pellentesque fermentum dolor. Aliquam quam lectus, facilisis auctor, ultrices ut, elementum vulputate, nunc.

Sed egestas, ante et vulputate volutpat, eros pede semper est, vitae luctus metus libero eu augue. Morbi purus libero, faucibus adipiscing, commodo quis, gravida id, est. Sed lectus. Praesent elementum hendrerit tortor. Sed semper lorem at felis. Vestibulum volutpat, lacus a ultrices sagittis, mi neque euismod dui, eu pulvinar nunc sapien ornare nisl. Phasellus pede arcu, dapibus eu, fermentum et, dapibus sed, urna.

Morbi interdum mollis sapien. Sed ac risus. Phasellus lacinia, magna a ullamcorper laoreet, lectus arcu pulvinar risus, vitae facilisis libero dolor a purus. Sed vel lacus. Mauris nibh felis, adipiscing varius, adipiscing in, lacinia vel, tellus. Suspendisse ac urna. Etiam pellentesque mauris ut lectus. Nunc tellus ante, mattis eget, gravida vitae, ultricies ac, leo. Integer leo pede, ornare a, lacinia eu, vulputate vel, nisl.
{% endnote %}
<!-- endtab -->

<!-- tab -->
**This is Sub-Sub Tab 2 of Sub Tab 3.**
{% note success %}
Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Phasellus hendrerit. Pellentesque aliquet nibh nec urna. In nisi neque, aliquet vel, dapibus id, mattis vel, nisi. Sed pretium, ligula sollicitudin laoreet viverra, tortor libero sodales leo, eget blandit nunc tortor eu nibh. Nullam mollis. Ut justo. Suspendisse potenti. Pellentesque fermentum dolor. Aliquam quam lectus, facilisis auctor, ultrices ut, elementum vulputate, nunc.

{% note warning %}
Sed egestas, ante et vulputate volutpat, eros pede semper est, vitae luctus metus libero eu augue. Morbi purus libero, faucibus adipiscing, commodo quis, gravida id, est. Sed lectus. Praesent elementum hendrerit tortor. Sed semper lorem at felis. Vestibulum volutpat, lacus a ultrices sagittis, mi neque euismod dui, eu pulvinar nunc sapien ornare nisl. Phasellus pede arcu, dapibus eu, fermentum et, dapibus sed, urna.

Morbi interdum mollis sapien. Sed ac risus. Phasellus lacinia, magna a ullamcorper laoreet, lectus arcu pulvinar risus, vitae facilisis libero dolor a purus. Sed vel lacus. Mauris nibh felis, adipiscing varius, adipiscing in, lacinia vel, tellus. Suspendisse ac urna. Etiam pellentesque mauris ut lectus. Nunc tellus ante, mattis eget, gravida vitae, ultricies ac, leo. Integer leo pede, ornare a, lacinia eu, vulputate vel, nisl.
{% endnote %}

{% endnote %}
<!-- endtab -->

<!-- tab -->
**This is Sub-Sub Tab 3 of Sub Tab 3.**

{% note success %}
Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Phasellus hendrerit. Pellentesque aliquet nibh nec urna. In nisi neque, aliquet vel, dapibus id, mattis vel, nisi. Sed pretium, ligula sollicitudin laoreet viverra, tortor libero sodales leo, eget blandit nunc tortor eu nibh. Nullam mollis. Ut justo. Suspendisse potenti. Pellentesque fermentum dolor. Aliquam quam lectus, facilisis auctor, ultrices ut, elementum vulputate, nunc.

{% note warning %}
Sed egestas, ante et vulputate volutpat, eros pede semper est, vitae luctus metus libero eu augue. Morbi purus libero, faucibus adipiscing, commodo quis, gravida id, est. Sed lectus. Praesent elementum hendrerit tortor. Sed semper lorem at felis. Vestibulum volutpat, lacus a ultrices sagittis, mi neque euismod dui, eu pulvinar nunc sapien ornare nisl. Phasellus pede arcu, dapibus eu, fermentum et, dapibus sed, urna.

{% note danger %}
Morbi interdum mollis sapien. Sed ac risus. Phasellus lacinia, magna a ullamcorper laoreet, lectus arcu pulvinar risus, vitae facilisis libero dolor a purus. Sed vel lacus. Mauris nibh felis, adipiscing varius, adipiscing in, lacinia vel, tellus. Suspendisse ac urna. Etiam pellentesque mauris ut lectus. Nunc tellus ante, mattis eget, gravida vitae, ultricies ac, leo. Integer leo pede, ornare a, lacinia eu, vulputate vel, nisl.
{% endnote %}

{% endnote %}

{% endnote %}
<!-- endtab -->
{% endsubtabs %}

<!-- endtab -->
{% endsubtabs %}

<!-- endtab -->
{% endtabs %}
```

{% tabs Tags %}
<!-- tab -->
**This is Tab 1.**

1. One
2. Two
3. Three

Indented code block:

    nano /etc

Tagged code block:

{% code %}
code tag
code tag
code tag
{% endcode %}

{% note default %}
Note default tag.
{% endnote %}
<!-- endtab -->

<!-- tab -->
**This is Tab 2.**

* Five
* Six
* Seven

{% note primary %}
{% youtube Kt7u5kr_P5o %}
{% endnote %}
<!-- endtab -->

<!-- tab -->
**This is Tab 3.**

{% subtabs Sub Tabs %}
<!-- tab -->
**This is Sub Tab 1.**
{% note success %}
Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Phasellus hendrerit. Pellentesque aliquet nibh nec urna. In nisi neque, aliquet vel, dapibus id, mattis vel, nisi. Sed pretium, ligula sollicitudin laoreet viverra, tortor libero sodales leo, eget blandit nunc tortor eu nibh. Nullam mollis. Ut justo. Suspendisse potenti. Pellentesque fermentum dolor. Aliquam quam lectus, facilisis auctor, ultrices ut, elementum vulputate, nunc.

{% note warning %}
Sed egestas, ante et vulputate volutpat, eros pede semper est, vitae luctus metus libero eu augue. Morbi purus libero, faucibus adipiscing, commodo quis, gravida id, est. Sed lectus. Praesent elementum hendrerit tortor. Sed semper lorem at felis. Vestibulum volutpat, lacus a ultrices sagittis, mi neque euismod dui, eu pulvinar nunc sapien ornare nisl. Phasellus pede arcu, dapibus eu, fermentum et, dapibus sed, urna.
{% endnote %}

Morbi interdum mollis sapien. Sed ac risus. Phasellus lacinia, magna a ullamcorper laoreet, lectus arcu pulvinar risus, vitae facilisis libero dolor a purus. Sed vel lacus. Mauris nibh felis, adipiscing varius, adipiscing in, lacinia vel, tellus. Suspendisse ac urna. Etiam pellentesque mauris ut lectus. Nunc tellus ante, mattis eget, gravida vitae, ultricies ac, leo. Integer leo pede, ornare a, lacinia eu, vulputate vel, nisl.
{% endnote %}
<!-- endtab -->

<!-- tab -->
**This is Sub Tab 2.**
{% note success %}
Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Phasellus hendrerit. Pellentesque aliquet nibh nec urna. In nisi neque, aliquet vel, dapibus id, mattis vel, nisi. Sed pretium, ligula sollicitudin laoreet viverra, tortor libero sodales leo, eget blandit nunc tortor eu nibh. Nullam mollis. Ut justo. Suspendisse potenti. Pellentesque fermentum dolor. Aliquam quam lectus, facilisis auctor, ultrices ut, elementum vulputate, nunc.

Sed egestas, ante et vulputate volutpat, eros pede semper est, vitae luctus metus libero eu augue. Morbi purus libero, faucibus adipiscing, commodo quis, gravida id, est. Sed lectus. Praesent elementum hendrerit tortor. Sed semper lorem at felis. Vestibulum volutpat, lacus a ultrices sagittis, mi neque euismod dui, eu pulvinar nunc sapien ornare nisl. Phasellus pede arcu, dapibus eu, fermentum et, dapibus sed, urna.

{% note danger %}
Morbi interdum mollis sapien. Sed ac risus. Phasellus lacinia, magna a ullamcorper laoreet, lectus arcu pulvinar risus, vitae facilisis libero dolor a purus. Sed vel lacus. Mauris nibh felis, adipiscing varius, adipiscing in, lacinia vel, tellus. Suspendisse ac urna. Etiam pellentesque mauris ut lectus. Nunc tellus ante, mattis eget, gravida vitae, ultricies ac, leo. Integer leo pede, ornare a, lacinia eu, vulputate vel, nisl.
{% endnote %}
{% endnote %}
<!-- endtab -->

<!-- tab -->
**This is Sub Tab 3.**

{% subtabs Sub-Sub Tabs %}
<!-- tab -->
**This is Sub-Sub Tab 1 of Sub Tab 3.**
{% note success %}
Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Phasellus hendrerit. Pellentesque aliquet nibh nec urna. In nisi neque, aliquet vel, dapibus id, mattis vel, nisi. Sed pretium, ligula sollicitudin laoreet viverra, tortor libero sodales leo, eget blandit nunc tortor eu nibh. Nullam mollis. Ut justo. Suspendisse potenti. Pellentesque fermentum dolor. Aliquam quam lectus, facilisis auctor, ultrices ut, elementum vulputate, nunc.

Sed egestas, ante et vulputate volutpat, eros pede semper est, vitae luctus metus libero eu augue. Morbi purus libero, faucibus adipiscing, commodo quis, gravida id, est. Sed lectus. Praesent elementum hendrerit tortor. Sed semper lorem at felis. Vestibulum volutpat, lacus a ultrices sagittis, mi neque euismod dui, eu pulvinar nunc sapien ornare nisl. Phasellus pede arcu, dapibus eu, fermentum et, dapibus sed, urna.

Morbi interdum mollis sapien. Sed ac risus. Phasellus lacinia, magna a ullamcorper laoreet, lectus arcu pulvinar risus, vitae facilisis libero dolor a purus. Sed vel lacus. Mauris nibh felis, adipiscing varius, adipiscing in, lacinia vel, tellus. Suspendisse ac urna. Etiam pellentesque mauris ut lectus. Nunc tellus ante, mattis eget, gravida vitae, ultricies ac, leo. Integer leo pede, ornare a, lacinia eu, vulputate vel, nisl.
{% endnote %}
<!-- endtab -->

<!-- tab -->
**This is Sub-Sub Tab 2 of Sub Tab 3.**
{% note success %}
Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Phasellus hendrerit. Pellentesque aliquet nibh nec urna. In nisi neque, aliquet vel, dapibus id, mattis vel, nisi. Sed pretium, ligula sollicitudin laoreet viverra, tortor libero sodales leo, eget blandit nunc tortor eu nibh. Nullam mollis. Ut justo. Suspendisse potenti. Pellentesque fermentum dolor. Aliquam quam lectus, facilisis auctor, ultrices ut, elementum vulputate, nunc.

{% note warning %}
Sed egestas, ante et vulputate volutpat, eros pede semper est, vitae luctus metus libero eu augue. Morbi purus libero, faucibus adipiscing, commodo quis, gravida id, est. Sed lectus. Praesent elementum hendrerit tortor. Sed semper lorem at felis. Vestibulum volutpat, lacus a ultrices sagittis, mi neque euismod dui, eu pulvinar nunc sapien ornare nisl. Phasellus pede arcu, dapibus eu, fermentum et, dapibus sed, urna.

Morbi interdum mollis sapien. Sed ac risus. Phasellus lacinia, magna a ullamcorper laoreet, lectus arcu pulvinar risus, vitae facilisis libero dolor a purus. Sed vel lacus. Mauris nibh felis, adipiscing varius, adipiscing in, lacinia vel, tellus. Suspendisse ac urna. Etiam pellentesque mauris ut lectus. Nunc tellus ante, mattis eget, gravida vitae, ultricies ac, leo. Integer leo pede, ornare a, lacinia eu, vulputate vel, nisl.
{% endnote %}

{% endnote %}
<!-- endtab -->

<!-- tab -->
**This is Sub-Sub Tab 3 of Sub Tab 3.**

{% note success %}
Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Phasellus hendrerit. Pellentesque aliquet nibh nec urna. In nisi neque, aliquet vel, dapibus id, mattis vel, nisi. Sed pretium, ligula sollicitudin laoreet viverra, tortor libero sodales leo, eget blandit nunc tortor eu nibh. Nullam mollis. Ut justo. Suspendisse potenti. Pellentesque fermentum dolor. Aliquam quam lectus, facilisis auctor, ultrices ut, elementum vulputate, nunc.

{% note warning %}
Sed egestas, ante et vulputate volutpat, eros pede semper est, vitae luctus metus libero eu augue. Morbi purus libero, faucibus adipiscing, commodo quis, gravida id, est. Sed lectus. Praesent elementum hendrerit tortor. Sed semper lorem at felis. Vestibulum volutpat, lacus a ultrices sagittis, mi neque euismod dui, eu pulvinar nunc sapien ornare nisl. Phasellus pede arcu, dapibus eu, fermentum et, dapibus sed, urna.

{% note danger %}
Morbi interdum mollis sapien. Sed ac risus. Phasellus lacinia, magna a ullamcorper laoreet, lectus arcu pulvinar risus, vitae facilisis libero dolor a purus. Sed vel lacus. Mauris nibh felis, adipiscing varius, adipiscing in, lacinia vel, tellus. Suspendisse ac urna. Etiam pellentesque mauris ut lectus. Nunc tellus ante, mattis eget, gravida vitae, ultricies ac, leo. Integer leo pede, ornare a, lacinia eu, vulputate vel, nisl.
{% endnote %}

{% endnote %}

{% endnote %}
<!-- endtab -->
{% endsubtabs %}

<!-- endtab -->
{% endsubtabs %}

<!-- endtab -->
{% endtabs %}

