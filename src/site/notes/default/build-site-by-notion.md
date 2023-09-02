---
{"title":"使用notion搭建网站","slug":"build-site-by-notion","description":"使用notion搭建网站","author":"six","created":"2023-04-11","updated":"2023-09-02","cover":"https://picsum.photos/720/400","tags":["dev","notion"],"categories":["default"],"dg-publish":true,"permalink":"/default/build-site-by-notion/","dgPassFrontmatter":true}
---

# 教程

> [史上最完整NOTION制作网站教程 (notions.ga)](https://notions.ga/)

# 申请一个域名解析到cloudflare

# 创建workers

可以修改一个喜欢的名字，也可以不改，使用默认的

![](https://s.sixmillions.cn/img/2023/04/07/213053dtgw.png)

创建service

![](https://s.sixmillions.cn/img/2023/04/07/2132467e3y.png)

添加worker域名

![](https://s.sixmillions.cn/img/2023/04/07/213336eeh0.png)

# 配置DNS解析

我这里将blog这个子域名解析到notion，配置CNAME，如下

![](https://s.sixmillions.cn/img/2023/04/07/214046mwwl.png)

# 配置worker路由

在解析的域名里面配置刚才创建worker的路由

![](https://s.sixmillions.cn/img/2023/04/07/2136018p6f.png)

访问测试，发现路由到了worker

![](https://s.sixmillions.cn/img/2023/04/07/214136myss.png)

# 配置worker的代理内容

> [React App (notions.ga)](https://edit02.notions.ga/)

![](https://s.sixmillions.cn/img/2023/04/07/2155500skl.png)

分享自己的notion地址：

![](https://s.sixmillions.cn/img/2023/04/07/215801eqaf.png)

配置：

![](https://s.sixmillions.cn/img/2023/04/07/215153porz.png)

可以设置网站内容

![](https://s.sixmillions.cn/img/2023/04/07/2159366amj.png)

编辑worker

![](https://s.sixmillions.cn/img/2023/04/07/220124qm17.png)


将代码copy到worker，修改域名

![](https://s.sixmillions.cn/img/2023/04/07/220047grlw.png)

# 最终效果

![](https://s.sixmillions.cn/img/2023/04/07/220244u4yd.png)

因为上面就是个代理的过程，你编辑notion后，会自动更新网站内容