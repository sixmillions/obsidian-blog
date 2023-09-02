---
title: zincsearch搜索引擎
slug: zincsearch
description: 相对于ES，zinc是一个轻量的全文搜索引擎
author: six
created: 2023-08-31
updated: 2023-08-31
cover: https://picsum.photos/720/400
tags:
 - search
categories:
 - ddefault
dg-publish: true
---
## Source

> 文档地址：https://zincsearch-docs.zinc.dev

> GitHub: https://github.com/zincsearch/zincsearch

> 简单使用：https://www.cnblogs.com/lingkang/p/16698366.html

## 介绍/特点

1. 全文搜索的搜索引擎
2. 开源的，内置在 Go 中
3. 构建在 bluge 之上，这是一个出色的索引库
4. 资源利用率低
5. 易于使用的轻量级 GUI
6. 内置身份验证
7. 编程使用的简单 API
8. 10w条数据内存大约10MB左右

## 安装

> https://zincsearch-docs.zinc.dev/installation/

### Windows

下载

> https://github.com/zincsearch/zincsearch/releases/download/v0.4.8/zincsearch_0.4.8_Windows_x86_64.tar.gz

j解压后运行

```powershell
set ZINC_FIRST_ADMIN_USER=admin
set ZINC_FIRST_ADMIN_PASSWORD=admin
mkdir data
zincsearch.exe
```

### docker

```bash
mkdir data
docker run -v /full/path/of/data:/data -p 4080:4080 \
    -e ZINC_DATA_PATH="/data" \
    -e ZINC_FIRST_ADMIN_USER=admin -e ZINC_FIRST_ADMIN_PASSWORD=admin \
    --name zincsearch public.ecr.aws/zinclabs/zincsearch:0.4.8
```

或者使用docker-compose

```bash
mkdir -p /opt/zincsearch/data && cd /opt/zincsearch
# 放开权限，不然一会没有权限
chmod 777 data
vim docker-compose.yml
```

`docker-compose.yml`

```yml
version: "3"

services:
  search_server:
    image: public.ecr.aws/zinclabs/zincsearch:0.4.8
    container_name: zincsearch
    networks:
      - zincsearch_network
    volumes:
      - ./data/:/data
    ports:
      - "4080:4080"
    environment:
      - TZ=Asia/Shanghai
      - ZINC_DATA_PATH=/data
      - ZINC_FIRST_ADMIN_USER=admin
      - ZINC_FIRST_ADMIN_PASSWORD=admin

networks:
  zincsearch_network:
```

运行

```bash
docker-compose up -d
```

## 地址

> http://localhost:4080

swagger接口地址

使用的时候，记得先认证，然后选择 schema（http或者https）

![](https://s.sixmillions.cn/img/2023/08/31/055446780.png)

> http://localhost:4080/swagger/index.html

## 简单使用

### 创建索引

![](https://s.sixmillions.cn/img/2023/08/31/052837871.png)

### 添加记录

![](https://s.sixmillions.cn/img/2023/08/31/054955590.png)

```json
{
  "id": 1,
  "slug": "post-test-01",
  "title": "评天价雕塑被威胁导游已报案",
  "cnt": "近日，鲁山县因花费715万元修建雕塑引发关注。8月31日，“小黑诸鸣”称其已在滨江派出所报案，滨江派出所已经受理此案件。“小黑诸鸣”表示，选择报警主要是为了保护家人的安全。此前，“小黑诸鸣”因对鲁山天价雕塑发表评论而收到威胁邮件，要求其删除关于鲁山的相关视频，还附上了其子身份证号和家庭住址。“小黑诸鸣”称，事发后为以防万一，孩子已经送到学校住校，“只要孩子没事，其他都好说。 "
}
```
### 查询

> https://zincsearch-docs.zinc.dev/api/search/search/

![](https://s.sixmillions.cn/img/2023/08/31/055310974.png)

```json
{
    "search_type": "match",
    "query": {
        "term": "天价雕塑",
        "field": "_all"
    },
    "sort_fields": ["-@timestamp"],
    "from": 0,
    "max_results": 20
}
```

结果

```json
{
  "took": 0,
  "timed_out": false,
  "_shards": {
    "total": 3,
    "successful": 3,
    "skipped": 0,
    "failed": 0
  },
  "hits": {
    "total": {
      "value": 1
    },
    "max_score": 0.770576979781556,
    "hits": [
      {
        "_index": "blog",
        "_type": "_doc",
        "_id": "21mQsTadhL2",
        "_score": 0.770576979781556,
        "@timestamp": "2023-08-31T05:48:02.91809024Z",
        "_source": {
          "@timestamp": "2023-08-31T05:48:02.91809024Z",
          "cnt": "近日，鲁山县因花费715万元修建雕塑引发关注。8月31日，“小黑诸鸣”称其已在滨江派出所报案，滨江派出所已经受理此案件。“小黑诸鸣”表示，选择报警主要是为了保护家人的安全。此前，“小黑诸鸣”因对鲁山天价雕塑发表评论而收到威胁邮件，要求其删除关于鲁山的相关视频，还附上了其子身份证号和家庭住址。“小黑诸鸣”称，事发后为以防万一，孩子已经送到学校住校，“只要孩子没事，其他都好说。 ",
          "id": 1,
          "slug": "post-test-01",
          "title": "评天价雕塑被威胁导游已报案"
        }
      }
    ]
  }
}
```
## nginx配置

因为是服务器运行的zincsearch，所以顺便配置一下nginx

> https://github.6bw.fun/zincsearch/zincsearch/issues/37

`zincsearch.conf`

```nginx
server {
  listen                443;
  proxy_connect_timeout 60s;
  proxy_read_timeout    60s;
  proxy_send_timeout    60s;
  
  server_name zinc.sixmillions.cn;

  client_max_body_size 1024M;

  location / {
      # https需要转一下
      proxy_redirect http:// https://;
      # 跨域配置
      add_header Access-Control-Allow-Origin *;
      proxy_set_header Host $host;
      proxy_set_header Origin-Host $host;
      proxy_set_header Origin-URI $request_uri;
      proxy_set_header X-Real-IP $remote_addr;
      proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
      proxy_pass http://127.0.0.1:4080;
  }
}

server {
  listen 80;
  server_name zinc.sixmillions.cn;
  rewrite ^/(.*)$ https://$host$1 permanent;
}
```

生效配置：`nginx -s reload`

## 中文分词配置

> https://zincsearch-docs.zinc.dev/api/index/analyze/#chinese-analyzers

创建索引的时候配置一下

```json
{
  "analysis": {
    "analyzer": {
      "default": {
        "type": "gse_standard"
      }
    }
  }
}
```

![](https://s.sixmillions.cn/img/2023/09/01/025845684.png)
