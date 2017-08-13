# 圣杯布局

> 圣杯布局是三栏式布局的一种经典解决方案，来源于 Matthew Levine 于 2006 年发表在 Alistapart 上的一篇文章。[原文链接](https://alistapart.com/article/holygrail)，其主要解决以下几种要求：

* 两边侧栏固定宽度，中间栏宽度自适应，
* 中间栏要放在文档流的前面以优先渲染。 
* 其父元素的高度始终是由三栏中高度最高的元素确定。

## 第一步 建立基本框架

写出基本的 html 框架，构建出基本盒模型，包括`header`, `container`和`footer`三个主体结构，再向`container`中加入三栏：

```html
<div class="header"></div>
<div class="container">
    <div class="column center"></div>
    <div class="column left"></div>
    <div class="column right"></div>
</div>
<div class="footer"></div>
```

### 第二步 构建基础布局

将 `container` 的内边距设置为左右两侧边栏各自的宽度，为两侧边栏留下空间。为三栏设置合适的宽度(`center`宽度为 100%，`left`宽度为 120px，`right`宽度为240px)，并且将三者设为向左浮动，同时清除`footer`的上下环境，避免其浮动。最后将`body`的最小宽度设为 480px(2*LC width + RC width)，避免因为`center`部分的宽度小`left`和`right`的宽度导致布局乱掉。

```css
        body {
            padding: 0;
            margin: 0; /* 初始化LCD */
            min-width: 480px;/* 2*LC-width + RC-width */
        }
        .header, .footer {
            background-color: #1c262f;
            color: white;
            text-align: center;
            font-size: 2em;
        }
        .container {
            padding-left: 120px;  /* LC-width */
            padding-right: 240px; /* RC-width */
        }
        .column {
            float: left;
            color: white;
            position: relative;
            text-align: justify; /* 文字两端对齐 */
        }
        h1 {
            text-align: center;
        }
        .center {
            background-color: #4285f3;
            width: 100%;
        }
        .left {
            background-color: #ea4335;
            width: 120px; /* LC-width */
        }
        .right {
            background-color: #34a853;
            width: 240px;  /* RC-width */
        }
        .footer {
            clear: both;
        }
```

### 第三步 将侧栏放到合适的位置

设置三栏的定位属性为相对定位。设置左边栏的外边距`margin-left: -100%;`(中间栏所占据的宽度)，左边栏上移到中间栏的左边，但是与中间栏部分重叠。此时利用相对定位属性，为左边栏设置一个与其等宽的偏移量`left：-120px;`(相对于`container`的左边线向左偏移 120px)，左边栏刚好占据`container`的左内边距位置。最后设置右边栏的外边距`margin-right: -240px;`(右边栏自身宽度)，使右边栏占据`container`的右内边距位置。

```css
        .column {
            float: left;
            position: relative;
        }
        .left {
            margin-left: -100%; 
            left: -120px;
        }
        .right {
            margin-right: -240px;
        }
```