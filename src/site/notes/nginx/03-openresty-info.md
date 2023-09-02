---
{"title":"openresty介绍","slug":"03-openresty-info","description":"openresty介绍","author":"six","created":"2023-03-03","updated":"2023-09-02","cover":"https://picsum.photos/720/400","tags":["nginx","openresty"],"categories":["nginx"],"dg-publish":true,"permalink":"/nginx/03-openresty-info/","dgPassFrontmatter":true}
---

# 高性能服务端

高性能要素

- 缓存
- 支持异步非阻塞

## 缓存

- 内存 > SSD > 机械硬盘
- 本机 > 网络
- 进程内 > 进程间

## 异步非阻塞

用事件驱动的方式去实现，不用让CPU傻等着

用同步的编码方式实现异步编程

# OpenResty

作者：章亦春

官方介绍

> OpenResty® 是一个基于 [Nginx](https://openresty.org/cn/nginx.html "Nginx") 与 Lua 的高性能 Web 平台，其内部集成了大量精良的 Lua 库、第三方模块以及大多数的依赖项。用于方便地搭建能够处理超高并发、扩展性极高的动态 Web 应用、Web 服务和动态网关。


