---
title: （二）hexo+NexT主题配置
date: 2023-07-25 12:45:04
tags:
 - hexo
 - 博客
categories:
 - hexo博客搭建
description: 介绍怎么通过修改站点配置文件、主题配置文件和自定义配置文件来配置博客。
typora-root-url: （二）hexo-NexT主题配置
---

<mark>23.10.15：主题更换为butterfly，但本文hexo基本配置部分是通用的</mark>

# 1、前言

网上许多hexo+NexT主题配置教程是2020年前的，但这些年hexo和NexT主题已经更新了许多版本，这些教程已经过时，部分操作已经无法实现。

可以打开在`站点根目录`打开`git bash`，输入`hexo -v`查看版本，我这里的版本为6.3.0。NexT在主题根目录下的`package.json`中查看，我的版本为8.17.1

其实最好的教程就是官方文档，小伙伴可以参考[hexo官方文档](https://hexo.io/zh-cn/docs/) 和 [NexT官方文档](https://theme-next.js.org/) ，有时相比在网上找到一堆过时的教程，效率更高。

当然，根据本教程也能实现我的配置，但还想自定义的小伙伴就要自己再折腾下了。我也是从慢慢折腾过来的，开始什么也不懂。我也会介绍我配置中学到的一些东西，并简单教一下我是怎么自定义配置的，如果有错误的话，欢迎在评论区指正。

推荐下我找到的比较好的教程：

[Hexo+NexT 打造一个炫酷博客](https://sun_xy.gitee.io/blog/2018/10/16/hexo_next_blog/)

[Hexo系列(四) NexT主题配置](https://blog.csdn.net/wsmrzx/article/details/81478595)

[个人博客第8篇——优化主题（持续更新）](https://zhuanlan.zhihu.com/p/106060640)

该节中会修改许多代码文件，最好使用一个好用的编辑器，推荐使用vscode。（当然记事本也行）

# 2、说明

本节中会多次出现一些术语，先给出对应的说明

`站点根目录`：在（一）中提到过，使用`hexo init myblog`创建的文件夹`myblog`就是站点根目录，里面有source，themes，_config.yml等文件夹和文件。

`主题根目录`：站点根目录下的themes文件夹里，跟所使用的主题名字相关的一个文件夹，在安装主题后才会有这个文件夹，我这里是next文件夹，即`站点根目录\themes\next`，里面有languages，source等。

`站点配置文件`：`站点根目录`下的`_config.yml`文件。

`主题配置文件`：其他大多数教程中指的都是`主题根目录`下的`_config.yml`，修改该文件也可以，但新版的Hexo和NexT推荐使用代替配置文件：[配置|Hexo](https://hexo.io/zh-cn/docs/configuration)，方便管理以及Hexo和NexT的更新。所以该教程中指的是`站点根目录`下的`_config.next.yml`文件（后面会创建该文件）。

`高级配置文件`：或者叫自定义样式文件，大多数教程中指的是`主题根目录\source\css\_custom\custom.styl`，但新版本的NexT已经弃用了该文件，现在已经找不到这个文件了，详情参考[NexT官方文档](https://theme-next.js.org/docs/advanced-settings/custom-files.html)。该教程指的是`站点根目录\source\_data\styles.styl`（后面会创建该文件）。

`打开Git Bash`：无特殊说明都是在`站点根目录`下右键打开Git Bash。

`本地预览效果`：修改任何配置后，都可以打开Git Bash输入`hexo s`，在浏览器输入http://localhost:4000/在本地查看效果。

# 3、hexo基本配置

修改站点配置文件，详情参考[官方的配置](https://hexo.io/zh-cn/docs/configuration)描述。下面只讲我修改了的部分。

**网站**

| 参数       | 描述                            |
| :--------- | :------------------------------ |
| `title`    | 网站标题                        |
| `subtitle` | 网站副标题                      |
| `author`   | 您的名字                        |
| `language` | 网站使用的语言，中文设置为zh-CN |

>  其中，`description`主要用于SEO，告诉搜索引擎一个关于您站点的简单描述，通常建议在其中包含您网站的关键词。`author`参数用于主题显示文章的作者。



**网址**

| 参数  |      |
| ----- | ---- |
| `url` | 网址 |

在这里，你需要把url改成你的网站域名。



**writing**

```yaml
highlight:
  enable: false
  line_number: true
  auto_detect: false
  tab_replace: ''
  wrap: true
  hljs: false
prismjs:
  enable: true
  preprocess: false
  line_number: true
  tab_replace: ''
```

这一段是关于代码块风格设置，参考[hexo官网的说明](https://hexo.io/zh-cn/docs/syntax-highlight#PrismJS)和[next官网说明](https://theme-next.js.org/docs/theme-settings/miscellaneous.html#Codeblock-Style)，hexo支持两种库： [highlight.js](https://github.com/highlightjs/highlight.js) 和 [prismjs](https://github.com/PrismJS/prism) 。next主题官方也只能设置这两种。在这两种库下都有多种风格可选。

要用哪个库把相应的`enable`设为`true`，另一个的`enable`设为`false`，我选择了`prismjs`。其他的设置根据需要参考官网调整，我这里设为默认。

具体使用`prismjs`的哪一个主题还需要在后续主题配置文件里修改。

**主题选择**

```yaml
theme: next
```

要用哪个主题，就把这里设为`站点根目录\themes`下相应主题所在的文件夹名。



# 4、NexT基本配置

主题的修改不完全是主题配置文件的修改以及高级配置文件的修改，有的配置需要改一些特殊的文件，遇到会特殊说明

## 4.1 安装主题

打开Git Bash，输入：

```
git clone https://github.com/next-theme/hexo-theme-next themes/next
```

如果出现问题，可以手动去https://github.com/next-theme/hexo-theme-next下载，放到`站点根目录/themes/next`

这样，就有了主题根目录，即`站点根目录/themes/next`

可以输入`hexo g`和`hexo s`本地预览效果

## 4.2 主题配置

复制主题根目录下的``_config.yml`文件，粘贴到站点根目录下，修改文件名为`_config.next.yml`（注意别把站点配置文件覆盖了）。这就是主题配置文件。打开该文件。

### 主题选择

![image-20230726151245933](image-20230726151245933.png)

通过注释和取消注释选择主题，这里选择Mist，后面也是根据Mist调整。也可以试下其他主题，在本地预览效果，挑自己喜欢的。

23.7.27：更换为Pisces，最后的高级配置修改为针对Pisces。其他设置通用

23.7.28：更换为Gemini，最后的高级配置修改为针对Gemini。其他设置通用

### 菜单

![image-20230726151423449](image-20230726151423449.png)

会在博客顶部根据上图中的顺序依次添加菜单，但此时标签，分类，关于都无法打开，需要添加页面

![image-20230726151519546](image-20230726151519546.png)

Git Bash依次输入：

```
hexo new page tags
hexo new page categories
hexo new page about
```

标签页面还要在`站点根目录/source/tags/index.md` 中加上 `type: "tags"`，才会在标签页面显示标签

![image-20230726151600771](image-20230726151600771.png)

### 关闭渐入效果

搜索`motion`，将`enable`后面改为`false`，喜欢这个效果的的也可以不关

![image-20230726151800143](image-20230726151800143.png)



### 字体和代码

字体和代码的部分设置是一起的，放在一起说。

先说修改字体。官网说的比较详细：[Fonts Customization](https://theme-next.js.org/docs/theme-settings/miscellaneous.html#Fonts-Customization)

**字体：**

在`主题配置文件`中

![image-20230726153050491](image-20230726153050491.png)

先把`enable`设为`true`。

`host` 和 后面的每个设置的 `external` 和 `family` 我任意修改之后似乎都没起作用，，我也不需要设置，就都保持默认了，想修改的可以参考下其他资料。我只设置了`size`，单位为em（`1em`等于`16px`）

- `global`：全局设置，size改变后所有字体大小都会变
- `title`：博客名称的字体设置。字体大小受`global`下的`size`设置和`title`的`size`设置的双重影响
- `heading`：文章中各级题目的设置，即用 `# 题目` 语法的部分。字体大小受`global`下的`size`设置和`heading`的`size`设置的双重影响
- `posts`：官网说是文章主要字体的设置，但因为这两项我改了都不起作用，所以无法判断具体是什么设置。我也尝试加上`size:`来设置大小，不起作用
- `codes`：代码块的设置，试图加上`size`设置大小，不起作用

**代码块**

前面提到了：

> hexo支持两种库： [highlight.js](https://github.com/highlightjs/highlight.js) 和 [prismjs](https://github.com/PrismJS/prism) 。next主题官方也只能设置这两种。在这两种库下都有多种风格可选。要用哪个库把先把站点配置文件下对用主题下的`enable`设为`true`，另一个的`enable`设为`false`，我选择了`prismjs`，其他的设置根据需要参考官网调整，我这里设为默认。

![image-20230726153648860](image-20230726153648860.png)

如果前面选择`highlight`，就是`theme`后面设置起作用，我选择了`prism`，所以`prism`后面两个设置起作用，分别是正常模式下的代码主题和黑暗模式下的代码主题，我博客没开黑暗模式，所以根据`light`选项的设置。不同的风格可以去上图中364行提到的网站预览。[NexT Highlight Theme Preview](https://theme-next.js.org/highlight/)

我这里选择了`prism-tomorrow`，但这个主题的代码字体太大，在后面的高级配置中会进行调整

博客中代码块右上角还可以添加复制按钮，并且可以设置复制按钮样式，将`copy_botton`下的`enable`设为`true`，样式有三种，可以自己试试喜欢哪一个

![image-20230726154526462](image-20230726154526462.png)

设置完成后，行内代码（即用\``包含的部分）的颜色也是黑色，会显得非常的突兀，后面的高级配置会修改。



### 博客目录序号

禁止自动添加序号，因为我自己会加，不需要自动添加。并且我想要默认展开全部目录。修改设置如下：

![image-20230726154954945](image-20230726154954945.png)

### 隐藏底部“由...强力驱动”

将`powered`修改为`false`

![image-20230730213548467](image-20230730213548467.png)



### 头像

![image-20230730214105518](image-20230730214105518.png)

将头像图片放在`主题根目录/source/images`下，url格式如图



## 4.3 高级配置

参考[NexT官方文档](https://theme-next.js.org/docs/advanced-settings/custom-files.html)

新建`站点根目录\source\_data`文件夹，里面新建`styles.styl`文件，将主题配置文件的`custom_file_path`下的`style`取消注释

![image-20230726155327746](image-20230726155327746.png)

`styles.styl`文件的优先级很高，许多自定义配置都能在这里面添加，这个是用的CSS语言，虽然我之前也没接触过，但折腾了几下也会一些基本的修改，不懂得也可以去网上查，以及问ChatGPT。

我简单介绍一下自定义配置的操作思路

![image-20230726160932524](image-20230726160932524.png)

在浏览器中打开本地预览，按F12打开控制台（不同浏览器显示位置可能不同，但操作逻辑是一样的，我这里使用的Edge）

- 鼠标点击1，用于选择一个网页元素
- 鼠标点击2，选择这一个行内代码
- 右下方显示了这个元素相关的设置，在3找到背景和字体颜色的设置
- 将这个代码复制到`styles.styl`文件，修改这两个属性即可。

![image-20230726161349059](image-20230726161349059.png)

注意：

1、各元素的相同设置可能会在多个地方出现，一定要找对这个元素独特的类，即上图中的`code, kbd, figure.highlight, pre`，你可以在上图的控制台更下面也找到color的设置，如果修改了这个设置，可能会影响多个地方。

2、并不是出现了的属性我们才能去设置，比如还能设置上边距等属性

### styles.styl文件

下面放上我使用的`styles.styl`文件，希望可以给出一些参考

```stylus
//23.8.4更新，使用的Gemini主题
//文章内链接文本样式
// .post-body p a{
//   color: #0593d3;
//   border-bottom: none;
//   border-bottom: 1px solid #0593d3;
//   &:hover {
//     color: #fc6423;
//     border-bottom: none;
//     border-bottom: 1px solid #fc6423;
//   }
// }
.post-body p {
  --link-color: #0593d3;
  --link-hover-color: #fc6423;  
}
// a:hover {
//     border-bottom-color: var(--link-hover-color);
//     color: var(--link-hover-color);
// }

//代码块
.code-container {
  font-size: 14px;
}
//行内代码
code {
  font-size: 14px;
}
code, kbd, figure.highlight, pre {
    background: #f9f2f4;
    color: #dd0055;
}

//博客名
.posts-expand .post-title {
    font-size: 24px;
    font-weight: 550;
}
.posts-expand .post-title-link::before {
    background-image: linear-gradient(90deg, #404040 0%, #707070 25%, #909090 50%, #707070 75%, #404040 100%);
}

//侧边栏
.sidebar {
  font-size: 16px;  
}
a {
    border-bottom: 0px; 
}
.post-toc .nav-item {
    line-height: 2;
}


//隐藏图片名
.post-body .image-caption, .post-body img + figcaption, .post-body .fancybox + figcaption {
  display: none;
}

//分类页
.category-all-page .category-list {
    list-style: disc;     //一级分类前加实心圆点
    font-size: 18px;      //调整字体
}

//菜单
.menu {
    font-size: 18px;    //字体
}

//链接网格取消动画
.link-grid .link-grid-container {
  transform: none !important;
}

//选中文字的颜色和背影颜色
::selection {
    background: #328cfa;
    color: #ffffff;
}


// .post-footer {
//     display: flex;
// }

//[Read More]按钮样式
// .post-button .btn {
//   color: #555 !important;
//   background-color: rgb(255, 255, 255);
//   border-radius: 3px;
//   font-size: 15px;
//   box-shadow: inset 0px 0px 10px 0px rgba(0, 0, 0, 0.35);
//   border: none !important;
//   transition-property: unset;
//   padding: 0px 15px;
// }
// .post-button .btn:hover {
//   color: rgb(255, 255, 255) //!important;
//   border-radius: 3px;
//   font-size: 15px;
//   //box-shadow: inset 0px 0px 10px 0px rgba(0, 0, 0, 0.35);
//   //background-image: linear-gradient(90deg, #404040 0%, #707070 25%, #909090 50%, #707070 75%, #404040 100%);
// }


//背景图片设置
// body {
//   background-image: url(/images/background.jpg);
//   background-repeat: no-repeat;
//   background-attachment: fixed;
//   background-size: 100% 100%;
// }

//文章块设置
// .post-block:first-of-type {
//     padding-top: 45px;
// }
// .post-block {
//   //margin-bottom: 50px;
//   margin-bottom: 20px;

//   //border-radius: 10px;
  
//   padding: 45px 36px 36px 36px;
//   box-shadow: 0px 0px 10px 0px rgba(0, 0, 0, 0.5);
//   background-color: rgba(255, 255, 255, 1);
// }

//归档
// .posts-collapse .post-content .post-header {
//   border-bottom: 0px dashed #ccc;
//   margin: 30px 2px 0;
//   padding-left: 15px;
//   position: relative;
//   transition: border 0.2s ease-in-out;

//   font-size: 16px;
//   box-shadow: 0px 0px 10px 0px rgba(0, 0, 0, 0.5);
//   width: 600px;
//   height: 40px;

//   padding-top: 25px;
//   padding-bottom: 15px;
// }
// .posts-collapse .post-content .post-meta-container {
//     display: inline;
//     font-size: 16px;
//     margin-right: 10px;
// }
// .posts-collapse .post-content .post-header::before {
//     top: 37px;
// }

//分类页面左边添加竖线，调整间距
// .category-all-page .category-list {
//   list-style: none;
// }
// .category-all-page .category-list li {
//   position: relative; /* 设置列表项为相对定位，以便容纳伪元素 */
//   padding-left: 20px; /* 设置列表项的左内边距，为伪元素的宽度预留空间 */

//   margin-top: 15px;
//   margin-right: 10px;
//   margin-bottom: 15px;
//   margin-left: 10px;
// }
// .category-all-page .category-list li::before {
//   content: ""; /* 添加伪元素的内容，此处为空 */
//   position: absolute; /* 将伪元素绝对定位到列表项内 */
//   top: 0; /* 设置伪元素的顶部位置 */
//   left: 0; /* 设置伪元素的左侧位置 */
//   width: 2px; /* 设置伪元素的宽度，即竖线的宽度 */
//   height: 100%; /* 设置伪元素的高度，与列表项的高度一致，即竖线的高度 */
//   background-color: #3E2EBF; /* 设置竖线的颜色 */
// }
// .category-all-page .category-list-child {
//   list-style: none;
// }
// .category-all-page .category-list-child li {
//   position: relative; /* 设置列表项为相对定位，以便容纳伪元素 */
//   padding-left: 20px; /* 设置列表项的左内边距，为伪元素的宽度预留空间 */
// }
// .category-all-page .category-list-child li::before {
//   content: ""; /* 添加伪元素的内容，此处为空 */
//   position: absolute; /* 将伪元素绝对定位到列表项内 */
//   top: 0; /* 设置伪元素的顶部位置 */
//   left: 0; /* 设置伪元素的左侧位置 */
//   width: 2px; /* 设置伪元素的宽度，即竖线的宽度 */
//   height: 100%; /* 设置伪元素的高度，与列表项的高度一致，即竖线的高度 */
//   background-color: #B1A7FE; /* 设置竖线的颜色 */
// }

//隐藏首页文章底部的横线
// .post-eof {
//   display: none;
// }

// article {
//   font-size: 18px;  //归档下文章名字体
// }

```

### variables.styl文件

将主题配置文件的`custom_file_path`下的`variables`取消注释

```stylus
//标签云颜色
$tag-cloud-start      = #9733EE;
$tag-cloud-end        = #FF512F;


//$content-desktop         = 'calc(100% - %s)' % unit($content-desktop-padding / 2, 'px')
$content-desktop-large   = 1160px
$content-desktop-largest = 73%
```



