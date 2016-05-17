~<{
    "title": "nodejs部署——PM2",
    "auther": "liucui",
    "mark": "web,前端",
    "cat": "fe",
    "tag": "web,前端,nodejs,pm2",
    "create_time": "2016-04-25",
    "introduction": "随着前端技术的不断发展，前端的工作早已不仅仅局限于写几个页面，切几张图那么单一，目前大部分的前端工作已经从最开始简单的切图延伸到移动端开发、后台nodejs开发等等更广泛的范畴，这篇文章给大家介绍下nodejs的高大上的部署方式-PM2",
    "thumb_img": "http://imgchr.com/images/how_to_use_pm2.jpg"
}>~

# nodejs部署——PM2

![pm2](http://imgchr.com/images/how_to_use_pm2.jpg)

随着前端技术的不断发展，前端的工作早已不仅仅局限于写几个页面，切几张图那么单一，目前大部分的前端工作已经从最开始简单的切图延伸到移动端开发、后台nodejs开发等等更广泛的范畴，这篇文章给大家介绍下nodejs的高大上的部署方式-PM2

### 一、nodejs 的部署方式汇总
Node.js 应用能够简单地通过命令行启动，只要有 Node 运行环境。对于生产环境，情况要复杂得多。不仅需要数据库等功能性组件，更对安全性、可靠性、可扩展性等方面有更高的要求。

- 最常用的其实就是在后台执行进程，末尾加个& 例：node app.js &，但这种写法极其不稳定，经常默默的进程在后台就挂了
- 其次是nohup了，nohup 命令是不挂断地运行命令，不仅在node的部署时会使用，这种写法也会在后台默默的把进程挂掉
- PM2，pm2 是一个带有负载均衡功能的Node应用的进程管理器，当你要把你的独立代码利用全部的服务器上的所有CPU，并保证进程永远都活着，0秒的重载， PM2是完美的。


### 二、PM2的使用
#### 1、安装：
npm install -g pm2

通过nodejs的包管理器 npm 可以很方便的安装pm2

#### 2、使用

运行控制相关:
- pm2 start app.js --name xxx  启动
- pm2 stop 进程id/app_name/all （参数可以是进程的id，或者是进程的name，或者停掉所有进程--all） 停止
- pm2 restart 进程id/app_name/all 重启
- pm2 reload 类似于pm2 restart
- pm2 resurrect 复活所有进程

管理进程相关:
- pm2 list 查看所有进程的基本信息，针对的是机器上的所有通过pm2启动的进程。可以看到类似下图中的信息

![pm2 list](http://imgchr.com/images/pm2_list.jpg)
- pm2 describe 进程id/app_name 可以看到更为详细的信息，针对的是某一个通过pm2启动的进程。可以看到类似下图中的信息

![pm2 describe](http://imgchr.com/images/pm2_describe.jpg)
- pm2 show 进程id/app_name 查看到的信息和pm2 describe相同的信息

杀掉进程相关:
- pm2 dump 硬重启
- pm2 delete 进程id/app_name/all
- pm2 kill 杀掉pm2

日志相关：
- pm2 logs 进程id/app_name/  会列出项目的log，没有参数的话则列出所写项目的log
- pm2 flush 清空所有日志
- pm2 reloadLogs 重新下载所有的日志

运行监测
- pm2 monit 会列出进程的CPU的使用率和内存占用
- pm2 web 监控所有被PM2管理的进程,而且同时还想监控运行这些进程的机器的状态（可在浏览器里面查看进程的json文件，端口是9615）

以上内容列举的是在使用 pm2 的过程中比较常用的一些用法，当然还有很多其他的用法等着你去发现。欢迎大家来评论交流
