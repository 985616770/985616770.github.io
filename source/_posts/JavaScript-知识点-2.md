---
title: js学习回顾(二)
date: 2018-10-17 17:39:48
tags: JS
categories: JavaScript
---
<!-- more -->
## JS 基础回顾(二)

### DOM

-   HTML : 展示信息
-   XML :存储信息
-   ELEMENT : 元素 标签
-   NODE:节点 所有内容
-   ROOT :根 HTML 树
-   DOCUMENT : 文档 页面

DOM 树

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8" />
        <title>My test page</title>
    </head>
    <body>
        <img src="images/firefox-icon.png" alt="My test image" />
    </body>
</html>
```

关于 dom 的各种属性

[DOM 接口](https://developer.mozilla.org/zh-CN/docs/Web/API/Document_Object_Model)

### 事件

1. 事件源
2. 事件名称
3. 触发事件
4. 响应

**绑定事件的流程**:

1. 获取事件源的位置
2. 为事件源注册事件,添加事件处理函数

### 练习的实现思路

1. 点击事件

根据 ID 获取按钮,按钮注册事件,添加处理函数,触发,实现效果

2. 排他功能

利用遍历设置默认值,点击的值发生变化,刷新其他值,

### 获取方法

> **id** document.getElementById('');

> **class** document.getElementByClassName('');

> **全能匹配** document.querySelector('')

> 类 : .class

> **ID** : #id

> **属性:** [name="ss"]

> **标签**: div

### 兼容代码

兼容低版本浏览器而写的代码

### 获取属性

-   `getAttribute(''[,''])` 设置一个属性获取,两个属性设置

-   `removeAttribute()`删除属性

### 节点

nodeType:

-   1 => 标签
-   2 => 属性
-   3 => 文本
-   8=>注释元素
-   9=> 文档元素

nodeName:

-   标签: 大写
-   属性: 小写
-   文本: #text

nodeValue:

-   标签:null
-   属性:属性值
-   文本: 文本内容

### 事件冒泡

* DOM 事件流:事件捕获阶段, 处于目标阶段, 事件冒泡阶段.

> **事件捕获（event capturing）：**通俗的理解就是，当鼠标点击或者触发 dom 事件时，浏览器会从根节点开始**由外到内**进行事件传播，即点击了子元素，如果父元素通过事件捕获方式注册了对应的事件的话，会先触发父元素绑定的事件。

> **事件冒泡（dubbed bubbling)**：与事件捕获恰恰相反，事件冒泡顺序是由内到外进行事件传播，直到根节点。

无论是事件捕获还是事件冒泡，它们都有一个共同的行为，就是**事件传播**.

dom 标准事件流的触发的先后顺序为：**先捕获再冒泡**，即当触发 dom 事件时，会先进行事件捕获，捕获到事件源之后通过事件传播进行事件冒泡.

不同的浏览器对此有着不同的实现，IE10 及以下不支持捕获型事件，所以就少了一个事件捕获阶段，IE11、Chrome 、Firefox、Safari 等浏览器则同时存在。

-   **addEventListener(event, listener, useCapture)**

    -   *参数定义* event---（事件名称，如 click，不带 on）
    -   listener---事件监听函数
    -   *useCapture---*是否采用事件捕获进行事件捕捉，

    -   默认为 false，即采用事件冒泡方式

addEventListener 在 IE11、Chrome 、Firefox、Safari 等浏览器都得到支持。

-   **attachEvent(event,listener)**

    -   _参数定义_：event---（事件名称，如 onclick，带 on），
    -   listener---事件监听函数。

attachEvent 主要用于 IE 浏览器，并且仅在 IE10 及以下才支持，IE11 已经废了这个方法了（微软还是挺识趣的，慢慢向标准靠拢）。

例子

```html
<html lang="zh-cn">
    <head>
        <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
        <title>js事件机制</title>
        <style>
            #parent {
                width: 200px;
                height: 200px;
                text-align: center;
                line-height: 3;
                background: green;
            }
            #child {
                width: 100px;
                height: 100px;
                margin: 0 auto;
                background: orange;
            }
        </style>
    </head>
    <body>
        <div id="parent">
            父元素
            <div id="child">
                子元素
            </div>
        </div>
        <script type="text/javascript">
            var parent = document.getElementById('parent');
            var child = document.getElementById('child');

            document.body.addEventListener(
                'click',
                function(e) {
                    console.log('click-body');
                },
                false
            );

            parent.addEventListener(
                'click',
                function(e) {
                    console.log('click-parent');
                },
                false
            );

            child.addEventListener(
                'click',
                function(e) {
                    console.log('click-child');
                },
                false
            );
        </script>
    </body>
</html>
```



事件触发顺序是由内到外的，这就是事件冒泡，虽然只点击子元素，但是它的父元素也会触发相应的事件，其实这是合理的，因为子元素在父元素里面，点击子元素也就相当于变相的点击了父元素，这样理解对吧？

这里有同学可能要问了，如果点击子元素不想触发父元素的事件怎么办？肯定可以的，那就是停止事件传播---event.stopPropagation();

修改栗 1 的代码，在子元素的监听函数中加入停止事件传播的操作，栗 2

```JS
child.addEventListener("click",function(e){
　　console.log("click-child");
  　e.stopPropagation();
},false);
```

**事件捕获**

```js
var parent = document.getElementById('parent');
var child = document.getElementById('child');

document.body.addEventListener(
    'click',
    function(e) {
        console.log('click-body');
    },
    false
);

parent.addEventListener(
    'click',
    function(e) {
        console.log('click-parent---事件传播');
    },
    false
); //新增事件捕获事件代码
parent.addEventListener(
    'click',
    function(e) {
        console.log('click-parent--事件捕获');
    },
    true
);

child.addEventListener(
    'click',
    function(e) {
        console.log('click-child');
    },
    false
);
```




#### 解绑事件

-   对象.on() = null
-   removeEventlistener();
-   detach()


