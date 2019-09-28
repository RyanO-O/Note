## new对象的四个过程
1. 创建一个新对象
2. 将构造函数的作用域赋给新对象（因此 this 就指向了这个新对象）
3. 执行构造函数中的代码（为这个新对象添加属性）
4. 返回新对象
    ~~~javascript
    function foo(name, age) {
	    this.name = name;
	    this.age = age;
    }
    var person = new foo("Ryan", 20);
- 创建一个空对象 var obj = new Object();
- 让foo中的this指向obj，并执行其函数体  var result = foo.call(obj);
- 设置原型链，将obj的__proto__成员指向foo函数对象的prototype成员对象
obj.__proto__ = foo.prototype;
- 判断foo的返回值类型，如果是值类型，返回obj；
如果是引用类型，就返回这个引用类型的对象。
    ~~~javascript
    if (typeof(result) == "object") 
	    person = result;  
    else
	    person = obj;