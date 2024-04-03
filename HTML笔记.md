---

title: HTML笔记
date: 2024-02-05 21：30
tags: "HTML"
categories: "编程学习"
---

**村雨的HTML学习笔记**

![](http://villagerain.oss-cn-huhehaote.aliyuncs.com/imgQQ%E5%9B%BE%E7%89%8720221103083336.jpg)

<!-- more -->

------



# HTML介绍

HTML 是用来**描述网页**的一种语言。

- HTML 指的是超文本标记语言: **H**yper**T**ext **M**arkup **L**anguage
- HTML 不是一种编程语言，而是一种**标记**语言
- 标记语言是一套**标记标签** (markup tag)
- HTML 使用标记标签来**描述**网页
- HTML 文档包含了HTML **标签**及**文本**内容
- HTML文档也叫做 **web 页面**

## 一个简单的例子

```html
<!DOCTYPE html>//声明定义该文档是 HTML5 文档
<html>//HTML页面的根元素
<head>//包含有关 HTML页面的信息
<title>Page Title</title>//指定 HTML 页面的标题（显示在浏览器的标题栏或页面的选项卡中）
</head>
<body>//HTML文档的主体，并且是所有可见内容的容器，例如标题、段落、图像、超链接、表格、列表等。

<h1>My First Heading</h1>//定义了一个大标题
<p>My first paragraph.</p>//定义了一个段落

</body>
</html>
```

<img src="http://villagerain.oss-cn-huhehaote.aliyuncs.com/imgSnipaste_2024-02-03_10-46-36.png"  />

HTML 元素由**开始标记、一些内容**和**结束标记**定义：

格式：<标记名> 内容放在这里... < /标记名>

例如：标题：<h1>My First Heading</h1>

​           段落：<p>My first paragraph.</p>

其中br元素称为**空元素**，没有内容，没有结束标记。//换行符

------

Web 浏览器（Chrome、Edge、Firefox、Safari）的用途是读取 HTML 文档并正确显示它们。

HTML页面结构的可视化：

![](http://villagerain.oss-cn-huhehaote.aliyuncs.com/imgSnipaste_2024-02-03_10-45-30.png)

## 使用记事本学习HTML

将下面代码保存在记事本中，用.htm 或 .html 作为文件扩展名，将编码设置为 **UTF-8**（这是 HTML 文件的首选编码）。

```c++
<!DOCTYPE html>
<html>
<body>

<h1>My First Heading</h1>

<p>My first paragraph.</p>

</body>
</html>
```

在浏览器中查看HTML文档：

<img src="http://villagerain.oss-cn-huhehaote.aliyuncs.com/imgSnipaste_2024-02-03_10-53-18.png"  />

------

# HTML基础

所有 HTML 文档都必须以文档类型声明**开头**：`<!DOCTYPE html>`。

HTML 文档本身以 开头`<html>`并以 结尾`</html>`。

HTML 文档的可见部分位于`<body>`和之间`</body>`。

------

## HTML元素

**HTML 标题**用`<h1>`to`<h6>`标签定义。

`<h1>`定义最重要的标题。`<h6>`定义最不重要的标题：

```c++
<h1>This is heading 1</h1>
<h2>This is heading 2</h2>
<h3>This is heading 3</h3>
```

------

**HTML 段落**用`<p>`标签定义：

```c++
<p>This is a paragraph.</p>
<p>This is another paragraph.</p>
```

------

**HTML 链接**是`<a>`标签定义：

```c++
<a href="https://www.w3schools.com">This is a link</a>
```

------

**HTML 图像**用`<img>`标签定义：

源文件 ( `src`)、替代文本 ( `alt`)、 `width`和`height`作为属性。

```c++
<img src="w3schools.jpg" alt="W3Schools.com" width="104" height="142">
```

------

HTML 标签不区分大小写：`<P>`与 含义相同`<p>`。//但建议使用小写

------

## HTML属性

HTML 属性提供有关 HTML 元素的附加信息。

**href 属性**

`<a>`标签定义了一个超链接。`href`属性指定链接转到的页面的 URL：

```c++
<a href="https://www.w3schools.com">Visit W3Schools</a>
```

**src属性**

`<img>`标签用于在 HTML 页面中嵌入图像。`src`属性指定要显示的图像的路径：

```c++
<img src="img_girl.jpg">
```

**宽度和高度属性**

<img>标签还应包含 width和 height属性，它们指定图像的宽度和高度（以像素为单位）：

```c++
<img src="img_girl.jpg" width="500" height="600">
```

**alt 属性**

如果由于某种原因无法显示图像，则alt`属性`<img>` 可以指定图像的替代文本。

这可能是由于连接速度慢、src属性错误或者用户使用屏幕阅读器造成的。

```c++
<img src="img_girl.jpg" alt="Girl with a jacket">
```

![](http://villagerain.oss-cn-huhehaote.aliyuncs.com/imgSnipaste_2024-02-04_11-10-46.png)

**样式属性**

`style`属性用于向元素添加样式，例如颜色、字体、大小等。

```c++
<p style="color:red;">This is a red paragraph.</p>
```

<p style="color:red;">This is a red paragraph.</p>

**语言属性**

应该始终在标记`lang`内包含属性`<html>`，以声明网页的语言。

指定英语作为语言：(zh是中文)

```c++
<!DOCTYPE html>
<html lang="en">
<body>
...
</body>
</html>
```

**标题属性**

`title`属性定义了有关元素的一些额外信息。

将鼠标悬停在元素上时，标题属性的值将显示：

```c++
<p title="I'm a tooltip">This is a paragraph.</p>
```

![](http://villagerain.oss-cn-huhehaote.aliyuncs.com/imgSnipaste_2024-02-04_11-20-55.png)

------

建议使用小写字母，为属性值加上引号。一般使用双引号。

若属性值本身包含双引号，则使用单引号；若属性值本身包含单引号，则使用双引号。

## HTML段落

对于 HTML，无法通过在 HTML 代码中添加额外的空格或额外的行来更改显示。

当页面显示时，浏览器会自动删除任何**多余的空格和行**。

**HTML分割线**

`<hr>`标签定义 HTML 页面中的内容中断，并且通常显示为水平直线。

```c++
<h1>This is heading 1</h1>
<p>This is some text.</p>
<hr>
<h2>This is heading 2</h2>
<p>This is some other text.</p>
<hr>
```

![](http://villagerain.oss-cn-huhehaote.aliyuncs.com/imgSnipaste_2024-02-04_17-40-55.png)

`<hr>`标签是一个空标签，这意味着它没有结束标签。

**HTML换行符**

`<br>`元素定义换行符。

```c++
<p>This is<br>a paragraph<br>with line breaks.</p>
```

<p>This is<br>a paragraph<br>with line breaks.</p>

`<br>`标签是一个空标签，这意味着它没有结束标签。

**`<pre>`元素**

使用`<pre>`元素定义预格式化文本。

`<pre>`元素内的文本以固定大小和字体（通常是 Courier）显示，并且保留空格和换行符。

```c++
<pre>
  My Bonnie lies over the ocean.

  My Bonnie lies over the sea.

  My Bonnie lies over the ocean.

  Oh, bring back my Bonnie to me.
</pre>
```

![](http://villagerain.oss-cn-huhehaote.aliyuncs.com/imgSnipaste_2024-02-04_17-49-35.png)

## HTML样式

HTML`style`属性用于向元素添加样式，例如颜色、字体、大小等。

**背景颜色**

CSS`background-color`属性定义 HTML 元素的背景颜色。

```c++
<body style="background-color:powderblue;">

<h1>This is a heading</h1>
<p>This is a paragraph.</p>

</body>
```

![](http://villagerain.oss-cn-huhehaote.aliyuncs.com/imgSnipaste_2024-02-04_17-57-16.png)

为两个不同的元素设置背景颜色：

```c++
<body>

<h1 style="background-color:powderblue;">This is a heading</h1>
<p style="background-color:tomato;">This is a paragraph.</p>

</body>
```

![](http://villagerain.oss-cn-huhehaote.aliyuncs.com/imgSnipaste_2024-02-04_17-58-41.png)

**文字颜色**

CSS`color`属性定义 HTML 元素的文本颜色。

```c++
<h1 style="color:blue;">This is a heading</h1>
<p style="color:red;">This is a paragraph.</p>
```

![](http://villagerain.oss-cn-huhehaote.aliyuncs.com/imgSnipaste_2024-02-04_17-59-43.png)

**字体**

CSS`font-family`属性定义 HTML 元素使用的字体。

```c++
<h1 style="font-family:verdana;">This is a heading</h1>
<p style="font-family:courier;">This is a paragraph.</p>
```

![](http://villagerain.oss-cn-huhehaote.aliyuncs.com/imgSnipaste_2024-02-04_18-01-30.png)

**字体大小**

CSS`font-size`属性定义 HTML 元素的文本大小。

```c++
<h1 style="font-size:300%;">This is a heading</h1>
<p style="font-size:160%;">This is a paragraph.</p>
```

![](http://villagerain.oss-cn-huhehaote.aliyuncs.com/imgSnipaste_2024-02-04_18-02-45.png)

**文本对齐**

CSS`text-align`属性定义 HTML 元素的文本水平对齐方式。

```c++
<h1 style="text-align:center;">Centered Heading</h1>
<p style="text-align:center;">Centered paragraph.</p>
```

![](http://villagerain.oss-cn-huhehaote.aliyuncs.com/imgSnipaste_2024-02-04_18-04-00.png)

## HTML文本格式

HTML格式化元素：

```c++
<b>- 加粗字体
<strong>- 重要文字
<i>- 斜体文本
<em>- 强调文字
<mark>- 标记文本
<small>- 较小的文字
<del>- 删除文本
<ins>- 插入的文本
<sub>- 下标文字
<sup>- 上标文字
```

------

**`<b>`元素定义粗体文本，没有任何额外的重要性。**

```c++
<b>This text is bold</b>
```

<b>This text is bold</b>

------

**`<strong>`元素定义非常重要的文本，内容以粗体显示。**

```c++
<strong>This text is important!</strong>
```

<strong>This text is important!</strong>

------

**`<i>`元素定义斜体文本，没有任何额外的重要性。**

```c++
<i>This text is italic</i>
```

<i>This text is italic</i>

------

**`<em>`元素强调文本的语义，内容通常以斜体显示。**

```c++
<em>This text is emphasized</em>
```

<em>This text is emphasized</em>

------

**`<small>`元素定义较小的文本。**

```c++
<small>This is some smaller text.</small>
```

<small>This is some smaller text.</small>

------

**`<mark>`元素定义应标记或突出显示的文本。**

```c++
<p>Do not forget to buy <mark>milk</mark> today.</p>
```

<p>Do not forget to buy <mark>milk</mark> today.</p>

------

**`<del>`元素定义已从文档中删除的文本，会在删除的文本中划一条线。**

```c++
<p>My favorite color is <del>blue</del> red.</p>
```

<p>My favorite color is <del>blue</del> red.</p>

------

**`<ins>`元素定义已插入到文档中的文本，会给插入的文本添加下划线。**

```c++
<p>My favorite color is <del>blue</del> <ins>red</ins>.</p>
```

<p>My favorite color is <del>blue</del> <ins>red</ins>.</p>

------

**`<sub>`元素定义下标文本。下标文本出现在法线下方半个字符处，有时会以较小的字体呈现。下标文本可用于化学式，例如 H<sub>2</sub>O。**

```c++
<p>This is <sub>subscripted</sub> text.</p>
```

<p>This is <sub>subscripted</sub> text.</p>

------

**`sup>`元素定义上标文本。上标文本显示在正常线上方半个字符，并且有时以较小的字体呈现。上标文本可用于脚注，例如 XXX<sup> [1]</sup>**

```c++
<p>This is <sup>superscripted</sup> text.</p>
```

<p>This is <sup>superscripted</sup> text.</p>

------

## HTML引用

**`<blockquote>`元素定义从另一个源引用的内容，浏览器会将内容缩进。**

```c++
<p>Here is a quote from WWF's website:</p>
<blockquote cite="http://www.worldwildlife.org/who/index.html">
For 60 years, WWF has worked to help people and nature thrive. As the world's leading conservation organization, WWF works in nearly 100 countries. At every level, we collaborate with people around the world to develop and deliver innovative solutions that protect communities, wildlife, and the places in which they live.
</blockquote>
```

<p>Here is a quote from WWF's website:</p><blockquote cite="http://www.worldwildlife.org/who/index.html">For 60 years, WWF has worked to help people and nature thrive. As the world's leading conservation organization, WWF works in nearly 100 countries. At every level, we collaborate with people around the world to develop and deliver innovative solutions that protect communities, wildlife, and the places in which they live.</blockquote>

------

**`<q>`标签定义一个简短的引用，浏览器通常在引文两边插入引号。**

```c++
<p>WWF's goal is to: <q>Build a future where people live in harmony with nature.</q></p>
```

<p>WWF's goal is to: <q>Build a future where people live in harmony with nature.</q></p>

------

**`<abbr>`标签定义缩写或首字母缩略词，例如“HTML”、“CSS”、“Mr.”、“Dr.”、“ASAP”、“ATM”。**

```c++
<p>The <abbr title="World Health Organization">WHO</abbr> was founded in 1948.</p>
```

<p>The <abbr title="World Health Organization">WHO</abbr> was founded in 1948.</p>

注：将鼠标悬停在元素上时,可显示缩写词/首字母缩略词的描述。 

------

**`<address>`标签定义文档或文章的作者/所有者的联系信息。**

联系信息可以是电子邮件地址、URL、实际地址、电话号码、社交媒体账号等。

元素中的文本`<address>`通常以斜体呈现。

```c++
<address>
Written by John Doe.<br>
Visit us at:<br>
Example.com<br>
Box 564, Disneyland<br>
USA
</address>
```

<address>
Written by John Doe.<br>
Visit us at:<br>
Example.com<br>
Box 564, Disneyland<br>
USA
</address>

------

**`<cite>`标签定义创意作品的标题**（例如，一本书、一首诗、一首歌、一部电影、一幅画、一件雕塑等）。

注：人名并非作品名称,元素中的文本通常以斜体呈现。

```c++
<p><cite>The Scream</cite> by Edvard Munch. Painted in 1893.</p>
```

<p><cite>The Scream</cite> by Edvard Munch. Painted in 1893.</p>

------

**`<bdo>`标签用于覆盖当前文本方向。**

```c++
<bdo dir="rtl">This text will be written from right to left</bdo>
```

<bdo dir="rtl">This text will be written from right to left</bdo>

从左到右变成从右到左。

------

## HTML注释

注释不会显示在浏览器中，但它们可以帮助记录 HTML 源代码。

使用以下语法向 HTML 源添加注释:

```c++
<!-- Write your comments here -->
```

<!-- Write your comments here -->

注：开始标记中有感叹号`!`，但结束标记中没有。

------

**隐藏内容**

```c++
<p>This is a paragraph.</p>

<!-- <p>This is another paragraph </p> -->

<p>This is a paragraph too.</p>
```

<p>This is a paragraph.</p><!-- <p>This is another paragraph </p> --><p>This is a paragraph too.</p>

**隐藏多行**

```c++
<p>This is a paragraph.</p>
<!--
<p>Look at this cool image:</p>
<img border="0" src="pic_trulli.jpg" alt="Trulli">
-->
<p>This is a paragraph too.</p>
```

<p>This is a paragraph.</p>
<!--
<p>Look at this cool image:</p><img border="0" src="pic_trulli.jpg" alt="Trulli">
-->
<p>This is a paragraph too.</p>

------

## HTML颜色

在 HTML 中，可以使用颜色名称来指定颜色。

**设置文本背景颜色**

```c++
<h1 style="background-color:Tomato;">Tomato</h1>
<h1 style="background-color:Orange;">Orange</h1>
<h1 style="background-color:DodgerBlue;">DodgerBlue</h1>
<h1 style="background-color:MediumSeaGreen;">MediumSeaGreen</h1>
<h1 style="background-color:Gray;">Gray</h1>
<h1 style="background-color:SlateBlue;">SlateBlue</h1>
<h1 style="background-color:Violet;">Violet</h1>
<h1 style="background-color:LightGray;">LightGray</h1>
```

<h1 style="background-color:Tomato;">Tomato</h1>
<h1 style="background-color:Orange;">Orange</h1>
<h1 style="background-color:DodgerBlue;">DodgerBlue</h1>
<h1 style="background-color:MediumSeaGreen;">MediumSeaGreen</h1>
<h1 style="background-color:Gray;">Gray</h1>
<h1 style="background-color:SlateBlue;">SlateBlue</h1>
<h1 style="background-color:Violet;">Violet</h1>
<h1 style="background-color:LightGray;">LightGray</h1>

HTML 支持[140 个颜色名称](https://www.w3schools.com/colors/colors_names.asp)。

------

**设置文本颜色**

```c++
<h1 style="color:Tomato;">Hello World</h1>
<p style="color:DodgerBlue;">Hello World</p>
<p style="color:MediumSeaGreen;">Hello World</p>
```

<h1 style="color:Tomato;">Hello World</h1>
<p style="color:DodgerBlue;">Hello World</p>
<p style="color:MediumSeaGreen;">Hello World</p>

------

**设置边框颜色**

```c++
<h1 style="border:2px solid Tomato;">Hello World</h1>
<h1 style="border:2px solid DodgerBlue;">Hello World</h1>
<h1 style="border:2px solid Violet;">Hello World</h1>
```

<h1 style="border:2px solid Tomato;">Hello World</h1>
<h1 style="border:2px solid DodgerBlue;">Hello World</h1>
<h1 style="border:2px solid Violet;">Hello World</h1>

------

**RGB**

RGB 颜色值代表红色red、绿色green和蓝色blue。

每个参数（红色、绿色和蓝色）定义颜色的强度，其**值介于 0 到 255 之间**。

这意味着有 256 x 256 x 256 = 16777216 种可能的颜色！

```c++
<h1 style="background-color:rgb(255, 0, 0);">rgb(255, 0, 0)</h1>
<h1 style="background-color:rgb(0, 0, 255);">rgb(0, 0, 255)</h1>
<h1 style="background-color:rgb(60, 179, 113);">rgb(60, 179, 113)</h1>
<h1 style="background-color:rgb(238, 130, 238);">rgb(238, 130, 238)</h1>
<h1 style="background-color:rgb(255, 165, 0);">rgb(255, 165, 0)</h1>
<h1 style="background-color:rgb(106, 90, 205);">rgb(106, 90, 205)</h1>
```

<h1 style="background-color:rgb(255, 0, 0);">rgb(255, 0, 0)</h1>
<h1 style="background-color:rgb(0, 0, 255);">rgb(0, 0, 255)</h1>
<h1 style="background-color:rgb(60, 179, 113);">rgb(60, 179, 113)</h1>
<h1 style="background-color:rgb(238, 130, 238);">rgb(238, 130, 238)</h1>
<h1 style="background-color:rgb(255, 165, 0);">rgb(255, 165, 0)</h1>
<h1 style="background-color:rgb(106, 90, 205);">rgb(106, 90, 205)</h1>

**灰色阴影**

通常使用所有三个参数的相同值来定义。

```c++
<h1 style="background-color:rgb(60, 60, 60);">rgb(60, 60, 60)</h1>
<h1 style="background-color:rgb(100, 100, 100);">rgb(100, 100, 100)</h1>
<h1 style="background-color:rgb(140, 140, 140);">rgb(140, 140, 140)</h1>
<h1 style="background-color:rgb(180, 180, 180);">rgb(180, 180, 180)</h1>
<h1 style="background-color:rgb(200, 200, 200);">rgb(200, 200, 200)</h1>
<h1 style="background-color:rgb(240, 240, 240);">rgb(240, 240, 240)</h1>
```

<h1 style="background-color:rgb(60, 60, 60);">rgb(60, 60, 60)</h1>
<h1 style="background-color:rgb(100, 100, 100);">rgb(100, 100, 100)</h1>
<h1 style="background-color:rgb(140, 140, 140);">rgb(140, 140, 140)</h1>
<h1 style="background-color:rgb(180, 180, 180);">rgb(180, 180, 180)</h1>
<h1 style="background-color:rgb(200, 200, 200);">rgb(200, 200, 200)</h1>
<h1 style="background-color:rgb(240, 240, 240);">rgb(240, 240, 240)</h1>

**RGBA**

RGBA 颜色值是带有 Alpha 通道（不透明度）的 RGB 的扩展。

alpha 参数是介于 0.0（完全透明）和 1.0（完全不透明）之间的数值。

```c++
<h1 style="background-color:rgba(255, 99, 71, 0);">rgba(255, 99, 71, 0)</h1>
<h1 style="background-color:rgba(255, 99, 71, 0.2);">rgba(255, 99, 71, 0.2)</h1>
<h1 style="background-color:rgba(255, 99, 71, 0.4);">rgba(255, 99, 71, 0.4)</h1>
<h1 style="background-color:rgba(255, 99, 71, 0.6);">rgba(255, 99, 71, 0.6)</h1>
<h1 style="background-color:rgba(255, 99, 71, 0.8);">rgba(255, 99, 71, 0.8)</h1>
<h1 style="background-color:rgba(255, 99, 71, 1);">rgba(255, 99, 71, 1)</h1>
```

<h1 style="background-color:rgba(255, 99, 71, 0);">rgba(255, 99, 71, 0)</h1>
<h1 style="background-color:rgba(255, 99, 71, 0.2);">rgba(255, 99, 71, 0.2)</h1>
<h1 style="background-color:rgba(255, 99, 71, 0.4);">rgba(255, 99, 71, 0.4)</h1>
<h1 style="background-color:rgba(255, 99, 71, 0.6);">rgba(255, 99, 71, 0.6)</h1>
<h1 style="background-color:rgba(255, 99, 71, 0.8);">rgba(255, 99, 71, 0.8)</h1>
<h1 style="background-color:rgba(255, 99, 71, 1);">rgba(255, 99, 71, 1)</h1>

------

**十六进制颜色**

通过以下方式指定：

`#rrggbb`

其中 rr（红色）、gg（绿色）和 bb（蓝色）是 **00 到 ff 之间**的十六进制值（与十进制 0-255 相同）

例如，#ff0000 显示为红色，因为红色设置为其最高值 (ff)，而其他两个（绿色和蓝色）设置为 00。

```c++
<h1 style="background-color:#ff0000;">#ff0000</h1>
<h1 style="background-color:#0000ff;">#0000ff</h1>
<h1 style="background-color:#3cb371;">#3cb371</h1>
<h1 style="background-color:#ee82ee;">#ee82ee</h1>
<h1 style="background-color:#ffa500;">#ffa500</h1>
<h1 style="background-color:#6a5acd;">#6a5acd</h1>
```

<h1 style="background-color:#ff0000;">#ff0000</h1>
<h1 style="background-color:#0000ff;">#0000ff</h1>
<h1 style="background-color:#3cb371;">#3cb371</h1>
<h1 style="background-color:#ee82ee;">#ee82ee</h1>
<h1 style="background-color:#ffa500;">#ffa500</h1>
<h1 style="background-color:#6a5acd;">#6a5acd</h1>

**灰色阴影**

通常使用所有三个参数的相同值来定义。

```c++
<h1 style="background-color:#404040;">#404040</h1>
<h1 style="background-color:#686868;">#686868</h1>
<h1 style="background-color:#a0a0a0;">#a0a0a0</h1>
<h1 style="background-color:#bebebe;">#bebebe</h1>
<h1 style="background-color:#dcdcdc;">#dcdcdc</h1>
<h1 style="background-color:#f8f8f8;">#f8f8f8</h1>
```

<h1 style="background-color:#404040;">#404040</h1>
<h1 style="background-color:#686868;">#686868</h1>
<h1 style="background-color:#a0a0a0;">#a0a0a0</h1>
<h1 style="background-color:#bebebe;">#bebebe</h1>
<h1 style="background-color:#dcdcdc;">#dcdcdc</h1>
<h1 style="background-color:#f8f8f8;">#f8f8f8</h1>

------

**HSL**

hsl(*色调*,*饱和度*,*亮度*)

色调是色轮上从 0 到 360 的一个度数。0 是红色，120 是绿色，240 是蓝色。

饱和度是一个百分比值。 0% 表示灰度，100% 表示全色。

亮度也是一个百分比值。 0% 为黑色，100% 为白色。

```c++
<h1 style="background-color:hsl(0, 100%, 50%);">hsl(0, 100%, 50%)</h1>
<h1 style="background-color:hsl(240, 100%, 50%);">hsl(240, 100%, 50%)</h1>
<h1 style="background-color:hsl(147, 50%, 47%);">hsl(147, 50%, 47%)</h1>
<h1 style="background-color:hsl(300, 76%, 72%);">hsl(300, 76%, 72%)</h1>
<h1 style="background-color:hsl(39, 100%, 50%);">hsl(39, 100%, 50%)</h1>
<h1 style="background-color:hsl(248, 53%, 58%);">hsl(248, 53%, 58%)</h1>
```

<h1 style="background-color:hsl(0, 100%, 50%);">hsl(0, 100%, 50%)</h1>
<h1 style="background-color:hsl(240, 100%, 50%);">hsl(240, 100%, 50%)</h1>
<h1 style="background-color:hsl(147, 50%, 47%);">hsl(147, 50%, 47%)</h1>
<h1 style="background-color:hsl(300, 76%, 72%);">hsl(300, 76%, 72%)</h1>
<h1 style="background-color:hsl(39, 100%, 50%);">hsl(39, 100%, 50%)</h1>
<h1 style="background-color:hsl(248, 53%, 58%);">hsl(248, 53%, 58%)</h1>

**饱和度**

饱和度可以描述为颜色的强度。

100% 是纯色，没有灰色阴影。

50%是50%灰色，但你仍然可以看到颜色。

0%是完全灰色的；你再也看不到颜色了。

```c++
<h1 style="background-color:hsl(0, 100%, 50%);">hsl(0, 100%, 50%)</h1>
<h1 style="background-color:hsl(0, 80%, 50%);">hsl(0, 80%, 50%)</h1>
<h1 style="background-color:hsl(0, 60%, 50%);">hsl(0, 60%, 50%)</h1>
<h1 style="background-color:hsl(0, 40%, 50%);">hsl(0, 40%, 50%)</h1>
<h1 style="background-color:hsl(0, 20%, 50%);">hsl(0, 20%, 50%)</h1>
<h1 style="background-color:hsl(0, 0%, 50%);">hsl(0, 0%, 50%)</h1>
```

<h1 style="background-color:hsl(0, 100%, 50%);">hsl(0, 100%, 50%)</h1>
<h1 style="background-color:hsl(0, 80%, 50%);">hsl(0, 80%, 50%)</h1>
<h1 style="background-color:hsl(0, 60%, 50%);">hsl(0, 60%, 50%)</h1>
<h1 style="background-color:hsl(0, 40%, 50%);">hsl(0, 40%, 50%)</h1>
<h1 style="background-color:hsl(0, 20%, 50%);">hsl(0, 20%, 50%)</h1>
<h1 style="background-color:hsl(0, 0%, 50%);">hsl(0, 0%, 50%)</h1>

**亮度**

亮度可以描述为您想要赋予该颜色多少光。

0%表示没有光（黑色）。

50%表示50%光（既不暗也不亮）。

100%表示完全亮度（白色）。 

```c++
<h1 style="background-color:hsl(0, 100%, 0%);">hsl(0, 100%, 0%)</h1>
<h1 style="background-color:hsl(0, 100%, 25%);">hsl(0, 100%, 25%)</h1>
<h1 style="background-color:hsl(0, 100%, 50%);">hsl(0, 100%, 50%)</h1>
<h1 style="background-color:hsl(0, 100%, 75%);">hsl(0, 100%, 75%)</h1>
<h1 style="background-color:hsl(0, 100%, 90%);">hsl(0, 100%, 90%)</h1>
<h1 style="background-color:hsl(0, 100%, 100%);">hsl(0, 100%, 100%)</h1>
```

<h1 style="background-color:hsl(0, 100%, 0%);">hsl(0, 100%, 0%)</h1>
<h1 style="background-color:hsl(0, 100%, 25%);">hsl(0, 100%, 25%)</h1>
<h1 style="background-color:hsl(0, 100%, 50%);">hsl(0, 100%, 50%)</h1>
<h1 style="background-color:hsl(0, 100%, 75%);">hsl(0, 100%, 75%)</h1>
<h1 style="background-color:hsl(0, 100%, 90%);">hsl(0, 100%, 90%)</h1>
<h1 style="background-color:hsl(0, 100%, 100%);">hsl(0, 100%, 100%)</h1>

**灰色阴影**

通常通过将色调和饱和度设置为 0 并将亮度从 0% 调整到 100% 以获得更暗/更亮的阴影来定义。

```c++
<h1 style="background-color:hsl(0, 0%, 20%);">hsl(0, 0%, 20%)</h1>
<h1 style="background-color:hsl(0, 0%, 30%);">hsl(0, 0%, 30%)</h1>
<h1 style="background-color:hsl(0, 0%, 40%);">hsl(0, 0%, 40%)</h1>
<h1 style="background-color:hsl(0, 0%, 60%);">hsl(0, 0%, 60%)</h1>
<h1 style="background-color:hsl(0, 0%, 70%);">hsl(0, 0%, 70%)</h1>
<h1 style="background-color:hsl(0, 0%, 90%);">hsl(0, 0%, 90%)</h1>
```

<h1 style="background-color:hsl(0, 0%, 20%);">hsl(0, 0%, 20%)</h1>
<h1 style="background-color:hsl(0, 0%, 30%);">hsl(0, 0%, 30%)</h1>
<h1 style="background-color:hsl(0, 0%, 40%);">hsl(0, 0%, 40%)</h1>
<h1 style="background-color:hsl(0, 0%, 60%);">hsl(0, 0%, 60%)</h1>
<h1 style="background-color:hsl(0, 0%, 70%);">hsl(0, 0%, 70%)</h1>
<h1 style="background-color:hsl(0, 0%, 90%);">hsl(0, 0%, 90%)</h1>

**HSLA**

HSLA 颜色值是 HSL 颜色值的扩展，带有 Alpha 通道 - 用于指定颜色的不透明度。

alpha 参数是 介于0.0（完全透明）和 1.0（完全不透明）之间的数值。

```c++
<h1 style="background-color:hsla(9, 100%, 64%, 0);">hsla(9, 100%, 64%, 0)</h1>
<h1 style="background-color:hsla(9, 100%, 64%, 0.2);">hsla(9, 100%, 64%, 0.2)</h1>
<h1 style="background-color:hsla(9, 100%, 64%, 0.4);">hsla(9, 100%, 64%, 0.4)</h1>
<h1 style="background-color:hsla(9, 100%, 64%, 0.6);">hsla(9, 100%, 64%, 0.6)</h1>
<h1 style="background-color:hsla(9, 100%, 64%, 0.8);">hsla(9, 100%, 64%, 0.8)</h1>
<h1 style="background-color:hsla(9, 100%, 64%, 1);">hsla(9, 100%, 64%, 1)</h1>
```

<h1 style="background-color:hsla(9, 100%, 64%, 0);">hsla(9, 100%, 64%, 0)</h1>
<h1 style="background-color:hsla(9, 100%, 64%, 0.2);">hsla(9, 100%, 64%, 0.2)</h1>
<h1 style="background-color:hsla(9, 100%, 64%, 0.4);">hsla(9, 100%, 64%, 0.4)</h1>
<h1 style="background-color:hsla(9, 100%, 64%, 0.6);">hsla(9, 100%, 64%, 0.6)</h1>
<h1 style="background-color:hsla(9, 100%, 64%, 0.8);">hsla(9, 100%, 64%, 0.8)</h1>
<h1 style="background-color:hsla(9, 100%, 64%, 1);">hsla(9, 100%, 64%, 1)</h1>

------

## HTML-CSS

层叠样式表 (CSS) 用于格式化网页的布局。

CSS 节省了大量工作。它可以同时控制多个网页的布局。

应用于父元素的样式也将应用于父元素中的所有子元素。

因此，如果将正文文本的颜色设置为“蓝色”，正文中的所有标题、段落和其他文本元素也将获得相同的颜色（除非特别指定内容）！

### 内联CSS

用于将独特的样式应用于**单个 HTML 元素**，使用`style`。

```c++
<h1 style="color:blue;">A Blue Heading</h1>

<p style="color:red;">A red paragraph.</p>
```

<h1 style="color:blue;">A Blue Heading</h1>

<p style="color:red;">A red paragraph.</p>

------

### 内部CSS

用于定义**单个 HTML 页面**的样式。

在`<head>` 页面的某个`<style>`元素内定义。

将（该页面上）所有`<h1>`元素的文本颜色设置为蓝色，并将所有`<p>`元素的文本颜色设置为红色。此外，页面将以“粉蓝色”背景色显示：

```c++
<!DOCTYPE html>
<html>
<head>//内部CSS
<style>
body {background-color: powderblue;}
h1   {color: blue;}
p    {color: red;}
</style>
</head>
<body>

<h1>This is a heading</h1>
<p>This is a paragraph.</p>

</body>
</html>
```

![](http://villagerain.oss-cn-huhehaote.aliyuncs.com/imgSnipaste_2024-02-08_01-08-49.png)

------

### 外部CSS

外部样式表用于定义许多 HTML 页面的样式，可以通过更改一个文件来更改整个网站的外观。

要使用外部样式表，要在每个 HTML 页面的 `<head>`部分中添加指向它的链接。

外部样式表可以在任何文本编辑器中编写。该文件不得包含任何 HTML 代码，并且必须以 .css 扩展名保存。

“styles.css”文件：

```c++
body {
  background-color: powderblue;
}
h1 {
  color: blue;
}
p {
  color: red;
}
```

引用“styles.css”文件：

```c++
<!DOCTYPE html>
<html>
<head>
  <link rel="stylesheet" href="styles.css">//调用css文件
</head>
<body>

<h1>This is a heading</h1>
<p>This is a paragraph.</p>

</body>
</html>
```

- `<link>`：这是HTML中的一个标签，用于定义文档与外部资源之间的关系。
- `rel="stylesheet"`：这是`<link>`标签的属性之一，用于指定被链接文档与当前文档的关系。在这里，`stylesheet`表示被链接的文档是一个样式表。
- `href="styles.css"`：这也是`<link>`标签的一个属性，用于指定被链接文档的URL或路径。在这里，`styles.css`是被链接的样式表文件的路径或URL。

将当前HTML文档与名为`styles.css`的外部样式表文件关联起来，以应用样式表中定义的样式规则来渲染HTML文档中的元素。

------

### CSS 颜色、字体和大小

CSS`color`属性定义要使用的文本颜色。

CSS`font-family`属性定义要使用的字体。

CSS`font-size`属性定义要使用的文本大小。

```c++
![Snipaste_2024-02-08_01-24-47](C:/Users/86176/Desktop/Snipaste_2024-02-08_01-24-47.png)<!DOCTYPE html>
<html>
<head>
<style>
h1 {//定义一级标题的样式
  color: blue;
  font-family: verdana;
  font-size: 300%;
}
p {//定义段落的样式
  color: red;
  font-family: courier;
  font-size: 160%;
}
</style>
</head>
<body>

<h1>This is a heading</h1>
<p>This is a paragraph.</p>

</body>
</html>
```

![](http://villagerain.oss-cn-huhehaote.aliyuncs.com/imgSnipaste_2024-02-08_01-24-47.png)

------

### CSS边框

CSS`margin`属性定义边框外的**边距**（空间）。

```c++
<head>
<style>
p {//定义边框
  border: 2px solid powderblue;//边框的样式
  margin: 50px;//边距
}
</style>
</head>
<body>
    
<p>This is a paragraph.</p>
<p>This is a paragraph.</p>
<p>This is a paragraph.</p>

</body>
```

![](http://villagerain.oss-cn-huhehaote.aliyuncs.com/imgSnipaste_2024-02-08_01-27-18.png)

------

### CSS填充

CSS`padding`属性定义文本和边框之间的填充（空间）。

```c++
p {
  border: 2px solid powderblue;
  padding: 30px;
}
```

<img src="http://villagerain.oss-cn-huhehaote.aliyuncs.com/imgSnipaste_2024-02-16_09-52-59.png" style="zoom:50%;" />

------

### 链接外部CSS

外部样式表可以通过完整的 URL 或路径来引用。

```c++
<head>
  <link rel="stylesheet" href="https://www.w3schools.com/html/styles.css">
</head>
```

![](http://villagerain.oss-cn-huhehaote.aliyuncs.com/imgSnipaste_2024-02-08_01-36-37.png)

------

## HTML链接

HTML 链接是超链接。

可以单击链接并跳转到另一个文档，将鼠标移到链接上时，鼠标箭头会变成一只小手。

`<a>`标签定义超链接。

```c++
<a href="https://www.w3schools.com/">Visit W3Schools.com!</a>
```

<p><a href="https://www.w3schools.com/">Visit W3Schools.com!</a></p>

**注意**：链接不一定是文本。链接可以是图像或任何其他 HTML 元素！

------

### 目标属性

默认情况下，链接页面将显示在**当前浏览器窗口**中。要更改此设置，必须为链接指定另一个目标。

`target`属性指定在哪里打开链接文档。

- `_self`- 默认。在单击时的同一窗口/选项卡中打开文档
- `_blank`- 在**新窗口**或选项卡中打开文档
- `_parent`- 在父框架中打开文档
- `_top`- 在整个窗口中打开文档

```c++
<a href="https://www.villagerain.cn/" target="_blank">这里是村雨的个人博客</a>
```

<p><a href="https://www.villagerain.cn/" target="_blank">这里是村雨的个人博客</a></p>

------

### 相对URL

上面的示例都在`href`属性中使用**绝对 URL**（完整网址）。

**本地链接（指向同一网站内页面的链接）使用相对 URL**指定 （不带“https://www”部分）

```c++
<h2>Absolute URLs</h2>//指向不同的网站
<p><a href="https://www.w3.org/">W3C</a></p>
<p><a href="https://www.google.com/">Google</a></p>

<h2>Relative URLs</h2>//都指向W3school网站内页面
<p><a href="html_images.asp">HTML Images</a></p>
<p><a href="/css/default.asp">CSS Tutorial</a></p>
```

------

### 使用图像作为链接

要使用图像作为链接，只需将`<img>` 标签放在标签内即可`<a>`

```c++
<a href="link">
<img src="smiley.gif" alt="HTML tutorial" style="width:42px;height:42px;">//img标签
</a>
```

![](http://villagerain.oss-cn-huhehaote.aliyuncs.com/imgSnipaste_2024-02-16_10-16-52.png)

点击图像即可跳转对应网页。

------

### 链接到电子邮箱

`mailto:`在` href`属性内部创建一个打开用户电子邮箱的链接

```c++
<a href="mailto:someone@example.com">Send email</a>
```

<p><a href="mailto:1796245865@qq.com">Send email</a></p>

------

### 使用按钮作为链接

要使用按钮作为链接，必须添加一些 JavaScript 代码。

```html
<button onclick="document.location='https://villagerain.cn/'">村雨的个人博客</button>
```

![](http://villagerain.oss-cn-huhehaote.aliyuncs.com/imgSnipaste_2024-02-16_10-30-56.png)

**点击按钮后跳转网站。**

![Snipaste_2024-02-16_10-31-14](http://villagerain.oss-cn-huhehaote.aliyuncs.com/imgSnipaste_2024-02-16_10-31-14.png)

------

### 链接书签

如果网页很长，书签会很有用，以便读者可以跳转到网页的特定部分。

首先，使用`id`属性创建书签：

```c++
<h2 id="C4">Chapter 4</h2>
```

<h2 id="C4">Chapter 4</h2>

然后，在同一页面中添加指向书签的链接（“跳转到第 4 章”）：

```c++
<a href="#C4">Jump to Chapter 4</a>
```

<p><a href="#C4">Jump to Chapter 4</a></p>

当点击链接时，就会自动找到Chapter 4。

------

## HTML图像

HTML`<img>`标签用于在网页中嵌入图像。

从技术上讲，图像并未插入网页；图像链接到网页。`<img>`标签为引用的图像创建了一个保存空间。

该`<img>`标签是空的，仅包含属性，并且**没有结束标签。**

该`<img>`标签有两个必需的属性：

- src - 指定图像的路径
- alt - 指定图像的替代文本

**语法：**

```c++
<img src="url" alt="alternatetext">
```

```c++
<img src="http://villagerain.oss-cn-huhehaote.aliyuncs.com/img%E5%AE%89%E5%BA%A6%E5%9B%A0.jpg" alt="安度因">
```

<img src="http://villagerain.oss-cn-huhehaote.aliyuncs.com/img%E5%AE%89%E5%BA%A6%E5%9B%A0.jpg" alt="安度因" style="zoom:50%;" >

------

### 图像尺寸

使用`style`属性来指定图像的宽度和高度：

```c++
style="width:500px;height:600px;"
```

使用`width`和`height`属性来指定图像的宽度和高度：

```c++
width="500" height="600"
```

**注意**：始终指定图像的宽度和高度。如果未指定宽度和高度，加载图像时网页可能会闪烁。

​            建议使用`style`属性。它可以防止样式表更改图像的大小。

------

### 图像浮动

使用 CSS`float`属性让图像浮动到文本的右侧right或左侧left：

```c++
<img src="http://villagerain.oss-cn-huhehaote.aliyuncs.com/img%E5%AE%89%E5%BA%A6%E5%9B%A0.jpg" alt="安度因" style="float:left;width:150px;height:150px;">
```

<img src="http://villagerain.oss-cn-huhehaote.aliyuncs.com/img%E5%AE%89%E5%BA%A6%E5%9B%A0.jpg" alt="安度因" style="float:left;width:150px;height:150px;">

------

### 图像映射

使用 HTML 图像映射，可以**在图像上创建可单击区域**。当点击对应区域时就会跳转到相应的页面。

由于涉及到像素点的位置，比较繁琐。更详细的内容请查看官网。

https://www.w3schools.com/html/html_images_imagemap.asp

`<map>`标签定义图像映射。被定义图像具有可点击区域。这些区域是用一个或多个`<area>`标签定义的。

```c++
<img src="workplace.jpg" alt="Workplace" usemap="#workmap">//整张图片

<map name="workmap">
  <area shape="rect" coords="34,44,270,350" alt="Computer" href="computer.htm">//矩形电脑区域
  <area shape="rect" coords="290,172,333,250" alt="Phone" href="phone.htm">//矩形手机区域
  <area shape="circle" coords="337,300,44" alt="Coffee" href="coffee.htm">//圆形咖啡杯区域
</map>
```

<img src="C:/Users/86176/Desktop/Snipaste_2024-02-19_23-16-32.png" style="zoom: 80%;" />

在该例子中，有三个图像映射的区域。当点击对应的区域，就会跳转到对应区域所指向的网页（href）

------

### 背景图片

要在 HTML 元素上添加背景图片，要使用 HTML`style`属性和 CSS`background-image`属性：

```c++
<p style="background-image: url('img_girl.jpg');">
```

还可以在`<head>`元素中的以下部分中指定背景图片 ：

```c++
<style>
p {
  background-image: url('img_girl.jpg');
}
</style>
```

如果希望**整个页面**都有背景图片，则必须在`<body>`元素上指定背景图片：

```c++
<style>
body {
  background-image: url('img_girl.jpg');
}
</style>
```

如果背景图像小于元素，图像将水平和垂直**重复**自身，直到到达元素的末尾。

要避免背景图像重复，可将该`background-repeat`属性设置为`no-repeat`。

```c++
<style>
body {
  background-image: url('example_img_girl.jpg');
  background-repeat: no-repeat;
}
</style>
```

如果希望背景图片覆盖整个元素，可以将该`background-size`属性设置为 `cover.`

另外，为了确保整个元素始终被覆盖，可以将 `background-attachment`属性设置为`fixed:`

这样，背景图像将覆盖整个元素，不会拉伸（图像将保持其原始比例）：

```c++
![Snipaste_2024-02-19_23-51-27](C:/Users/86176/Desktop/Snipaste_2024-02-19_23-51-27.png)<!DOCTYPE html>
<html>
<head>
<style>
body {
  background-image: url('http://villagerain.oss-cn-huhehaote.aliyuncs.com/img%E9%A9%AC%E7%AB%9E%E5%A4%BA%E5%86%A0.jpg');
  background-repeat: no-repeat;
  background-attachment: fixed; 
  background-size: 100% 100%;
}
</style>
</head>
<body>

<h2>马德里竞技20/21夺冠赛季</h2>

<p>海神之子，永不言弃！</p>

</body>
</html>
```




<img src="http://villagerain.oss-cn-huhehaote.aliyuncs.com/imgSnipaste_2024-02-19_23-51-27.png" style="zoom:50%;" />

如果希望背景图像拉伸以适合整个元素，可以将该`background-size`属性设置为 `100% 100%`

------

### 图片元素

HTML`<picture>`元素允许为不同的设备或屏幕尺寸显示不同的图片，为 Web 开发人员指定图像资源提供了更大的灵活性。

`<picture>`元素包含一个或多个`<source>`元素，每个元素通过属性引用不同的图像`srcset` 。

这样浏览器就可以选择最适合当前视图和/或设备的图像。

每个`<source>`元素都有一个 `media`属性，用于定义图像何时最合适。

```c++
//针对不同的屏幕尺寸显示不同的图像：
<picture>
  <source media="(min-width: 650px)" srcset="img_food.jpg">
  <source media="(min-width: 465px)" srcset="img_car.jpg">
  <img src="img_girl.jpg">
</picture>
```

**注意**：始终将某个`<img>`元素指定为`<picture>`元素的最后一个子元素。该`<img>`元素由不支持该`<picture>`元素的浏览器使用，或者如果没有`<source>`标签匹配时使用。

（本内容了解即可）

------

## HTML网站图标

将网站图标图像保存到网络服务器的根目录中，或者在**根目录**中创建一个名为 images 的文件夹，并将您的网站图标图像保存在此文件夹中。网站图标图像的通用名称是“favicon.ico”。

接下来，将一个`<link>`元素添加到“index.html”文件中的`<title>`元素后面。

```c++
<!DOCTYPE html>
<html>
<head>
  <title>网站图标测试</title>//网站页面标题
  <link rel="icon" type="image/x-icon" href="/images/favicon.ico">
</head>
<body>

<h1>你干嘛~</h1>
<p>练习时长两年半。</p>

</body>
</html>
```

**测试结果**：

![](http://villagerain.oss-cn-huhehaote.aliyuncs.com/imgSnipaste_2024-02-26_10-41-11.png)

**注意**：要将html文件和images文件夹要放在同一目录下，本例中我都放到了D盘根目录。

------

## HTML表格

### 定义表格

**表行**

每个表行以`<tr>`开头并以`</tr>`标签结尾。

```c++
<table>//表格
  <tr>//表示行的开始table row
    <td>格里兹曼</td>//表中的数据table date
    <td>梅西</td>
    <td>C罗</td>
  </tr>//表示行的结束
  <tr>
    <td>1</td>//表中的数据
    <td>2</td>
    <td>3</td>
  </tr>
</table>
```

<table>
  <tr>
    <td>格里兹曼</td>
    <td>梅西</td>
    <td>C罗</td>
  </tr>
  <tr>
    <td>1</td>
    <td>2</td>
    <td>3</td>
  </tr>
</table>

一个表中可以有任意多的行，只需确保每行中的**单元格数量相同**即可。

------

### **表格标题**

希望单元格成为标题单元格时，使用表头`<th>`标签。

```c++
<table>//表格
  <tr>
    <th>金球奖第一</th>//标题单元格table head
    <th>金球奖第二</th>
    <th>金球奖第三</th>
  </tr>
  <tr>
    <td>格里兹曼</td>
    <td>梅西</td>
    <td>C罗</td>
  </tr>
  <tr>
    <td>1</td>
    <td>2</td>
    <td>3</td>
  </tr>
</table>
```

<table>
  <tr>
    <th>金球奖第一</th>
    <th>金球奖第二</th>
    <th>金球奖第三</th>
  </tr>
  <tr>
    <td>格里兹曼</td>
    <td>梅西</td>
    <td>C罗</td>
  </tr>
  <tr>
    <td>1</td>
    <td>2</td>
    <td>3</td>
  </tr>
</table>

若要使第一列成为标题，则设置每行的第一个单元格为表头：

```c++
<table>
  <tr>
    <th>金球奖第一</th>//设置为表头
    <td>金球奖第二</td>
    <td>金球奖第三</td>
  </tr>
  <tr>
    <th>格里兹曼</th>//设置为表头
    <td>梅西</td>
    <td>C罗</td>
  </tr>
  <tr>
    <th>1</th>//设置为表头
    <td>2</td>
    <td>3</td>
  </tr>
</table>
```

<table>
  <tr>
    <th>金球奖第一</th>
    <td>金球奖第二</td>
    <td>金球奖第三</td>
  </tr>
  <tr>
    <th>格里兹曼</th>
    <td>梅西</td>
    <td>C罗</td>
  </tr>
  <tr>
    <th>1</th>
    <td>2</td>
    <td>3</td>
  </tr>
</table>

**对齐标题**

在网页中，默认情况下，表标题为粗体并居中。

要左对齐**标题**，使用 CSS中`text-align`属性：

```c++
th {
  text-align: left;
}
```

![](http://villagerain.oss-cn-huhehaote.aliyuncs.com/imgSnipaste_2024-02-26_22-03-58.png)

**多列标题**

使用元素 `<th>`上的属性`colspan`可以设置跨越两列或更多列的标题：

```c++
<table>
  <tr>
    <th colspan="2">金球奖前二</th>//标题跨越两列
    <th>金球奖第三</th>
  </tr>
  <tr>
    <td>格里兹曼</td>
    <td>梅西</td>
    <td>C罗</td>
  </tr>
  <tr>
    <td>1</td>
    <td>2</td>
    <td>3</td>
  </tr>
</table>
```

<table>
  <tr>
    <th colspan="2">金球奖前二</th>
    <th>金球奖第三</th>
  </tr>
  <tr>
    <td>格里兹曼</td>
    <td>梅西</td>
    <td>C罗</td>
  </tr>
  <tr>
    <td>1</td>
    <td>2</td>
    <td>3</td>
  </tr>
</table>

**添加整个表格的标题**

使用`<caption>`标签：

```c++
<table>
    <caption>金球奖排行</caption>//在<table>标签下，<tr>标签上添加
    <tr>
    <th>金球奖第一</th>
    <th>金球奖第二</th>
    <th>金球奖第三</th>
  </tr>
  <tr>
    <td>格里兹曼</td>
    <td>梅西</td>
    <td>C罗</td>
  </tr>
  <tr>
    <td>1</td>
    <td>2</td>
    <td>3</td>
  </tr>
</table>
```

<table>
    <caption>金球奖排行</caption>
    <tr>
    <th>金球奖第一</th>
    <th>金球奖第二</th>
    <th>金球奖第三</th>
  </tr>
  <tr>
    <td>格里兹曼</td>
    <td>梅西</td>
    <td>C罗</td>
  </tr>
  <tr>
    <td>1</td>
    <td>2</td>
    <td>3</td>
  </tr>
</table>

------

### 表格边框

HTML 表格可以具有不同样式和形状的边框。

要添加边框，则在 `table`、`th`和 `td`元素上使用 CSS 属性`border`

```c++
<!DOCTYPE html>//整个网页的代码
<html>
<head>
<style>//内部CSS
table, th, td {//添加边框
  border: 1px solid black;
}
</style>
</head>
<body>

<table>
  <tr>
    <th>金球奖第一</th>
    <th>金球奖第二</th>
    <th>金球奖第三</th>
  </tr>
  <tr>
    <td>格里兹曼</td>
    <td>梅西</td>
    <td>C罗</td>
  </tr>
  <tr>
    <td>1</td>
    <td>2</td>
    <td>3</td>
  </tr>
</table>

</body>
</html>
```

在网页上添加表格与不添加表格的效果对比：

![](http://villagerain.oss-cn-huhehaote.aliyuncs.com/imgSnipaste_2024-02-26_21-14-26.png)

![](http://villagerain.oss-cn-huhehaote.aliyuncs.com/imgSnipaste_2024-02-26_21-14-37.png)

**设置表格为单边框**

将 CSS`border-collapse` 属性设置为`collapse`。

```c++
table, th, td {
  border: 1px solid black;
  border-collapse: collapse;
}
```

![](http://villagerain.oss-cn-huhehaote.aliyuncs.com/imgSnipaste_2024-02-26_21-17-21.png)

**设置单元格背景颜色**

在内部CSS中添加以下代码：

```c++
th, td {
  background-color: #96D4D4;//颜色可自行设置
}
```

![](http://villagerain.oss-cn-huhehaote.aliyuncs.com/imgSnipaste_2024-02-26_21-24-29.png)

**设置圆桌边框**

添加`border-radius`属性，边框变为圆角：

```c++
table, th, td {
  border: 1px solid black;
  border-radius: 10px;
}
```

![](http://villagerain.oss-cn-huhehaote.aliyuncs.com/imgSnipaste_2024-02-26_21-26-48.png)

**设置边框样式**

使用`border-style`属性，可以设置边框的外观。

```c++
th, td {
  border-style: dotted;//设置为虚线
}
```

![](http://villagerain.oss-cn-huhehaote.aliyuncs.com/imgSnipaste_2024-02-26_21-30-39.png)

其他样式：

![](http://villagerain.oss-cn-huhehaote.aliyuncs.com/imgSnipaste_2024-02-26_21-30-54.png)

**边框颜色**

通过`border-color`属性，可以设置边框的颜色。

```c++
th, td {
  border-color: #96D4D4;
}
```

![](http://villagerain.oss-cn-huhehaote.aliyuncs.com/imgSnipaste_2024-02-26_21-32-33.png)

------

### 表格大小

HTML 表格的每列、行或整个表格可以有不同的大小。

让`<style>` 带有`width`或`height` 属性来指定行或列的大小。

```c++
<table style="width:100%">//设置表格宽度为100%
  <tr>
    <th style="width:50%">金球奖第一</th>//设置第一列宽度为50%
    <th>金球奖第二</th>
    <th>金球奖第三</th>
  </tr>
  <tr style="height:100px">//设置第二行的列高为100px
    <td>格里兹曼</td>
    <td>梅西</td>
    <td>C罗</td>
  </tr>
  <tr>
    <td>1</td>
    <td>2</td>
    <td>3</td>
  </tr>
</table>
```

<table style="width:100%">
  <tr>
    <th style="width:50%">金球奖第一</th>
    <th>金球奖第二</th>
    <th>金球奖第三</th>
  </tr>
  <tr style="height:100px">
    <td>格里兹曼</td>
    <td>梅西</td>
    <td>C罗</td>
  </tr>
  <tr>
    <td>1</td>
    <td>2</td>
    <td>3</td>
  </tr>
</table>

**注意**:使用百分比作为宽度的大小单位意味着该元素与其父元素（在本例中为`<body>`元素）相比有多宽 。

------

### **单元格填充和间距**

单元格填充是单元格边缘和单元格内容之间的空间，默认情况下，填充设置为 0。

要在单元格上添加填充，需使用 CSS`padding`属性：

```c++
th, td {
  padding: 15px;
}
```

![](http://villagerain.oss-cn-huhehaote.aliyuncs.com/imgSnipaste_2024-02-26_22-19-54.png)

要仅在内容上方添加填充，使用`padding-top`属性。

还支持`padding-bottom`、`padding-left`和`padding-right`属性：

```c++
th, td {
  padding-top: 10px;
  padding-bottom: 0px;
  padding-left: 0px;
  padding-right: 0px;
}
```

![](http://villagerain.oss-cn-huhehaote.aliyuncs.com/imgSnipaste_2024-02-26_22-22-05.png)

**单元格间距**

单元格间距是每个单元格之间的空间，默认情况下，空间设置为 2 像素。

要更改表格单元格之间的间距，请使用元素` border-spacing`上的 CSS 属性`table` ：

```c++
table {
  border-spacing: 10px;
}
```

![](http://villagerain.oss-cn-huhehaote.aliyuncs.com/imgSnipaste_2024-02-26_22-25-55.png)

------

### 列跨度和行跨度

要使单元格跨越多列，使用`colspan`属性，**表格标题**一栏中已举例说明。

要使单元格跨越多行，使用`rowspan`属性：

```c++
<table>
  <tr>
    <th>姓名</th>
    <td>德佩</td>
  </tr>
  <tr>
    <th rowspan="2">职业</th>
    <td>足球运动员</td>
  </tr>
  <tr>
    <td>说唱歌手</td>
</tr>
</table>
```

<table>
  <tr>
    <th>姓名</th>
    <td>德佩</td>
  </tr>
  <tr>
    <th rowspan="2">职业</th>
    <td>足球运动员</td>
  </tr>
  <tr>
    <td>说唱歌手</td>
</tr>
</table>

------

### 表格样式

**斑马条纹**

如果在每隔一个表格行添加背景颜色，将获得漂亮的斑马条纹效果：

```c++
tr:nth-child(even) {//只设置偶数行有颜色
  background-color: #D6EEEE;
}
```

![](http://villagerain.oss-cn-huhehaote.aliyuncs.com/imgSnipaste_2024-02-26_22-40-58.png)

**垂直斑马条纹**

要制作垂直斑马条纹，需每隔一**列**设置样式，而不是每隔一行设置样式：

```c++
td:nth-child(even), th:nth-child(even) {//只设置偶数列和偶数列标题有颜色
  background-color: #D6EEEE;
}
```

![](http://villagerain.oss-cn-huhehaote.aliyuncs.com/imgSnipaste_2024-02-26_22-42-59.png)

**组合垂直和水平斑马纹**

结合上面两个示例中的样式，每隔一行和每一列都会有条纹：

```c++
tr:nth-child(even) {//只设置偶数行有颜色
  background-color: rgba(150, 212, 212, 0.4);
}
//使用rgba()来指定颜色的透明度：
td:nth-child(even),th:nth-child(even) {//只设置偶数列和偶数列标题有颜色
  background-color: rgba(150, 212, 212, 0.4);
}
```

![](http://villagerain.oss-cn-huhehaote.aliyuncs.com/imgSnipaste_2024-02-26_22-48-07.png)

**水平分割线**

如果仅在每个表格行的底部指定边框，将产生一个带有水平分隔线的表格。

将`border-bottom`属性添加到所有 `tr`元素以获取水平分隔线：

```c++
tr {
  border-bottom: 1px solid #ddd;
}
```

![](http://villagerain.oss-cn-huhehaote.aliyuncs.com/imgSnipaste_2024-02-26_22-52-08.png)

**悬浮表格**

使用 `tr:hover`选择器在**鼠标悬停时**突出显示表行：

```c++
tr:hover {background-color: #D6EEEE;}
```

![](http://villagerain.oss-cn-huhehaote.aliyuncs.com/imgSnipaste_2024-02-26_22-53-32.png)

### 表格列成组

如果要设置**表格前两列**的样式，使用`<colgroup>` 和`<col>` 元素。

`<colgroup>`元素应用作列规格的容器。

每个组都用一个元素指定`<col>`。

`span`属性指定有多少列获得该样式。

`style`属性指定列的样式。

```c++
<table style="width:100%">
  <colgroup>
    <col span="2" style="background-color: #D6EEEE">
  </colgroup>
  <tr>
  ...
```

![](http://villagerain.oss-cn-huhehaote.aliyuncs.com/imgSnipaste_2024-02-26_22-58-39.png)

**使用不同的样式设置更多列**

```c++
<table style="width:100%">
<colgroup>
    <col span="1" style="background-color: #D6EEEE">//第一列成组
    <col span="2" style="background-color: pink">//第二三列成组（第一组的后面两列成组）
  </colgroup>
  <tr>
  ...
```

![](http://villagerain.oss-cn-huhehaote.aliyuncs.com/imgSnipaste_2024-02-26_23-04-50.png)

**空列成组**

如果要为表格中间的列设置样式，请 `<col>`在前面的列中插入一个“空”元素（没有样式）：

```c++
<colgroup>
    <col span="1">//一个道理
    <col span="1" style="background-color: pink">
    <col span="1">
  </colgroup>
  <tr>
  ...
```

![](http://villagerain.oss-cn-huhehaote.aliyuncs.com/imgSnipaste_2024-02-26_23-07-34.png)

**隐藏列**

使用`visibility: collapse`属性隐藏列：

```c++
<table style="width:100%">
<colgroup>
    <col span="1" style="background-color: #D6EEEE">
    <col span="1" style="visibility: collapse">
    <col span="1" style="background-color: #D6EEEE">
  </colgroup>
  <tr>
```

![](http://villagerain.oss-cn-huhehaote.aliyuncs.com/imgSnipaste_2024-02-26_23-10-46.png)

------

## HTML列表

### 无序列表

无序列表以`<ul>`标签开头。每个列表项都以标签开头 `<li>`。

```c++
<ul>
 <li>格里兹曼</li>
 <li>梅西</li>
 <li>C罗</li>
</ul>
```

<ul>
 <li>格里兹曼</li>
 <li>梅西</li>
 <li>C罗</li>
</ul>

可以通过CSS`list-style-type`属性改变标签的**样式**

例如，空心圆圈circle：

```c++
<ul style="list-style-type:circle;">
  <li>格里兹曼</li>
  <li>梅西</li>
  <li>C罗</li>
</ul>
```

<ul style="list-style-type:circle;">
  <li>格里兹曼</li>
  <li>梅西</li>
  <li>C罗</li>
</ul>

此外，还有实心圆圈disc、正方形square、无none。效果依次如下：

<ul style="list-style-type:disc;">
  <li>格里兹曼</li>
  <li>梅西</li>
  <li>C罗</li>
</ul>

<ul style="list-style-type:square;">
  <li>格里兹曼</li>
  <li>梅西</li>
  <li>C罗</li>
</ul>

<ul style="list-style-type:none;">
  <li>格里兹曼</li>
  <li>梅西</li>
  <li>C罗</li>
</ul>

------

### 嵌套列表

```c++
<ul>//无序列表嵌套
  <li>格里兹曼</li>
  <li>梅西//展开此标签
    <ul>
      <li>呦西</li>
      <li>球玉</li>
    </ul>
  </li>//此标签结束
  <li>C罗</li>
</ul>
```

<ul>
  <li>格里兹曼</li>
  <li>梅西
    <ul>
      <li>呦西</li>
      <li>球玉</li>
    </ul>
  </li>
  <li>C罗</li>
</ul>

------

### 有序列表

`<ol>`标签定义了一个有序列表。有序列表可以是数字的或字母的。

列表项默认会标有数字：

```c++
<ol>
  <li>格里兹曼</li>
  <li>梅西</li>
  <li>C罗</li>
</ol>
```

<ol>
  <li>格里兹曼</li>
  <li>梅西</li>
  <li>C罗</li>
</ol>

若想使用字母，需要使用`type`属性：

```c++
<ol type="A">
  <li>格里兹曼</li>
  <li>梅西</li>
  <li>C罗</li>
</ol>
```

<ol type="A">
  <li>格里兹曼</li>
  <li>梅西</li>
  <li>C罗</li>
</ol>

使用罗马数字：

```c++
<ol type="I">
  <li>格里兹曼</li>
  <li>梅西</li>
  <li>C罗</li>
</ol>
```

<ol type="I">
  <li>格里兹曼</li>
  <li>梅西</li>
  <li>C罗</li>
</ol>

其他标签头使用方法依次类推。

**控制列表计数**

默认情况下，有序列表会从 1 开始计数。如果想从指定的数字开始计数，可以使用`start`属性：

```
<ol start="50">
  <li>格里兹曼</li>
  <li>梅西</li>
  <li>C罗</li>
</ol>
```

<ol start="50">
  <li>格里兹曼</li>
  <li>梅西</li>
  <li>C罗</li>
</ol>

有序也可以嵌套，与无序列表方法相同。

### 描述列表

标签`<dl>`定义描述列表，` <dt>`标签定义术语（名称），` <dd>`标签描述每个术语：

```c++
<dl>
  <dt>格里兹曼</dt>
  <dd>- 足球大师</dd>
  <dt>梅西</dt>
  <dd>- 没礼貌的小偷</dd>
  <dt>C罗</dt>
  <dd>- 不如格子</dd>
</dl>
```

<dl>
  <dt>格里兹曼</dt>
  <dd>- 足球大师</dd>
  <dt>梅西</dt>
  <dd>- 没礼貌的小偷</dd>
  <dt>C罗</dt>
  <dd>- 不如格子</dd>
</dl>

------

## 块和内联

每个 HTML 元素都有一个**默认显示值**，具体取决于元素的类型。

两个最常见的显示值是块和内联。

**块级元素**总是从新行开始，浏览器会自动在元素前后添加一些空格（边距）。

块级元素始终占据可用的全部宽度（尽可能向左和向右延伸）。

两个常用的块级元素是：`<p>` 和`<div>`。

`<p>`元素定义 HTML 文档中的一个段落。

`<div>`元素定义 HTML 文档中的一个分区或一个部分。

```c++
<p>格里兹曼</p>
<div>姆巴佩</div>//<div>元素通常用作其他 HTML 元素的容器。
```

<p>格里兹曼</p>
<div>姆巴佩</div>

**HTML中的块级元素：**

```c++
<address> <article> <aside> <blockquote> <canvas> <dd> <div> <dl> <dt> <fieldset> <figcaption> <figure> <footer><form> <h1>-<h6> <header> <hr> <li> <main> <nav> <noscript> <ol> <p> <pre> <section> <table> <tfoot> <ul> <video>
```

**内联元素**

内联元素不会从新行开始。

内联元素仅占用必要的宽度。

例如段落内的 <span> 元素。

```c++
<p>格里兹曼<span>是足球大师</span></p>//<span>元素是一个内联容器，用于标记文本的一部分或文档的一部分。
```

<p>格里兹曼<span>是足球大师</span></p>

**HTML中的内联元素**：

```c++
<a> <abbr> <acronym> <b> <bdo> <big> <br> <button> <cite> <code> <dfn> <em> <i> <img> <input> <kbd> <label> <map><object> <output> <q> <samp> <script> <select> <small> <span> <strong> <sub> <sup> <textarea> <time> <tt> <var>
```

------

## HTML-Div分区

`<div>`元素用作其他 HTML 元素的容器,是块级元素，这意味着它占用所有可用宽度，并且前后带有换行符。

`<div>`元素通常用于将网页的各个部分分组在一起。

```c++
<style>
div {
  background-color: #FFF4A3;//黄色
}
</style>

<div>//分区
  <h2>London</h2>
  <p>London is the capital city of England.</p>
  <p>London has over 13 million inhabitants.</p>
</div>
```

这样，只有div分区的部分具有div所定义的样式。

### **居中对齐`<div>`元素**

如果希望`<div>`元素不是 100% 宽，并且想要将其居中对齐，需将 CSS `margin`属性设置为` auto`。

```c++
<style>
div {
  width:300px;
  margin:auto;
}
</style>
```

可以在一个页面上拥有多个div分区，每个分区设置自己独特的样式：

```c++
<div style="background-color:#FFF4A3;">
  <h2>London</h2>
  <p>London is the capital city of England.</p>
  <p>London has over 13 million inhabitants.</p>
</div>

<div style="background-color:#FFC0C7;">
  <h2>Oslo</h2>
  <p>Oslo is the capital city of Norway.</p>
  <p>Oslo has over 600.000 inhabitants.</p>
</div>

<div style="background-color:#D9EEE1;">
  <h2>Rome</h2>
  <p>Rome is the capital city of Italy.</p>
  <p>Rome has almost 3 million inhabitants.</p>
</div>
```

<div style="background-color:#FFF4A3;">
  <h2>London</h2>
  <p>London is the capital city of England.</p>
  <p>London has over 13 million inhabitants.</p>
</div>

<div style="background-color:#FFC0C7;">
  <h2>Oslo</h2>
  <p>Oslo is the capital city of Norway.</p>
  <p>Oslo has over 600.000 inhabitants.</p>
</div>

<div style="background-color:#D9EEE1;">
  <h2>Rome</h2>
  <p>Rome is the capital city of Italy.</p>
  <p>Rome has almost 3 million inhabitants.</p>
</div>

### **并排对齐`<div>`元素**

构建网页时，通常希望 `<div>`并排有两个或多个元素，如下所示：

![](http://villagerain.oss-cn-huhehaote.aliyuncs.com/imgSnipaste_2024-02-28_22-49-16.png)

**方法1：CSS-float属性**

------

## HTML类

`class`属性用于指定 HTML 元素的类，不同的HTML 元素可以共享同一个类。

**语法**：写一个句点 (.) 字符，后跟类名。然后，在大括号 {} 内定义 CSS 属性

```c++
<style>
.city {//city类
  background-color: tomato;
  color: white;
  padding: 10px;
}

.note {//note类
  font-size: 120%;
  color: red;
}
</style>
```

**绑定类**：元素括号中加上class="类名"

```c++
<div class="city">//该分区属于city类
  <h2>London</h2>
  <p>London is the capital of England.</p>
</div>

<div class="city">//该分区属于city类
  <h2>Paris</h2>
  <p>Paris is the capital of France.</p>
</div>

<h1>My <span class="note">Important</span> Heading</h1>//该分区属于note类

    <p>This is some <span class="note">important</span> text.</p>//该分区属于note类
```

**注意**：类名区分大小写！

**一个HTML元素也可以绑定多个类**

```c++
<h2 class="city note">London</h2>//两个类名用空格分开即可
```

------

## HTML-id

`id`属性用于指定 HTML 元素的**唯一**ID，用于指向样式表中的特定样式声明。

在 HTML 文档中不能有多个具有相同 id 的元素。

**语法**：写入一个哈希字符 (#)，后跟一个 id 名称。然后，在大括号 {} 内定义 CSS 属性。

```c++
<!DOCTYPE html>
<html>
<head>
<style>
#myHeader {//通过id来指定样式
  background-color: lightblue;
  color: black;
  padding: 40px;
  text-align: center;
}
</style>
</head>
<body>

<h1 id="myHeader">My Header</h1>//设置元素h1的id为myHeader

</body>
</html>
```

**注意** ：id名称区分大小写，必须至少包含一个字符，不能以数字开头，并且不能包含空格（空格、制表符等）。

**类和id的区别**：类名可以由多个 HTML 元素使用，而 id 名称只能由页面中的一个 HTML 元素使用。

id还可以实现书签的功能，具体语法在HTML链接一节。

------

## HTML内嵌框架

HTML `<iframe>` 用于在网页中显示网页。（在当前 HTML 文档中嵌入另一个文档。）

```c++
<iframe src="https://www.bilibili.com/" style="border:none;" //删除边框，还可以自定义其他CSS样式
    height="500" width="800"//高度和宽度
    title="B站"></iframe>
```

<iframe src="https://www.bilibili.com/" style="border:none;" height="500" width="800" title="Iframe Example"></iframe>

------

## HTML其他

### HTML -meta 元素

`<meta>`元素通常用于指定字符集、页面描述、关键字、文档作者和视口设置。

数据**不会显示在页面上**，但由浏览器（如何显示内容或重新加载页面）、搜索引擎（关键字）和其他 Web 服务使用。

**定义使用的字符集：**

`<meta charset="UTF-8">`

**定义搜索引擎的关键字：**

`<meta name="keywords" content="HTML, CSS, JavaScript">`

**定义网页的描述：**

`<meta name="description" content="Free Web tutorials">`

**定义页面的作者：**

`<meta name="author" content="John Doe">`

**每 30 秒刷新一次文档：**

`<meta http-equiv="refresh" content="30">`

**设置视口以使您的网站在所有设备上看起来都不错：**

`<meta name="viewport" content="width=device-width, initial-scale=1.0">`

```c++
<!DOCTYPE html>//示例
<html>
<head>
  <meta charset="UTF-8">
  <meta name="description" content="Free Web tutorials">
  <meta name="keywords" content="HTML, CSS, JavaScript">
  <meta name="author" content="John Doe">
</head>
<body>

<p>All meta information goes inside the head section.</p>

</body>
</html>
```

![](C:/Users/86176/Desktop/Snipaste_2024-03-02_11-04-48.png)

**设置视口**

视口是网页的用户可见区域。它因设备而异 - 在手机上它会比在电脑屏幕上小。

应该在**所有网页**中包含以下元素：

`<meta name="viewport" content="width=device-width, initial-scale=1.0">`

这为浏览器提供了如何控制页面尺寸和缩放的说明。

`width=device-width`设置页面的宽度以遵循设备的屏幕宽度（这将根据设备而变化）。

`initial-scale=1.0`设置浏览器首次加载页面时的初始缩放级别。

------

### HTML -script元素

`<script>`元素用于定义客户端 JavaScript。

下面的 JavaScript 会写“Hello JavaScript!” 到 id="demo" 的 HTML 元素中：

```c++
<script>
function myFunction() {
  document.getElementById("demo").innerHTML = "Hello JavaScript!";
}
</script>
```

JavaScript的具体知识请看相关章节。

------

### HTML -base标签

`<base>`为页面上所有的链接指定默认 URL 和默认目标：

```c++
<head>
<base href="https://www.w3schools.com/" target="_blank">//默认路径就是w3school 打开方式为新建窗口
</head>

<body>//之后的所有路径都将基于w3school去查询 打开方式都为新建窗口
<img src="images/stickman.gif" width="24" height="39" alt="Stickman">
<a href="tags/tag_base.asp">HTML base Tag</a>
</body>
```

`<base>`标记必须具有 href 或 target 属性，或两者兼而有之。

html文档中**只能有一个**`<base>`元素，并且它必须位于 `<head> `元素内。

