---
{"title":"联想小新pro16","slug":"lenovo-pro-16","description":"验机，使用问题","author":"six","created":"2023-04-10","updated":"2023-09-02","cover":"https://picsum.photos/720/400","tags":["QA"],"categories":["default"],"dg-publish":true,"permalink":"/default/lenovo-pro-16/","dgPassFrontmatter":true}
---

# 视频自动播放

暂停了视频，但是有时候会自动播放

关闭智能感知

![](https://s.sixmillions.cn/img/2023/02/02/215517rtwt.png)

# edge浏览器总是自动回到顶部

> [edge浏览器总是自动回到顶部 - Microsoft Community](https://answers.microsoft.com/zh-hans/microsoftedge/forum/all/edge%E6%B5%8F%E8%A7%88%E5%99%A8%E6%80%BB%E6%98%AF/6ed8bf5c-6029-4325-9d8d-b4af4a7aa6af)

![](https://s.sixmillions.cn/img/2023/02/08/221234yl9j.png)

# 输入法快捷键

右键输入法，输入法设置  
关闭 `ctrl + shift + f` 切换繁体  
中英切换保留一个 `shift`

![](https://s.sixmillions.cn/img/2023/02/08/211457evpt.png)

# alt+tab 切换

Win11 `alt + tab` 组合键在打开edg浏览器的情况下，会将浏览器tab也也显示出来  
我习惯，浏览器就显示一个窗口就行

![](https://s.sixmillions.cn/img/2023/02/08/211257c5mr.png)

# 验机

## 背景

京东买了一台联想小新pro16酷睿核显版本

1. 购买日期 20230128
2. 店铺 联想京东自营旗舰店
3. 价格5499
4. i5 12500H 16G 512G
5. 核显版本

## 验机参考

https://www.butiao.com/t/28933.html

https://www.xiaohongshu.com/explore/62b42352000000002103c266

## 准备

1. U盘
2. [图吧工具箱](http://www.tbtool.cn/)
3. 一个视频，最好是2k视频，可以从B站等网站下一个

## 实际

全程手机录像

1. 外包装有没有破损，封箱标有没有撕
2. 充电器电源应该有包装
3. 电脑外观查验，有没有划痕磕碰，
4. 尤其是D面，有没有磨损，螺丝有没有拆卸痕迹，脚垫有没有磨损，风扇有没有明显灰尘
5. 因为有运输保护，<span style="font-weight: bold; color: red">不插入充电器，是没法开机的</span>
6. 三码合一，外包装，机器背面，系统里面的S/N码

重点，<span style="font-weight: bold; color: red">开机后不要联网</span>

跳过联网步骤：  
①按shift+Fn+F10+回车
②输入taskmgr 按回车  
③在详细信息里找到 OOBENetworkConnectionFlow.exe 右键结束任务，就可以跳过了
或者
**Shift + F10**（**或者Fn+Shift+F10**），打开**cmd窗口**，输入命令：**oobe\BypassNRO.cmd**

图吧工具检测

1. 屏幕是否漏光
2. 闪烁，盒盖打开是否正常
3. Fn+空格，打开键盘灯，看一下有没有坏的不亮的

右键新建文档

1. 修改文件名
2. 测试键盘输入

播放视频

1. 屏幕清晰度
2. 两侧喇叭声音正常吗

其他测试

1. 测试摄像头/麦克风录音
2. USB插口
3. 耳机接口

