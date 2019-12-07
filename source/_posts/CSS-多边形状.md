---
title: css形状学习
date: 2018-10-06 08:37:04
tags: CSS
categories: CSS
---

**CSS 能够根据给的各种属性制作各种各样的图形,像正方形,矩形,圆,椭圆,三角形,不规律的图形都能实现**

<!-- more -->

## 规律图形

### 正方形



<div id="square" style="width:100px;height:100px;background: red;">

```css
#square {
      width: 100px;
      height: 100px;
      background: red;
}
```

### 矩形

<div id="rectangle" style="  width: 200px;
      height: 100px;
      background: red;">

```css
   #rectangle {
      width: 200px;
      height: 100px;
      background: red;
    }
```

### 圆

<div id="circle" style="  width: 100px;
      height: 100px;
      background: red;
      border-radius: 50%">

```css
    #circle {
      width: 100px;
      height: 100px;
      background: red;
      border-radius: 50%
    }

```

### 椭圆

<div id="oval" style=" width: 200px;
      height: 100px;
      background: red;
      border-radius: 100px / 50px;">

```css3
   #oval {
      width: 200px;
      height: 100px;
      background: red;
      border-radius: 100px / 50px;
    }
```

### 三角形
<div id="triangle-up" style="   width: 0;
      height: 0;
      border-left: 50px solid transparent;
      border-right: 50px solid transparent;
      border-bottom: 100px solid red;">


```css
    #triangle-up {
      width: 0;
      height: 0;
      border-left: 50px solid transparent;
      border-right: 50px solid transparent;
      border-bottom: 100px solid red;
    }

```

### 倒三角形
<div id="triangle-down" style="  width: 0;
      height: 0;
      border-left: 50px solid transparent;
      border-right: 50px solid transparent;
      border-top: 100px solid red;">

```css3
 #triangle-down {
      width: 0;
      height: 0;
      border-left: 50px solid transparent;
      border-right: 50px solid transparent;
      border-top: 100px solid red;
    }
```

### 左三角形
<div id="triangle-left" style="  width: 0;
      height: 0;
      border-top: 50px solid transparent;
      border-right: 100px solid red;
      border-bottom: 50px solid transparent;">

```

    #triangle-left {
      width: 0;
      height: 0;
      border-top: 50px solid transparent;
      border-right: 100px solid red;
      border-bottom: 50px solid transparent;
    }
```

### 右三角形
<div id="triangle-right" style="   width: 0;
      height: 0;
      border-top: 50px solid transparent;
      border-left: 100px solid red;
      border-bottom: 50px solid transparent;">

```css
   #triangle-right {
      width: 0;
      height: 0;
      border-top: 50px solid transparent;
      border-left: 100px solid red;
      border-bottom: 50px solid transparent;
    }
```

### 三角形左上角
<div id="triangle-topleft" style="    width: 0;
      height: 0;
      border-top: 100px solid red;
      border-right: 100px solid transparent;">

```
 #triangle-topleft {
      width: 0;
      height: 0;
      border-top: 100px solid red;
      border-right: 100px solid transparent;
    }

```

### 三角形右上方
<div id="triangle-topright" style=" width: 0;
      height: 0;
      border-top: 100px solid red;
      border-left: 100px solid transparent;">

```css

    #triangle-topright {
      width: 0;
      height: 0;
      border-top: 100px solid red;
      border-left: 100px solid transparent;
    }

```

### 三角形左下角
<div id="triangle-bottomleft" style=" width: 0;
      height: 0;
      border-bottom: 100px solid red;
      border-right: 100px solid transparent;">

```css
    #triangle-bottomleft {
      width: 0;
      height: 0;
      border-bottom: 100px solid red;
      border-right: 100px solid transparent;
    }
```

### 三角形右下角
<div id="triangle-bottomleft" style=" width: 0;
      height: 0;
      border-bottom: 100px solid red;
      border-right: 100px solid transparent;">

```

    #triangle-bottomright {
      width: 0;
      height: 0;
      border-bottom: 100px solid red;
      border-left: 100px solid transparent;
    }
```

### 梯形
<div id="trapezoid" style="  border-bottom: 100px solid red;
      border-left: 25px solid transparent;
      border-right: 25px solid transparent;
      height: 0;
      width: 100px;">

```css
#trapezoid {
      border-bottom: 100px solid red;
      border-left: 25px solid transparent;
      border-right: 25px solid transparent;
      height: 0;
      width: 100px;
    }
```

### 平行四边形
<div id="parallelogram" style="  width: 150px;
      height: 100px;
      transform: skew(20deg);
      background: red;">

```css
  #parallelogram {
      width: 150px;
      height: 100px;
      transform: skew(20deg);
      background: red;
    }

```

## 不规律图形

### 六角星
<div id="star-six" style="   width: 0;
      height: 0;
      border-left: 50px solid transparent;
      border-right: 50px solid transparent;
      border-bottom: 100px solid red;
      position: relative;">

```css

    #star-six {
      width: 0;
      height: 0;
      border-left: 50px solid transparent;
      border-right: 50px solid transparent;
      border-bottom: 100px solid red;
      position: relative;
    }
    #star-six:after {
      width: 0;
      height: 0;
      border-left: 50px solid transparent;
      border-right: 50px solid transparent;
      border-top: 100px solid red;
      position: absolute;
      content: "";
      top: 30px;
      left: -50px;
    }

```

### 五角星



```

    #star-five {
      margin: 50px 0;
      position: relative;
      display: block;
      color: red;
      width: 0px;
      height: 0px;
      border-right: 100px solid transparent;
      border-bottom: 70px solid red;
      border-left: 100px solid transparent;
      transform: rotate(35deg);
    }
    #star-five:before {
      border-bottom: 80px solid red;
      border-left: 30px solid transparent;
      border-right: 30px solid transparent;
      position: absolute;
      height: 0;
      width: 0;
      top: -45px;
      left: -65px;
      display: block;
      content: '';
      transform: rotate(-35deg);
    }
    #star-five:after {
      position: absolute;
      display: block;
      color: red;
      top: 3px;
      left: -105px;
      width: 0px;
      height: 0px;
      border-right: 100px solid transparent;
      border-bottom: 70px solid red;
      border-left: 100px solid transparent;
      transform: rotate(-70deg);
      content: '';
    }

```

### 五角形


```
   #pentagon {
      position: relative;
      width: 54px;
      box-sizing: content-box;
      border-width: 50px 18px 0;
      border-style: solid;
      border-color: red transparent;
    }
    #pentagon:before {
      content: "";
      position: absolute;
      height: 0;
      width: 0;
      top: -85px;
      left: -18px;
      border-width: 0 45px 35px;
      border-style: solid;
      border-color: transparent transparent red;
    }
```

### 六边形


```
#hexagon {
      width: 100px;
      height: 55px;
      background: red;
      position: relative;
    }
    #hexagon:before {
      content: "";
      position: absolute;
      top: -25px;
      left: 0;
      width: 0;
      height: 0;
      border-left: 50px solid transparent;
      border-right: 50px solid transparent;
      border-bottom: 25px solid red;
    }
    #hexagon:after {
      content: "";
      position: absolute;
      bottom: -25px;
      left: 0;
      width: 0;
      height: 0;
      border-left: 50px solid transparent;
      border-right: 50px solid transparent;
      border-top: 25px solid red;
    }
```

### 爱心


```
  #heart {
      position: relative;
      width: 100px;
      height: 90px;
    }
    #heart:before,
    #heart:after {
      position: absolute;
      content: "";
      left: 50px;
      top: 0;
      width: 50px;
      height: 80px;
      background: red;
      border-radius: 50px 50px 0 0;
      transform: rotate(-45deg);
      transform-origin: 0 100%;
    }
    #heart:after {
      left: 0;
      transform: rotate(45deg);
      transform-origin: 100% 100%;
    }

```

### 无限大


```
    #infinity {
      position: relative;
      width: 212px;
      height: 100px;
      box-sizing: content-box;
    }
    #infinity:before,
    #infinity:after {
      content: "";
      box-sizing: content-box;
      position: absolute;
      top: 0;
      left: 0;
      width: 60px;
      height: 60px;
      border: 20px solid red;
      border-radius: 50px 50px 0 50px;
      transform: rotate(-45deg);
    }
    #infinity:after {
      left: auto;
      right: 0;
      border-radius: 50px 50px 50px 0;
      transform: rotate(45deg);
    }
```

### 菱形


```

    #diamond {
      width: 0;
      height: 0;
      border: 50px solid transparent;
      border-bottom-color: red;
      position: relative;
      top: -50px;
    }
    #diamond:after {
      content: '';
      position: absolute;
      left: -50px;
      top: 50px;
      width: 0;
      height: 0;
      border: 50px solid transparent;
      border-top-color: red;
    }
```

### 蛋


```
 #egg {
      display: block;
      width: 126px;
      height: 180px;
      background-color: red;
      border-radius: 50% 50% 50% 50% / 60% 60% 40% 40%;
    }
```

阴阳盘


```
 #yin-yang {
      width: 96px;
      box-sizing: content-box;
      height: 48px;
      background: #eee;
      border-color: red;
      border-style: solid;
      border-width: 2px 2px 50px 2px;
      border-radius: 100%;
      position: relative;
    }
    #yin-yang:before {
      content: "";
      position: absolute;
      top: 50%;
      left: 0;
      background: #eee;
      border: 18px solid red;
      border-radius: 100%;
      width: 12px;
      height: 12px;
      box-sizing: content-box;
    }
    #yin-yang:after {
      content: "";
      position: absolute;
      top: 50%;
      left: 50%;
      background: red;
      border: 18px solid #eee;
      border-radius: 100%;
      width: 12px;
      height: 12px;
      box-sizing: content-box;
    }
```

### 太空入侵者


```

    #space-invader {
      box-shadow: 0 0 0 1em red,
      0 1em 0 1em red,
      -2.5em 1.5em 0 .5em red,
      2.5em 1.5em 0 .5em red,
      -3em -3em 0 0 red,
      3em -3em 0 0 red,
      -2em -2em 0 0 red,
      2em -2em 0 0 red,
      -3em -1em 0 0 red,
      -2em -1em 0 0 red,
      2em -1em 0 0 red,
      3em -1em 0 0 red,
      -4em 0 0 0 red,
      -3em 0 0 0 red,
      3em 0 0 0 red,
      4em 0 0 0 red,
      -5em 1em 0 0 red,
      -4em 1em 0 0 red,
      4em 1em 0 0 red,
      5em 1em 0 0 red,
      -5em 2em 0 0 red,
      5em 2em 0 0 red,
      -5em 3em 0 0 red,
      -3em 3em 0 0 red,
      3em 3em 0 0 red,
      5em 3em 0 0 red,
      -2em 4em 0 0 red,
      -1em 4em 0 0 red,
      1em 4em 0 0 red,
      2em 4em 0 0 red;
      background: red;
      width: 1em;
      height: 1em;
      overflow: hidden;
      margin: 50px 0 70px 65px;
    }
```

### 锁


```
#lock {
  font-size: 8px;
  position: relative;
  width: 18em;
  height: 13em;
  border-radius: 2em;
  top: 10em;
  box-sizing: border-box;
  border: 3.5em solid red;
  border-right-width: 7.5em;
  border-left-width: 7.5em;
  margin: 0 0 6rem 0;
}
#lock:before {
  content: "";
  box-sizing: border-box;
  position: absolute;
  border: 2.5em solid red;
  width: 14em;
  height: 12em;
  left: 50%;
  margin-left: -7em;
  top: -12em;
  border-top-left-radius: 7em;
  border-top-right-radius: 7em;
}
#lock:after {
  content: "";
  box-sizing: border-box;
  position: absolute;
  border: 1em solid ted;
  width: 5em;
  height: 8em;
  border-radius: 2.5em;
  left: 50%;
  top: -1em;
  margin-left: -2.5em;
}
```

### Facebook


```
 #facebook-icon {
      background: red;
      text-indent: -999em;
      width: 100px;
      height: 110px;
      box-sizing: content-box;
      border-radius: 5px;
      position: relative;
      overflow: hidden;
      border: 15px solid red;
      border-bottom: 0;
    }
    #facebook-icon:before {
      content: "/20";
      position: absolute;
      background: red;
      width: 40px;
      height: 90px;
      bottom: -30px;
      right: -37px;
      border: 20px solid #eee;
      border-radius: 25px;
      box-sizing: content-box;
    }
    #facebook-icon:after {
      content: "/20";
      position: absolute;
      width: 55px;
      top: 50px;
      height: 20px;
      background: #eee;
      right: 5px;
      box-sizing: content-box;
    }
```
