~<{
    "title": "博客诞生记一：服务器相关",
    "auther": "liucui",
    "mark": "web,blog,前端",
    "create_time": "2014-10-28",
    "cat": "linux,fe",
    "introduction": "做前端的时间不算短，已有两三年了，看着前端行业不断的蓬勃发展，接触到了从兼容IE6到各种安卓系统的痛苦挣扎，近些日子开始接触nodejs，懵懵懂懂的，便开始试着自己用nodejs搭一个博客来玩，于是便有了现在你看到的这个博客。",
    "thumb_img": "http://imgchr.com/images/birth_bg1.jpg"
}>~

# 博客诞生记一：服务器相关

做前端的时间不算短，已有两三年了，看着前端行业不断的蓬勃发展，接触到了从兼容IE6到各种安卓系统的痛苦挣扎，近些日子开始接触nodejs，懵懵懂懂的，便开始试着自己用nodejs搭一个博客来玩，于是便有了现在你看到的这个博客。

### 一、服务器问题
两年前，最开始自己架博客时用的是各种免费开源的东西，从免费的sae到免费的bae（现在都开始做大规模，开始收费）。后来想到了阿里的阿里云服务器，貌似可以免费用半年，申请了一个，开始各种折腾。

- 系统：这个说起来话长，由于我自己在linux方面不是很熟悉，很多东西都是变查资料边弄，速度比较慢，没有经验，好在阿里云可以更换服务器系统，感谢伟大的阿里云，给像我这样的菜鸟提供了便利，从linux换到ubuntu再到现在的centos，系统被我换了个遍。
- 软件：系统搞定了，开始各种软件的折腾，nodejs、npm、各种安装

### 二、linux的一些基础知识（基础知识，大牛请自行绕过）

#### 1、连接公网ip，在本地终端进行操作

```shell
ssh name@ip
ssh liucui@123.57.38.206
```

> @符号前是当前要登录的用户名

#### 2、修改密码
终端输入 passwd 即可更改当前用户的密码

#### 3、创建用户
```shell
# adduser joe  （键入用户名字）
# passwd  joe   （键入joe的密码）
```

### 三、安装nodejs
1、linux、centos系统安装方法
``` shell
wget http://nodejs.org/dist/node-latest.tar.gz
tar zxvf node-xxxx.tar.gz 
cd node-xxxx
./configure
make 
make install
```

2、ubuntu 系统安装方法
```shell
apt-get install nodejs
```

这里使用的ubuntu的apt-get 命令安装node，注意，在ubuntu系统里面node叫做nodejs，安装时要注意，安装好还要安装npm，同样使用apt-get命令，有时会出现安装不成功现象，可能是apt-get 版本比较低，使用apt-get update 命令更新apt-get，再进行npm的安装即可。

### 四、centos 添加用户
- 1、同样使用adduser命令创建用户，passwd命令设置密码
- 2、修改 /etc/sudoers 文件，修改文件内容：找到*root    ALL=(ALL)       ALL*一行，在下面插入新的一行，内容是：*name  ALL=(ALL)       ALL*  然后在vi键入命令“x!”强制保存并退出。`注：这个文件是只读的，不加“!”保存会失败`。
- 3、退出root用户，就可以尽情使用sudo命令了
- 4、ssh name@ip 输入密码即可用普通用户登录

### 五、本地使用ssh命令连接服务器报错解决方案
更换过系统后，同一机器不能使用ssh连接ip，是因为本地该用户的文件夹里面有个类似于证书的文件，know_hosts  将其删掉即可使用ssh。例：`/var/root/.ssh` 里面的know_hosts文件