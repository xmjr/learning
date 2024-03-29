﻿# Sass的学习与使用

#### [一、Sass的特色](#Sass的特色)
#### [二、Sass与Less](#Sass与Less)
#### [三、Sass和Scss](#Sass和Scss)
#### [四、使用Sass](#使用Sass)
- [（一）安装并使用sass](#安装并使用sass)
- [（二）将sass文件编译（转换）成css文件](#将sass文件编译（转换）成css文件)
#### [五、学习Sass](#学习Sass)
- [（一）使用变量 \$](#使用变量)
- [（二）嵌套CSS规则](#嵌套CSS规则)
- [（三）导入Sass文件 @import](#导入Sass文件)
- [（四）静默注释 //](#静默注释)
- [（五）混合器 @mixin @include](#混合器)
- [（六）选择器继承 @extend](#选择器继承)
#### [六、参考资料](#参考资料)


<div id="Sass的特色">

## 一、Sass的特色

Sass是对css的扩展，在css语言基础上添加了变量、嵌套（nesting）、混合（mixin）等扩展功能，赋予了css动态语言的特性，并且完全兼容css语法，有助于更方便的维护和管理css代码，以及更高效地开发项目。

<div id="Sass与Less">

## 二、Sass与Less

两者都是css的预处理器，功能上大同小异。Sass基于Ruby语言编写，所以编译Sass文件需要Ruby环境；Less则主要运行在node环境下。

<div id="Sass和Scss">

## 三、Sass和Scss

SCSS是Sass3引入新的语法，其语法完全兼容CSS3，同时继承了Sass的强大功能；两者其实是同一种东西，平时都称之为Sass，两者的不同在于：    

- 文件扩展名不同
Sass以“.sass”后缀为扩展名，SCSS以“.scss”后缀为扩展名

- 语法书写方式不同
Sass 是以严格的缩进式语法规则来书写，不带大括号({})和分号(;)，而 SCSS 的语法书写和CSS语法书写方式非常类似。

<div id="使用Sass">

## 四、使用Sass

Sass有三种使用方式：命令行工具、独立的Ruby模块，以及包含 Ruby on Rails 和 Merb 作为支持 Rack 的框架的插件。作为前端开发，一般是用用命令行工具。（用ruby命令行、电脑命令行都行）

<div id="安装并使用sass">

### （一）[安装并使用sass](https://www.cnblogs.com/qqqiangqiang/p/5359986.html)

一般来说，可分为三个步骤：

- windows系统先安装Ruby
- 下载并安装sass
- 在sublime中安装sass插件（我一般是用sublime敲代码，所以是在sublime中安装sass插件）

<div id="将sass文件编译（转换）成css文件">

### （二）[将sass文件编译（转换）成css文件](https://www.cnblogs.com/wuzhiquan/p/5912146.html)

- 直接在命令行中运行Sass    
 （input.scss代表需要转换的sass文件名，input.css代表转换成的css文件名，别忘了在文件前加上各自相应的路径）
> sass input.scss output.css

- 监视单个Sass文件，每次修改并保存时自动编译
（左边代表sass输入文件，右边是css输出文件，别忘了加路径）
> sass --watch 
input.scss:output.css

- 监视整个文件夹
（左边代表监视的文件夹路径，右边代表输出的文件夹路径）
> sass --watch sass:css


- 举例

虽然网上教程很多，但我当初还是绕了很久，挽尊....

（1）我用sublime编辑了个sass文件common.scss，保存在d盘的Web文件夹中，我现在要将该文件编译成同名的css文件并放在同一文件夹中；
（2）在电脑命令行（或Ruby命令行）输入
> sass d:\Web\common.scss d:Web\common.css

（3）之后，在Web文件夹中，多了两个文件，除了css，还有一个map文件，sass文件相当于源文件，css相当于编译后的文件，当检查到页面问题的时候，你看到的是css，但是需要修改的是sass文件，这个map就是两个文件的对应关系表。

<div id="学习Sass">

## 五、学习Sass

<div id="使用变量">

###（一）使用变量 \$

可以把反复使用的css属性值定义为变量，然后通过变量名来引用它们，而无需重复书写这一书写值。

    $nav-color:#f90;
    
    nav {
        $width:100px;  
    width:$width;   
        color:$nav-color;
    }
    
    //编译后
    nav {
        width:100px;
        color:#f90;
    }
    
在上面这段代码中，#nav-color这个变量定义在了规则块外边，所以在这个样式表中都可以向nav规则块那样引用它；$width这个变量定义在了nav的{}规则块内，所以只能在nav规则块内使用。

变量值可以引用其他变量：

    $highlight-color:#f90;
$highlight-border:1px solid $hightlight-color;
    selected {
        border:$highlight-border;
    }
    
    //编译后
    .selected {
        border:1px solid #f90;
    }

在sass中，中划线命名的内容和下划线命名的内容是互通的，比如$link-color和$link_color；不过，在sass中，纯css部分不互通，比如类名、id或属性名。

<div id="嵌套CSS规则">

### （二）嵌套CSS规则

避免在css中重复写一大串选择器

    // css
    #content article h1 { color: #333 }
    #content article p { margin-bottom: 1.4em }
    #content aside { background-color: #EEE }
    
    // sass
    #content {
        article {
            h1 { color: #333 }
            p { margin-bottom: 1.4em }
        }
        aside { background-color: #EEE }
    }

当同时要为一个容器元素及其子元素编写特定样式时，就非常有用了：

    #content {
        background-color: #f5f5f5;
        aside { background-color: #eee }
    }
    
    // 编译后
    #content { background-color: #f5f5f5 }
    #content aside { background-color: #eee }

父选择器的标识符 & 

在为父元素添加:hover等伪类时，避免父元素以空格形式添加到子元素中从而形成后代选择器。如下例，若在:hover前无&元素，则article元素内链接的所有子元素在被hover时都会变成红色；而我们其实只想将这条规则应用到超链接自身。

    article a {
    color: blue;
    &:hover { color: red }
    }
    
    // 编译后
    article a { color: blue }
    article a:hover { color: red }

<div id="导入Sass文件">

### （三）导入Sass文件 @import

css中的@import，允许在一个css文件中导入其他css文件；不过，只有执行到@import时，浏览器才会去下载其他css文件，这导致页面加载较慢。

sass的@import规则在生成css文件时就把相关文件导入进来，所有相关的样式被归纳到了同一个css文件中，而无需发起额外的下载请求。

导入时，可省略文件后缀（.sass、.scss）

> @import "common";

####（1）局部文件  _文件名.scss

那些专门为@import命令而编写的时sass文件，并不需要生成对应的独立css文件，这样的sass文件称为局部文件。
sass局部文件的文件名以下划线开头，这样sass就不会在编译时单独编译这个文件输出css，而只把这个文件用作导入。局部文件可以被多个不同的文件引用。

当@import一个局部文件时，还可以不写文件的全名，即省略文件名开头的下划线。比如，想导入themes/_night-sky.scss这个局部文件里的变量，只需在样式表中写@import "themes/night-sky"。

####（2）默认变量值 !default

一般来说，反复声明一个变量，只有最后一处声明有效且会覆盖前边的值。!default标签：如果这个变量被声明赋值了，那就用它声明的值，否则就有这个默认值。（像是css中的!important标签的对立面。）

    $link-color:blue;
$link-color:red !default;

    a {
        color: $link-color;
    }
    
    // 编译结果是
    a {
        color:blue;
    }

####（3）嵌套导入

    // 局部文件 _blue-theme.scss
    aside {
        background: blue;
        color:white;
    }
    
    // 把它导入到一个css规则内：
    .blue-theme {@import "blue-theme"}
    
    // 生成的结果跟直接在.blue-theme选择器内写_blue-theme.scss文件的内容完全一样:
    
    .blue-theme {
        aside {
            background:blue;
            color:white;
        }
    }

<div id="静默注释">

### （四）静默注释 //

不同于css标注注释格式/* ... */，sass提供一种静默注释 //，其内容不会出现在生成的css文件中，以//开头，注释内容直到行末。

<div id="混合器">

### （五）混合器 @mixin @include 

整个网站中基础小小的样式类似（例如一致的颜色和字体），可以使用变量来统一处理；当样式复杂，需要大段的重用样式代码时，则可通过混合器来处理。

混合器用@mixin标识符定义，给一大段样式赋予一个名字，通过@include调用整个名字重用这段样式：

    @mixin rounded-corners {
        -moz-border-radius: 5px;
        -webkit-border-radius: 5px;
        border-radius: 5px;
    }
    
    // 调用 
    notice {
        background-color: green;
        border: 2px solid #00aa00;
        @include rounded-corners;
    }
    
    // 编译后
    
    .notice {
        background-color: green;
        border: 2px solid #00aa00;
        -moz-border-radius: 5px;
        -webkit-border-radius: 5px;
        border-radius: 5px;
    }

#### （1）混合器中的css规则

混合器中不仅可以包含属性，也可以包含css规则：

    @mixin no-bullets {
        list-style: none;
        li {
            list-style-image: none;
            list-style-type: none;
            margin-left: 0px;
        }
    }
    
    ul.plain {
        color: #444;
        @include no-bullets;
    }
    
    // 编译后
    ul.plain {
        color: #444;
        list-style: none;
    }
    ul.plain li {
        list-style-image: none;
        list-style-type: none;
        margin-left: 0px;
    }
    
#### （2）给混合器传参 

可以通过在@include混合器时给混合器传参，来定制混合器生成的精确样式：
    
    @mixin link-colors($normal, $hover, $visited) {
    color: $normal;
    &:hover { color: $hover; }
    &:visited { color: $visited; }
    }
    
    a {
        @include link-colors(blue, red, green);
    }
    
    // 编译后
    a { color: blue; }
    a:hover { color: red; }
    a:visited { color: green; }
    
为了区分每个参数是什么意思，sass允许通过语法$name:value 的形式来指定每个参数的值。这种形式的传参，不必在乎参数顺序，别漏掉参数即可：

    a {
        @include link-colors(
        $normal: blue,
        $visited: green,
        $hover: red
        );
    }

#### （3）默认参数值 

为了在@include混合器时不必传入所有的参数，可以给参数指定一个默认值。
参数默认值使用$name:default-value的声明形式，默认值可以时任何有效的css属性值，甚至是其他参数的引用：

    @mixin link-colors(
        $normal,
    $hover: $normal,
    $visited: $normal
  )
{
    color: $normal;
    &:hover { color: $hover; }
    &:visited { color: $visited; }
    }

    // 若这样调用，则$hover和$visited也会自动赋值为red。
    @include link-colors(red)

<div id="选择器继承">

### （六）选择器继承 @extend 

选择器继承是说一个选择器可以继承为另一个选择器定义的所有样式，通过@extend语法实现：

    //通过选择器继承继承样式
    .error {
        border: 1px solid red;
        background-color: #fdd;
    }
    .seriousError {
        @extend .error;
        border-width: 3px;
    }

在上边的代码中，.seriousError将会继承样式表中任何位置处为.error定义的所有样式。以class="seriousError" 修饰的html元素最终的展示效果就好像是class="seriousError error"。相关元素不仅会拥有一个3px宽的边框，而且这个边框将变成红色的，这个元素同时还会有一个浅红色的背景，因为这些都是在.error里边定义的样式。

.seriousError不仅会继承.error自身的所有样式，任何跟.error有关的组合选择器样式也会被.seriousError以组合选择器的形式继承，如下代码:

    //.seriousError从.error继承样式
    .error a{  //应用到.seriousError a
        color: red;
        font-weight: 100;
    }
    h1.error { //应用到hl.seriousError
        font-size: 1.2rem;
    }

如上所示，在class="seriousError"的html元素内的超链接也会变成红色和粗体。

<div id="参考资料">

## 六、参考资料 

[css预处理器sass使用教程](https://www.cnblogs.com/wuzhiquan/p/5912146.html)

[Sass中文文档](https://www.sass.hk/docs/)

[Sass基础教程](https://www.sass.hk/guide/)

