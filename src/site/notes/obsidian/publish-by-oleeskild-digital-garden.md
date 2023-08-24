---
{"title":"obsidian发布Web","slug":"publish-by-oleeskild-digital-garden","description":"通过oleeskild提供的模板(digitalgarden)，将笔记部署到vercel，方便分享和访问","author":"six","created":"2023-08-23","cover":"https://s.sixmillions.cn/img/logo/logo.png","tags":["obsidian"],"categories":["obsidian"],"dg-publish":true,"updated":"2023-08-24","permalink":"/obsidian/publish-by-oleeskild-digital-garden/","dgPassFrontmatter":true}
---

## 发布笔记

使用 `Digital Obsidian Garden` 发布Obsidian笔记

> https://dg-docs.ole.dev/
## 准备

1. GitHub账号，并且申请一个token
2. Vercel账号，先登录，关联GithHub账号

## 部署

### 点击部署

访问

https://github.com/oleeskild/digitalgarden

点击 “Deploy” 按钮，会跳转到vercel部署界面

### 填写仓库地址

vercel会自动创建该Git仓库

![](https://s.sixmillions.cn/ddd/nihao.png)

## 下载插件

Obsidian下载插件 `Digital Garden` ，然后配置插件

- GItHub仓库名（上面创建的）
- GitHub用户名
- GetHub的token

## 发布笔记

新建笔记，然后输入front-matter

```yaml
---
dg-home: true
dg-publish: true
---
```

- dg-home是主页，有一个文件配置即可
- dg-publish，只有配置了，并且是true，才会发布

`ctrl + p` -> `dgps` (Digital Garden: Publish Single Note)

访问vercel项目的地址

## 修改

知道了它的套路

1. 发布笔记的时候就是向 `src/site/notes` 上传md文件
2. obsidian更新该插件的配置的时候，本地存在 `data.json` ,修改Git仓库的 `.env` 中对应值
3. 升级了一些依赖包版本
4. 修改了 `favicon.svg`
5. 修改了图片的式样，修改了文章显示的式样

按照自己的喜好定制后，上传到Git仓库，然后在Vercel部署

部署模板选择 `Eleventy`

![](https://s.sixmillions.cn/img/2023/08/24/061540050.png)


插件本地配置

![](https://s.sixmillions.cn/img/2023/08/24/060255509.png)

`data.json` 如下

```json
{
  "githubRepo": "obsidian-blog",
  "githubToken": "xxxxx",
  "githubUserName": "sixmillions",
  "gardenBaseUrl": "https://blog.6bw.fun",
  "prHistory": [],
  "baseTheme": "dark",
  "theme": "{\"name\":\"Red Graphite\",\"author\":\"SeanWcom\",\"repo\":\"seanwcom/Red-Graphite-for-Obsidian\",\"screenshot\":\"thumbnail.png\",\"modes\":[\"dark\",\"light\"],\"cssUrl\":\"https://raw.githubusercontent.com/seanwcom/Red-Graphite-for-Obsidian/HEAD/theme.css\"}",
  "faviconPath": "",
  "noteSettingsIsInitialized": true,
  "siteName": "Six Blog",
  "slugifyEnabled": false,
  "noteIconKey": "dg-note-icon",
  "defaultNoteIcon": "",
  "showNoteIconOnTitle": false,
  "showNoteIconInFileTree": false,
  "showNoteIconOnInternalLink": false,
  "showNoteIconOnBackLink": false,
  "showCreatedTimestamp": true,
  "createdTimestampKey": "created",
  "showUpdatedTimestamp": true,
  "updatedTimestampKey": "updated",
  "timestampFormat": "MMM dd, yyyy h:mm a",
  "styleSettingsCss": "",
  "pathRewriteRules": "",
  "customFilters": [],
  "contentClassesKey": "dg-content-classes",
  "defaultNoteSettings": {
    "dgHomeLink": true,
    "dgPassFrontmatter": true,
    "dgShowBacklinks": false,
    "dgShowLocalGraph": false,
    "dgShowInlineTitle": true,
    "dgShowFileTree": true,
    "dgEnableSearch": true,
    "dgShowToc": true,
    "dgLinkPreview": false,
    "dgShowTags": true
  }
}
```







