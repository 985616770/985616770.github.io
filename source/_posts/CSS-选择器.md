---
title: CSS学习路线(二)选择器
date: 2018-05-02 11:58:09
tags: CSS
categories: CSS
---
<!-- more -->
# 选择器

## 规则结构:

-   分两个基本部分: 选择器`selector`和声明块`declaration block` 组成

-   声明块: 由一个或多个声明组成,每一个声明都是属性-值对

**选择器分为:**

1. 元素选择器
2. 类选择器
3. 后代选择器
4. 通配选择器
5. ID 选择器
6. 属性选择器
7. 伪类选择器
8. 子元素选择器
9. 相邻兄弟选择器

---

## 元素选择器:往往是 html 元素,但是在 XML 允许创造新的标记语言.

```css
h1 {
    font-size: 14px;
}
```

---

## 类选择器:应用样式而不考虑具体涉及的元素.

```css
.main{
  font-size:14px;
}

<p class="main">123</p>
```

---

## ID 选择器

-   和类选择器差不多.区别在于只能在文档运用一次,多次不符合规范,

```css
main{
  font-size:14px;
}
<p id="main">123</p>
```

---

## 通配选择器

-   运用在全局,但是不推荐.易出错
-   选择全部性能消耗大)

```css
* {
    font-size: 14px;
}
```

---

## 后代选择器

-   运用在父元素的所有子元素上,

```css
h1 p {
    font-size: 14px;
} //运用在 h1 下的所有 p 元素
```

## 子元素选择器

-   运用在父元素的第一代子元素上

```css
h1 > p {
    font-size: 14px;
} //运用在 h1 下的第一代 p 元素
```

## 相邻兄弟选择器

-   相同父元素下,选择紧跟着另一个元素后的元素

```css
//运用在 h1 和 p 的父元素下,接下来的 P 元素
h1 + p {
    font-size: 14px;
}
```

## 属性选择器

-   根据元素的属性来选择元素
-   分为四种:
-   -   简单属性选择
-   -   具体属性选择
-   -   部分属性选择
-   -   特定元素选择

### 简单属性选择:

```css
h1[class]{color:red;}

<p class="main">hello world</p>
```

### 具体属性选择:

```css
h1[class="main"]{color:red;}
<p class="main">hello world</p>
```

### 部分属性选择:

```css
h1[class*="main"]{color:red;}//含有就可以

h1[class^="main"]{color:red;}//main 开头的元素

h1[class$="main"]{color:red;}//main 结尾的元素

h1[class~="main"]{color:red;}//独立单词的元素

<p class="main qq">hello world</p>
```

### 特定属性选择:

```css
*[lang|="en"]{color:red;}

<p lang="en-ss">Hello</p>
```

## 伪类元素选择器

-   为链接选择

```css
/*顺序为 LVHA */

a:link {
    color: red;
} //未访问的链接

a:visited {
    color: green;
} //已访问的链接

a:hover {
    color: red;
} //悬浮在链接上

a:active {
    color: yellow;
} //激活后的链接
```

```css
还有 p:first-child 第一个子元素

:first-letter /*首字母样式*/

:first-line /*第一行样式*/

:before /*之前插入内容*/ 
body:before{content:"hello ";}

:after /*之后插入内容*/ 
body:after{content:"hello ";}
```
