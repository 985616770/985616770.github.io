---
title: JavaScript-面向对象
date: 2019-11-06 23:47:04
tags:
  - 面向对象
  - JavaScript
categories: JavaScript
---

# 面向对象

> 定义

对代码的一种抽象,对外统一提供接口的编程思想

> 在 JavaScript 中的实现

基于原型的面向对象方式中,对象则是依靠构造器`constructor`,利用原型`prototype`构造出来的

---

## 属性

> 属性

事务的特性

> 方法

事物的功能

> 对象

事物的一个实例

> 原型

JavaScript 函数由`prototype`引用了一个对象,即**原型**

---

## 构造函数

> 定义

实现面向对象的根源

## 闭包

> 定义

闭包是一个拥有许多变量和绑定了这些变量的环境的表达式(通常是一个函数)
闭包是一个拥有上层函数的引用，且不会被立即释放的一个作用域，

- 实现的功能是函数内部拥有对外部函数的引用，可以防止及外部函数改变内部函数的状态，

> 优点:

- 有利于封装和可以访问局部变量
  > 缺点
- 内存占用严重，容易内存泄露，

---

## ES6

```javascript
class A {
  constructor() {
    super();
  }
}
```

## 继承方式

> 6 种

> 寄生式组合式继承

- es5
  > 原型继承:
- 用于写框架和 js 库
  > 构造继承

```javascript
function A(name) {
  this.name = name;
}
A.prototype.say = function() {
  console.log(this.name);
};
function B(name, age) {
  A.call(this, name);
  this.age = age;
}
B.prototype = Object.create(A.prototype);
B.constructor = B;
```

## 原型和原型链

> 原型

- 利用 prototype 添加属性和方法

> 原型链

- Js 在创建对象(无论是普通对象还是函数对象)的时候，都有一个叫做`__proto__`的内置属性，用于指向创建它的函数的的原型对象 prototype，

```js
function A() {}

let a = new A();
// 默认执行
// let p = {}
// p.__proto__ = A.prototype => true
// A.call(p)
```

> `__proto__`
> 实例对象的隐式原型
> 指向它的构造函数的原型对象

![](https://yimg.xjdd.xyz//原型链图.png)

> 规则:

1. 实例对象的隐式原型指向构造函数的原型对象
2. Function 的原型对象和隐式原型都指向 Function 的原型对象
3. Object 原型对象是所有原型对象的终点,它的隐式原型为 null
4. 函数的隐式原型指向 function 原型对象

## this

4种情况

- 一般函数调用this ,指向全局对象,在严格模式下指向undefined
- 作为方法调用,构造函数中的this
- Call ,apply, bind
- 对象中的this

对象冒充
1. 冒充对象传递特权属性和特权方法给子类
2. 不能继承共有方法和属性(prototype)