---
title: FCC Truncate a string 解决方法
date: 2018-06-06 11:58:18
tags: IFE
categories: 刷题
---

三行搞定

```javascript
function truncate(str, num) {
  ab =
    str.length > num
      ? num > 3
        ? str.slice(0, num - 3) + '...'
        : str.slice(0, num) + '...'
      : str;
  return ab;
}

truncate('A-tisket a-tasket A green and yellow basket', 11);
```

<!-- more -->

> 截断字符串

（用瑞兹来截断对面的退路）

如果字符串的长度比指定的参数`num`长，则把多余的部分用`...`来表示。

切记，插入到字符串尾部的三个点号也会计入字符串的长度。

但是，如果指定的参数`num`小于或等于 3，则添加的三个点号不会计入字符串的长度
