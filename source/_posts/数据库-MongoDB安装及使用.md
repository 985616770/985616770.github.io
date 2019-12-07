---
title: MongoDB安装及使用
tags: 
- 入门
- MongoDB
date: 2018-12-01 07:59:35
categories: 数据库
---

# MongoDB 安装及使用

### 下载

下载地址 : https://www.mongodb.com/download-center/community

根据版本下载

选择`custom`

自定义安装路径

取消左下角 comonjs 的勾选

<!-- more -->

### 使用

默认数据库位置在 `C:/data/db`

开启服务

在 C 盘位置输入

```
mongod
```

修改存储目录

```
mongod --dbpath 绝对路径
```

停止服务

```
ctrl + C
直接关闭窗口
```

连接服务

另开 cmd,输入

```
# 连接
mongo
# 断开
exit
```

### 基本命令

```
#查看数据库
show dbs

#切换到数据库
use 数据库名称

#查看当前的数据库
db

#插入数据
```

### MongoDB 介绍

- 可以有多个数据库
- 一个数据库可以有多个集合(表)
- 一个集合可以有多个文档(表记录)
- 文档结构很灵活,没有任何限制
- MongoDB 非常灵活,不需要像 mysql 一样先创建数据库,表,设计表结构
  - 在这里只需要: 当你需要插入数据的时候,只需要指定往哪个数据库的哪个集合操作就可以
  - MongoDB 自动完成建库建表的事情

```javascript
{
    qq:{
        users:[
            {name:'zhansan',age:11},
            {name:'zhansan',age:11},
            {name:'zhansan',age:11},
            {name:'zhansan',age:11},
            {name:'zhansan',age:11},
        ],
        products:[

        ]
    },
    taobao:{}
}
```

### node 中使用

#### 官方`mongodb`

**[node-mongodb-native](https://github.com/mongodb/node-mongodb-native)**

官方使用的接口 api

#### mongoose 第三方的包

基于官方的包开发的

```
npm i mongoose
```

### 实际开发

```javascript
// 连接
var mongoose = require('mongoose');
mongoose.connect('mongodb://localhost/test');
// 2. 设计文档结构（表结构）
// 字段名称就是表结构中的属性名称
// 约束的目的是为了保证数据的完整性，不要有脏数据
var userSchema = new Schema({
  username: {
    type: String,
    required: true // 必须有
  },
  password: {
    type: String,
    required: true
  },
  email: {
    type: String
  }
});
// 3. 将文档结构发布为模型
//    mongoose.model 方法就是用来将一个架构发布为 model
//    第一个参数：传入一个大写名词单数字符串用来表示你的数据库名称
//                 mongoose 会自动将大写名词的字符串生成 小写复数 的集合名称
//                 例如这里的 User 最终会变为 users 集合名称
//    第二个参数：架构 Schema
//
//    返回值：模型构造函数
var User = mongoose.model('User', userSchema);
// 4,增删改查
```

##### 增

```javascript
var admin = new User({
  username: 'zs',
  password: '123456',
  email: 'admin@admin.com'
});

admin.save(function(err, ret) {
  if (err) {
    console.log('保存失败');
  } else {
    console.log('保存成功');
    console.log(ret);
  }
});
```

##### 查

```javascript
User.find(function(err, ret) {
  if (err) {
    console.log('查询失败');
  } else {
    console.log(ret);
  }
});

User.find(
  {
    username: 'zs'
  },
  function(err, ret) {
    if (err) {
      console.log('查询失败');
    } else {
      console.log(ret);
    }
  }
);
User.findOne(
  {
    username: 'zs'
  },
  function(err, ret) {
    if (err) {
      console.log('查询失败');
    } else {
      console.log(ret);
    }
  }
);
```

##### 删除

```javascript
// 条件删除
User.remove(
  {
    username: 'zs'
  },
  function(err, ret) {
    if (err) {
      console.log('删除失败');
    } else {
      console.log('删除成功');
      console.log(ret);
    }
  }
);
// ID删除
findByIdAndDelete;
```

##### 改

```javascript
User.findByIdAndUpdate(
  '5a001b23d219eb00c8581184',
  {
    password: '123'
  },
  function(err, ret) {
    if (err) {
      console.log('更新失败');
    } else {
      console.log('更新成功');
    }
  }
);
```

## node 使用 MySQL
