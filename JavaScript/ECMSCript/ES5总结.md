### 文章导航：
[1.ES5是ECMAScript标准最新修正](#1es5是ecmascript标准最新修正)

[2.JSON对象](#2json对象)

[3.object对象方法扩展](#3object对象方法扩展)

[4.数组扩展](#4数组扩展)

[5.Function(函数)扩展](#5function函数扩展)
## 1.ES5是ECMAScript标准最新修正
+ ES5通过对现有JS方法添加语句和原生ECMAScript对象做合并实现标准化。
+ ES5还引入了一个语法的严格变种，被称为”严格模式(strict mode)”。
    
    1.理解”严格模式”： 这种模式使得Javascript在更严格的语法条件下运行。
    
    2.目的/作用：
    - 消除Javascript语法的一些不合理、不严谨之处，减少一些怪异行为
    - 消除代码运行的一些不安全之处，为代码的安全运行保驾护航
    - 为未来新版本的Javascript做好铺垫

    3.使用：在全局或函数的第一条语句定义为: 'use strict';

    4.语法和行为改变：
    - 必须用var声明变量（没有用var，默认是window全局变量，会污染代码）
    - 禁止自定义的函数中的this指向window（当前自定义的this对象指向window，需要加个new，让this指向实例对象）
    - 创建eval作用域（eval是个函数，能解析里边的字符串，例如：var str=‘hhh’ eval（‘elert（str）’）；不使用严格模式的话，eval没有自己的作用域，在里边声明的变量，相当于在全局声明，会覆盖原有的变量的声明。严格模式创建eval作用域，避免污染全局。
    - 对象不能有重名的属性
    - 函数不能有重名的形参
## 2.JSON对象
1. JSON.stringify(obj/arr) —— js对象(数组)转换为json对象(数组)
2. JSON.parse(json) —— json对象(数组)转换为原生js对象(数组)

    - JSON是数据传输的格式。服务器发送给我们的很可能是一长串普通的字符串，里面包含了多个数据，无法对数据进行分类，并不能直接使用。

    - 因此我们需要的是JSON的对象（数组）可以与原生的对象和数组进行转化，即，一一对应的关系。（对象(数组)都是用来保存数据的。）
    ~~~ javascript
    <script type="text/javascript">
    var obj = {
        name : 'Ryan'
    };
    obj = JSON.stringify(obj);
    console.log( typeof obj);//结果为：string
    obj = JSON.parse(obj);
    console.log(obj);//结果为：object
    </script>
## 3.object对象方法扩展
1. Object.create(prototype[, descriptors]) :创建一个新的对象

    （1）以指定对象（prototype）为原型创建新的对象

    （2）指定新的属性, 并对属性进行描述

    - value : 指定值

    - writable : 标识当前属性值是否可修改, 默认为false

    - configurable : 标识当前属性值是否是可删除, 默认为false

    - enumerable : 标识当前属性值是否可用for in枚举, 默认为false
    ~~~javascript
    <script type="text/javascript">
	var obj = {username: 'Ryan' }//属性可继承
	var obj1 = {};
	obj1 = Object.create(obj);//obj1原是空对象，通过Object.create(obj)，_proto_继承obj的属性
	console.log(obj1);
    </script>

    //可以给当前的对象(obj1)扩展属性
    obj1 = Object.create(obj , {
		age: {
			value: 18，
            writable：true，//设为true，属性值才能在外部被更改
            configurable：true
		}
	});
    obj1.age = 20;          //需要指定writable: true才能修改成功
    console.log(obj1.age);  //成功返回20
    delete obj1.seagex;     //需要指定configurable: true才能删除成功
    for (var i in obj1){
        console.log(i);     //需要指定enumerable: 才能枚举扩展的属性age
    }
2. Object.defineProperties(object,descriptors)：为指定object对象定义扩展多个属性
    - get：用来获取当前属性值的回调函数，获取扩展属性值时get方法自动调用
    - set：监听当前属性值的触发的回调函数，扩展属性变化时会自动调用，后会将变化的值作为实参注入到set函数
    - 存取器属性：setter，getter一个用来存值一个用来取值
    ~~~javascript
    <script type="text/javascript">
	var obj2 = {firstName: 'Taylor' , lastName: 'Swift'};
	Object.defineProperties(obj2 , {
		fullName: {//方法实际上是指定的对象obj2去调用
			get: function () {//获取扩展属性fullName的值
				return this.firstName + ' ' + this.lastName;
			},
			set: function (data) {//修改当前属性值，这里的data为'Justin Biber'
				console.log(data);//仍输出Taylor Swift
				//修改不了扩展属性(fullName)的值，但能去修改原来属性的值
				var names = data.split(' ');//将'Justin Biber'拆分为数组
				//指定对象obj2调用方法，从原来的属性中获取相应的值
				this.firstName = names[0];//值为：Justin
				this.lastName = names[1];//值为：Biber
			}
		}
	})
    /* 当没有以下代码时，不会自动调用get/set方法 */
	console.log(obj2.fullName);     //获取扩展属性值，自动调用get方法，输出Taylor Swift
	obj2.fullName = 'Justin Biber'; //监听扩展属性值，自动调用set方法;
                                    //fullName是扩展属性，无法进行修改，传入实参'Justin Biber'
	console.log(obj2.fullName);//再次获取扩展属性值，再次自动调用get方法，输出Justin Biber
    </script>

 3. 对象本身的两个方法
    - get propertyName(){} 用来得到当前属性值的回调函数
    - set propertyName(){} 用来监视当前属性值变化的回调函数
    ~~~javascript
    <script type='text/javascript'>
    var obj = {
        firstName : 'Taylor',
        lastName : 'Swift',
        get fullName(){          //fullName是根据已有的值动态计算出来的
            return this.firstName + ' ' + this.lastName
        },
        set fullName(data){     //通过get方法拿到的属性值，没有办法直接修改，需要用set方法
            var names = data.split(' ');
            this.firstName = names[0];
            this.lastName = names[1];
        }
    };
    console.log(obj.fullName);//结果为Taylor Swift
    obj.fullName = 'Justin Biber';
    console.log(obj.fullName);//结果为Justin Biber
    </script>
## 4.数组扩展
1. Array.prototype.indexOf(value) : 得到值在数组中的第一个下标
2. Array.prototype.lastIndexOf(value) : 得到值在数组中的最后一个下标
3. Array.prototype.forEach(function(item, index){}) : 遍历数组
4. Array.prototype.map(function(item, index){}) : 遍历数组返回一个新的数组，返回加工之后的值
5. Array.prototype.filter(function(item, index){}) : 遍历过滤出一个新的子数组， 返回条件为true的值
## 5.Function(函数)扩展
1. 在不传参的情况下，call、apply的使用方法一样
2. 传入参数的情况下，call直接接后边传，apply放到数组里传
3. call、apply绑定this的特点：立即调用函数
    ~~~javascript
    <script type="text/javascript">
	var obj = {username: 'Ryan'};
	function foo() {
		console.log(this);
	}
	foo();               //this对象是window，要指定obj对象，需要强行绑定

    //不传参的情况下：
	foo.call(obj);       //结果为{username: "Ryan"}
    foo.apply(obj);      //结果为：{username: "Ryan"} undefined

    //传参的情况下：
	foo.call(obj , 7);   //call 直接从第二个参数开始，依次传参，结果为：{username: "Ryan"} 7
	foo.apply(obj , 7);  //报错，apply 第二参数必须是数组，传入的参数放在数组中
	foo.apply(obj , [7]);//结果为：{username: "Ryan"} 7
4. bind绑定this的特点：
    - bind 传参的方法同call一样
    - 绑定完this不会立即调用当前的函数，而是将函数返回
    - bind通常指定回调函数的this（回调函数：函数作为参数传入到另一个函数）
~~~javascript
	foo.bind(obj);//无输出，本质原因是foo函数未调用
	foo.bind(obj)();//不需要用var定义，直接调用;结果为：{username: "Ryan"} undefined
	foo.bind(obj , 7)();//结果为：{username: "Ryan"} 7

	setTimeout(function () {
		console.log(this);//结果为：{username: "Ryan"}
	}.bind(obj), 1000)//bind将this由window改为obj
