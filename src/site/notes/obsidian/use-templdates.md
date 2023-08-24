---
{"title":"obsidian中使用模板","slug":"use-templdates","description":"在OB中使用模板，快速创建内容","author":"six","created":"2023-08-24 15:15","updated":"2023-08-24 15:15","cover":"https://picsum.photos/720/400","tags":["obsidian"],"categories":["obsidian"],"dg-publish":true,"permalink":"/obsidian/use-templdates/","dgPassFrontmatter":true}
---

## 模板简创建

建立存放模板的文件夹，一般起名 `templdates`

新建模板笔记，例如，我需要在每一篇笔记之前增加front-matter

![](https://s.sixmillions.cn/img/2023/08/24/073743352.png)


```yaml
---
title: 笔记标题
slug: "{{date}}-{{time:HH}}"
description: 描述
author: six
created: "{{date}} {{time}}"
updated: "{{date}} {{time}}"
cover: https://picsum.photos/720/400
tags:
 - obsidian
 - dev
categories:
 - js
 - cloudflare
dg-publish: false
---
```

点击右下角 Settings -> Templdates -> 选择刚才存放目录的文件夹

![](https://s.sixmillions.cn/img/2023/08/24/071039071.png)

## 使用

新建一篇笔记，需要插入刚才的模板，就可以

`ctrl + p` -> `tempi` -> 选择要插入的模板

![templdate-insert](https://s.sixmillions.cn/img/2023/08/24/071346617.png)

