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
## 6. class类使用详解
1. 通过class定义类/实现类的继承
2. 在类中通过constructor定义构造方法
3. 通过new来创建类的实例
4. 通过extends来实现类的继承
5. 通过super调用父类的构造方法
6. 重写从父类中继承的一般方法
## 7. 对象
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
## 8. Generator函数
- 可理解为**生成器**，和普通函数没多大区别，普通函数是只要开始执行，就一直执行到底，而Generator函数是中间可以停，搭配使用next函数继续执行，像挤牙膏

- 最直观的表现就是比普通的function多了个星号*，在其函数体内可以使用yield关键字，有函数会在每个yield后暂停。

     ###   另外：**迭代器**

- 当你调用一个generator时，它将返回一个迭代器对象。
- 这个迭代器对象拥有一个叫做next的方法来帮助你重启generator函数并得到下一个值。
- next方法不仅返回值，它返回的对象具有两个属性：done和value。
value是你获得的值，done用来表明你的generator是否已经停止提供值。

  ### 生成器和迭代器的用处？
- 生成器可以让我们的代码进行等待。就不用嵌套的回调函数。
- 使用generator可以确保当异步调用在我们的generator函数运行一下行代码之前完成时暂停函数的执行。
- 可创建外观清晰的异步操作代码
- 不必到处使用回调函数，而是可以建立貌似同步的代码，但实际上却使用 yield 来等待异步操作结束。

## 9. async await
1. 概念： 真正意义上去解决异步回调的问题，同步流程表达异步操作
2. 本质： Generator的语法糖
3. 语法：
~~~JavaScript
    async function foo(){
      await 异步操作;
      await 异步操作；
    }
~~~
4. 特点：
- 不需要像Generator去调用next方法，遇到await等待，当前的异步操作完成就往下执行
- 返回的总是Promise对象，可以用then方法进行下一步操作
- async取代Generator函数的星号*，await取代Generator的yield
- 语意上更为明确，使用简单，经临床验证，暂时没有任何副作用