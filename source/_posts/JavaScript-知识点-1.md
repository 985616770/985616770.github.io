---
title: js学习回顾(一)
date: 2018-10-17 17:39:48
tags: JavaScript
categories: JavaScript
---

# 回顾基础

## 基础语法的回顾

### Math.random()

产生的是 [0,1) 左闭右开区间 eg:JS 原生 设置密码:

```js
var array = new Uint32Array(10);
window.crypto.getRandomValues(array);

console.log('Your lucky numbers:');
for (var i = 0; i < array.length; i++) {
  console.log(array[i]);
}
```

<!-- more -->

> 拓展知识:

### arguments

伪数组对象 是一个对应于传递给函数的参数的类数组**对象**,类数组是除了 length 属性和索引元素外没有任何 Array 的方法.

- 应用的方面 : 用与传入不确定的参数 可以遍历和输出 eg:

  ```JS
  function myConcat(separator) {
    var args = Array.prototype.slice.call(arguments, 1);
    return args.join(separator);
  }
  // returns "red, orange, blue"
  myConcat(", ", "red", "orange", "blue");
  ```

- \*高级方面待了解:剩余参数、默认参数和解构赋值参数----

  > 引申的知识 :
  >
  > > > - `Array.from()` => 转换伪数组为真正的数组(ES6)
  > > > - 第二种转换 [...arguments] 拓展运算符(ES6)
  > > > - JavaScript 的签名 : JS 是一种类型松散或动态语言,意味着不必提前声明变量的类型.,类型会在程序员处理时确定.签名是提供该方法的一些信息.
  > > > -

### call(), bind(), apply()

1. call(thisArg, arg1, arg2, ...) 转换 this 的指向 (第一个参数为 null 或者 undefined 会指向全局对象)

   apply(this,[arg1,arg2,...])

2. 允许我们明确指定方法中的 this 指向

   ```JS
   // <button>Get Random Person</button>
   // <input type="text">

   var user = {
       data        :[
           {name:"T. Woods", age:37},
           {name:"P. Mickelson", age:43}
       ],
       clickHandler:function(event) {
           var randomNum = ((Math.random () * 2 | 0) + 1) - 1; // random number between 0 and 1

           // 从 data 数组中随机选取一个名字填入 input 框内
           $("input").val(this.data[randomNum].name + " " + this.data[randomNum].age);
       }
   }

   // 给点击事件添加一个事件处理器
   $("button").click(user.clickHandler);
   ```

3. .实现函数借用

   ```js
   // cars 对象
   var cars = {
     data: [
       { name: 'Honda Accord', age: 14 },
       { name: 'Tesla Model S', age: 2 }
     ]
   };

   // 我们从之前定义的 user 对象借用 showData 方法
   // 这里我们将 user.showData 方法绑定到刚刚新建的 cars 对象上
   cars.showData = user.showData.bind(cars);
   cars.showData(); // Honda Accord 14
   ```

4. 柯里化(curry)

   柯里化的概念很简单, 只传递给函数一部分参数来调用它, 让它返回一个函数去处理剩下的参数. 你可以一次性地调用 curry 函数, 也可以每次只传一个参数分多次调用, 以下为一个简单的示例. - [JS 函数是编程指南 第 4 章: 柯里化（curry）](https://llh911001.gitbooks.io/mostly-adequate-guide-chinese/content/ch4.html)

   ```js
   var add = function(x) {
     return function(y) {
       return x + y;
     };
   };

   var increment = add(1);
   var addTen = add(10);

   increment(2);
   // 3

   addTen(2);
   // 12
   ```

   现在, 我们使用 bind() 方法来实现函数的柯里化. 我们首先定义一个接收三个参数的 greet() 函数:

   ```js
   function greet(gender, age, name) {
     // if a male, use Mr., else use Ms.
     var salutation = gender === 'male' ? 'Mr. ' : 'Ms. ';

     if (age > 25) {
       return 'Hello, ' + salutation + name + '.';
     } else {
       return 'Hey, ' + name + '.';
     }
   }
   // 在 greet 函数中我们可以传递 null, 因为函数中并未使用到 this 关键字
   var greetAnAdultMale = greet.bind(null, 'male', 45);

   greetAnAdultMale('John Hartlove'); // "Hello, Mr. John Hartlove."

   var greetAYoungster = greet.bind(null, '', 16);
   greetAYoungster('Alex'); // "Hey, Alex."
   greetAYoungster('Emma Waterloo'); // "Hey, Emma Waterloo."
   ```

5. 利用 call 调用数组的方法使用数组方法

   ```JS
   // Make a quick copy and save the results in a real array:
   // First parameter sets the "this" value
   var newArray = Array.prototype.slice.call(anArrayLikeObj, 0);

   console.log(newArray); // ["Martin", 78, 67, Array[3]]

   // Search for "Martin" in the array-like object
   console.log(Array.prototype.indexOf.call(anArrayLikeObj, "Martin") === -1 ? false : true); // true

   // Try using an Array method without the call () or apply ()
   console.log(anArrayLikeObj.indexOf("Martin") === -1 ? false : true); // Error: Object has no method 'indexOf'

   // Reverse the object:
   console.log(Array.prototype.reverse.call(anArrayLikeObj));
   // {0: Array[3], 1: 67, 2: 78, 3: "Martin", length: 4}

   // Sweet. We can pop too:
   console.log(Array.prototype.pop.call(anArrayLikeObj));
   console.log(anArrayLikeObj); // {0: Array[3], 1: 67, 2: 78, length: 3}

   // What about push?
   console.log(Array.prototype.push.call(anArrayLikeObj, "Jackie"));
   console.log(anArrayLikeObj); // {0: Array[3], 1: 67, 2: 78, 3: "Jackie", length: 4}
   ```

6. 当我们使用 apply 或者 call 时, 传入的第一个参数为目标函数中 this 指向的对象, 以下为一个简单的例子:

   ```javascript
   // 全局变量
   var avgScore = "global avgScore";

   // 全局函数
   function avg(arrayOfScores) {
       // 分数相加并返回结果
       var sumOfScores = arrayOfScores.reduce(function(prev, cur, index, array) {
           return prev + cur;
       });

       // 这里的 "this" 会被绑定到全局对象上, 除非使用 Call 或者 Apply 明确指定 this 的指向
       this.avgScore = sumOfScores / arrayOfScores.length;
   }

   var gameController = {
       scores  :[20, 34, 55, 46, 77],
       avgScore:null
   }

   // 调用 avg 函数, this 指向 window 对象
   avg(gameController.scores);
   // 证明 avgScore 已经被设置为 window 对象的属性
   console.log(window.avgScore); // 46.4
   console.log(gameController.avgScore); // null

   // 重置全局变量
   avgScore = "global avgScore";

   // 使用 call() 方法明确将 "this" 绑定到 gameController 对象
   avg.call(gameController, gameController.scores);

   console.log(window.avgScore); // 全局变量 avgScore 的值
   console.log(gameController.avgScore); // 46.4

   ```

   以上例子中 call() 中的第一个参数明确了 this 的指向, 第二参数被传递给了 avg() 函数.

7. 在回调函数中用 call 或者 apply 设置 this

   以下为一个例子, 这种做法允许我们在执行 callback 函数时能够明确 其内部的 this 指向以下为一个例子, 这种做法允许我们在执行 callback 函数时能够明确 其内部的 this 指向

   ```js
   // 定义一个方法
   var clientData = {
     id: 094545,
     fullName: 'Not Set',
     // clientData 对象中的一个方法
     setUserName: function(firstName, lastName) {
       this.fullName = firstName + ' ' + lastName;
     }
   };

   function getUserInput(firstName, lastName, callback, callbackObj) {
     // 使用 apply 方法将 "this" 绑定到 callbackObj 对象
     callback.apply(callbackObj, [firstName, lastName]);
   }

   getUserInput('Barack', 'Obama', clientData.setUserName, clientData);
   console.log(clientData.fullName); // Barack Obama
   ```

   递给 callback 函数 中的参数将会在 clientData 对象中被设置/更新.

8. 使用 Apply 或者 Call 借用函数

   相比 bind 方法, 我们使用 apply 或者 call 方法实现函数借用能够有很大的施展空间. 接下来我们考虑从 Array 中借用方法的问题, 让我们定义一个**类数组对象(array-like object)**然后从数组中借用方法来处理我们定义的这个对象, 不过在这之前请记住我们要操作的是一个对象, 而不是数组;

   ```js
   // An array-like object: note the non-negative integers used as keys
   var anArrayLikeObj = {
     0: 'Martin',
     1: 78,
     2: 67,
     3: ['Letta', 'Marieta', 'Pauline'],
     length: 4
   };
   // Make a quick copy and save the results in a real array:
   // First parameter sets the "this" value
   var newArray = Array.prototype.slice.call(anArrayLikeObj, 0);

   console.log(newArray); // ["Martin", 78, 67, Array[3]]

   // Search for "Martin" in the array-like object
   console.log(
     Array.prototype.indexOf.call(anArrayLikeObj, 'Martin') === -1
       ? false
       : true
   ); // true

   // Try using an Array method without the call () or apply ()
   console.log(anArrayLikeObj.indexOf('Martin') === -1 ? false : true); // Error: Object has no method 'indexOf'

   // Reverse the object:
   console.log(Array.prototype.reverse.call(anArrayLikeObj));
   // {0: Array[3], 1: 67, 2: 78, 3: "Martin", length: 4}

   // Sweet. We can pop too:
   console.log(Array.prototype.pop.call(anArrayLikeObj));
   console.log(anArrayLikeObj); // {0: Array[3], 1: 67, 2: 78, length: 3}

   // What about push?
   console.log(Array.prototype.push.call(anArrayLikeObj, 'Jackie'));
   console.log(anArrayLikeObj); // {0: Array[3], 1: 67, 2: 78, 3: "Jackie", length: 4}
   ```

   **arguments** 对象是所有 JavaScript 函数中的一个类数组对象, 因此 call() 和 apply() 的一个最常用的用法是从 arguments 中提取参数并将其传递给一个函数.

   以下为 Ember.js 源码中的一部分, 加上了我的一些注释:

   ```js
   function transitionTo(name) {
     // 因为 arguments 是一个类数组对象, 所以我们可以使用 slice()来处理它
     // 参数 "1" 表示我们返回一个从下标为1到结尾元素的数组
     var args = Array.prototype.slice.call(arguments, 1);

     // 添加该行代码用于查看 args 的值
     console.log(args);

     // 注释本例不需要使用到的代码
     //doTransition(this, name, this.updateURL, args);
   }

   // 使用案例
   transitionTo('contact', 'Today', '20'); // ["Today", "20"]
   ```

   考虑到字符串是不可变的, 如果使用 apply 或者 call 方法借用字符串的方法, 不可变的数组操作对他们来说才是有效的, 所以你不能使用类似 reverse 或者 pop 等等这类的方法.,可以借用我们自定义的方法

9. 使用 apply() 执行参数可变的函数

   关于 Apply, Call 和 Bind 方法的多功能性和实用性, 我们将讨论一下 Apply 方法的一个很简单的功能: 使用参数数组执行函数.

   ```js
   var students = [
     'Peter Alexander',
     'Michael Woodruff',
     'Judy Archer',
     'Malcolm Khan'
   ];

   // 不定义参数, 因为我们可以传递任意多个参数进入该函数
   function welcomeStudents() {
     var args = Array.prototype.slice.call(arguments);

     var lastItem = args.pop();
     console.log('Welcome ' + args.join(', ') + ', and ' + lastItem + '.');
   }

   welcomeStudents.apply(null, students);
   // Welcome Peter Alexander, Michael Woodruff, Judy Archer, and Malcolm Khan.
   ```

10. bind 是返回对应函数, 便于稍后调用; apply, call 则是立即调用

11. , 在 ES6 的箭头函数下, call 和 apply 的失效, 对于箭头函数来说:

    - 函数体内的 this 对象, 就是定义时所在的对象, 而不是使用时所在的对象;
    - 不可以当作构造函数, 也就是说不可以使用 new 命令, 否则会抛出一个错误;
    - 不可以使用 arguments 对象, 该对象在函数体内不存在. 如果要用, 可以用 Rest 参数代替;
    - 不可以使用 yield 命令, 因此箭头函数不能用作 Generator 函数;

### 作用域

- 全局作用域:全局能使用的函数

- 局部作用域:只能在函数内部使用的

- 块级作用域: ES6 const let 花括号内使用的

- 隐式全局变量: 能被删除,未使用 var
- 作用域链: script 标签为零级作用域,函数嵌套,嵌套越深层级值越大,零级最大
- 预解析(变量提升) : 解析代码,会将声明提前,只能在当前的 script 标签中,只是提升说明,不会初始化,如果提前调用,报 undefined

### 面向过程

亲力亲为,注重过程.

### 面向对象

需求找对象,注重结果.

**特性** :

- **命名空间** :使用命名空间也最大程度地减少应用程序的名称冲突的可能性。

- **类** : JavaScript 是一种基于原型的语言，它没类的声明语句

- **封装** :对于所有继承自父类的方法，只需要在子类中定义那些你想改变的即可。

- **对象** :我们使用 new obj 创建对象 obj 的新实例, 将结果（obj 类型）赋值给一个变量方便稍后调用。
- **构造器** :在实例化时构造器被调用 (也就是对象实例被创建时)。构造器是对象中的一个方法。
- **属性** (对象属性) : 属性就是 类中包含的变量;每一个对象实例有若干个属性. 为了正确的继承，属性应该被定义在类的原型属性 (函数)中。
- **方法** (对象属性): 方法与属性很相似， 不同的是：一个是函数，另一个可以被定义为函数。

- **继承**: 单继承,创建的专门版本的类通常叫做子类，另外的类通常叫做父类。

- **多态** : 不同的类可以定义具有相同名称的方法;方法是作用于所在的类中。并且这仅在两个类不是父子关系时成立（继承链中，一个类不是继承自其他类）。
- **抽象** : 通过继承（具体化）或组合来实现。JavaScript 通过继承实现具体化，通过让类的实例是其他对象的属性值来实现组合。

继承的实现

```JS
// 定义Person构造器
function Person(firstName) {
  this.firstName = firstName;
}

// 在Person.prototype中加入方法
Person.prototype.walk = function(){
  alert("I am walking!");
};
Person.prototype.sayHello = function(){
  alert("Hello, I'm " + this.firstName);
};

// 定义Student构造器
function Student(firstName, subject) {
  // 调用父类构造器, 确保(使用Function#call)"this" 在调用过程中设置正确
  Person.call(this, firstName);

  // 初始化Student类特有属性
  this.subject = subject;
};

// 建立一个由Person.prototype继承而来的Student.prototype对象.
// 注意: 常见的错误是使用 "new Person()"来建立Student.prototype.
// 这样做的错误之处有很多, 最重要的一点是我们在实例化时
// 不能赋予Person类任何的FirstName参数
// 调用Person的正确位置如下，我们从Student中来调用它
Student.prototype = Object.create(Person.prototype); // See note below

// 设置"constructor" 属性指向Student
Student.prototype.constructor = Student;

// 更换"sayHello" 方法
Student.prototype.sayHello = function(){
  console.log("Hello, I'm " + this.firstName + ". I'm studying " + this.subject + ".");
};

// 加入"sayGoodBye" 方法
Student.prototype.sayGoodBye = function(){
  console.log("Goodbye!");
};

// 测试实例:
var student1 = new Student("Janet", "Applied Physics");
student1.sayHello();   // "Hello, I'm Janet. I'm studying Applied Physics."
student1.walk();       // "I am walking!"
student1.sayGoodBye(); // "Goodbye!"

// Check that instanceof works correctly
console.log(student1 instanceof Person);  // true
console.log(student1 instanceof Student); // true
// 是不是属于该变量的方法 1. instanceof
//2.person.hasOwnProperty('name')；//
// 3. in 操作符  'name' in person
// 4. Object.keys()
```

红宝书的各种方式:

1. **调用构造函数**

   ```js
   var obj = new Object();
   obj.name = 'sss';
   ```

2. **工厂模式**

   ```js
   function creatPerson(name) {
     var o = new Object();
     o.name = name;
     return o;
   }
   var person = creatPerson('sssa');
   console.log(person.name);
   ```

3. **字面量创建对象**

   ```js
   var o = {};
   o.name = 'sss';
   ```

​ 缺陷一次性的对象

**使用构造函数创建对象**

1.  在内存中开辟空间申请一块空闲的空间,创建新的对象
2.  将构造函数的作用域赋给新对象,this 指向当前的对象
3.  设置对象属性和方法的值
4.  返回新的对象

**获取和设置对象属性和方法**

1. 点法 eg :obj.属性
2. obj['属性']

### json 格式的数据

1. 两头都是双引号
2. 键值对
3. 没有注释
4. 是对象

### 类型

#### **基本类型**

- Number
- String
- Boolean
- Symbol(ES6)
- Undefined
- Null

**约定**：基本数据类型与原始数据类型等意。

1. 基本类型的值是不可变的

   ```JS
   var str = "123hello321";
   str.toUpperCase();     // 123HELLO321
   console.log(str);      // 123hello321
   ```

2. 基本类型的比较是它们的值的比较

```JS
var a = 1;
var b = true;
console.log(a == b);    // true
console.log(a === b);   // false
```

A 与 B 数据类型不同,但是也可以进行值的比较,是因为自动进行数据类型的**隐式转换**.

- `==` : 只进行值的比较
- `===` : 不仅进行值得比较，还要进行数据类型的比较

3. 基本类型的变量是放在栈(stack)内存中的

   ```JS
   var a,b;
   a = "玄机";
   b = a;
   console.log(a);   // 玄机
   console.log(b);   // 玄机
   a = "呵呵";       // 改变 a 的值，并不影响 b 的值
   console.log(a);   // 呵呵
   console.log(b);   // 玄机
   ```


#### **引用类型**

- Object(统称)
- Array
- Date
- RegExp
- Function

1. 引用类型的值是可变的

   ```JS
   var obj = {name:"玄机"};   // 创建一个对象
   obj.name = "percy";       // 改变 name 属性的值
   obj.age = 21;             // 添加 age 属性
   obj.giveMeAll = function(){
     return this.name + " : " + this.age;
   };                        // 添加 giveMeAll 方法
   obj.giveMeAll();
   ```

2. 引用类型的比较是引用的比较

   ```js
   var obj1 = {}; // 新建一个空对象 obj1
   var obj2 = {}; // 新建一个空对象 obj2
   console.log(obj1 == obj2); // false
   console.log(obj1 === obj2); // false
   ```

   > 因为 obj1 和 obj2 分别引用的是存放在堆内存中的 2 个不同的对象，故变量 obj1 和 obj2 的值（引用地址）也是不一样的！

3. 引用类型的值是保存在堆内存（Heap）中的对象（Object）,与其他编程语言不同，JavaScript 不能直接操作对象的内存空间（堆内存）。所以重新赋值引用的值 不会改变.会创建新的对象,重新指向.

   ```JS
   var a = {name:"percy"};
   var b;
   b = a;
   a.name = "玄机";
   console.log(b.name);    // 玄机
   b.age = 22;
   console.log(a.age);     // 22
   var c = {
     name: "玄机",
     age: 22
   };
   ```


图解如下：

- 栈内存中保存了变量标识符和指向堆内存中该对象的指针
- 堆内存中保存了对象的内容

#### 检测类型

[typeof]经常用来检测一个变量是不是最基本的数据类型

```JS
var a;
typeof a;    // undefined

a = null;
typeof a;    // object

a = true;
typeof a;    // boolean

a = 666;
typeof a;    // number

a = "hello";
typeof a;    // string

a = Symbol();
typeof a;    // symbol

a = function(){}
typeof a;    // function

a = [];
typeof a;    // object
a = {};
typeof a;    // object
a = /aaa/g;
typeof a;    // object
```

[instanceof](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/instanceof)：用来判断某个构造函数的 prototype 属性所指向的对象是否存在于另外一个要检测对象的原型链上

简单说就是判断一个引用类型的变量具体是不是某种类型的对象

```JS
({}) instanceof Object              // true
([]) instanceof Array               // true
(/aa/g) instanceof RegExp           // true
(function(){}) instanceof Function  // true
```

#### 基本包装类型

- Boolean

- Number

- String

  特殊的行为:具有方法

  1. 创建 String 类型的一个实例；

  2. 在实例上调用指定的方法；

  3. 销毁这个实例。

     ```js
     var s1 = new String('some text');

     var s2 = s1.substring(2);

     s1 = null;
     ```

与基本类型的区别主要在于: **对象的生存期**

使用 new 操作符创建的引用类型的实例,在执行流离开当前作用域之前都一直保存在内存中,自动创建的基本包装类型的对象,仅仅存在于一行代码执行瞬间,然后销毁,这意味着不能为运行时的基本类型值添加属性方法.

布尔表达式的所有对象都会被转为 true;

### 内存

栈(地址)

值传递的是值

堆(对象)

引用类型传递的是地址

### 内置对象

- 内置对象

  Math

  ```
  Math.pow(x,y);
  返回x的y次幂.
  Math.random();
  返回0到1之间的伪随机数.
  Math.round(x);
  返回四舍五入后的整数.
  ```

Date:

```js
var dt = new Date();
dt.getFullYear(); // 当前年份
dt.getMonth(); // 当前月-1
dt.getDate(); // 当前日期
dt.getHours(); // 当前小时
dt.getMinute(); // 当前分钟
dt.getSeconds(); // 当前秒
dt.getDay(); // 当前天
dt.toString(); // 当前地区标准时间
dt.toDateString(); // 星期 月份 日 年份
dt.toTimeString(); // 时分秒 GMT时区
dt.toLocaleDateString(); // 年月日
dt.toLocaleTimeString(); // 上午/下午 时分秒
dt.valueOf(); | dt.getTime() // 获取从1970 开始的毫秒数
```

String:

```js
var str = "xuanji";
str.length(); // 字符串的长度
str.charAt(num); //  返回指定位置的字符串
String.fromCharCode(num,num..); //  静态方法 传入Unicode值 输出字符串
str.concat('string'); // 拼接字符串 在后面开始,返回新的字符串
str.indexOf('string'); // 返回索引位置
str.lastindexOf('string'); //从后往前找 返回索引位置
*str.replace(替换的字符或者正则,换的字符); // 替换所有符合的字符  新的字符串
str.split('分割字符/正则',前num个元素); //  将string对象分割成字符串数组(Array)
str.substr(num,length); // 开始数字和提取长度
str.substring(num,num); // 截取  负值和NaN当做0 会自动切换大小排序
str.trim(); //去除两端的空白

```

Array:

```JS
var num = ['A','B'];
num.concat(); // 拼接数组
num.every(callback); //  测试每个值是否满足callback的要求,不满足返回false callback有三个参数
num.some(callback); // 测试是否有值满足callback的要求,遇到true就返回true
num.filter(callback); // 过滤掉不符合的数组,形成新数组
num.push(); // 添加到数组末尾的后面
num.pop(); // 删除最后一个值,返回删除的值
num.shift(); // 删除第一个值,返回删除的值
num.unshift(); // 添加第一个值,返回长度
num.foreach(); // 遍历数组,为每一个数组执行callback
num.indexOf(); // 查找值 ,返回索引 没有返回-1
num.join('字符'); // 连接数组 使其变成字符串 默认为逗号
num.map(); //  为该数组的每一个元素调用一个提供的函数后返回的结果
num.reverse(); //反转数组
num.sort(); // 按照Unicode码点排序
num.slice(num, num); // 截取产生新的数组对象,是浅拷贝(当原数组值改变也会跟着变化)
*num.reduce(); // 累计器和数组的每个元素从左到右应用一个函数,将其简化为单个值

```

