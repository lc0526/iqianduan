~<{
	"title": "mac上安装 mongo 环境以及使用（二）",
	"author": "liucui",
	"mark": "web,数据库,mongodb,robomongo",
	"create_time": "2015-08-20",
	"cat": "fe",
	"introduction": "因为公司的项目，近一年一直在使用 nodejs + mongodb，不过一直也没好好总结，今天就mongo在mac上面的安装及使用做简单的总结。",
	"thumb_img": "http://imgchr.com/images/install_mongodb_interview_bg.jpg"
}>~

# mac上安装 mongo 环境以及使用（二）

上一次介绍了通过下载安装包的形式在mac上面安装mongodb，（传送门：[mac上安装 mongo 环境以及使用（一）](http://iqianduan.net/blog/how-to-install-mongo-for-mac)）今天来介绍下通过 brew 来安装mongo

### 一、更新brew：
在之前的文章里面也有提到郭brew，实在是mac党的必备利器，更新命令：brew update
### 二、通过brew安装mongodb：
brew可以用来安装很多包、程序、环境等，安装命令：brew install mongodb
### 三、安装过程：
接下来就是downloading的过程了，好在有进度提示
### 四、启动mongod：
第一个终端面板用来启动mongod服务
``` shell
mongod
```
### 五、启动mongod的过程报错的处理：
- 没有权限：则使用  sudo mongod 命令
- 如果报错：
```shell
ERROR: dbpath (/data/db) does not exist.
Create this directory or give existing directory in --dbpath.
See http://dochub.mongodb.org/core/startingandstoppingmongo 
```
则需要手动创建/data/db文件目录，mkdir -p /data/db(如果有data文件夹，则在data文件夹下创建db文件夹，否则创建一个data，里面再创建一个db文件夹)

### 六、查看mongo数据：
- 第二个终端面板用来查看数据库
```shell
mongo
```

- 查看mongo数据的时候可能会有警告的内容提示，如：
```shell
MongoDB shell version: 3.0.5
connecting to: test
Server has startup warnings:
2015-08-19T10:53:49.020+0800 I CONTROL  [initandlisten] ** WARNING: You are running this process as the root user, which is not recommended.
2015-08-19T10:53:49.020+0800 I CONTROL  [initandlisten]
>
```
这里是因为你的 mongod 启动的时候用的是root权限，当然不影响你的操作。

### 七、接下来就是mongo的语法的使用了，下面介绍一些基础的语法：
```
> show dbs: 显示都有哪些数据库
> use local: 选择使用哪个库
> show collections: 显示都有哪些表
> db.article.find(): 查看表 article 里面的数据
{ "_id" : ObjectId("55d3f25417d2b6e066c5e339"), "title" : "你好", "author" : "liucui" }
{ "_id" : ObjectId("55d41c4fd6bf7c5394ab51e9"), "title" : "hello world", "time" : "20150819", "author" : "wmq" }
> db.article.findOne(): 查看表 article 里面的一条数据
{
    "_id" : ObjectId("55d3f25417d2b6e066c5e339"),
    "title" : "你好",
    "author" : "liucui"
}
```

mongo 的语法还有很多，尤其是各种带条件的查找，以及索引的使用等，还在探索当中，待整理完毕，再做分享
​
### TIPS：
- 更新mongodb的版本：brew upgrade mongodb // 更新到最新的mongodb
- 通过以上方式安装的mongo的配置文件位置为： /usr/local/etc/mongod.conf






