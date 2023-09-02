---
{"title":"File Browser 搭建使用","slug":"filebrowser","description":"轻量文件管理软件，上传下载分享","author":"six","created":"2023-09-02","updated":"2023-09-02","cover":"https://picsum.photos/720/400","tags":["dev"],"categories":["tools"],"dg-publish":true,"permalink":"/tools/filebrowser/","dgPassFrontmatter":true}
---

## 介绍

> 中文介绍：https://www.filebrowser.cn/

filebrowser 是一个使用go语言编写的软件，功能是可以通过浏览器对服务器上的文件进行管理。可以是修改文件，或者是添加删除文件，甚至可以分享文件，是一个很棒的文件管理器，你甚至可以当成一个网盘来使用。总之使用非常简单方便，功能很强大。

> 官网：https://filebrowser.org/

## 安装

这里我在群晖的docker上安装

> [Installation - File Browser](https://filebrowser.org/installation)

先创建配置文件和数据库文件用来占位，使用root安装

```bash
sudo su -
mkdir filebrowser && cd filebrowser
touch filebrowser.db filebrowser.json docker-compose.yml
```

```json
{
  "port": 80,
  "baseURL": "",
  "address": "",
  "log": "stdout",
  "database": "/database.db",
  "root": "/srv"
}
```

```yml
version: '3'
services:
  filebrowser:
    image: filebrowser/filebrowser:v2.24.2
    restart: always
    container_name: filebrowser
    ports:
      - 3453:80
    volumes:
      - /volume1/share:/srv
      - ./filebrowser.json:/.filebrowser.json
      - ./filebrowser.db:/database.db
```

```bash
docker-compose up -d
```

> http://192.168.31.69:3453/
## 配置

默认用户名 admin/admin

修改语言和默认密码

![](https://s.sixmillions.cn/img/2023/09/02/125202851.png)

## 分享文件

![](https://s.sixmillions.cn/img/2023/09/02/131657039.png)

可以在分享管理中管理分享链接

![](https://s.sixmillions.cn/img/2023/09/02/131802888.png)

## 下载

window用户，就正常浏览器访问链接，下载即可

linux可以使用命令行

> https://filebrowser.org/cli

### linux使用curl下载

#### 分享链接是文件

打开链接，然后右键复制下载链接

![](https://s.sixmillions.cn/img/2023/09/02/132716932.png)


```bash
curl -o "Coodesker.exe" http://192.168.31.69:3453/api/public/dl/SpLc5MVG
```

#### 分享链接是文件夹

右键复制该文件夹分享链接的下载链接

![](https://s.sixmillions.cn/img/2023/09/02/133203047.png)

找到自己要下载的文件

例如 `win/Coodesker-x64_1.0.4.1.exe`，将斜杠转移成 `%2F`

将复制的文件夹最后一个斜杠也变成 `%2F`，然后拼起来

```bash
curl -o "Coodesker.exe" http://192.168.31.69:3453/api/public/dl/Lh0Ja5uq%2Fwin%2FCoodesker-x64_1.0.4.1.exe
```

## 创建用户

创建一个只有下载权限的用户

![](https://s.sixmillions.cn/img/2023/09/02/134502612.png)

### 认证下载

对于需要认证才能下载的文件，为了安全，专门创建一个只有下载权限的用户

需要认证才能下载的资源链接格式

`http://192.168.31.69:3453/api/raw/资源路径转义?auth=xxx`

auth是jwt token，可以通过登录接口获取

```bash
curl 'http://192.168.31.69:3453/api/login' \
  --data-raw '{"username":"user","password":"user"}'
```

那么下载 `黑群晖安装/rufus-3.21.exe`

![](https://s.sixmillions.cn/img/2023/09/02/134809332.png)

的链接就是 
`http://192.168.31.69:3453/api/raw/%E9%BB%91%E7%BE%A4%E6%99%96%E5%AE%89%E8%A3%85/rufus-3.21.exe?auth=`

注意 raw 后面的斜杠不用转义

转义方式 浏览器命令行

![](https://s.sixmillions.cn/img/2023/09/02/135052037.png)

最终组合起来就是

```bash
token=$(curl -s 'http://192.168.31.69:3453/api/login' --data-raw '{"username":"user","password":"user"}')
curl -o "rufus-3.21.exe" http://192.168.31.69:3453/api/raw/%E9%BB%91%E7%BE%A4%E6%99%96%E5%AE%89%E8%A3%85/rufus-3.21.exe?auth=${token}
```

#### 验证

md5校验

![](https://s.sixmillions.cn/img/2023/09/02/135425136.png)


## Cloudflare域名配置

域名 + Zero Trust + Tunnel 配置穿透

![](https://s.sixmillions.cn/img/2023/09/02/135910404.png)

### 测试

```bash
curl -o 'coodesker.exe' https://fb.6bw.fun/api/public/dl/SpLc5MVG
```