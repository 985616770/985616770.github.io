---
title: jQuery
date: 2019-10-01 21:26:27
author: xuanji
tags: jQuery
categories: jQuery
---

# jQuery

- 写的少，做的多 JavaScript 库
- 化大为小化繁为简
- 简化代码,程序更高效

> 特点

1. 轻量级
2. 强大选择器
3. Dom 操作极其封装
4. 事件处理机制
5. Ajax.
6. 不污染顶级变量
7. 出色的浏览器兼容
8. 链式操作
9. 隐式迭代
10. 行为层和结构层
11. 插件支持
12. 组件化,模块化

## 安装

- 标签引入
- Cdn
- NPM YARn Node.
- 框架的使用

\$ = JQuery

- 被占用
- jQuery.noConflict(); 释放对\$的引用

## jQuery 书写方式

> 入口函数:

1. `$(document().ready(function(){}))`
2. `$(function(){})`
3. `$().ready({})`

> 区别 onload ready

1. onload 是所有资源加载完毕
2. ready dom 结构加载完成, 不包括图片和非文本

## 选择器

- 最为强大的一点
  > 返回的都是 jquery 对象,每一个对象都是引用 Dom 节点的对象

> 如果传入的是 undefined || null ,返回空数组[]

### 基本选择器

1. Id 选择器
1. 标签选择器
1. Class 选择器
1. 通配选择器

### 多项选择器

1. 用逗号分割,将匹配的选择器,合并到一起返回
1. 选择会按照 DOM 顺序选择

### 层级选择器

1. 后代选择器
1. 子代选择器
1. 相邻兄弟选择器
1. 通用兄弟选择器

### 属性选择器

1. 属性名选择器 `[attr]`
1. 属性值选择器 `[attr=val]`
1. 属性值不等于值选择`[attr!=val]`
1. 开头选择器`[attr^=val]`
1. 结尾选择题`[attr$=val]`
1. 包含选择器 `[attr*=val]`
1. 筛选属性选择器`[attr][attr2]`

### 过滤器

1. 第 1 个子标签
1. 最后一个子标签
1. 第 n 个子标签`nth-child(n)`
1. 只有一个子标签 `only-child`
1. 第 1 个指定属性子标签 `first-of-type`
1. 最后一个指定属性子标签
1. 第 n 个指定属性子标签 `nth-of-type(n)`
1. 从后往前选第 n 个指定属性子标签
1. 只有一个指定属性子标签

### 表单相关

1. `:input` 选择
1. `:text` 匹配所有的单行文本框
1. `:[type]` 有的类型都能匹配

- `:password | :radio`

> 状态

1. `:enabled` 所有可用的
1. `:disabled` 所有不可用的
1. `:checked` 单选复选
1. `:selected` Option.中的 Selected.

### 查找和过滤

1. find() 搜索所有与指定表达式匹配的元素
1. children() 子代选择器
1. parent() 父元素
1. next() 相邻的下一个元素
1. prev() 相邻的上一个元素
1. eq() 选择索引为
1. siblings() 同一层的所有兄弟元素
1. filter() 筛选出与指定表达式匹配的元素

## Jq 事件

