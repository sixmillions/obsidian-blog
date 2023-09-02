---
{"title":"lua开发环境搭建","slug":"01-init-lua-dev-env","description":"笔记描述","author":"six","created":"2023-06-06","updated":"2023-09-02","cover":"https://picsum.photos/720/400","tags":["lua"],"categories":["lua"],"dg-publish":true,"permalink":"/other/lua/01-init-lua-dev-env/","dgPassFrontmatter":true}
---

# windows

## 准备

- [idea社区版](https://www.jetbrains.com/idea/download/#section=windows)
- [插件emmylua](https://emmylua.github.io/zh_CN/installation/repo.html)
- l[ua54_win](https://sourceforge.net/projects/luabinaries/files/5.4.2/Tools%20Executables/)

## 安装

### idea

安装idea社区版就行，如果已经再使用旗舰版也没问题

> https://www.jetbrains.com/idea/download/#section=windows

### lua

> https://sourceforge.net/projects/luabinaries/files/5.4.2/Tools%20Executables/

![](https://s.sixmillions.cn/img/2023/02/27/151106e5vx.png)

下载解压到自己习惯的目录下，配置环境变量

![](https://s.sixmillions.cn/img/2023/02/27/151414gesm.png)

### 插件

在idea插件市场搜索安装即可

![](https://s.sixmillions.cn/img/2023/02/27/15001473lt.png)

安装后重启

## 新建lua项目

![](https://s.sixmillions.cn/img/2023/02/27/150257fzwu.png)

![](https://s.sixmillions.cn/img/2023/02/27/150414dvvc.png)

## 配置lua SDK

打开项目设置

![](https://s.sixmillions.cn/img/2023/02/27/150606n6kv.png)

选中lua，点击右侧 `Edit`  
将path指向自己lua的路径

![](https://s.sixmillions.cn/img/2023/02/27/150900y2tq.png)

## 设置src目录

必须将源码的根目录设置为 `Sources` 目录。不然运行起来有问题。如果按照上面步骤创建，src就应该是蓝色的 `Sources` 目录

![](https://s.sixmillions.cn/img/2023/02/27/152243roz6.png)

如果不是，按照下面方法去设置指定 `Source` 目录

具体做法是打开菜单 `File` -> `Project Structure` 打开 `Project Structure` 设置面板，点击右侧的 `Add Content Root` 来添加你的源码根目录，然后点击 `Mark as Sources` 标记。

![](https://s.sixmillions.cn/img/2023/02/27/15240147mc.png)

## 修改运行模板

该插件默认运行lua文件的解释器是 `lua.exe`，但是我们安装的是 `lua54.exe`  

![](https://s.sixmillions.cn/img/2023/02/27/152955v8yt.png)


**不修改运行模板是找不到lua解释器的**

默认配置是 `lua.exe`

![](https://s.sixmillions.cn/img/2023/02/27/1528016p0v.png)

修改为 `lua54.exe`，修改后运行的时候就能找到我们配置的lua SDK了

![](https://s.sixmillions.cn/img/2023/02/27/153110up1s.png)

刚才我们配置的SDK如下

![](https://s.sixmillions.cn/img/2023/02/27/153321e5j3.png)

## 运行HelloWorld

开始运行我们第一个例子，HelloWorld

运行前最好重启一下idea，我配置后第一次没识别出来lua54命令

和java一样，我习惯建一个包，放到包里面，不然都放到src，时间长了很乱

![](https://s.sixmillions.cn/img/2023/02/27/153734lmn7.png)

![](https://s.sixmillions.cn/img/2023/02/27/16041234cz.png)

输入代码

```lua
print("Hello World")
```

右键，运行代码

![](https://s.sixmillions.cn/img/2023/02/27/160547i282.png)

结果

![](https://s.sixmillions.cn/img/2023/02/27/160618yitx.png)

## 修改文件注释模板

```text
---
--- Author:      sixmillions
--- DateTime:    ${DATE} ${TIME}
--- Description: #[[$DESCRIPTION$]]#
---

#[[$END$]]#
```

![](https://s.sixmillions.cn/img/2023/02/27/163034ak71.png)

勾选上 `Enable Live Templates`

这样新建一个文件，首先会编辑DESCRIPTION，编辑好后一回车（或者tab），光标就定位到了END位置

## lua编译级别

![](https://s.sixmillions.cn/img/2023/02/27/175020n22a.png)
