---
title: Ubuntu基本使用
tags: 
- Ubuntu
- 入门
date: 2018-12-01 07:59:35
categories: 服务器
---

# ubuntu 基本使用

## 后台进程查看

#### 运行

```
nohup（不会被kill） python -u R.py > out.log 2>&1 &（后台运行）
```

<!-- more -->

#### 查看

```shell
ps -ef

ps -aux|grep chat.js
```

#### 终止

```shell
kill -9  强行删除进程号
```



## 文件目录操作

亲爱的，在 Ubuntu 下面使用命令行来对文件进行批量操作是非常方便的，以前在 windows 底下对文件进行复制、移动、删除的时候，都是用鼠标一框，然后右键或者快捷键执行操作，还要几个窗口之间来回切换，窗口多了之后会很麻烦，在 ubuntu 底下就只需记得下面几个命令：

1.进入文件夹

先按 ctrl + alt + T 打开命令行终端，在终端里一般使用`cd 目录名`的命令，例如：

```text
cd /home/ubuntu/downloads/
```

这样就能进入到 downloads 这个文件夹里面了，还有一些更方便的命令：

```python3
cd ..    # 进入上一个文件夹
cd ../..    # 进入上两个文件夹
cd -    # 去到进入当前文件夹之前的那个文件夹
```

2.复制文件

一般用 cp 命令：

```text
cp 目标文件路径 你想移动到的目录
```

一些例子：

```text
cp file.txt /home/ubuntu/downloads/    # 把当前文件夹底下的file.txt文件复制到downloads文件夹下
cp /home/ubuntu/a/a.txt /home/ubuntu/b/    #把其它文件夹里的文件复制到别的文件夹里，只需写全文件夹的绝对路径
cp -r files/ ..    # 把当前文件夹底下的files文件夹，全部复制到上一层目录当中去， 复制整个文件夹就需要加上-r
```

3.移动文件

移动文件就要用 mv，也就是 move 的缩写：

```text
mv 目标文件路径 你想移动到的目录
```

命令跟 cp 基本上是一样的：

```text
mv file.txt /home/ubuntu/downloads/    # 把当前文件夹底下的file.txt文件移动到downloads文件夹下
mv /home/ubuntu/a/a.txt /home/ubuntu/b/    #把其它文件夹里的文件复制到别的文件夹里，只需写全文件夹的绝对路径
mv -r files/ ..    # 把当前文件夹底下的files文件夹，全部复制到上一层目录当中去， 复制整个文件夹就需要加上-r
```

4.删除文件

在工作的时候，删除文件是一个很危险的行为，假如输错了命令，很可能会把一些重要的文件删除掉，而且 ubuntu 是没有回收站这一概念的，当然一般公司的运维同事会让你用别的命令来代替，这样就安全多了。

```text
rm 你想删除的文件名
rm -r 你想删除的文件夹    # 涉及到文件夹都加-r
```

**注意！以下命令慎用！**

```text
rm -rf 文件夹    # 这是强制删除文件夹内所有文件的命令，很危险，实在删除不了才用，删除前反复确认文件夹名字
```

## vim 编辑器

ubuntu 的命令行终端是没有像 windows 底下的 txt 编辑器或者 pycharm 这种有图形界面的编辑软件的，在终端下面，你想要编辑你的代码文件的话，就要用`vim`命令。

比如，你想编辑某个.py 文件，可以使用以下命令：

```text
vim helloworld.py    # vim + 你想编辑的文件夹路径
```

![img](https://pic2.zhimg.com/80/v2-4127b4baf4aa3e650a2f8a467bbf5d7d_hd.jpg)图 1

如图 1，vim 打开 helloworld.py 文件就是这个界面，这时你想直接打字是没反应的，必须先按下键盘上的“i”键，进入编辑模式，如图 2：

![img](https://pic1.zhimg.com/80/v2-110fec41c2146556cf4dc4dd83646794_hd.jpg)图 2

从图 2 可以看到，现在是“INSERT”模式。这里输入一句新的命令之后，要保存退出的话，必须先按下键盘左上角的“ESC”键，退出编辑模式，然后输入`:wq`，注意是冒号加上 wq 两个字母，这是确认修改保存并退出的命令，按下回车即可退出。（当时连如何保存退出都琢磨了好久才知道……）

![img](https://pic3.zhimg.com/80/v2-365d26a90dca10e1e0aa6519067321ea_hd.jpg)图 3

如果你不想保存就退出，可以在退出编辑模式后输入`:q!`回车，即可退出。下面还有一些有用的链接，vim 还有很多实用的命令：

[vim 编辑器操作命令大全-绝对全 - CSDN 博客](http://link.zhihu.com/?target=http%3A//blog.csdn.net/xuesnowce/article/details/53117352)

## 安装软件

windows 安装软件的时候都是下载一个.exe 文件，双击打开一路 next 就可以安装，ubuntu 的话经常实用命令行来安装软件，下面有几种常见的方式：

\1. deb 包

ubuntu 的 deb 包相当于 windows 的 exe 文件，如果你用 ubuntu 的桌面版，是可以直接双击安装的（只能是 ubuntu 官方指定的软件，其它软件无法用这种方式安装）。如果用命令行，可以输入以下命令：

```text
sudo dpkg -i *.deb    # 注意“*.deb”的意思是你的deb包的全称，请用软件包的名字替换掉星号
```

2.apt-get 安装

ubuntu 有包含了很多各式各样的软件的官方软件源，你可以用以下命令来从官方源中安装软件：

```text
sudo apt-get update    # 更新一下软件源，获取最新软件的列表
sudo apt-get install 软件名    # 安装软件
```

\3. .sh、.py、.run 文件

[如果你下载了后缀为 .sh](http://link.zhihu.com/?target=http%3A//%25E5%25A6%2582%25E6%259E%259C%25E4%25BD%25A0%25E4%25B8%258B%25E8%25BD%25BD%25E4%25BA%2586%25E5%2590%258E%25E7%25BC%2580%25E4%25B8%25BA.sh)、.py、.run 这些文件，一般可以用下面这种方法来安装：

```text
sh 软件名.sh
sh 软件名.run
python xxx.py
```

.run 文件也有这样的安装方法：

```text
chmod +x  *.run    # 先给这个run文件可执行的权限
./*.run    # 文件名前面加上./即可安装
```

还有更多的文件安装方式，比如二进制文件、rpm 包等等，遇到的话就点进这个链接看看吧：

[Ubuntu Linux 下安装软件方法](http://link.zhihu.com/?target=http%3A//www.linuxidc.com/Linux/2015-01/111216.htm)

## 一些提高工作效率的命令

1.tmux

tmux 是一个多窗口工具，你只需要在一个窗口当中输入 tmux，然后输入一些命令可以把窗口分成一块一块，可以在一个窗口里面执行多个任务，不需要切换窗口。

图 4

tmux 可以允许在同一个会话窗口当中显示多个子窗口，方便在同一个屏幕内进行多个任务处理，如上图所示，新建了 3 个子窗口，可以同时进行多个任务。

ubuntu 下安装 tmux 见这里：[tmux+ubuntu 64 安装](http://link.zhihu.com/?target=http%3A//www.jianshu.com/p/03971b5ed5da)

CentOS 下安装 tmux 见这里：[CentOS 下安装 tmux - 作业部落 Cmd Markdown 编辑阅读器](http://link.zhihu.com/?target=https%3A//www.zybuluo.com/mwumli/note/149542)

安装完毕后，使用操作是先在命令行输入 tmux，进入 tmux 新窗口界面后，先按下键盘上`ctrl + B`，**然后松开**（记得要松开），接着马上按下`shift + %`就可以实现左右分隔窗口。或者先按下`ctrl + B`，**然后松开**，再按下`shift + "`就可以实现上下分隔窗口。详细命令看这里：[Tmux 快捷键 & 速查表](http://link.zhihu.com/?target=https%3A//gist.github.com/ryerh/14b7c24dfd623ef8edc7)

2.资源监控命令

有时候你需要考虑到运行代码时，电脑资源的使用情况，ubuntu 没有像 windows 那样的资源管理器的界面，但是可以用命令来监控：

显卡内存监控：

```text
watch -n 0.1 nvidia-smi    # watch -n 0.1的意思是以0.1秒的时间间隔刷新nvidia-smi的数据显示
```

![img](https://pic1.zhimg.com/80/v2-7b92c5530321377a828e4d281662990c_hd.jpg)

内存使用监控：

```text
watch -n 0.1 free -h    # free是内存显示命令，-h是以人类能读懂的格式显示
```

![img](https://pic4.zhimg.com/80/v2-9282bb108c02c2e3e6a5801b8b4ce6e7_hd.jpg)

3.后台运行命令

有些时候你需要把任务扔到后台让它慢慢执行，然后你继续干其它工作，这时候可以用到下面的命令：

```text
python helloworld.py &    # 最后面加个&即可进入后台运行
```

如果你不想你的代码在后台运行的时候被杀掉，就在前面加上“nohup”：

```text
nohup python helloworld.py &
```

4.杀死进程

如果后台有一些进程你不想再运行了，但又不会自动关闭，就要手动 kill 掉进程，首先你必须找到这个进程的 pid：

```text
ps -aux | grep python    # grep python的意思是过滤出跟python相关的进程
```

找到你的进程之后，看 PID 那一列，这个数字就是你的进程 ID，然后输入：

```text
kill 你的PID
kill -9 你的PID    # 中间加上-9是强制杀死的命令
```

更详细的可以看这里：

[ubuntu 常用命令：[1\]ps 查看所有运行程序](http://link.zhihu.com/?target=https%3A//jingyan.baidu.com/article/a24b33cd55c3ba19ff002b4f.html)

5.一些快捷键

任务强行退出：键盘按下“ctrl + c”

任务后台运行：键盘按下“ctrl + z”

复制命令行某段文字：鼠标选中文字，键盘按下“ctrl + Ins”

把文本粘贴到命令行：键盘按下“shift + Ins”
