~<{
	"title": "mac上安装 mongo 环境以及使用（一）",
	"author": "liucui",
	"mark": "web,数据库,mongodb,robomongo",
	"create_time": "2015-06-25",
	"cat": "fe",
	"introduction": "因为公司的项目，近一年一直在使用 nodejs + mongodb，不过一直也没好好总结，今天就mongo在mac上面的安装及使用做简单的总结。",
	"thumb_img": "http://imgchr.com/images/install_mongodb_interview_bg.jpg"
}>~

# mac上安装 mongo 环境以及使用（一）

因为公司的项目，近一年一直在使用 nodejs + mongodb，不过一直也没好好总结，今天就mongo在mac上面的安装及使用做简单的总结。

公司的项目用的是nodejs的框架----meteor，框架配套使用的是 mongodb 数据库，因为meteor别身集成了一个mini-mongo，所以一直没在电脑上面安装mongo环境，用的时间也不短了，于是想安装个mongo的环境，以便查看。(传送门：[mac上安装 mongo 环境以及使用（二）](http://iqianduan.net/blog/how-to-install-mongo-for-mac2))

对于mac用户来说，还有个更方便的方式，就是用homebrew来安装，方便快捷，以后再来分享通过brew来安装的方法，今天主要来说说用浏览器或第三方工具安装的方法。

### 一、下载安装包
当前版本的下载地址： http://downloads.mongodb.org/osx/mongodb-osx-x86_64-2.4.6.tgz

下载好后，解压，放到你喜欢的位置，（建议给文件夹改个名字，太长不方便记）我放到了我的家目录下面。

### 二、在 mongo 的根目录下创建 data 文件夹，里面继续创建两个文件夹，分别为 db 和 log，用于放置mongodb 数据和日志，并且给该目录设置权限

- mkdir data
- cd data
- mkdir db
- mkdir log
- sudo chown -R  userName /data

### 三、启动 mongod 服务，并指定mongo的数据库

进入安装存放的下载安装文件目录的bin文件夹 运行 ./mongod
通过dbpath 来指定数据库（~/Documents/wedo_new/.meteor/local/db）

```shell
~/mongodb/bin/mongod --dbpath ~/Documents/wedo_new/.meteor/local/db
```

> 这个命令实在是太长了，每次启动mongo的时候都要敲一遍，试着简化一下，mac下面家目录下有个 .bash_profile 文件，通过alias可以将复杂的命令缩短来写。

针对 mongo 指定路径的启动方式，vim ~/.bash_profile 添加下面的语句

```shell
alias mongodMeteor="~/mongodb/bin/mongod --dbpath ~/Documents/wedo_new/.meteor/local/db"
```

更改完我们来让 .bash_profile 文件执行一下

```shell
source ~/.bash_profile
```

这样下次再启动的时候，直接使用mongodbMeteor 就可以了，方便了不少。

当然你也可以更改其他你用的较多的命令，大大的提高了你的工作效率。

例如：
mac 上面没有 ll 命令，需要是用 ls -l 命令，我们将ll命令写进alias

alias ll="ls-l"

记住，alias 里面的简写命令后面不能有空格。

> 如果不记得写过了哪些简写命令，可以再终端里面直接输入 alias 来查看你设置的简写命令。

### 五、在 meteor 环境下指定数据库地址，运行meteor

由于我的项目是用的meteor框架，因此要指定mongo数据库为本地的数据库

```shell
export MONGO_URL=mongodb://localhost:27017/meteor
```

mongo 默认的端口号是27017，你也可以指定其他的。

接下来就可以运行meteor啦!

### 六、打开另外一个终端，同样是进入bin 目录，运行 ./mongo

> 从这里开始就可以查看数据库，查看数据库里面的各种数据了。

mac上面终端虽然好用，但可读性略差，我在mac上面使用的是 [robomongo](http://www.robomongo.org/) 这个第三方工具，非常好用。

![robomongo](http://imgchr.com/images/robomongo.png)
