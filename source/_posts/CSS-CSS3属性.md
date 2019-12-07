---
title: CSS3
date: 2019-10-01 21:26:03
tags:
    - CSS3
    - CSS
categories: CSS
---
<!-- more -->
# 什么是 CSS

定义: Cascading style sheets 层叠样式表

用与: 调整页面的样式

---

## **CSS3**

添加了很多新的东西,如 动画,圆弧,变量,渐变,阴影 ,flex,gird 等等 很多的新花样

但是: 兼容性还是存在一定的问题

_写了没效果,所以要经常查兼容性_

比较常见的: margin 高度塌陷,float 清除浮动,负值 margin 的 应用

## 容易出问题的地方

### 权重,css 选择器的问题

选择器分为

1. 标签选择器
2. 类选择器
3. id 选择器
4. 伪元素选择器
5. 伪类选择器
6. 自定义属性选择器
7. 通配符选择器

大的就分这几种

细分的话还有: `后代( )`,`群组(,)`,`兄弟(+)`,`通用兄弟(~)`,`子代(>)`,

> 权重排行 !important >>> 行内样式 >>> id(1000) >> 类,伪类,自定义属性(10) >
> 标签,伪元素(1) > 通配,继承(0)

**比较规则**:

-   必须在同级下比,例如 100 个类叠加,还是比不上个 id 选择器
-   两个权重不同的选择器作用在同一元素上，权重值高的 css 规则生效
-   两个相同权重的选择器作用在同一元素上：以后面出现的选择器为最后规则.

---

### margin 高度塌陷和负值应用

> 我的文章有一篇有比较详细的介绍了,不在啰嗦 `margin负值及应用`

---

### BFC 的应用

定义 : (block formatting context) **块级格式上下文**

**触发条件** :

1. `float` 不为 `none`
2. `overflow:auto/scroll/hidden` 3.`display:table-cell,table-caption,inline-block`
3. `position` 不为 `relative,static`

mdn 有很详细的介绍,我只挑了几个常见的(我用过的) => [mdn](https://developer.mozilla.org/zh-CN/docs/Web/Guide/CSS/Block_formatting_context)

**优点** :

1. 自适应内容,由于封闭,更健壮,容错性高

2. 自适应内容,自动填充区域形成两列布局

3. 所以先构建网页的结构的原因

---

### 清除浮动

定义: 由于浮动导致高度塌陷,下面文章自动上移.

**清除浮动**:

1. 浮动元素上加 类`.clearfix` (类上属性 `clear:both`)
2. 父容器加`overflow:hidden`(小块,注意内容的溢出)
3. 利用伪元素 添加清除浮动(大内容)比较完美 `::before ::after`
4. 设置父元素高度
5. 父级元素也浮动(不推荐)
    > 常用 2,3

---

## 常用属性:

### **font**

> -   **可以继承**
>     > 语法
>     >
>     > -   `font-family` 字体
>     > -   `font-size` 字体的大小
>     > -   `color` 字 的颜色
>     > -   `font-weight` 宽粗
>     > -   `font-style` 字体样式(斜体)
>     > -   `font-variant` 字体变形(拉丁文) 小型大写
>     >     简写(不推荐,增加阅读难度): style variant weight (size)/line-height (family)

> > **括号的必须有才能生效**

---

### **自定义字体**

```css
@font-face {
    font-family: 'iconfont';
    src: url('../fonts/iconfont.eot?t=1522237704791');
    /* IE9*/
    src: url('../fonts/iconfont.eot?t=1522237704791#iefix') format('embedded-opentype'),
        /* IE6-IE8 */ url('../fonts/iconfont.ttf?t=1522237704791') format('truetype'),
        /* chrome, firefox, opera, Safari, Android, iOS 4.2+*/
            url('../fonts/iconfont.svg?t=1522237704791#iconfont') format('svg');
    /* iOS 4.1- */
}
```

```css
.iconfont {
    font-family: 'iconfont' !important;
    font-size: 16px;
    font-style: normal;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
}
1.
.icon-backtop:before {
    content: '\e689';
}
2.
添加类 .icon .icon-backtop

3.
添加类 且直接书写
Unicode码
```

---

### **文本样式 text**

> **语法**

> > -   text-shadow 文本创造阴影
> >     > 语法 : `h-shadow v-shadow blur color`
> > -   text-outline 文本轮廓(没得支持)
> > -   text-align 水平对齐方式
> > -   line-height 行高
> > -   vertical-align 文本垂直对齐方式(默认基于基线)
> >     > % 百分比相对于 line-height 行内或者行内块生效
> > -   word-spacing 单词之间间距,空格为准
> > -   letter-spacing 字母之间间距,中文可以用
> > -   text-transform 文本的大小写
> > -   text-decoration 文体的装饰(a 标签常用)
> > -   text-align-last 规定如何对齐最后一栏
> >     > 属性 `auto left right center justify start end inital inherit`
> > -   text-overflow 文本溢出包括元素发生的事情(各个版本浏览器有不同的支持)
> >     > clip,ellipsis(...),string
> > -   word-break 规定自行换行的处理方法,针对{拉丁文}
> > -   word-wrap 允许长单词换行,如 {邮箱} {网址}

---

### 列表样式`list`

> -   list-style-type
>     > 很多选项(基本用不到,都是自己定义图标)
>     > none
> -   list-style-image 一样,边上 的图标
> -   list-style-position
>     > inside(默认)内环绕 | outside 隔出来,不会跑到下面去
> -   list-style 简写 三个属性

---

### 背景(相当常用)`background`

> > -   background-color 背景颜色
> > -   background-image 背景图
> >     *background-repeat 重复方式
> >     *background-attachment 图片固定方式
> > -   background-clip 指定背景绘制区域(少见,比较有意思)
> > -   background-origin 指定 positon 的相对位置
> >     background-size 背景图像大小
> > -   background-position 背景图的位置
> > -   background(简写)
> >     > 属性 *color *position size *repeat origin clip attachment *image

> > 渐变
> >
> > -   linear-gradient
> >     > -   定义 :两个或者多个指定的颜色之间,显示平稳的过渡
> >     > -   语法 `direction ,color 节点...`方向 颜色节点
> > -   repeating-linear-gradient
> >     > -   重复渐变

> > 圆形渐变
> >
> > -   radial-gradient > - 定义: 起点到终点,圆心到外,
> >     > -   语法 `shape size at 圆心位置(x y) , 颜色节点...`
> > -   repeating-radial-gradient

> > IE 渐变
> >
> > -   filter

---

### **过渡 transition**

> > transition :
> >
> > -   定义: css 属性值在一定时间内平滑的过渡
> > -   属性
> >     > -   property 过渡属性的名称
> >     > -   duration 过渡持续的时间
> >     > -   timing-function 动画类型
> >     >     > -   ease(平滑) linear(线性) ease-in(慢到快) ease-out(快到慢) ease-in-out(慢快慢) cubic-bezier(贝塞尔曲线) step-start|step-end|steps(不常用)
> >     > -   delay 延迟过渡时间
> >     > -   transition(简写): `property duration timing-function delay`

---

### **转换(分 3d 和 2d)transform**

> **定义** 让元素在坐标系中变形,包括一系列变形函数
> 语法
>
> -   transform
>     > 方法(2d):
>     >
>     > -   rotate:旋转
>     >     > -   语法: 传角度(angle)
>     >     > -   正顺时针,负数逆时针
>     > -   translate:位移
>     >     > -   语法:`translate() translateX() translateY()`
>     >     > -   传 x y 水平 竖直
>     > -   scale:放大,缩小
>     >     > -   语法: `scale() scaleX() scaleY()`
>     >     > -   传数值(num),可以实现镜像翻转 `scale(1,-1)`
>     > -   skew: 倾斜
>     >     > -   语法:`skew() skewX() skewY()`
>     >     > -   传角度

> > 方法((3d): 差不多,但是参数不许省略,可以触发优化
> >
> > -   rotate3d:
> >     > -   `ratate3d(x,y,z,angle)
> > -   translate3D
> > -   scale()
> >     > -   区别是参数不可省略
> >     > -   (矩阵) :高大上,所有的上面都是由它简化而来
> > -   matrix:
> >     > -   2d 平面移动转换
> >     > -   方法:
> >     >     > -   `matrix(1,0,0,1,x,y) == translate(x,y)`
> >     >     > -   `matrix(sx,0,0,sy,0,0) == scale(sx,sy)`
> >     >     > -   `matrix(cos,sin,-sin,cos,0,0) == rotate`
> >     >     > -   `matrix(1,tanx,tany,1,0,0) == skew(xdeg,ydeg)`
> > -   matrix3d: 3d 平面移动转换

> -   转换的一些属性
>     > -   transform-origin
>     >     更换元素转换的源位置
>     > -   transform-style
>     >     指定嵌套元素怎么样在 3d 中显示(会有类似的 3d 效果出现)
>     > -   perspective
>     >     观察者与 z 的距离,是具有三维位置变化,元素产生透视效果(不容易看出效果)
>     > -   perspective-origin
>     >     透视点的位置(和上面属性配合使用)
>     > -   backface-visiblity
>     >     元素背向用户是否可见(翻转后能否看到背面,骰子)

---

### **阴影 shadow**

> 盒子
>
> -   box-shadow
> -   属性 :一个,或多个阴影的框
> -   语法 `h-shadow v-shadow blur spread color inset[,]`
> -   水平位移 竖直位移 模糊度 拓展 颜色 内阴影 ,可以多个

> 文字阴影
>
> -   text-shadow
> -   上面一样,兼容性有一点问题

---

### **圆弧(角)radius**

> border-radius : 圆角边框
>
> -   属性 八个值
>     > -   左上水平 右上水平 右下水平 左下水平 / 左上竖直 右上竖直 右下竖直 左下竖直
> -   方向
> -   border-top|bottom-left|right-radius
> -   值: 百分比 参照对本身
> -   特性:
>     > 1. 大值特性 足够大的值会直接成 ⚪
>     > 2. 等比例特性 : 与高宽成比例. 可以实现 50%的效果,各种几何平面图像都能用它实现,css 动画可以用它

---

### **动画 animation**

> **定义** : 元素从一种样式到另一种样式的效果
>
> -   animation:
>     > 属性
>     >
>     > -   name 动画名称
>     > -   duration 持续时间
>     > -   timing-function 动画类型
>     > -   delay 延迟时间
>     > -   iteration 循环次数
>     > -   direction 是否反向运动
>     > -   fill-mode 动画完成时或有延迟时未开始播放,应用到元素的样式(会保持状态)
>     > -   play-state 运行还暂停(js 控制的多)
>     > -   简写 :
>     >     `name duration timing-functio-time delay iteration direction fill-mode play-state`

> @keyframes
>
> -   定义 控制动画变化的关键位置
> -   语法

```
@keynames name{
to{} .. from{} || 0%{} .. 100%{}
}
```

> will-change
>
> 1.  增强页面渲染性能
> 2.  还可以使用 translateZ 触发
>     > -   语法 `auto scroll-position contents 名称`

---

### **定位 position**

> position:
>
> -   static 自然定位
> -   relative 相对定位
> -   absolute 绝对定位
>     > -   基于最近的相对定位(子绝父相)
> -   fixed 固定定位
> -   sticky 磁贴定位(新 css3) 脱离文档流

> 属性
>
> -   left
> -   top
> -   right
> -   bottom
> -   z-index 层叠顺序

---

### **盒模型 box**

-   width,height
    > 宽高
-   padding
    > 填充 上左下右
-   margin
    > 边距 上左下右

---

## CSS3 变量

-   类似 sass,但是是官方的

-   用法:

```css
/* 全局 */
:root {
    --h: 10px;
}
/* 局部 */
p {
    --color: red;
    color: var(--color);
}
```

## 无单位需要计算 `calc()函数`

## 布局

### 行布局

-   height 和 line-height

---

### 两列布局

-   float + margin
-   ​float + BFC
-   absolute
-   flex
-   ​gird

---

### 三列布局

-   双飞翼,圣杯
-   ​absolute
-   ​float
-   ​flex
-   ​gird
