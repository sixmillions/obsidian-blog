---
{"title":"EOF使用","slug":"linux-bash-eof","description":"linux系统中EOF的使用","author":"six","created":"2023-02-11","updated":"2023-09-02","cover":"https://picsum.photos/720/400","tags":["linux","bash"],"categories":["linux"],"dg-publish":true,"permalink":"/linux/linux-bash-eof/","dgPassFrontmatter":true}
---

## 文件描述

1.  STDIN_FILENO (标准输入) 文件描述符是0
2.  STDOUT_FILENO(标准输出) 文件描述符是1
3.  STDERR_FILENO(标准错误） 文件描述2

## 重定向

`>` 覆盖原文件内容
`>>` 向文件末尾追加

## cat和tee

### cat

cat（英文全拼：concatenate）命令用于连接文件并打印到标准输出设备上。

> [Linux cat 命令 | 菜鸟教程 (runoob.com)](https://www.runoob.com/linux/linux-comm-cat.html)

### tee

`tee` 从Stdin 读取数据，并同时输出到Stdout 和文件

例如:   

将用户输入的数据同时保存到文件"file1"和"file2"中

```shell
tee file1 file2
```

![](https://s.sixmillions.cn/img/2023/02/04/182733om5t.png)

## EOF使用

> [linux tee和cat使用EOF往文件中添加内容 - 二柒席地而坐 - 博客园 (cnblogs.com)](https://www.cnblogs.com/EQ1024/p/15692520.html)

- **EOF**是**END Of File**的缩写，表示**自定义终止符**。
- 既然自定义,那么**EOF**就不是固定的,可以随意设置别名
- 在linux按**ctrl+d**就代表**EOF**
- **EOF**一般会配合cat能够多行文本输出.

### 覆盖原文件

也就是用来重定向 `>`

下面两种写法区别就是输出文件位置

#### 写法一

```shell
cat << EOF > /tmp/test.txt
Hello World!!
My name is six.
EOF
```

#### 写法二

```shell
cat > /tmp/test.txt <<EOF
Hello World!!
My name is six.
EOF
```

### 追加到原文件

也就是用来重定向 `>>`

下面两种写法区别就是输出文件位置

#### 写法一

```shell
cat << EOF >> /tmp/test.txt
Hello World!!
My name is six.
EOF
```

#### 写法二

```shell
cat >> /tmp/test.txt <<EOF
Hello World!!
My name is six.
EOF
```

### 注意

#### 变量需要转义

```shell
cat > /tmp/test.txt <<EOF
export JAVA_HOME=/usr/local/java8
export PATH=\$JAVA_HOME/bin:\$PATH
EOF
```

#### 转义

> [（cat<<EOF）不使用反斜杠转义的技巧_51CTO博客_java转义反斜杠](https://blog.51cto.com/xiaozhenkai/2608853)

在分界符EOF前添加反斜杠 `\`，或者用单引号、双引号括起来

## EOF和-EOF的区别

EOF必须顶头写，但是-EOF，前后可以有制表符

> [here document - What is different between "<<-EOF" and "<<EOF" in bash script? ](https://unix.stackexchange.com/questions/583782/what-is-different-between-eof-and-eof-in-bash-script)

![](https://s.sixmillions.cn/img/2023/02/04/2159145s8h.png)


-EOF可以让脚本更漂亮，比如下面的脚本中的EOF

> [https://get.docker.com](https://get.docker.com/)

![](https://s.sixmillions.cn/img/2023/02/04/185254s1k4.png)

```shell
if true
then
        cat > 1.txt <<-'EOF'
        11111
            222
        3333
        EOF
fi
```

### 注意

EOF前面必须是制表符

![](https://s.sixmillions.cn/img/2023/02/04/215658zz5m.png)

![](https://s.sixmillions.cn/img/2023/02/04/191606h13v.png)

这个和下面的google规范冲突，规范建议用空格

## Google shell规范

> [styleguide | Style guides for Google-originated open-source projects](https://google.github.io/styleguide/shellguide.html)

![](https://s.sixmillions.cn/img/2023/02/04/215551t0bz.png)
