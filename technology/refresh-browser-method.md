~<{
    "title": "JS刷新当前页面的几种方法总结",
    "auther": "liucui",
    "mark": "web,js,前端",
    "create_time": "2014-10-31",
    "cat": "fe",
    "introduction": "JS刷新当前页面有几种方法可以实现，这篇文章针对刷新当前页面做了详细的总结，大家可以根据需要参考！",
    "thumb_img": "http://imgchr.com/images/refresh_bg.jpg"
}>~

# JS刷新当前页面的几种方法总结
### 1、reload 方法，该方法强迫浏览器刷新当前页面。
**语法：**location.reload([bForceGet]) 
**参数：** bForceGet， 可选参数， 默认为 false，从客户端缓存里取当前页。true, 则以GET方式，从服务端取最新的页面,相当于客户端点击 F5("刷新")

### 2、replace 方法
> 该方法通过指定URL替换当前缓存在历史里（客户端）的项目，因此当使用replace方法之后，你不能通过“前进”和“后退”来访问已经被替换的URL。

**语法：**  location.replace(URL)
在实际应用的时候，重新刷新页面的时候，我们通常使用： location.reload() 或者是 history.go(0) 来做。因为这种做法就像是客户端点F5刷新页面，所以页面的method="post"的时候，会出现"网页过期"的提示。那是因为Session的安全保护机制。可以想到： 当调用 location.reload() 方法的时候， aspx页面此时在服务端内存里已经存在， 因此必定是 IsPostback 的。如果有这种应用： 我们需要重新加载该页面，也就是说我们期望页面能够在服务端重新被创建， 我们期望是 Not IsPostback 的。这里，location.replace() 就可以完成此任务。被replace的页面每次都在服务端重新生成。
你可以这么写： location.replace(location.href);

#### 返回并刷新页面：
　　location.replace(document.referrer);
　　document.referrer //前一个页面的URL
　　不要用 history.go(-1)，或 history.back();来返回并刷新页面，这两种方法不会刷新页面。

### 3、Javascript刷新页面的几种方法：
- 1、history.go(0)
- 2、location.reload()
- 3、location=location
- 4、location.assign(location)
- 5、document.execCommand('Refresh')
- 6、window.navigate(location)
- 7、location.replace(location)
- 8、document.URL=location.href

### 4、自动刷新页面的方法:
- 1、页面自动刷新：把如下代码加入<head>区域中
``` html
    <meta http-equiv="refresh" content="20">
    <!-- 其中20指每隔20秒刷新一次页面.-->
```
- 2、页面自动跳转：把如下代码加入<head>区域中
``` html
    <meta http-equiv="refresh" content="20; url="http://baidu.com">
    <!--其中20指隔20秒后跳转到 http://baidu.com 页面-->
```
- 3、页面自动刷新js版：
``` javascript
    function myrefresh(){
        window.location.reload();
    }
    setTimeout('myrefresh()',1000);  //指定1秒刷新一次
```
- 4、JS刷新框架的脚本语句：
``` javascript
    // 如何刷新包含该框架的页面用
    parent.location.reload();

    // 子窗口刷新父窗口
    self.opener.location.reload();
    // (或<a href="javascript:opener.location.reload()">刷新</a>)

    // 如何刷新另一个框架的页面用
    parent.另一FrameID.location.reload();
```

### 5、如果想关闭窗口时刷新或者想打开窗口时刷新的话，在中调用以下语句即可。
``` html
    <body onload="opener.location.reload()">  <!--开窗时刷新-->
    <body onUnload="opener.location.reload()"> <!--关闭时刷新-->
    <script language="javascript">
        window.opener.document.location.reload();
    </script>
```