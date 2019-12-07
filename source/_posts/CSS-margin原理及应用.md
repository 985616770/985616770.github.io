---
title: margin原理及应用
date: 2019-09-09 18:10:33
author: 玄机
tags:
    - CSS
    - margin
categories: CSS
---
<!-- more -->
今天看到圣杯，双飞翼，就想搞懂 margin 的原理，以前一直避而不谈。

# 什么是 margin

> CSS 边距属性定义元素周围的空间。通过使用单独的属性，可以对上、右、下、左的外边距进行设置。也可以使用简写的外边距属性同时改变所有的外边距。——W3School

> 边界，元素周围生成额外的空白区。“空白区”通常是指其他元素不能出现且父元素背景可见的区域。——CSS 权威指南

大家都喜欢使用**外边距**这个词来解释 margin，我们可以很清楚的了解到 margin 的最基本用途就是控制元素周围空间的间隔，从视觉角度上达到相互隔开的目的。

# Margin 的特性

margin 始终是透明的。

# margin 基本用法

margin 通过使用单独的属性，可以对上、右、下、左的外边距进行设置。即：

`margin-top margin-right margin-bottom margin-left`

外边距的 margin-width 的值类型有：

`auto | length | percentage`

也可以使用简写的外边距属性同时改变所有的外边距：margin: `top | right| bottom |left`;

记忆方式是元素周围正上方**顺时针**“上右下左”记忆。

并且规范还提供了省略的数值写法，基本如下：

1. 如果 margin 只有一个值，表示上右下左的 margin 同为这个值。

2. 如果 margin 只有两个值，第一个值表示上下 margin 值，第二个值为左右 margin 的值。

3. 如果 margin 有三个值，第一个值表示上 margin 值，第二个值表示左右 margin 的值，第三个值表示下 margin 的值。

4. 如果 margin 有四个值，那这四个值分别对应上右下左这四个 margin 值。

---

> **不推荐使用三个值的 margin**，一是容易记错，二是不容易日后修改，一开始如果写成 margin:10px 20px 30px;日后需求改动为上 10px，右 30px，下 30px，左 20px，你不得不还是得把这个 margin 拆开为 margin:10px 30px 30px 20px;费力且不讨好，不如一开始就老老实实的写成 margin:10px 20px 30px 20px;来的实在，不要为了现在节省俩个字节而让日后再次开发的成本上升。

# 垂直外边距合并问题

外边距合并指的是，当两个垂直外边距相遇时，它们将形成一个外边距。合并后的外边距的高度等于两个发生合并的外边距的高度中的较大者。你可以查看[W3Shool CSS 外边距合并](http://www.w3school.com.cn/css/css_margin_collapsing.asp)了解这个基本知识。

合并外边距的计算方式是：

垂直方向上：

$$（一正一负） 正外边距值max + |负外边距值max| = 显示的外边距值 $$

$$
（全负）
0 -|负外边距值max| = |显示的外边距值|
$$

全是正值：取最大值。

左右正常相加。

# margin 移动问题

![](https://yimg.xjdd.xyz//marginMoveDefault.gif)

为了形象、易懂的解释负 margin，我们将引入 W3C 上没有的参考线的说法。何谓参考线？参考线就是 margin 移动的基准点，此基准点相对于 box(自身)是静止的。而 margin 的数值，就是 box 相对于参考线的位移量。

一个完整的 margin 属性是这么写的 margin: top right bottom left;(eg: margin:10px 20px 30px 40px)。**在 margin 属性中一共有两类参考线，top 和 left 的参考线属于一类，right 和 bottom 的参考线属于另一类。top 和 left 是以外元素为参考，right 和 bottom 是以元素本身为参考。margin 的位移方向是指 margin 数值为正值时候的情形，如果是负值则位移方向相反。**

bottom 和 right 属性设置并不会对元素自身产生唯一效果。。

这样写肯定很抽象，主要是引入参考线的说法，理解 margin 值设定后的走向。

可以做一些有意思的事情，比如，

1. 通过套 div，实现两层像素的 css 圆角功能，正是利用 margin 移动后，显示的大小，和存在的逻辑大小（也就是调试工具中，设置 margin 负值的元素，选择后显示的大小），产生区别而形成的重叠现象;如下图所示：

<a href="#" style =" display:inline-block;vertical-align:top;background-color:#e0e"><span style=" display:inline-block;vertical-align:top; margin:1px -1px;background-color:#e0e">确定</span></a>

## margin 负值 问题

margin 设定负值不会影响的正常的**文档流**，上图所示的比较清晰了，文档流只能是后面的流向前面的，即文档流只能向左或向上流动，不能向下或向右移动。

**所以，一切只要是由文档流决定的东西，负边距就能起作用了。**

形成一种覆盖样式，有很多应用。下面会记录下。

在元素不指定宽度的情况下，如果设置 `margin-left` 或者 `margin-right` 为**负值**的话，会在元素对应的方向上增加其宽度。效果就和设置 `padding-left` 或者 `padding-right` 一样。

### 负值与定位

1. 元素没有设置浮动且没有设置定位或者 `position` 为 `static`

如果元素没有设置浮动并且没有设置定位或者 `position` 属性为 `static` 的情况下，对元素的 margin 设置负值会有以下的效果：

**设置的 margin 的方向为 top 或者 left**

当设置负值的 margin 的方向为 top 或者 left 的时候，元素会按照设置的方向移动相应的距离。

比如，设置 `margin-left: -100px;`。 那么，元素会往左移动 100px。对于设置 `margin-top` 也是一样的道理。

**设置的 margin 的方向为 bottom 或者 right**

当设置负值的 margin 的方向为 bottom 或者 right 的时候，元素本身并不会移动，元素后面的其他元素会往该元素的方向移动相应的距离，并且覆盖在该元素上面。

比如，设置 `margin-right: -100px;`。那么，元素本身并不会移动，后面的元素会向左移动 100px 到该元素上。对于设置 `margin-bottom` 也是同样的道理。

2. 元素没有设置浮动且 `position` 为 `relative`

    如果元素没有设置浮动，但是设置了相对定位，设置 margin 为负值的时候，表现如下：

    **设置的 margin 的方向为 top 或者 left**

    当设置负值的 margin 的方向为 top 或者 left 的时候，元素也会按照设置的方向移动相应的距离。

    **设置的 margin 的方向为 bottom 或者 right**

    当设置 `margin-bottom/left` 的时候，元素本身也不会移动，元素后面的其他元素也会往该元素的方向移动相应的距离，但是，该元素会覆盖在后面的元素上面 (当然，此处说的情况肯定是后面的元素没有设置定位以及 `z-index` 的情况)。

3. 元素没有设置浮动且 `position` 为 `absolute`

如果元素没有设置浮动，但是设置了绝对定位，设置 margin 为负值的时候，表现如下：

**设置的 margin 的方向为 top 或者 left**

当设置负值的 margin 的方向为 top 或者 left 的时候，元素也会按照设置的方向移动相应的距离。

**设置的 margin 的方向为 bottom 或者 right**

由于设置绝对定位的元素已经脱离了标准文档流，所以，设置 `margin-right/bottom` 对后面的元素并没有影响。

### 负值与浮动

> 肯定没有既设置了浮动又设置绝对定位的情况，那样太荒唐了。
> 设置了浮动的元素，再设置 `postion: relative;` 的话，元素的行为和单独设置 `float` 是一样的。

对于设置了浮动的元素，设置 margin 为负值的时候，表现如下：

如果设置的 margin 的方向与浮动的方向相同，那么，元素会往对应的方向移动对应的距离。

eg：

```html
.elem { float: right; margin-right: -100px; background-color：#eee }
```

该元素则会向右移动 100px。

如果设置 margin 的方向与浮动的方向相反，则元素本身不动，元素之前或者之后的元素会向该元素的方向移动相应的距离。

```html
.elem { float: right; margin-left: -100px; }
```

位于该元素左边的元素则会向右移动 100px，同时覆盖在该元素上。

如果后面的元素也设置了浮动的话，我们以一个具体的例子来说明。

```html
<div class="container">
    <div class="left"></div>
    <div class="right"></div>
</div>
```

```css
.container {
    min-height: 300px;
    margin: 30px auto;
    overflow: hidden;
    border: 1px solid #000000;

    .left {
        float: left;
        width: 400px;
        height: 200px;
        margin-right: -300px;
        background: purple;
    }

    .right {
        float: left;
        width: 300px;
        height: 200px;
        background: #cccccc;
    }
}
```

`.left` 和 `.right` 都设置了浮动，在 `.left` 上设置了 `margin-right: -300px;`，那么，`.right` 会向左移动 300px，从而覆盖在 `.left` 上。这种行为与没有既没有设置浮动也没有设置定位的表现类似。

# margin 百分比问题

规范中注明 `margin` 的百分比值参照其**包含块的宽度（width）**进行计算。

非常出名的圣杯布局，双飞翼布局利用的就是这点。但是：

只发生在默认的 `writing-mode: horizontal-tb;` 和 `direction: ltr;` 的情况下。

当书写模式变成纵向的时候，其参照将会变成包含块的高度。我们改变 CSS 书写模式：

### CSS:

```css
#demo {
    -webkit-writing-mode: vertical-rl; /* for browsers of webkit engine */
    writing-mode: tb-rl; /* for ie */
}
```

现在变成了：参照对象变成了**包含块的高度（height）**

为什么要选择宽度做参照而不是高度呢？？？

> 其实更多的要从 CSS 设计意图上去想，因为 CSS 的基础需求是排版，而通常我们所见的横排文字，其水平宽度一定（仔细回想一下，如果没有显式的定义宽度或者强制一行显示，都会遇到边界换行，而不是水平延展），垂直方向可以无限延展。但当书写模式为纵向时，其参照就变成了高度而不再是宽度了。这也解释了为什么 `margin：auto`在垂直方向为什么不生效的原因了。

## 失效场景

1. inline 水平元素的垂直 margin 无效（margin-top/margin-bottom）
2. margin 重叠发生
3. 绝对定位元素非定位方位的 margin 值 "无效" 因为 绝对定位元素 脱离了文档流，与相邻元素没有关系，所以它不可能像普通元素一样，设置 margin，推走其他元素
4. margin 鞭长莫及 因为 有某些元素破坏了 文档流，设置了 float absolute，造成了假象，margin 不会根据 这些破坏元素作为标准
5. display:table-cell/display:table-row 等声明的 margin 无效！某些替换元素除外，根据各个浏览器的实现方式作为区分。比如，给 button 元素声明 display:table-cell，但在 chrome 中,button 的 display 属性是 inline-block 。
6. 内联特性导致 margin 失效 margin-top: 负无穷， 但是，小到 1em 便无效了。 因为它是内联元素，默认是基线对齐，x 字母下边缘对齐，margin 值再大，也不会起作用。 示例如下：

# margin 应用

1. 像素圆角
2. 已知宽高的元素水平垂直居中
3. tab 底边栏，重叠显示
4. 布局的应用，应用的很多
5. 半遮挡的标题

## 引用地址

[理解并运用 CSS 的负 margin 值](https://segmentfault.com/a/1190000007184954)

[你有所不知的 margin 属性](https://juejin.im/post/5a94d67ff265da4e732ef535#heading-18)

[CSS 布局奇淫巧计之-强大的负边距](https://www.cnblogs.com/2050/archive/2012/08/13/2636467.html)

[margin 系列之 bug 巡演](https://blog.doyoe.com/2013/12/20/css/margin%E7%B3%BB%E5%88%97%E4%B9%8Bbug%E5%B7%A1%E6%BC%94%EF%BC%88%E4%B8%89%EF%BC%89/)
