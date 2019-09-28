## 1. this 的指向
**this 永远指向最后调用它的那个对象**
## 2. 改变 this 的指向
- 使用 ES6 的箭头函数
- 在函数内部使用 _this = this
- 使用 apply、call、bind
- new 实例化一个对象

1. **箭头函数语法比函数表达式更短，并且不绑定自己的this**

    箭头函数没有 this，所以也不能用 call()、apply()、bind() 方法改变 this 的指向。

    需要通过查找作用域链来确定 this 的值，如果箭头函数被非箭头函数包含，this 绑定的就是最近一层非箭头函数的 this。

2. **在函数内部使用 _this = this**

    先将调用这个函数的对象保存在变量 _this 中，然后在函数中都使用这个 _this
    ~~~javascript
    var name = "windows";
    var a = {
        name : "Ryan",
        foo1: function () {
            console.log(this.name)
        },
        foo2: function () {
            var _this = this;
            setTimeout( function() {
                _this.foo1()
            },100);
        }
    };
    a.foo2()       // Ryan
    //在 foo2 中，首先设置 var _this = this;（this 是调用 foo2 的对象 a）
      为了防止在 foo2 中的 setTimeout 被 window 调用而导致 this 为 window
      将 this(指向变量 a) 赋值给一个变量 _this，这样，在 foo2 中我们使用 _this 就是指向对象 a
3. **使用 apply、call、bind改变 this 的指向**
    - apply调用一个函数, 其具有一个指定的this值，还有数组参数
    - call 接受的是若干个参数列表
    - bind 创建一个新的函数，必须要手动调用
4. **用new调用函数，改变指向new的实例对象**
    ~~~javascript
    function foo1(){
        this.name = "Ryan";
    }
    var foo2 = new foo1();
    console.log(foo1.name);