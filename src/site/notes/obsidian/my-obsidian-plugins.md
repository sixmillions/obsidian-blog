---
{"title":"obsidian插件","slug":"my-obsidian-plugins","description":"常用插件介绍","author":"six","created":"2023-08-28 08:30","updated":"2023-08-28 15:15","cover":"https://picsum.photos/720/400","tags":["obsidian"],"categories":["obsidian"],"dg-publish":true,"permalink":"/obsidian/my-obsidian-plugins/","dgPassFrontmatter":true}
---

## 允许使用社区插件

![](https://s.sixmillions.cn/img/2023/08/28/005955483.png)

浏览下载社区插件

![](https://s.sixmillions.cn/img/2023/08/28/010046829.png)

## Image Uploader

图片上传的时候调用自定义图片上传接口

![](https://s.sixmillions.cn/img/2023/08/28/011931392.png)

如果你api需要认证信息，可以填写到Header中

例如，我的接口返回是，那我就填写 `url`

```json
{
  "url": "https://xxx/xxx.png"
}
```

我的插件配置文件 `data.json`

```json
{
  "apiEndpoint": "https://cfw.6bw.fun/s3/obj/img",
  "uploadHeader": "{\n  \"Authorization\": \"Bearer yourToken\"\n}",
  "uploadBody": "{\n  \"file\": \"$FILE\"\n}",
  "imageUrlPath": "url",
  "maxWidth": 4096,
  "enableResize": false
}
```

## digital-garden

将笔记上传到GitHub，然后部署到Vercel，实现在线访问

[[obsidian/publish-by-oleeskild-digital-garden\|publish-by-oleeskild-digital-garden]]

## Calendar

方便创建/跳转到当天的工作报告

## obsidian-image-toolkit

图片查看插件，点击可以放大旋转图片

## url-into-selection

复制一个url，然后选文字可以粘贴成链接

## file-explorer-note-count

统计每个目录下的笔记数量

## recent-files-obsidian

最近打开的笔记

## remotely-save

> https://github.com/remotely-save/remotely-save

将笔记保存到支持S3协议的OSS

![](https://s.sixmillions.cn/img/2023/08/28/043509403.png)

1. 配置地址，区域，密钥
2. 自建的MinIO，需要使用 `Path-Style` 这种风格
3. 点击 `Check` 检查连通性
4. 其他使用了默认配置，没有上传 `.obsidian` 下的内容
5. 如果语言设置为中文，则上面的也会是中文解释

## table-editor-obsidian

方便操作Markdown中的表格

> https://github.6bw.fun/tgrosinger/advanced-tables-obsidian

1. 输入 `|` ;
2. 输入列标题，然后按 `Tab`键；
3. 重复第二步，直到所有标题输入完毕，然后按`回车`键；
4. 此时光标来到表格的第一行；
5. 输入列的内容，然后按`Tab`键；
6. 重复第五步，直到所有列的内容输入完毕，如果需要增加新行，按`回车`键；

| 快捷键（Hotkey） | 效果                     |
| ---------------- | ------------------------ |
| Tab              | 切换到下一个单元格       |
| Shift + Tab      | 切换到前一个单元格       |
| Enter            | 切换到下一行             |
| Ctrl + Shift + D | 在侧边栏打开表格控制面板 |

## webpage-html-export

导出html插件，可以保留主题式样

## obsidian-tasks-plugin

任务管理插件

## obsidian-git

笔记同步到GIt

## obsidian-excalidraw-plugin

手绘风格白板应用

![](https://s.sixmillions.cn/img/2023/08/28/055434725.png)

## dataview

数据查询插件

- [[obsidian/my-obsidian-config\|my-obsidian-config]]
- [[obsidian/my-obsidian-plugins\|my-obsidian-plugins]]
- [[obsidian/obsidian-calendar-plugin\|obsidian-calendar-plugin]]
- [[obsidian/publish-by-oleeskild-digital-garden\|publish-by-oleeskild-digital-garden]]
- [[obsidian/use-templdates\|use-templdates]]

{ .block-language-dataview}

