---
title: JavaScript-对象和函数
date: 2019-11-06 21:44:41
tags:
  - 对象
  - 函数
  - JavaScript
categories: JavaScript
---
<!-- more -->
# 对象

---

> 定义

- 值的集合:键值对|名称值对

## 创建方式

1. 字面量

```javascript
let a = {};
let b = {};
const c = {};
```

2.  构造函数创建

```javascript
let a = new Object();
```

3. Object.create()

```javascript
let b = Object.create(null);
// 完全的空对象, 没有任何属性
```

## 方法及属性

> 修改

- `.`法
- []法

区别在于两者后者更通用些

```JavaScript
obj['s d'] = ... // 有空格
obj.s = ...
```

> 删除

- `delete obj[name]|.name`

> 是否存在

- `'name' in object` 返回布尔值

> 循环对象

```JavaScript
// for ... in ...
for(let key in object){

}
```

> 对象的深浅拷贝

**浅拷贝**

- 浅拷贝是对象共用一个内存地址，对象的变化相互影响
- 只复制一层对象

1. `Object.assign()`当属性有对象时

```javascript
let srcObj = { name: '明', grade: { chi: '50', eng: '50' } };
let copyObj = Object.assign({}, srcObj);
copyObj.name = '红';
copyObj.grade.chi = '60';
console.log('copyObj', copyObj);
/**
grade: {chi: "60", eng: "50"}
name: "红",

*/
console.log('srcObj', srcObj);
/* 
grade: {chi: "60", eng: "50"}
name: "明"

 */
```

2. 直接赋值

```javascript
let obj = { a: 2, b: 3 };
let objCopy = obj;
console.log('objCopy', objCopy);
// {a: 2, b: 3}
console.log(' obj', obj);
// {a: 2, b: 3}
objCopy.a = 4;
```

3. 函数实现

```javascript
function shallowClone(source) {
  let target = {};
  for (let i in source) {
    if (source.hasOwnProperty(i)) {
      target[i] = source[i];
    }
  }

  return target;
}
```

**深拷贝**

- 简单理解深拷贝是将对象放到一个新的内存中，两个对象的改变不会相互影响。

1. `JSON.parse()` 和 `JSON.stringify()`

```javascript
srcObj = { name: '明', grade: { chi: '50', eng: '50' } };
copyObj = JSON.parse(JSON.stringify(srcObj));
copyObj.name = '红';
copyObj.grade.chi = '60';
console.log('srcObj', srcObj); /* grade: {chi: "50", eng: "50"}
name: "明" */
console.log('copyObj', copyObj); /* 
grade: {chi: "60", eng: "50"}
name: "红"
 */
```

- JSON.stringify(..) 在对象中遇到 undefined 、 function 和 symbol 时会自动将其忽略， 在 数组中则会返回 null （以保证单元位置不变）。

2. 函数实现

```javascript
let deepCopy = function(obj) {
  if (typeof obj !== 'object') return;
  let newObj = obj instanceof Array ? [] : {};
  for (let key in obj) {
    if (obj.hasOwnProperty(key)) {
      newObj[key] =
        typeof obj[key] === 'object' ? deepCopy(obj[key]) : obj[key];
    }
  }
  return newObj;
};
```

以上针对的只是简单的对象,复杂的拷贝在 JavaScript 一直以来都是一个难题

---

# 函数

> 定义

- 一次封装,四处使用

> 分类

- 命名函数
- 匿名函数

> 优点

1. 复用代码
2. 统一修改和维护
3. 可读性

> 本质

- 二象性
- 调用
- 对象

## 封装

把对象内部数据和操作细节进行隐藏，把闭包的方法叫做特权方法，

在构造函数中返回对其内部变量的访问，实现外部访问内部变量的方法，

> 缺点

- 一占用内存
- 二不利于继承，

## 创建

1. 字面量

```JavaScript
let newFun = ()=>{};
let newFun = function(){}
```

2. 声明式

```JavaScript
function name(){}
```

3. 构造函数

```JavaScript
let newf = new Function(参数,函数体)
```

> 函数声明和函数表达式(var)都有预解析

## 函数作用域

- 全局作用域
- 函数作用域

> 作用域链

![作用域图](https://yimg.xjdd.xyz//20191106232415.png)

## 调用

- 普通调用

`a();`

- 匿名调用

```javascript
// iife
(function() {})();
```

- 递归调用

```javascript
function f(num) {
  if (num === 1) return 1;
  return num * f(num - 1);
}
f(3); // 6
```

- 方法调用

```javascript
// 事件模拟(dom事件)
// 链式调用
...
return this
// 对象方法调用
```

- 构造函数

```JavaScript
// 首字母大写
function Aa(name){
  this.name = name
}
let b = new Aa('xx')
```

- 间接调用

```JavaScript
// call,apply,bind
// 改变this的指向
obj.fun.call(null)
obj.fun.apply(null)
```

## 参数

### 分类

- 形参

占位符,相当于定义变量

- 实参

传递值,给形参,代替形参

### 参数的个数

1.  实参 < 形参

- 未赋值,undefined<可选参数>

- 设置默认值 值 = 值 || 固定值

2. 实参 > 形参

> arguments

- 类数组 每一个函数都有自己的 arguments
- 多余的参数存储在类数组中
- `arguments.callee`代表自身(递归常用)

### 能作为参数的

- 空 ""
- 数字 number
- 字符串 string
- boolean 布尔
- undefined
- null
- array 数组
- object 对象
- function(回调函数)

### 控制语句

> return
> continue
> break
