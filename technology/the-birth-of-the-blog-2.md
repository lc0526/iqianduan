~<{
    "title": "博客诞生记二：centos6.5 安装nodejs",
    "auther": "liucui",
    "mark": "web,blog,前端",
    "create_time": "2014-10-30",
    "cat": "linux,fe",
    "introduction": "这篇文章接上一篇，简单介绍下在centos 6.5 上安装nodejs的方法和一些注意事项，希望对你有所帮助",
    "thumb_img": "http://imgchr.com/images/birth_bg2.jpg"
}>~

# 博客诞生记二：centos6.5 安装nodejs
### 一、在编译安装nodejs之前，应该有三个工具
1、 gcc等c++编译器
- 原因：因为在nodejs编译时需要C++编译
- 检测：可以在linux终端上敲下命令gcc -v
- 本人情况：版本为 4.4.7
 

2、 Python2.6以上
- 原因：因为在nodejs编译时也需要Python环境
- 检测：可以在linux终端上敲下命令python --version
- 本人情况：Python 2.6.6
- 没有python下载，版本低于2.6要升级

3、 openssl-devel
- 原因：提供SSL/TLS加密验证，保证通信安全性
- 检测：可以在linux终端上敲下命令openssl version
- 本人情况：OpenSSL 1.0.1e-fips 11 Feb 2013
- 没有的话下载也不难的，就在命令行敲下yum install openssl-devel


### 二、Procedure(步骤)

1、 进入/usr/local/src文件夹
- 原因：其实可以自己选择下载目录的，但是我们要归类。/usr/local这个文件夹就是代表你手动安装的程序
- 命令：cd /usr/local/src

2、 从网络上获取nodejs包
- 原因：巧妇难为无米之炊，要玩nodejs肯定要有nodejs包了
- 命令：wget http://nodejs.org/dist/node-latest.tar.gz
- 言外话：13M左右，还是比较少的

3、 在/usr/local/src文件夹中解压node-latest.tar.gz
- 命令：tar zxvf node-latest.tar.gz
- 个人情况：解压后在/usr/local/src中出现一个文件夹是 node-v0.10.28(不一样的话，应该是版本不一样，没事)

4、 进入到解压后的文件夹node-v0.10.28中
- 命令：cd node-v0.10.28

5、 编译安装三部曲
- 命令：
```shell
./configure
make && make install
```

- 题外话：好像要安装很久呀，最少10分钟吧，还有就是我对这个./configure命令不是很熟，应该是可以配置一些参数的

6、 检查安装成功
- 命令：node -v
- 个人情况：v0.10.28
