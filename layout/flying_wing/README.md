# 淘宝双飞翼布局

> 淘宝双飞翼布局和圣杯布局在前半部分的思路都差不多，只是在解决中间栏内容被挡住时所采用的方法不同。双飞翼布局在 main 下多一个增加 div，不使用相对定位，只用浮动和负边距，解决三栏液态式布局。

## DOM 结构

在 DOM 中按照主列、子列、附加列的顺序排列，保证主列优先加载。

```html
<div class="header">
        <strong>三栏布局之双飞翼布局</strong>
    </div>
    <div class="container">
        <div class="col main">
             <div class="main-wrap">我是一个宽度自适应的主列。</div>
        </div>
        <div class="col sub">我是一个子列。</div>
        <div class="col extra">我是一个附加列。</div>
    </div>
    <div class="footer"></div>
```

以上 DOM 结构中，在 main 中添加了一个子 div，用来解决中间列内容被遮挡问题。

## CSS 样式

去掉相对定位的使用，去掉了父容器的 padding，使用中间栏新增 div 的 margin 解决遮挡问题。

```css
        body {
            padding: 0;
            margin: 0;
            min-width: 440px; 
        }
        .header,
        .footer {
            background-color: #1c262f;
            color: white;
            text-align: center;
            font-size: 1.5em;
        }
        .container {
            width: 100%;
            min-height: 200px;
        }
        .col {
            float: left;
            color: white;
            text-align: justify; /* 文字两端对齐 */
            min-height:120px;
        }
        .main{
            width: 100%;
        }
        .sub {
            background-color: #ea4335;
            width: 120px;
            margin-left: -100%;
        }
        .extra {
            background-color: #34a853;
            width: 200px;
            margin-left: -200px;
        }
        .main-wrap {
            margin-left: 120px;
            margin-right: 200px;
            background-color: #4285f3;
        }
        .footr {
            clear: both;
        }
```

为 body 加上一个最小宽度(2 * sub width + extra width),避免网页放大时中间栏被挤到消失。