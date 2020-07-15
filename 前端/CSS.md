---
typora-copy-images-to: CSS
typora-root-url: CSS
---

# CSS

### 1.CSS简介

1. Cascading Style Sheets  级联样式单。 层叠样式表单
2. 样式表现语言，对HTML的补充， 且于网页样式定义，例如布局颜色文本等。  用于精确控制页面中的各个元素。
3. CSS3.0,分成一系列独立的模块
4. ![image-20200704093816973](image-20200704093816973.png)

```
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>import CSS</title>
    <!-- <style type="text/css">
        h1{
            color: seagreen;
        }
    </style> -->
    <!-- <link rel="stylesheet" href="demo.css" type="text/css" /> -->
    <!-- this is the method applicate in enterprise -->
    <style>
        @import 'demo.css';
    </style>
</head>
<body>
    <!-- <h1 style="color: red;">phone distribute</h1> -->
    <!-- <h1>import from style</h1> -->
    <h1>import from link </h1>
```

### 2.基本语法

![image-20200704095741262](image-20200704095741262.png)

一个基本结构，三个注意事项

- 选择器{样式名：样式值；}
  1. 分号分割
  2. 小写（本身是大小写不敏感）
  3. 选择器中元素项用逗号分割

```
    <style>
        h1,h2{
            color: red;text-align: center;text-shadow:5px 5px 5px blue;
        }
    </style>
```



### 3.CSS特性

1. 层叠。 相同属性最后一个生效
2. 继承特性。 内部的标签继承外部的标签。

### 4.选择器

![image-20200705095327485](image-20200705095327485.png)

元素选择器。   实际上就是{}前加标签

![image-20200705100112490](image-20200705100112490.png)

![image-20200705100435913](image-20200705100435913.png)

![image-20200705105920540](image-20200705105920540.png)

```
    <style>
        /* p[title] {color: red;} */
        /* p[title=huawei]{color: blue;} */
        /* p[title~="hua"]{color: yellow;} */
        p[title|="hua"]{color: pink;}
    </style>
</head>
<body>
    <p title="hua-wei">HUAWEI</p>
```

后两种应用不是特别广。   前缀的要以 - 为分隔符。 

![image-20200705110744190](image-20200705110744190.png)

![image-20200705110905197](image-20200705110905197.png)

伪类选择器常用于 a  链接中。

```
        a:link{color: red;}
        a:visited{color: blue;}
        a:hover{color: green;}
        a:active{color: pink;}
```

![image-20200705111638517](image-20200705111638517.png)

![image-20200705112028083](image-20200705112028083.png)

![image-20200705112428929](image-20200705112428929.png)

```
        span {color: blue;}
        p span {color: red;}
        p > span {color: blue;}
        div + p {color: pink;}
```

![image-20200705112804657](image-20200705112804657.png)

 

```
        div {
            color: green ;
        }
        .title{
            color: yellow;
        }
        #title{
            color: pink;
        }
        div#title{color: orange;}   /*1+100*/
```

### 5.常用属性

- 字体

![image-20200705113832226](image-20200705113832226.png)

![image-20200705114139183](E:\00MyWorkSpace\markdown file\CSS\image-20200705114139183.png)

- 文本

  ![image-20200705183512443](image-20200705183512443.png)

![image-20200705183839723](image-20200705183839723.png)

![image-20200705184100287](image-20200705184100287.png)

```
    <style>
        .text{
            text-align: center;
            direction: rtl;
            text-indent: 1em;
            text-decoration: underline;
            line-height: 50px;
            letter-spacing: 10px;
            text-shadow: 10px 5px 5px yellow;
        }
    </style>
```

- 尺寸

  ![image-20200705184331501](image-20200705184331501.png)

- 列表

  ![image-20200705185159010](image-20200705185159010.png)

![image-20200705185348529](image-20200705185348529.png)

列表属性就是控制前面列表项标记。

```
    <style>
        .list1{
            list-style-position: inside;
            list-style-type: square;
            list-style-image: url("image.png");
        }
        .list2
        {
            list-style-type: decimal; 
        }
    </style>
```

- 背景

  ![image-20200705191047292](image-20200705191047292.png)

![image-20200705191611669](image-20200705191611669.png)

![image-20200705191950830](image-20200705191950830.png)

### 6.盒模型 box model

布局， 每个相关属性是作用在一个抽象盒子上

![image-20200705192505620](image-20200705192505620.png)

![image-20200705192852715](image-20200705192852715.png)

![image-20200705201019133](image-20200705201019133.png)

![image-20200705201105493](image-20200705201105493.png)

![image-20200705201331915](image-20200705201331915.png)

​	属性中，样式不能省略

![image-20200705201717634](image-20200705201717634.png)

margin有叠加属性。 

块级元素两个元素同时设置magin时， margin取决于两个元素间最大的margin.

内联元素例如span ，没有重叠属性。



```
    <style>
        .box{
            border: 1px solid red;
            /* padding-top: 10px;
            padding-bottom: 30px; */
            padding: 10px 20px 30px 40px;
            border-style: solid;
            border-width: 10px;
            border-color: green;
            border-bottom: 5px dotted red;
            margin: 50px auto ; /*let element aligen center*/
            width: 200px;
            margin-left: auto;
            margin-right: auto;
        }
        
    </style>
```

![image-20200705202716188](image-20200705202716188.png)

只有块级元素，才可以设置宽高。  内联元素无这属性

内联元素排布的时候，中间是有一定的间隙的。 回车换行会引入空隙。

```
    <style>
        .box{
            border: 1px solid red;
            /* padding-top: 10px;
            padding-bottom: 30px; */
            padding: 10px 20px 30px 40px;
            border-style: solid;
            border-width: 10px;
            border-color: green;
            border-bottom: 5px dotted red;
            margin: 50px auto ; /*let element aligen center*/
            width: 200px;
            margin-left: auto;
            margin-right: auto;
        }
        .box2{
            display: inline-block;
            background: blue;
            width: 200px;
            height: 100px;
        }
        .box1{
            display: none;
            border: 1px solid red;
        }
        body {
            font-size: 0px;
        }
        .box3 {
            background: red;
            font-size: 14px;
        }
        .box4 {
            background: green;
            font-size: 14px;
        }
    </style>
</head>
<body>
    <div class="box">huawei</div>
    <div class="box1">interview</div>
    <div class="box2">validate</div>
    <span class="box3">inline element</span>
    <span class="box4">element2</span>
</body>
```

### 7.浮动

![image-20200705203634575](image-20200705203634575.png)

```
    <style>
        .box{
            border: 1px solid red;
        }
        .swim{
            width: 100px;
            height: 100px;
            background: yellow;
            float: left;
        }
    </style>
</head>
<body>
    <div class="box">float fish
        <div class="swim">this is me</div>
    </div>
```

![image-20200705204533907](image-20200705204533907.png)

![image-20200705204728314](image-20200705204728314.png)

```
    <style>
        .box{
            border: 1px solid red;
            width: 500px;
            /* height: 100px; */
            overflow: hidden;
        }
        .swim{
            width: 100px;
            height: 100px;
            background: yellow;
            float: left;
        }
        .right{
            widows: 200px;
            height: 200px;
            background: green;
            float: right;
        }
        .clear{
            clear: both;
        }
    </style>
</head>
<body>
    <div class="box">float fish
        <div class="swim">this is me</div>
        <div class="right">swim to right</div>
        <!-- <div class="clear"></div> -->
    </div>
```

大厂实际开发中清除浮动的方案

![image-20200705222220126](image-20200705222220126.png)

clear 要作用在块级元素，  不能作用于内联元素

```
        .clearfix::after{            /*add clear at last*/
            content: "";
            clear: both;   
            display: block;

            height: 0px;
            font-size: 0px;
            visibility: hidden;
        }
    </style>
</head>
<body>
    <div class="box clearfix">float fish
        <div class="left">this is me</div>
        <div class="right">swim to right</div>
        <!-- <div class="clear"></div> -->
    </div>
```

- 实战

  ![image-20200705222912576](image-20200705222912576.png)

![image-20200705224519375](image-20200705224519375.png)

### 8.定位

![image-20200705225141295](image-20200705225141295.png)

![image-20200705225317144](image-20200705225317144.png)

![image-20200705225917038](image-20200705225917038.png)

![image-20200705230451101](image-20200705230451101.png)

相对于已经定位的父元素。

![image-20200705231424703](image-20200705231424703.png)