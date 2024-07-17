---
title: butterfly
tags:
  - null
categories:
  - null
date: 2024-07-17 16:05:20
description: Hexo 的特殊语法
mathjax: false
---

[https://theme-next.js.org/docs/tag-plugins/](https://theme-next.js.org/docs/tag-plugins/)

[https://butterfly.js.org/posts/2df239ce/](https://butterfly.js.org/posts/2df239ce/)

# Tabs

## 使用方法

[参考另一个主题的教程](https://theme-next.js.org/docs/tag-plugins/tabs)

```
{% tabs Unique name, [index] %}
<!-- tab [Tab caption] [@icon] -->
标签页内容 (support inline tags too).
<!-- endtab -->
{% endtabs %}
```

- `Unique name`：

  标签块标签的唯一名称，不能含逗号。

  将在 #id 中使用，作为每个标签页的前缀和索引号。

  如果名称中有空格，生成 #id 时将用破折号替换所有空格。

- `[index]`：**可选**。

  活动选项卡的索引号。

  如果未指定，将选择第一个选项卡（1）。

  如果索引为-1，则不会选择任何标签页。

- `[Tab caption]`：**可选**。

  当前选项卡的标题。

  如果未指定标题，带有标签页索引后缀的 Unique name 将用作标签页的标题。

  如果未指定标题，但指定了图标，标题将为空。

- `[@icon]`：**可选**。

  Font Awesome 图标名称。

  可指定带空格或不带空格；例如，"Tab caption @icon "与 "Tab caption@icon "相同。

## 示例

````
{% tabs 标签 %}

<!-- tab -->
**这是标签页1**
1. One
2. Two
3. Three
```
nano /etc
```
<!-- endtab -->

<!-- tab 自定义标签名-->
**这是标签页2.**
<!-- endtab -->

<!-- tab -->
**这是标签页3.**
{% subtabs 子标签页,2 %}
<!-- tab 自定义标签名-->
**这是子标签页1.**
<!-- endtab -->
<!-- tab -->
**这是子标签页2.**
<!-- endtab -->
{% endsubtabs %}

<!-- endtab -->
{% endtabs %}
````

{% tabs 标签 %}

<!-- tab -->
**这是标签页1**
1. One
2. Two
3. Three
```
nano /etc
```
<!-- endtab -->

<!-- tab 自定义标签名-->
**这是标签页2.**
<!-- endtab -->

<!-- tab -->
**这是标签页3.**
{% subtabs 子标签页,2 %}
<!-- tab 自定义标签名-->
**这是子标签页1.**
<!-- endtab -->
<!-- tab -->
**这是子标签页2.**
<!-- endtab -->
{% endsubtabs %}

<!-- endtab -->
{% endtabs %}



# Button

## 使用方法

[参考教程](https://theme-next.js.org/docs/tag-plugins/button#)

```
{% button url, text, icon [class], [title] %}
```

或

```
{% btn url, text, icon [class], [title] %}
```

- `url`：URL 的绝对或相对路径。
- `text`：按钮文本。如果没有指定图标，则为必填项。
- `icon`：Font Awesome 图标名称。如果未指定文本，则为必填项。
- `[class]`：可选参数。字体 Awesome class（es）： fa-fw fa-lg fa-2x fa-3x fa-5x
- `[title]` ：可选参数。鼠标悬停时的提示。

## 示例

```
<div class="text-center">{% btn #, Text %}{% btn #, Text & Title,, Title %}</div>
```

<div class="text-center">{% btn #, Text %}{% btn #, Text & Title,, Title %}</div>

```
{% btn #,1 %}{% btn #,2 %}
```

{% btn #,1 %}{% btn #,2 %}

# Group Pictures

[参考教程](https://theme-next.js.org/docs/tag-plugins/group-pictures)

# Note

[参考教程](https://theme-next.js.org/docs/tag-plugins/note)
