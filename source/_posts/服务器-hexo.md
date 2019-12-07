---
title: hexo配置以及美化
date: 2018-09-23 08:34:26
tags: 
- hexo
- 美化
- 主题
categories: 服务器
---

额...

为了重新记忆起以前如何配置的本网站的页面,决定直接更新 next 主题最新的版本,来开始一步步的折腾:heart:
<!-- more -->
# 开始

安装完 next 6.0 以上主题之后

默认的 muse 布局可以接受,就直接开始搞:smile:

<!-- more -->

## 1.去除页脚的版本信息

虽然很感谢 nextz 主题,但是版本信息摆在那也是难看

打开主题根目录的`_config.yml` 文件

找到

![mark](http://pcnlwhjrw.bkt.clouddn.com/blog/180923/bm2I7j1g0h.png?imageslim)

都改成 false 就 OK![mark](http://pcnlwhjrw.bkt.clouddn.com/blog/180923/a44C0iLhhd.png?imageslim)

![mark](http://pcnlwhjrw.bkt.clouddn.com/blog/180923/39JiA39D2J.png?imageslim)

hexo 同理....

## 2.更改页面标签的小图标

我直接按着主题配置的循序开始优化

在 http://iconfont.cn 阿里的矢量图库 挑好图标后

在https://realfavicongenerator.net 生成网页用的图标

然后在![mark](http://pcnlwhjrw.bkt.clouddn.com/blog/180923/JDJdbH1iIm.png?imageslim)

把下载的图标放在 source/images

对应的 source 文件夹下图片对应的路径改变 即可

3.页脚的开始年份以及动态小心心

![mark](http://pcnlwhjrw.bkt.clouddn.com/blog/180923/mdiIEjmb8d.png?imageslim)

和上面一样改就行 下面是改变颜色的选项

## 4.设置头像

![mark](http://pcnlwhjrw.bkt.clouddn.com/blog/180923/Dblk2jFJh5.png?imageslim)

next 6.0 支持头像自定义呢 可以旋转 真心不错看图就可以啦 :smile:

5.设置打赏和版权信息

![mark](http://pcnlwhjrw.bkt.clouddn.com/blog/180923/EBal7KD56H.png?imageslim)

没想到现在都是自带啦...

![mark](http://pcnlwhjrw.bkt.clouddn.com/blog/180923/m33CE7ABCH.png?imageslim)

都很简单 如果没有的话 就下插件来搞定

## 6.本地搜索和保存书签

![mark](http://pcnlwhjrw.bkt.clouddn.com/blog/180923/hgF3hJjJCB.png?imageslim)

# 主题美化

## 1.页面布局美化

有前端基础即可

在浏览器中打开调试工具 F12

按 ctrl + shift +c 选择要修改的元素 可以直接在网页上修改 确定好属性后 在 source\css_custom\custom.styl 中添加即可

以后不需要了可以直接删除

##
