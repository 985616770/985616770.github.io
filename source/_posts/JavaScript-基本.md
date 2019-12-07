---
title: JavaScript-基本
date: 2019-10-01 21:26:17
author: xuanji
tags: JavaScript
categories: JavaScript
---
<!-- more -->
# javaScript 组成

> 基于对象和事件驱动的脚本语言

ECMAscript, brower object(DOM,BOM) 三部分组成,平时用 Ecmascript 多

主要讲 ECMA script

## 数据类型

### 基本数据类型

> 7 种

##### **String**

**定义**:由多个,0 个 16 位 Unicode 字符组成字符序列
转换方法:

> toString()

-   转化为字符串,返回副本
-   值可为 number,布尔值,object,字符串

> String()

-   强制转换

##### **Number**

> 基于 64 位双精度浮动数
> 范围为

$$
2^{-53} -2^{53}
$$

**检测方法**

> isNaN()

-   NaN
-   任何数与它操作返回 NaN
-   NaN 不与任何数相等,包括自身
    转换方法
    > parseInt()
-   转换为整数从左开始
-   第二个参数为为基数
    > parseFloat
-   转换为浮点数.从左边开始,保留一位小数
    > Number()
-   强制转换 针对 string

#### **Boolean**

> 表示真假

**转换方法**

> Boolean()

-   除 0,nNaN 外,其他数字全为 true
-   除"",其他字符串为 true
-   undefined,null 为 false

#### **Undefined**

> 唯一值,派生于 null

#### **Null**

> 空指针对象

#### Symbol

> ES6 标识符 独一无二

#### bigInt

> 大数值

### 复杂数据类型

**Object**

内置对象

#### **Array**:**数组**

> 创建

`var arr= new Array()`

`var arr = [];`

**栈方法** :

> push(num) :num 添加数值参数到 arr 尾部

> unshift(num)
> num 添加到数组头部

> pop()
> 删除最后一个

> shift()
> 删除第一个

> join(符号)
> 数组根据符号发,分成字符串
> 返回 字符串

> reverse()
>
> -   倒转数组
> -   返回 数组(返回倒)

> sort(函数)
>
> -   根据函数规则来排序
> -   返回 排序后的数组

> concat(数组)
>
> -   连接多个数组
> -   返回 新数组

> slice(start,end)
>
> -   从已有数组返回选定的元素
> -   无 end',选择 starat 后所有数
> -   有负数,加之为正确的长度

> splice(index,count,[],[])
>
> -   是集删除,替换,添加为一体的方法
> -   返回 删除的数
> -   index 索引 count 数量 ,后面新添加的

> indexOf(value,索引)
>
> -   在数组中从索引开始找 value 值
> -   找到返回索引
> -   没找到'-1

> lastIndexOf(value,索引)
>
> -   从后往前找
> -   返回数组长度
> -   返删除值

> map(callback)
>
> -   为数组的每个元素执行回调函数
> -   返回 处理的后的新数组

> find(item=>{操作})
>
> -   查找值,找到返回值

> filter(ele,index,arr => {操作})
>
> -   返回通过测试的数值

> reduce(acc,cur,index,arr)=>{},initValue)
>
> -   返回经过处理的数值

> flat(depth)
>
> -   多维数组 转化为 一维数组

> fill(value,index,end)
>
> -   从 index 起,到 end 的长度 用 value 来填充

> withCopy(index,start,end)
>
> -   将 index 处的值 复制到 start 的地方

> 属性
>
> -   length

#### Math

一些数学运算方法

> 方法

> Math.ceil(数组)
> 向上取整

> Math.floor(数组)
> 向下取整

> Math.round(数组)
> 四舍五入取整

> Math.abs(数)
> 取绝对值

> Math.random()
> 随机 0-1

随机整数

Math.floor(Math.random() \* (m-n + 1) +n)

#### Date:日期

方法
`let date = new Date()`

> date.getFullYear()
>
> -   4 位年份

> date.getMonth()
>
> -   月份 0-11

> date.getDate()
>
> -   月份的天数

> date.getDay()
>
> -   返回星期

> date.getHours()
>
> -   返回小时

> date.getMinutes()
>
> -   返回分钟

> date.getSeconds()
>
> -   返回秒

> date.getTime()
>
> -   返回毫秒

#### 检测方法

> typeof `检测的数据`

-   返回
-   `string, number, boolean , object, undefined,function,symbol,bigint`

## 变量

1. var,let,const
2. 松散类型-保存任何类型的数据
3. 多个变量要用逗号

## 操作符

### 算数操作符

> -   `-`加

> -   `*`减

> -   `-` 乘

> -   `/`除

> -   `%`取余

> -   递增和递减

> -   ++x ;x--

### 赋值操作符

> -   `=` 赋值
> -   `+=`加等
> -   `-=`减等
> -   `\*=` 乘等
> -   `/=`除等
> -   `%=` 取余等

### 逻辑操作符

> `&& 逻辑与

-   非布尔值时
-   从左往右执行,遇到 false 值 返回 false 值
-   遇到 false 值为 undefined,null,NaN ,直接返回他们三值
-   全为 true,返回最后值

> || 逻辑或

-   非布尔值时

-   从左往右执行,遇到 true 值 返回 true 值

-   遇到全为 false 值为 undefined,null,NaN ,直接返回他们三值

-   全为 false 返回最后值

> ! 非

-   !!val 返回布尔值

### 比较操作符

> -   `>` 大于
> -   `<` 小于
> -   `> =` 大于等于
> -   `<=` 小于等于
> -   `==` 是否相等
> -   `===` 是否全等(判断类型)
> -   `!=` 是否不等
> -   `!==` 是否不全等

### 三元操作符

`条件? 执行代码 1 : 执行代码 2`

-   代替简单的 if 语句

## 表达式

> **将同类型的数据(常量,变量,函数等),运用运算符号按照一定规则链接起来,成为有意义的式子**

### 语句

#### if 语句

```javascript
if(){

}else if(){

}else{

}
```

#### switch 语句

```javascript
switch(){

case 值 :语句;

break;

default :语句;

break;

}
```

> **区别**

-   if 和 while 已知次数,和未知次数

#### while

```javascript
while(){

}
```

#### do..while

```javascript
do{}while()
```

#### for 语句

```javascript
for(执行前定义,循环条件,执行后语句){

}
```

-   循环嵌套时,先外层后内层,内层 false 后返回外层
    > `while` 和 `do while` 区别
-   区别在于执行次数,do while 至少执行一次

#### break continue

> break

-   跳出语句,终止语句
    > continue
-   跳过语句 ,继续执行

### 函数

#### function

语法

```javascript
function name(参数) {}

var a = function() {};
```

#### return 语句

-   函数会在执行完 return,结束函数

-   可以不带值返回

#### 参数

> ECMAscript 函数参数内部用一个数组来表示

-   **arguments**

> 类数组

-   不是 array 的实例
-   有 length 可以用[] 来取值

### 错误调试

#### 分类

##### 语法错误

1. 漏打,少打,多打,错打

2. 不合法的变量名

3. 语法错误

##### 运行时错误

1. ReferenceError: 变量引用错误

2. TypeError: 类型使用错误

3. RangeError: 递归爆栈

##### 逻辑错误

计算结果不符合预期

#### try-catch -finally 语句

> 用法

```javascript
try {
} catch (error) {
} finally {
}
```

-   主动抛出错误
-   语法错误无法识别
-   接受 throw Error()

##### finally

-   清理性工作
-   一定执行()

### 事件

**定义** : 文档或浏览器窗口中发生的一些特定的交互瞬间

#### 事件分类

> HTML 事件

```html
<input type="submit" onclick="function(){}" />
```

写在行内样式中

> DOM0 级事件

```javascript
ele.onclick = function() {};
```

> DOM2 级事件

```javascript
ele.addEventListenr('click', function() {}, false);
ele.attachEvent('onclick', function() {}, false);
```

#### 事件增删

> 添加事件

-   addEventListener;

-   attachEvent;

> 移出事件

-   removeEventListener;
-   detachEvent;

> **区别**

-   HTML 事件:强耦合,不利于复用代码

-   DOM 0 级事件:松耦合,代码 js 代码分离

-   不能绑定多次绑定同一类型事件

-   DOM2 级事件 :优点全有,增加了冒泡捕获

#### 组成

1. 事件对象

2. 事件对象绑定事件

3. 事件句柄:事件处理函数,事件监听函数

#### 冒泡与捕获

> 捕获:

-   点击子元素,会先触发父元素的事件,再依次向下触子元素的事件

> 冒泡:

-   直系亲属树结构,点底部树结构的某个元素,(亲属树上)的父级元素会依次向上触发

#### 事件委托:

-   利用冒泡,点击子元素触发父元素的事件委托对象(event)

##### **event**

> 属性
>
> -   type
>     事件类型
> -   target
>     事件源(点击哪个就是哪个)
> -   currentarget
>     事件绑定的对象
> -   preventDeault()
>     阻止默认行为(链接跳转)
> -   stopPropagation()
>     阻止冒泡

> ie 属性
>
> -   returnValue = false
>     同 preventDefault
> -   cancelBubble = true
>     同 stopPropagation
> -   srcElement = target

#### 常见的事件类型

> load
> 页面加载后

> unload
> 当文档或一个子资源正在被卸载时

> resized
> 窗口变换大小

> scroll
> 滚动

> blur
> 失去焦点

> focus
> 得到焦点(不支持冒泡)

> focusin
> 得到焦点

> focusout
> 失去焦点

> DOMFoucusIn
> 得到焦点

> DOmFoucsOut
> 失去焦点

> click
> 点击

> dblclick
> 双击

> mouseup
> 松开鼠标

> mousedown
> 鼠标按下

> mouseout
> 鼠标离开元素区域

> mouseover
> 鼠标进入元素区域

> mousemove
> 鼠标在区域移动

> mousenter
> 鼠标进入目标区域

> mouseleave
> 鼠标离开目标区域

> event.
>
> -   shiftkey
> -   ctrlkey
> -   altkey
> -   metakey

> keydown
> 键盘按下
> 返回 keycode 码

> keyup
> 键盘抬起

> keypress
> 键盘按下,比 keydouwn 慢
> 只返回数,和字符 返回 ASCII 码

> textInput
> 输在 input text 类型中和值 会在 event.data 返回

> DOMNodeRemoved
> 文档任意元素删除触发

> DOMSubtreeModified
> 文档任意变化触发

> DOMNodeRemovedFromDocument
> 在文档移除前触发

> DOMNodeInserted
> 任何元素被添加时触发

> DOMNodeInsertedIntoDocument
> 在文档添加前触发

> DOMContentLoaded
> 在 dom 树之后就会触发

> readystatechange
> 不支持 chrome,提供文档或者元素加载过程中,很难预料结果

> hashchange
> 网址后的#后的值变化

> touchstart
> 手指触摸屏幕

> touchmove
> 手指在滑动

> touchend
> 手指离开

> touchcancel
> 当系统停止跟踪触摸时触发

> 手机端
>
> -   event.
>     > -   touches
>     >     触摸点数目

> > -   changeTouces
> >     引起事件的触摸点

> > -   targetTouches
> >     放在目标元素的触摸信息

注意事项: 兼容代码的书写

### 基本包装对象

##### String

-   字符串

> 方法

> charCodeAt(索引)

-   返回索引处字符编码(unicode)

> indexOf(value)

-   按顺序查找 value
-   返回 索引
-   -1 没有找到

> lastIndexOf(value)

-   倒着找

> slice(start,end)

-   截取 start 到 end -1 的字符

> substring(start,end)

-   截取 start 到 end -1 的字符,start 遇到负数转为 0

> substr(start,length)

-   截取 start 到最后 ,length 的长度

> split(符号)

-   根据符号,分成数组

> replace('被替换',替换)

-   替换字符

> toUpperCase()

-   转为大写

> toLowerCase()

-   转为小写
