---
{"title":"openresty学习开发环境","slug":"01-openresty-dev-env","description":"在windows环境，基于docker搭建openresty学习开发环境","author":"six","created":"2023-03-03","updated":"2023-09-02","cover":"https://picsum.photos/720/400","tags":["nginx","openresty"],"categories":["nginx"],"dg-publish":true,"permalink":"/nginx/01-openresty-dev-env/","dgPassFrontmatter":true}
---

# 目标

在 `windows` 环境，基于docker搭建 `openresty` 学习开发环境

# 文件

新建几个文件

```
mkdir {conf.d,html,logs,lua}
# win下手动创建
# lua文件是我用来存放lua代码的文件夹
```

如果我们进行目录映射，会导致原来容器中的文件丢失  
所以我们先运行一个将我们需要的文件copy出来

```shell
docker run -d --rm --name resty openresty/openresty:1.21.4.1-buster-fat
```

进入容器看看结构，默认 `openresty` 安装到了 `/usr/local` 下

```shell
docker exec -it resty bash
```

![](https://s.sixmillions.cn/img/2023/02/28/201442gi8e.png)

看一下 `nginx.conf` 配置文件

```conf
root@28851913dd8c:/# cat /usr/local/openresty/nginx/conf/nginx.conf
# nginx.conf  --  docker-openresty
#
# This file is installed to:
#   `/usr/local/openresty/nginx/conf/nginx.conf`
# and is the file loaded by nginx at startup,
# unless the user specifies otherwise.
#
# It tracks the upstream OpenResty's `nginx.conf`, but removes the `server`
# section and adds this directive:
#     `include /etc/nginx/conf.d/*.conf;`
#
# The `docker-openresty` file `nginx.vh.default.conf` is copied to
# `/etc/nginx/conf.d/default.conf`.  It contains the `server section
# of the upstream `nginx.conf`.
#
# See https://github.com/openresty/docker-openresty/blob/master/README.md#nginx-config-files
#

#user  nobody;
#worker_processes 1;

# Enables the use of JIT for regular expressions to speed-up their processing.
pcre_jit on;



#error_log  logs/error.log;
#error_log  logs/error.log  notice;
#error_log  logs/error.log  info;

#pid        logs/nginx.pid;


events {
    worker_connections  1024;
}


http {
    include       mime.types;
    default_type  application/octet-stream;

    # Enables or disables the use of underscores in client request header fields.
    # When the use of underscores is disabled, request header fields whose names contain underscores are marked as invalid and become subject to the ignore_invalid_headers directive.
    # underscores_in_headers off;

    #log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
    #                  '$status $body_bytes_sent "$http_referer" '
    #                  '"$http_user_agent" "$http_x_forwarded_for"';

    #access_log  logs/access.log  main;

        # Log in JSON Format
        # log_format nginxlog_json escape=json '{ "timestamp": "$time_iso8601", '
        # '"remote_addr": "$remote_addr", '
        #  '"body_bytes_sent": $body_bytes_sent, '
        #  '"request_time": $request_time, '
        #  '"response_status": $status, '
        #  '"request": "$request", '
        #  '"request_method": "$request_method", '
        #  '"host": "$host",'
        #  '"upstream_addr": "$upstream_addr",'
        #  '"http_x_forwarded_for": "$http_x_forwarded_for",'
        #  '"http_referrer": "$http_referer", '
        #  '"http_user_agent": "$http_user_agent", '
        #  '"http_version": "$server_protocol", '
        #  '"nginx_access": true }';
        # access_log /dev/stdout nginxlog_json;

    # See Move default writable paths to a dedicated directory (#119)
    # https://github.com/openresty/docker-openresty/issues/119
    client_body_temp_path /var/run/openresty/nginx-client-body;
    proxy_temp_path       /var/run/openresty/nginx-proxy;
    fastcgi_temp_path     /var/run/openresty/nginx-fastcgi;
    uwsgi_temp_path       /var/run/openresty/nginx-uwsgi;
    scgi_temp_path        /var/run/openresty/nginx-scgi;

    sendfile        on;
    #tcp_nopush     on;

    #keepalive_timeout  0;
    keepalive_timeout  65;

    #gzip  on;

    include /etc/nginx/conf.d/*.conf;

    # Don't reveal OpenResty version to clients.
    # server_tokens off;
}
```

可以看到配置文件指向的是 `/etc/nginx/conf.d/*.conf`  
所以我们只需要将配置文件映射这个目录就行了

我们先将原来的配置文件copy出来

```shell
docker cp resty:/etc/nginx/conf.d/default.conf ./conf.d
```

我这里也将 `html` 里面的也copy出来了，可以不copy，自己新建也行

```shell
docker cp resty:/usr/local/openresty/nginx/html/index.html ./html
docker cp resty:/usr/local/openresty/nginx/html/50x.html ./html
```

![](https://s.sixmillions.cn/img/2023/02/28/202235qykn.png)

完事可以停掉这个容器， 因为加了 `--rm` 会自己删除

```shell
docker stop resty
```

# Docker-compose

官方镜像：[openresty/openresty - Docker Image | Docker Hub](https://hub.docker.com/r/openresty/openresty)

`docker-compose.yml` 文件

```yaml
version: '3'
services:
  minio:
    image: openresty/openresty:1.21.4.1-buster-fat
    container_name: resty
    hostname: "resty"
    environment:
      TZ: Asia/Shanghai
    privileged: true
    volumes:
      - ./conf.d:/etc/nginx/conf.d
      - ./html:/usr/local/openresty/nginx/html
      - ./logs:/usr/local/openresty/nginx/logs
      - ./lua:/usr/local/openresty/nginx/lua
    ports:
      - 8080:80
```

启动

```shell
docker-compose up -d
```

# 访问页面

> http://localhost:8080/

![](https://s.sixmillions.cn/img/2023/02/28/202517iezt.png)

# 运行lua

用openresty运行我们第一个脚本

在 `lua` 文件夹下新建文件 `hello.lua`

```lua
ngx.header["Content-Type"] = "text/html"
ngx.say("Hello World")
```

修改 `default.conf` 文件，将访问执行我们的lua脚本  

```conf
    location /hello {
        content_by_lua_file lua/hello.lua;
    }
```

因为我们lua文件夹和 `html` 还有 `conf` 文件夹同级，所以这里使用了相对目录

重启容器，让配置生效，或者直接 `reload` 

```shell
docker exec -it resty sh -c "openresty -s reload"
# 或者
docker-compse restart
```

再次访问

> http://localhost:8080/hello

![](https://s.sixmillions.cn/img/2023/02/28/203548t17y.png)

# 关闭缓存

学习开发环境关闭lua脚本缓存，这样修改lua脚本，能及时反映  
**生产环境关闭会严重影响性能**  

`location` 或者 `server` 中配置都可以

```conf
    location /hello {
        lua_code_cache off;
        content_by_lua_file lua/hello.lua;
    }
```

# 目录结构

最后的目录结构

![](https://s.sixmillions.cn/img/2023/02/28/203324uxzr.png)

# 插件

## EmmyLua 

lua语法插件

vscode和idea可以直接在软件市场搜索到

也可以手动安装

> https://github.com/EmmyLua/VSCode-EmmyLua
> https://github.com/EmmyLua/IntelliJ-EmmyLua

![](https://s.sixmillions.cn/img/2023/03/02/161009oy2s.png)


## openresty

vscode直接搜索 `openresty`

或者手动下载安装

> https://marketplace.visualstudio.com/items?itemName=benemohamed.openresty-snippets

![](https://s.sixmillions.cn/img/2023/03/02/1609311e4y.png)

