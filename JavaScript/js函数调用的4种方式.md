## 1. 作为函数调用
**当函数没有被自身的对象调用时 this 的值就会变成全局对象**
~~~javascript
    function myFunction(a, b) {
        return a * b;
    }
    myFunction(10, 2);           // myFunction(10, 2) 返回 20
~~~
## 2. 作为方法调用
- 方法：当一个函数被保存为对象的一个属性时
- 当一个方法被调用时，this 被绑定到该对象。
- 若调用表达式包含一个提取属性的动作（.xx），那么它就被当做一个方法来调用
~~~javascript
    var myObject = {
        firstName:"John",
        lastName: "Doe",
        fullName: function () {
            return this.firstName + " " + this.lastName;
        }
    }
    myObject.fullName();         // 返回 "John Doe"
~~~
## 3. 使用构造函数调用函数
- 如果函数调用前使用了 new 关键字, 则是调用了构造函数。
- 构造函数的调用会创建一个新的对象。新对象会继承构造函数的属性和方法。
~~~javascript
    function myFunction(arg1, arg2) {
        this.firstName = arg1;
     this.lastName  = arg2;
    }
    var x = new myFunction("John","Doe");
    x.firstName;                // 返回 "John"
~~~
## 4. 作为函数方法调用函数
**通过 call() 或 apply() 方法你可以设置 this 的值, 且作为已存在对象的新方法调用**
