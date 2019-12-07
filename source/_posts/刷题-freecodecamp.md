---
title: freecodecamp
tags: fcc 
date: 2018-12-01 07:59:35
categories: 刷题
---

## 解题

### 1. Check for Palindromes

```js
function palindrome(str) {
  // 请把你的代码写在这里
  var string = str.toLowerCase().replace(/[\W_]+/g, '');
  var rString = string
    .split('')
    .reverse()
    .join('');
  if (string == rString) {
    return true;
  }

  return false;
}

palindrome('almostomla');
```

考察正则及 js 基础的应用

<!-- more -->

### 2. Find the Longest Word in a String

```js
function findLongestWord(str) {
  // 请把你的代码写在这里
  var string = str.split(' ');
  var firstString = string[0];
  for (var i = 0; i < string.length; i++) {
    if (string[i].length > firstString.length) {
      firstString = string[i];
    }
  }
  return firstString.length;
}

findLongestWord('The quick brown fox jumped over the lazy dog');
```

循环遍历找到

### 3.Title Case a Sentence

```js
function titleCase(str) {
  // 请把你的代码写在这里
  var string = str.split(' ');
  var sum = [];
  for (var i = 0; i < string.length; i++) {
    var list = string[i].split('');

    for (var j = 0; j < list.length; j++) {
      if (list.length == 1) {
        list[j] = list[j].toUpperCase();
      } else {
        list[0] = list[0].toUpperCase();
        list[j] = list[j].toLowerCase();
      }
    }

    sum[i] = list.join('');
  }
  return sum.join(' ');
}

titleCase("I'm a little tea pot");
```

自己写的方法 只是符合题目

```js
// 更好的解决方案
function titleCase(str) {
  return str
    .toLowerCase()
    .split(' ')
    .map(function(word) {
      return word.charAt(0).toUpperCase() + word.slice(1); // 创建新的字符串
    })
    .join(' ');
}
titleCase("I'm a little tea pot");
```

### 4. Return Largest Numbers in Arrays

```js
// 相当原始的解决方法
function largestOfFour(arr) {
  // 请把你的代码写在这里
  var sum = [];
  for (var i = 0; i < arr.length; i++) {
    var max = arr[i];
    var maxF = max[0];

    for (var j = 0; j < max.length; j++) {
      if (maxF < max[j]) {
        maxF = max[j];
      }
    }
    sum.push(maxF);
  }

  return sum;
}

largestOfFour([
  [4, 5, 1, 3],
  [13, 27, 18, 26],
  [32, 35, 37, 39],
  [1000, 1001, 857, 1]
]);
```

纯粹的比较大小

```js
function largestOfFour(arr) {
  // 请把你的代码写在这里
  var sum = [];
  for (var i = 0; i < arr.length; i++) {
    var max = Math.max.apply(null, arr[i]);
    sum[i] = max;
  }
  return sum;
}

largestOfFour([
  [4, 5, 1, 3],
  [13, 27, 18, 26],
  [32, 35, 37, 39],
  [1000, 1001, 857, 1]
]);
```

### 5. Confirm the Ending

```js
function confirmEnding(str, target) {
  // 请把你的代码写在这里
  return str.substr(-target.length) === target;
}

confirmEnding('Bastian', 'n');
```

### 6. Repeat a string repeat a string

```js
function repeat(str, num) {
  // 请把你的代码写在这里
  var sum = '';
  while (num > 0) {
    num--;
    sum += str.substr(0);
  }
  return sum;
}

repeat('abc', 3);
```
