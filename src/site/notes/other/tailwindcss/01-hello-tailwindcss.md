---
{"title":"tailwindcss简单使用","slug":"01-hello-tailwindcss","description":"笔记描述","author":"six","created":"2023-03-27","updated":"2023-09-02","cover":"https://picsum.photos/720/400","tags":["css","tailwindcss"],"categories":["css"],"dg-publish":true,"permalink":"/other/tailwindcss/01-hello-tailwindcss/","dgPassFrontmatter":true}
---


# Tailwind CSS

一个css原子类框架

> [Tailwind CSS - Rapidly build modern websites without ever leaving your HTML.](https://tailwindcss.com/)

# Hello World

> https://play.tailwindcss.com/

```html
<div class="max-w-xl p-2 text-center">
  <h2 class="mb-2 text-2xl font-bold">Hello World</h2>
</div>
```

```html
<div class="flex flex-col md:flex-row md:space-x-3">
  <div><a href="" class="hover:text-blue-500">Item1</a></div>
  <div><a href="" class="hover:text-blue-500">Item2</a></div>
</div>
```

# 工具

- VS Code
- node.js
- git
- Live Server
- Tailwind CSS IntelliSense
- PostCss Language Support
- Prettier - Code formatter
- Auto Rename Tag

# Emmet语法

```text
# 快速生成10个div，内容是Item和序号
div{Item $}*5

# div类名是text-center
div.text-center
.text-center

# 复杂一些
div.text-center>a.text-bold{Link $}*2
# 结果
<div class="text-center">
  <a href="" class="text-bold">Link 1</a>
  <a href="" class="text-bold">Link 2</a>
</div>
```

**提示**需要一个配置文件 `tailwind.config`，根据情况适当修改

```js
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: [
    "./**/*.{html,vue,js,ts,jsx,tsx}",
  ],
  theme: {
    extend: {},
  },
  plugins: [],
}
```