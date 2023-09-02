---
{"title":"obsidian markdown语法扩展","slug":"obsidian-markdown","description":"obsidian对markdown语法的扩展，比如 Callouts","author":"six","created":"2023-09-02","updated":"2023-09-02","cover":"https://picsum.photos/720/400","tags":["obsidian"],"categories":["obsidian"],"dg-publish":true,"permalink":"/obsidian/obsidian-markdown/","dgPassFrontmatter":true}
---

## 标注(Callouts)

[官网演示](https://help.obsidian.md/How+to/Use+callouts)

> [!NOTE] 我是标注title
> 我是标注内容

> [!INFO] 我是标注title
> 我是标注内容

> [!ERROR] 我是标注title
> 我是标注内容

用加减可以展开折叠内容

> [!BUG]- 减号是折起来，预览模式点击可以展开/折叠
> 我是标注内容

> [!fail]+ 加号是展开，预览模式点击可以展开/折叠
> 我是标注内容

## 调整图片宽度

不用[[obsidian学习使用/Markdown语法展示.md#^3e20d6\|通过html编写样式了]]，可以直接在 `alt` 后面加上 `|` 加上具体宽度

![我是百度图片|200](https://s.sixmillions.cn/img/2023/01/15/125615467qvf9.png)

## 评论

语法 `%%评论内容%%` ，评论在编辑模式下可见，预览模式不可见

我说今天天气不错，你觉得呢？  
你说的对。



## 视频

可以使用图片语法嵌入YouTube视频，其他网站的不可以

> [Embedding web pages - Obsidian Help](https://help.obsidian.md/Editing+and+formatting/Embedding+web+pages)

![](https://www.youtube.com/watch?v=NnTvZWp5Q7o)

## 多行编辑

`alt + 鼠标左键`

1. aaaaa
2. bbbbb
3. cccc

