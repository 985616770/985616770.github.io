---
title: HTML-知识1
date: 2019-10-02 00:55:13
tags: HTML
categories: HTML
---
<!-- more -->
## 什么是 html

> 文本标记语言(**hypertext markup language**),已经是第五代

_HTML5_

> html 的增量式更新,新增许多东西,eg: 表单的属性,音视频的 api

> 是 HTML 的第五次修订版本,添加更多的标签,以及过期的标签,使得页面结构语义化,利于搜索的搜索权重,

---

## 基本的常识

### HTML 网页构成

**声明标签**:<!DOCTYPE html> html5 的声明 ,用于浏览器解析判断版本,不加的话会陷入混杂模式

**根标签**: <html> 网页的根标签,内包括两个大标签 head body

**head 标签**: 里面包含着网页的图标,描述信息,网站名称,引入的资源,样式脚本,移动端的识别.

**body 标签**: 内容的载体,是数据的存放的地方,所有的展现给用户的界面都在这里

**meta 标签**: 元数据存放,网页图标,描述信息,移动端判断

**引入标签**: `link` `img` `script`以及 h5 的新标签 音视频标签 `audio` `video` `soruce`

> 常用标签

```html
<div></div>
<h1-h5></h1-h5>
<span></span>
<input />
<img />
// head 中的元标签<meta />
// 还有html5新增的许多语义化标签
<header></header>
<section></section>
<nav></nav>
<footer></footer>
<article></article>
<aside></aside>
<hgroup></hgroup>
<figure></figure>
<figcaption></figcaption>
<dialog></dialog>
// 多媒体标签
<audio></audio>
<video></video>
<source />
<canvas></canvas>
<embed />
<iframe></iframe>
```

> 常用属性

```js
type: 类型(常用input)
name: (input)
class: 通用类型;
id id
style 行内样式
data-* 自定义的属性;
```

### **标签的分类**

-   块级元素
-   行内元素
-   行内块元素(可替换元素)

#### 块级元素

`div, ul, li, dl, dt, dd,h1-h5, p, form`

1. 可以设置宽高
2. margin,padding ,border
3. 自动换行
4. 多个块状元素，排列方式为从上至下

#### 行内元素

`span, i, sup, sub, strong, b`

1. 宽高由自身决定
2. margin-left|right 有效 padding 都有效
3. 不会自动进行换行

#### 行内块元素

`img, input`

1. 可以设置宽高
2. margin,padding ,border
3. 自动换行
4. 多个块状元素，从左到右

#### 嵌套规则

1. 块级元素可包行内元素,和某些块级元素
2. 行内元素不可包含块级元素,只能包含其他行内元素
3. 特殊块级元素只能包含行内元素,不能包含块级元素(h1-h5,p,dt)
4. 块级元素和块级元素并列,行内元素与行内元素并列

### 拓展知识

#### INPUT ElELEMENT (input 用法)

属性:

-   name
-   placeholder
-   required
-   disabled
-   type
    > type 是其中最重要的 由 type 引申了很多的新的属性

type 属性:

1. text

<input type="text" placeholder="请输入文本">

2. email

<input type="email" placeholder="请输入邮箱">

3. number

<input type="number" placeholder="请输入数值">

4. checkbox

唱<input type="checkbox" name="hobby">
跳<input type="checkbox" name="hobby">
打篮球<input type="checkbox" name="hobby">

5. radio

男<input type="radio" name="sex">
女<input type="radio" name="sex">

6. submit

<input type="submit">

7. tel

<input type="tel" placeholder="请输入号码">

8. datetime-local

<input type="datetime-local">

9. range

<input type="range">

10. search

<input type="search" placeholder="请输入搜索内容">

11. color
    <input type="color">
