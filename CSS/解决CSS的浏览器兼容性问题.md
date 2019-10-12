### 文章导航：
[1. 为什么会有浏览器兼容性问题？](#1-为什么会有浏览器兼容性问题)

[2. 如何解决CSS浏览器兼容性问题？](#2-如何解决css浏览器兼容性问题)

[（1）浏览器CSS样式初始化](#1浏览器css样式初始化)

[（2）浏览器私有属性](#2浏览器私有属性)

[（3）自动化插件](#3自动化插件)

[（4）CSS hack](#4CSShack)


## 1. 为什么会有浏览器兼容性问题？

都是浏览器厂商太多的锅！！！Chrome啥时候能够一统江湖啊T~T

关键是不同厂商，甚至同一厂商不同版本，对同一段CSS的解析效果也不一致，这就导致了页面显示效果不统一，也就带来了兼容性问题。

浏览器这么多，我们也不可能每一个都要去兼容，对于用户量一般的产品，把主流浏览器chrome、火狐、ie的适配做好，就已经很不错啦。
## 2. 如何解决CSS浏览器兼容性问题？
解决思路，主要包括4个方面：

浏览器CSS样式初始化、浏览器私有属性，CSS hack语法和自动化插件

### （1）浏览器CSS样式初始化
由于每个浏览器的css默认样式不尽相同，所以最简单有效的方式就是对其进行初始化，以防不同浏览器的显示效果不一样。

例如，在所有CSS开始前，先把marin和padding都设为0。
### （2）浏览器私有属性

在某个CSS的属性前添加一些前缀，比如-webkit-，-moz- ，-ms-，这些就是浏览器的私有属性。

**为什么会出现私有属性呢？**

这是因为制定HTML和CSS标准的组织W3C动作很慢，提出一个新属性要制定标准，走很复杂的程序。而浏览器商市场推广时间紧，如果一个属性已经够成熟了，就会在浏览器中加入支持。为避免日后W3C公布标准时有所变更，会加入一个私有前缀，等到日后W3C公布了标准写法，再让新版的浏览器支持这种写法。

**常用的私有属性前缀有：**

* -moz代表firefox
* -ms代表IE浏览器
* -webkit代表chrome、safari
* -o代表opera

对于私有属性的顺序要注意：**把标准写法放到最后，兼容性写法放到前面**
```css
 -webkit-transform:rotate(-3deg); /*为Chrome/Safari*/
 -moz-transform:rotate(-3deg); /*为Firefox*/
 -ms-transform:rotate(-3deg); /*为IE*/
 -o-transform:rotate(-3deg); /*为Opera*/
 transform:rotate(-3deg);
 ```
每个CSS属性写这么一堆兼容性代码，无疑是对生命最大的浪费，后面讲一下通过**自动化插件**来处理这块
### （3）自动化插件
Autoprefixer是一款自动管理浏览器前缀的插件，它可以解析CSS文件并且添加浏览器前缀到CSS内容里，使用Can I Use（caniuse网站）的数据来决定哪些前缀是需要的。

把Autoprefixer添加到资源构建工具（例如Grunt）后，可以完全忘记有关CSS前缀的东西，只需按照最新的W3C规范来正常书写CSS即可。如果项目需要支持旧版浏览器，可修改browsers参数设置 。
```css
//我们编的代码
div {
 transform: rotate(30deg);
}

// 自动补全的代码，具体补全哪些由要兼容的浏览器版本决定，可以自行设置
div {
 -ms-transform: rotate(30deg);
 -webkit-transform: rotate(30deg);
 -o-transform: rotate(30deg);
 -moz-transform: rotate(30deg);
 transform: rotate(30deg);
}
```
### （4）CSS hack

有时需要针对不同的浏览器或不同版本写特定的CSS样式，这种过程叫做CSS hack

**CSS hack的写法**大致归纳为3种：**条件hack**、**属性级hack**、**选择符级hack**
* 条件hack(针对IE浏览器进行一些特殊的设置)
```css
<!--[if <keywords>? IE <version>?]>
 代码块，可以是html，css，js
<![endif]-->
/*
if后面跟的条件共包含6种选择方式：
是否、大于、大于或等于、小于、小于或等于、非指定版本

1.是否：指定是否IE或IE某个版本。关键字：空

2.大于：选择大于指定版本的IE版本。关键字：gt（greater than）

3.大于或等于：选择大于或等于指定版本的IE版本。关键字：gte（greater than or equal）

4.小于：选择小于指定版本的IE版本。关键字：lt（less than）

5.小于或等于：选择小于或等于指定版本的IE版本。关键字：lte（less than or equal）

6.非指定版本：选择除指定版本外的所有IE版本。关键字：!

version是IE浏览器版本，如6、7、8

IE10及以上版本已将条件注释特性移除，使用时需注意。
*/

<!--[if IE]>
 <p>你在非IE中将看不到我的身影</p>
<![endif]-->
```
* 属性级hack(在CSS样式属性名前加上一些只有特定浏览器才能识别的hack前缀)
```css
 selector{<hack>?property:value<hack>?;}
/*如在不同的IE浏览器中设置不同的颜色，注意顺序：低版本的兼容性写法放到最后*/
.test {
 color: #0909; /* For IE8+ */
 *color: #f00; /* For IE7 and earlier */
 _color: #ff0; /* For IE6 and earlier */
}
 ```
* 选择符级hack(针对一些页面表现不一致或者需要特殊对待的浏览器，在CSS选择器前加上一些只有某些特定浏览器才能识别的前缀进行hack)
```css
<hack> selector{ sRules }
/*
常见的选择符级hack有：
1. *html *前缀只对IE6生效
2. *+html *+前缀只对IE7生效
@media screen\9{...}只对IE6/7生效
@media \0screen {body { background: red; }}只对IE8有效
@media \0screen\,screen\9{body { background: blue; }}只对IE6/7/8有效
@media screen\0 {body { background: green; }} 只对IE8/9/10有效
@media screen and (min-width:0\0) {body { background: gray; }} 只对IE9/10有效
@media screen and (-ms-high-contrast: active), (-ms-high-contrast: none) {body { background: orange; }} 只对IE10有效
*/

* html .test { color: #090; } /* For IE6 and earlier */
* + html .test { color: #ff0; } /* For IE7 */
```
