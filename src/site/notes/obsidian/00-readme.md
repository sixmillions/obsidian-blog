---
{"title":"00-readme","slug":"obsidian-env-init","description":"obsidian新工作区初始化","author":"six","created":"2023-08-28","updated":"2023-08-28","cover":"https://picsum.photos/720/400","tags":["obsidian"],"categories":["js"],"dg-publish":true,"permalink":"/obsidian/00-readme/","dgPassFrontmatter":true}
---


## 环境初始化

使用自己的工作区模板

```bash
git clone https://github.com/sixmillions/obsidian-starter.git
```

## 配置介绍

[[obsidian/my-obsidian-config\|my-obsidian-config]]

## 插件介绍

[[obsidian/my-obsidian-plugins\|my-obsidian-plugins]]
## 修改

clone模板后，新工作区要修改的地方

###  `Remotely Save` 存储桶修改

在MinIO建立新的Bucket后，修改备份到MinIO的存储位置

![](https://s.sixmillions.cn/img/2023/09/02/001323630.png)


### `Digital Garden` 修改

GitHub建立新的笔记发布仓库后，发布到Vercel，然后修改插件配置中的仓库名字

Cloudflare建立子域名，指向Vercel
![](https://s.sixmillions.cn/img/2023/09/02/001810285.png)
