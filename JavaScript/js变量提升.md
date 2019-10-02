## 1. 什么是变量提升？？？
其实，就是解释器悄咪咪地把定义在方法后面的**变量**或**函数**，提升到最前面
## 2. 那什么时候变量不会提升？！！
JavaScript 只有声明的变量会提升，初始化的不会（也就是说，赋值的不会）

举个栗子：
~~~JavaScript
//实例1
var x = 5; // 初始化 x
var y = 7; // 初始化 y
elem.innerHTML = x + " " + y;           // 显示 x 和 y，结果是5 7

//实例2
var x = 5; // 初始化 x
elem.innerHTML = x + " " + y;           // 显示 x 和 y，结果是5 undefined
var y = 7; // 初始化 y
//为森么y是undefined而不是报错：y is not defined

//实例2相当于下面实例3
var x = 5; // 初始化 x
var y;     // 声明 y
elem.innerHTML = x + " " + y;           // 显示 x 和 y
y = 7;    // 设置 y 为 7，但是没有用（嘻嘻嘻。。）
//因为变量声明 (var y) 提升了，但是初始化(y = 7) 不会提升，
//也就是y不会被赋值，所以 y 变量默认undefined吖
~~~
- 浏览器会先解析脚本，完成一个初始化的步骤
- 遇到 var 变量时会先初始化变量为 undefined
- 变量提升——浏览器遇到 JS 执行环境的初始化，引起变量提前定义
## 3. 听说还有函数提升
两种写法：一种是函数表达式，另外一种是函数声明方式

@重点来啦！！！同上，**只有函数声明形式才能被提升**

po上栗子：
~~~JavaScript
//实例1，函数声明方式提升【成功】
function test(){
    foo();
    function foo(){
        alert("我来自foo");
    }
}
test();

//实例2，函数表达式方式提升【失败】
function test(){
    foo();
    var foo =function foo(){
        alert("我来自foo");
    }
}
test();//报错：TypeError：foo is not a function
~~~
## 4. 怎么防止上面出现的意外嘞？？？
**记住：在每个作用域开始前声明这些变量！！！**
（“噗~~~什么是作用域”  小声嘀咕。。。)

All right . . .下一篇讲一下
[js作用域和作用域链](./js作用域和作用域链.md)
