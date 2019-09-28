## ES6是什么
- ECMA和js的关系：ECMA是标准，Javascript是ECMA的实现。
- js是一种语言，但凡语言都有一套标准，而ECMA就是javascript的标准。
- ES6（ECMAscript6.0）在2015年正式发布，又称为ECMAscript2015。
## 1. let、const
- ES6之前，定义变量都是使用var，但var存在一些问题，比如：可以重复声明，仅支持函数作用域。所以es6设计了let和const来弥补不足
- let表示变量、const表示常量，let和const**不能重复声明**，都是**块级作用域**
- 通常来说{}大括号内的代码块即为let和const的作用域
- const 声明的变量被认为是常量，表示它的值被设置完成后就不能再修改。
- 如果const的是一个对象，对象所包含的值是可以被修改的。只要对象所指向的地址没有变就行。
## 2. 箭头函数（函数的简写）
- 可以省略function
- 同名的函数可以省略不写
- 省略 return 关键字
- 继承当前上下文的 this 关键字
~~~javascript
let a = (arg)=>{ //  这里=>符号就相当于function关键字
    return arg+=1
}
// 也可以简写为
let a = arg => arg+=1
~~~
## 3. 解构赋值
**为了简化提取信息，ES6新增了解构，这是将一个数据结构分解为更小的部分的过程**
解构赋值必须符合下面三条规则：
- 左右结构必须一样
- 右边必须是一个合法的数据
- 声明和赋值必须一句话完成，不能把声明与赋值分开
~~~javascript
var [a,b] = [1,2]

let [a, b] = [1, 2]                // 左右都是数组，可以解构赋值
let {a, b} = {a:1, b:2}            // 左右都是对象，可以解构赋值
let [obj, arr] = [{a:1}, [1, 2]]   // 左右都是对象，可以解构赋值

let [a, b] = {a:1, b:2}            // err 左右结构不一样，不可以解构赋值
let {a,b} = {1, 2}                 // err 右边不是一个合法的数据，不能解构赋值

let [a, b];
[a, b] = [1, 2]                    // err 声明与赋值分开，不能解构赋值
~~~
## 4. 模板字符串
1.  基本的字符串格式化

**将表达式嵌入字符串中进行拼接。用${}来界定。**
~~~javascript
//ES5
var way = 'String'
console.log('ES5:' + way)

//ES6
let way = 'String Template'
console.log(`ES6: ${way}`)
~~~
2. 多行字符串拼接

**ES5通过反斜杠拼接(多行)字符串,ES6用反引号``**
~~~javascript
let name = 'Jone'
`hello ${name},
how are you
`
~~~
3. startsWith(), endsWith(), includes()
- startsWith() 表示参数字符串是否在原字符串的头部，返回布尔值
- endsWith() 表示参数字符串是否在原字符串的尾部，返回布尔值
- includes() 表示是否在原字符串找到了参数字符串，返回布尔值
~~~javascript
let s = 'Hello world!';
//第二个参数，表示开始搜索的位置
s.startsWith('world', 6) // true
s.endsWith('Hello', 5) // true
s.includes('Hello', 6) // false
~~~
## 5. Spread Operator 展开运算符
**三个点（...），它可以组装对象或者数组**
~~~javascript
// 将一个数组拆分为参数序列
let arr = [1,2]
function add (a,b) {
    return a+b
}
add(...arr)

// 收集剩下的所有的参数
function f(a, ...arr) {
    console.log(...arr) // 2 3
}
f(1,2,3)

// 用于数组复制
let arr1 = [1,2]
let arr2 = [...arr1] // 或者let [...arr2] = arr1
~~~
## 6. 面向对象 class
通过class关键字，可以定义类
~~~javascript
class User {
    constructor(name) {          // 构造器，相当于es5中的构造函数
        this.name = name         // 实例属性
    }
    showName(){                  // 定义类的方法，不能使用function关键字，不能使用逗号分隔
        console.log(this.name)   
    }
}
var foo = new User('foo')
~~~
1. constructor
    
    - es6中class类专用的构造器，相当于之前定义的构造函数，每个类都必须有constructor，如果没有则自动添加一个空的constructor构造器。
    - 创建实例的时候自动执行constructor函数
constructor中的this指向实例，并且默认返回this（实例）
2. class类的prototype
    - class的基本类型就是函数（typeof User = "function"），既然是函数，那么就会有prototype属性。
    - 类的所有方法都是定义在prototype上
~~~javascript
class User {
  constructor() {
    // ...
  }

  toString() {
    // ...
  }

  toValue() {
    // ...
  }
}
User.toValue()             // err User.toValue is not a function
User.prototype.toValue()   // 可以调用toValue方法

// 等同于

User.prototype = {
  constructor() {},
  toString() {},
  toValue() {},
};
~~~
3. 类的实例
    - 类的实例只能通过new来创建
    - 除了静态方法，定义在类上的所有的方法都会被实例继承
    - 除非定义在类的this对象上才是实例属性，否则都是定义在类的原型（prototype）上
~~~javascript
class Point {

  constructor(x, y) {
    this.x = x;
    this.y = y;
  }

  toString() {
    return '(' + this.x + ', ' + this.y + ')';
  }

}

var point = new Point(2, 3);

point.toString() // (2, 3)

point.hasOwnProperty('x') // true
point.hasOwnProperty('y') // true
point.hasOwnProperty('toString') // false
point.__proto__.hasOwnProperty('toString') // true
~~~
4. 静态方法
    - 如果在类中定义一个方法的前面加上static关键字，就表示定义一个静态方法
    - 静态方法不会被实例继承，但会被子类继承
    - 不能通过实例使用静态方法，而是通过类直接调用
~~~javascript
class User {
    constructor(name){
        this.name = name
    }
    static show(){
        console.log('123')
    }
}
class VipUser extends User{}
VipUser.show()                    // 123
User.show()                       // 123
var foo = new User('foo')
foo.show()                        // foo.show is not a function
~~~
5. 静态属性
    - class的静态属性指的是 Class 本身的属性，
    - 目前只能通过Class.propName定义静态属性
    - 静态属性可以被子类继承，不会被实例继承
~~~javascript
class User{}
User.name = 'foo' // 为class定义一个静态属性

class VipUser extends User{}
console.log(VipUser.name)         // foo

var foo = new User()
console.log(foo.name)             // undefined
~~~
## 7. 类的继承

**class通过extends关键字实现继承**
1. super
    - super可以当做函数使用，也可以当做对象使用。
    - ES6规定，在子类中使用super对象调用父类方法时，方法内部的this指向子类

2. 类的prototype和__proto__属性
    - es5中每一个对象都有__proto__属性，指向对应构造函数的prototype属性。
    - Class 作为构造函数的语法糖，同时有prototype属性和__proto__属性，因此同时存在两条继承链。
    - 子类的__proto__属性，表示构造函数的继承，总是指向父类。
    - 子类prototype属性的__proto__属性，表示方法的继承，总是指向父类的prototype属性。

3. 实例的__proto__属性
    - 子类实例的__proto__属性指向子类的原型（子类的prototype）
    - 子类实例的__proto__属性的__proto__属性指向父类的原型（父类的prototype）

## 8. 对象
1. 对象的扩展运算符 ...（可以把对象可枚举的属性拆分为键值对序列）
~~~javascript
//用于对象拷贝
let obj1 = {a:1,b:2}
let obj2 = {...obj1}
console.log(obj2)   // {a:1,b:2}
//用于合并对象
let obj1 = {a:1,b:2}
let obj2 = {c:3,d:4}
let obj3 = {a:100, ...obj1, ...obj2, e:5, f:6}  // {a: 1, b: 2, c: 3, d: 4, e: 5, f: 6}
let obj4 = { ...obj1, ...obj2, e:5, f:6, a:100} // {a: 100, b: 2, c: 3, d: 4, e: 5, f: 6}
//如果后面的属性和前面的属性key相同，则会覆盖前面的值
~~~
2. Object.assign

    - 用于对象的合并，将源对象的所有可枚举属性，拷贝(浅拷贝)到目标对象
    - 若目标对象与源对象有同名属性，或多个源对象有同名属性，后覆盖前
~~~javascript
const target = { a: 1 };

const source1 = {a: 100, b: 2 };
const source2 = { c: 3 };

Object.assign(target, source1, source2);
target // {a:100, b:2, c:3}

~~~
3. Object.keys()，Object.values()，Object.entries()

    作为遍历一个对象的补充手段，供for...of循环使用。
~~~javascript
Object.keys() 返回一个数组，成员是参数对象所有可枚举的属性的键名
var obj = { foo: 'bar', baz: 42 };
Object.keys(obj) // ["foo", "baz"]
Object.values() 返回一个数组，成员是参数对象所有可枚举属性的键值。
const obj = { 100: 'a', 2: 'b', 7: 'c' };
Object.values(obj)  // ["b", "c", "a"]
Object.entries() 返回一个数组，成员是参数对象所有可枚举属性的键值对数组。
const obj = { foo: 'bar', baz: 42 };
Object.entries(obj)  // [ ["foo", "bar"], ["baz", 42] ]
~~~
## 9. Generator函数
- 可理解为**生成器**，和普通函数没多大区别，普通函数是只要开始执行，就一直执行到底，而Generator函数是中间可以停，搭配使用next函数继续执行，像挤牙膏

- 最直观的表现就是比普通的function多了个星号*，在其函数体内可以使用yield关键字，有函数会在每个yield后暂停。

     ###   另外：**迭代器**

- 当你调用一个generator时，它将返回一个迭代器对象。
- 这个迭代器对象拥有一个叫做next的方法来帮助你重启generator函数并得到下一个值。
- next方法不仅返回值，它返回的对象具有两个属性：done和value。
value是你获得的值，done用来表明你的generator是否已经停止提供值。

那生成器和迭代器又有什么用处呢？

围绕着生成器的许多兴奋点都与异步编程直接相关。异步调用对于我们来说是很困难的事，我们的函数并不会等待异步调用完再执行，你可能会想到用回调函数，（当然还有其他方案比如Promise比如Async/await）。

生成器可以让我们的代码进行等待。就不用嵌套的回调函数。使用generator可以确保当异步调用在我们的generator函数运行一下行代码之前完成时暂停函数的执行。

生成器与迭代器最有趣、最令人激动的方面，或许就是可创建外观清晰的异步操作代码。你不必到处使用回调函数，而是可以建立貌似同步的代码，但实际上却使用 yield 来等待异步操作结束。

9. async await
async其实就是对Generator的封装，只不过async可以自动执行next()。

async function read () {
    let data1= await new Promise(resolve => {
        resolve('100')
    })
    let data2 = await 200
    
    return 300
}
(1)async 返回值
async默认返回一个Promise，如果return不是一个Promise对象，就会被转为立即resolve的Promise，可以在then函数中获取返回值。

async必须等到里面所有的await执行完，async才开始return，返回的Promise状态才改变。除非遇到return和错误。

async function fn () {
    await 100
    await 200
    return 300
}
fn().then(res => {
    console.log9(res) // 300
})
(3)await
await也是默认返回Promise对象，如果await后面不是一个Promise对象，就会转为立即resolve的Promise

如果一个await后面的Promise如果为reject，那么整个async都会中断执行，后面的awiat都不会执行，并且抛出错误，可以在async的catch中捕获错误

async function f() {
  await Promise.reject('error');
  await Promise.resolve('hello world'); // 不会执行
}
f().then(res =>{

}).catch(err=>{
    console.log(err)  // error
})
如果希望一个await失败，后面的继续执行，可以使用try...catch或者在await后面的Promise跟一个catch方法：

// try...catch
async function f() {
  try {
    await Promise.reject('出错了');
  } catch(e) {
  }
  return await Promise.resolve('hello world');
}

f()
.then(v => console.log(v))   // hello world

// catch
async function f() {
  await Promise.reject('出错了')
    .catch(e => console.log(e));   // 出错了
  return await Promise.resolve('hello world');
}

f()
.then(v => console.log(v))  // hello world