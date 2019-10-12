### 文章导航：
[1. 边框](#1-边框)

[2. 背景](#2-背景)

[3. 字体](#3-字体)

[4. 2D转换](#4-2d转换)

[5. 3D转换](#5-3d转换)

[6. 过渡](#6-过渡)

[7. 动画](#7-动画)

[8. 双倍浮动bug](#8-双倍浮动bug)

[9. 表单元素行高不一致](#9-表单元素行高不一致)

[10. IE6（默认16px为最小）不识别较小高度的标签（一般为10px）](#10-ie6默认16px为最小不识别较小高度的标签一般为10px)

[11. 图片添加超链接时，在IE浏览器中会有蓝色的边框](#11-图片添加超链接时在ie浏览器中会有蓝色的边框)

[12. 最小高度min-height不兼容IE6](#12-最小高度min-height不兼容ie6)

[13. 图片默认有间隙](#13-图片默认有间隙)

[14. 按钮默认大小不一](#14-按钮默认大小不一)

[15. 百分比bug](#15-百分比bug)

[16. 鼠标指针bug](#16-鼠标指针bug)

[17. 透明度设置，IE不识别opacity属性](#17-透明度设置ie不识别opacity属性)

[18. 上下margin重叠问题](#18-上下margin重叠问题)

[19. 给子元素设置margin-top，应用在了父元素上](#19-给子元素设置margin-top应用在了父元素上)

[20. div的垂直居中问题](#20-div的垂直居中问题)

[21. margin加倍的问题](#21-margin加倍的问题)

[22. DIV浮动IE文本产生3象素的bug](#22-div浮动ie文本产生3象素的bug)

[23. float的清除浮动、自适应高度、排版、div闭合](#23-float的清除浮动自适应高度排版div闭合)

[24. IE6下图片有空隙产生](#24-ie6下图片有空隙产生)

[25. 对齐文本与文本输入框](#25-对齐文本与文本输入框)

[26.  li中内容超过长度后以省略号显示的方法](#26--li中内容超过长度后以省略号显示的方法)

[27. 无法定义1px左右高度的容器](#27-无法定义1px左右高度的容器)
### 1. 边框
* border-radius: 最低兼容至 IE9,其它浏览器兼容情况优良。
* box-shadow: 最低兼容至IE9, 其它浏览器兼容情况优良。
### 2. 背景

* background-size: 最低兼容至IE9, 其它浏览器兼容情况优良。

### 3. 字体

* @font-face: IE9及以上版本的IE浏览器，支持引入任何格式的字体文件，而在IE9之前的浏览器，只支持引入EOT格式的字体文件。 其它浏览器兼容情况优良。

### 4. 2D转换

* transform: 最低兼容至IE9（需要添加-ms-前缀），其它浏览器兼容情况优良。

    在transform属性前加入浏览器内核前缀是很好的实践。不建议在svg元素上使用transform属性，最新版本的IE并不支持这一使用方式。

### 5. 3D转换

* IE10 和 Firefox 支持 3D 转换。Chrome 和 Safari 需要前缀 -webkit-。Opera 仍然不支持 3D 转换，它只支持2D 转换。

### 6. 过渡

* transition:最低兼容至IE10，其它浏览器兼容情况优良。

    Safari浏览器需要前缀-webkit-，其它大部分浏览器对此并未有前缀要求，因此除了特殊情况，可以不添加其它浏览器的前缀。

### 7. 动画

* animation:兼容情况与transition属性大致相同。

### 8. 双倍浮动bug
（块状元素设置了float属性后，又设置了横向的margin值，在IE6下显示的margin值要比设置的值大）

* 给float的元素添加 display:inline;将其转换为内联元素；

### 9. 表单元素行高不一致

* 给表单元素添加vertical-align:middle;

* 给表单元素添加float:left；

### 10. IE6（默认16px为最小）不识别较小高度的标签（一般为10px）
* 给标签添加overflow:hidden;
* 给标签添加font-size:0;

### 11. 图片添加超链接时，在IE浏览器中会有蓝色的边框
* 给图片添加border:0或者border：none;

### 12. 最小高度min-height不兼容IE6
* min-height:100px;_height:100px;
* min-height:100px;height:auto!important;height:100px;
### 13. 图片默认有间隙
* 给img添加float属性；
* 给img添加display：block;
### 14. 按钮默认大小不一
* 如果按钮是一张图片，直接用背景图作为按钮图片；
* 用a标记模拟按钮，使用JS实现其他功能；
### 15. 百分比bug
（父元素设置100%，子元素各50%，在IE6下，50%+50%>100%）
* 给右边的浮动元素添加clear:right；
### 16. 鼠标指针bug
* cursor:hand 只有IE浏览器识别；
* cursor:pointer;IE及以上浏览器和其他浏览器都识别（手型）；

### 17. 透明度设置，IE不识别opacity属性
* 标准写法：opacity:value;(取值范围0-1)；
* 兼容IE浏览器 filter:alpha(opacity=value);(取值范围1-100)；
### 18. 上下margin重叠问题
(给上面的元素设置margin-bottom，给下面的元素设置margin-top,只能识别其中较大的那个值)
* margin-top和margin-bottom 只设置其中一个值；
* 给其中一个元素再包裹一个盒子，并设置over-flow:hidden;
### 19. 给子元素设置margin-top，应用在了父元素上
* top改为给父元素设置padding-top;
* 给父元素设置1px的border,即border-top:1px solid transparent;
* 给父元素设置over-flow:hidden;
* 给父元素设置float:left；
### 20. div的垂直居中问题
* vertical-align:middle; 将行距增加到和整个div一样高
* line-height:200px; 然后插入文字，就垂直居中了。缺点是要控制内容不要换行
### 21. margin加倍的问题
（设置为float的div在ie下设置的margin会加倍。这是一个ie6都存在的bug）
* 在这个div里面加上 display:inline;
### 22. DIV浮动IE文本产生3象素的bug
（左边对象浮动，右边采用外补丁的左边距来定位，右边对象内的文本会离左边有3px的间距
```css
<div id="box">
    <div id="left"></div>
    <div id="right"></div>
</div>

#box{ float:left; width:800px;}
#left{ float:left; width:50%;}
#right{ width:50%;}
*html #left{ margin-right:-3px; //这句是关键}
```
### 23. float的清除浮动、自适应高度、排版、div闭合
1. 清除浮动：
```css
<#div id=”floatA” >
<#div id=”floatB” >
<#div id=” NOTfloatC” >
/*
这里的NOTfloatC并不希望继续平移，而是希望往下排。
(其中floatA、floatB的属性已经设置为 float:left;)
这段代码在IE中毫无问题，问题出在FF。

原因是NOTfloatC并非float标签，必须将float标签闭合。
在 <#div class=”floatB”>
<#div class=”NOTfloatC”>
之间加上 < #div class=”clear”>

这个div一定要注意位置，而且必须与两个具有float属性的div同级，
之间不能存在嵌套关系，否则会产生异常。
并且将clear这种样式定义为为如下即可：
.clear{ clear:both;}*/
```
2. 自适应高度

* 作为外部 wrapper 的 div 不要定死高度
* 为了让高度能自动适应，要在wrapper里面加上overflow:hidden;
* 当包含float的 box的时候，高度自动适应在IE下无效
* 这时候应该触发IE的layout私有属性，用zoom:1;可以做到，这样就达到了兼容。
```css
.colwrapper{ overflow:hidden; zoom:1; margin:5px auto;}
```
3. 排版
* 用得最多的css描述可能就是float:left；
* 有时候我们需要在n栏的float div后面做一个统一的背景,例如:
```css
<div id=”page”>
    <div id=”left”></div>
    <div id=”center”></div>
    <div id=”right”></div>
</div>
/*
比如我们要将page的背景设置成蓝色,以达到所有三栏的背景颜色是蓝色的目的,
但是我们会发现随着left center right的向下拉长,page居然保存高度不变,
问题来了,原因在于page不是float属性,而我们的page由于要居中,不能设置成float,
所以我们应该再嵌入一个float left，而宽度是100%的div解决*/
<div id=”page”>
    <div id=”bg” style=”float:left;width:100%”>
        <div id=”left”></div>
        <div id=”center”></div>
        <div id=”right”></div>
    </div>
</div>
```
4. 万能float 闭合(非常重要!)

将以下代码加入公共的 CSS 中，给需要闭合的div加上 class="clearfix" 即可
```css
.clearfix:after {
    content:".";
    display:block;
    height:0;
    clear:both;
    visibility:hidden;
    }
.clearfix {
    display:inline-block;
    }
.clearfix {display:block;}
/*或者这样设置：*/
.hackbox{ display:table; //将对象作为块元素级的表格显示
}
```
### 24. IE6下图片有空隙产生
* 改变html的排版
* 或者设置img 为display:block
* 或者设置vertical-align 属性为
```css
vertical-align:top/bottom/middle/text-bottom
```
### 25. 对齐文本与文本输入框
* 加上 vertical-align:middle;
### 26.  li中内容超过长度后以省略号显示的方法
* 此方法适用与IE与OP浏览器
```css
li {
    width:200px;
    white-space:nowrap;
    text-overflow:ellipsis;
    -o-text-overflow:ellipsis;
    overflow: hidden;
    }
```
### 27. 无法定义1px左右高度的容器
IE6下这个问题是因为默认的行高造成的，解决方法：
```css
1. overflow:hidden；
2. zoom:0.08；
3. line-height:1px；
```