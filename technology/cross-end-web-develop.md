~<{
    "title": "跨终端web开发",
    "auther": "liucui",
    "mark": "web,html5,前端",
    "cat": "fe",
    "tag": "web,html5,移动端,前端",
    "create_time": "2016-03-30",
    "introduction": "移动端的工作已经越来越成为前端工作的重要内容，继上一篇关于移动开发的文章后系统了解了下移动web开发，本章节是针对《跨终端Web》这阵书的学习与理解总结而来，内容比较基础，但很实用，用来作为查询使用",
    "thumb_img": "http://imgchr.com/images/cross_end_web_develop.jpg"
}>~

> 移动端的工作已经越来越成为前端工作的重要内容，继上一篇关于移动开发的文章后系统了解了下移动web开发，本章节是针对《跨终端Web》这阵书的学习与理解总结而来，内容比较基础，但很实用，用来作为查询使用

![跨终端web开发](http://imgchr.com/images/cross_end_web_develop.jpg)

### 一、跨终端web
一提到跨终端，第一反应往往就是响应式布局。这至少说明两点：首先，响应式本身与跨终端之间有着某种本质的联系；其次，人们误以为跨终端和响应式是同一件事。“跨终端 Web”是最终希望达到的目的，而达到这个目的的手段有很多，响应式仅仅是其中的一种方式而已。这些方式至少包括：
- 响应式
- 多站点
- 多模板
- 多平台

#### 1、响应式(单域)
**缺点：**

- **DOM冗余，javascript冗余**：对于DOM结构异常庞大复杂的页面而言，响应式不能解决移动端DOM冗余的问题，JavaScript 脚本冗余也是一个问题；
- **耦合度高**：从工程实践来看，单个复杂响应式页面的维护成本并不比单独维护多个版本的页面成本低，并且由于响应式存在的内在耦合性，这个维护成本在复杂页面频繁更新时反而更高。
- **超出css可控制范围**：响应式本质上是依靠 CSS 处理展现层面的差异，大部分项目的移动端和 PC 端存在着不仅仅是展示上的差异，在交互形式上的巨大差异也会导致 DOM 结构上的差异，这种差异已经远远超出 CSS 所能控制的范围。

#### 2、多站点(单域)
**缺点：**

通常一个网站要适配几个版本，针对手机、IPAD、小屏笔记本、大屏台式机，仅仅首页就要适配多个站点，整站下来维护成本太高。

#### 3、多模板(多域)
> 多模板是响应式和多站点相结合的一种方案。

多模板的优点在于一个页面只有一个 URL，无须服务器端复杂的 URL 映射规则和终端检测等手段进行跳转。虽然解决了响应式中 DOM 冗余的问题，但是由于单个页面存在多套模板，还需要在模板动态加载和首次服务器渲染等环节进行优化。

#### 4、多平台
Native App 的确也是实现跨终端 Web 的一种途径

**优点：**
- 更好的性能、
- 更丰富的系统级功能的调用、
- 标准的发布渠道（通常是应用商店）

**缺点：**
- 发布成本高
- 开发成本高
- 潜在的风险：如：ios严重依赖app store

### 二、Mobile Web
html5有几大特性，虽然表面看上去只是一个版本的html，但其实我们通常意义上所说的html ~= html5 + css3 + javascript

#### 1、html5特点
- 语意化：新增了一系列的语意化标签，更利于网页的seo优化等等
- 离线存储：包括local storage等
- 设备访问：如定位信息、移动设备传感器等
- 多媒体：增加video、audio标签，提供原生的视频、音频访问
- 图形接口：增加canvas 标签
- 性能&优化：
- css3：

#### 2、针对移动web的页面模板
针对移动web页面，html5增加了一系列的 meta 标签，在上一篇文章中做过详细介绍，这里就不在赘述了，[传送门：移动前端的html5头标签head](http://iqianduan.net/blog/mobile_web_html5_head)

#### 3、触屏事件
touch 以及 基于touch 的各种事件，drag（拖拽）、hold（长按）、pinch（捏）、rotate（旋转）、shake（重力感应等）

| 事件类别 | 事件描述 | 简称 | 别称|
|:---------|:--------|:--------|:---------|
| tap| 移动平台默认浏览器的click事件有300ms+的延时,通常使用touch事件模拟, 为区别点击称为拍击:</br> . tap拍击 </br>  . doubletap 双击</br> . hold 长按</br> . tapn n(2,3..)指拍击 | 拍击 | . android: touch</br> . hold称呼较多: </br> . android/ios: long press</br> .wp: tap and hold</br> . 也有称为press |
| swipe | 按方向细分为:</br>. swipe 单指滑动</br> . swipeleft 单指向左滑动</br> . swiperight 单指向右滑动</br> . swipeup 单指向上滑动</br> . swipedown 单指向下滑动</br> . swipen n(2,3..)指滑动    | 滑动 | wp: flick |
| drag | . drag 拖拽</br> . dragstart 拖拽开始</br> . dragend 拖拽结束</br> . dragup 向上拖拽</br> . dragdown 向下拖拽</br> . dragleft 向左拖拽</br> . dragright 向右拖拽  | 拖拽     | ios/wp: pan |
| pinch | 常用于放大(zoom in)缩小(zoom out)视图:</br> . pinchin 双指捏合</br> . pinchout 双指展开</br> . squeeze 五指捏合</br> . splay 五指展开 | 捏 | . android: pinch open/close</br> . pinchout也有称为spread |
| rotate | 常用于旋转视图 </br> . rotatecw 顺时针旋转</br> . rotateccw 逆时针旋转    | 旋转     |   |
| shake | 常用于游戏中控制方向, 细分为:</br> . shake 移动设备</br> . shakeup 向上移动设备</br> . shakedown 向下移动设备</br> . shakeleft 向左移动设备</br> . shakeright 向右移动设备</br> . shakeforward 向前移动设备</br> . shakeback 向后移动设备</br> . shakeleftright 左右移动设备</br> . shakeforwardback 前后移动设备</br> . shakeupdown 上下移动设备 | 重力感应 | &nbsp; |


#### 4、调试
1、远程调试
- Mobile Emulation：chrome 上面启动开发者工具，即可开启移动仿真状态
- ios 远程调试
手机上 safari 浏览器开启开发者模式（设置--safari--高级--打开web检查器），电脑上面打开 safari 浏览器的开发模式，连接上手机，找到你手机上面打开的页面即可进行调试了。
- Android 远程调试
安装Addroid Chrome 31+，使用USB 连接上手机，开启android的 USB debugger，安装ADB 扩展，安装后手动启动，PC chrome 使用 about: inspect 开启远程调试的控制台，单击 inspect 开始调试
- weinre
- HTTP 代理服务器

2、设备调试
- 设备模拟器
- 远程设备

#### 5、兼容性
> 虽然Android和iOS平台的大部分独立浏览器以及webview都是用WebKit内核，尽管移动端不存在像IE6/7 那样的古老的浏览器，但是移动端仍然存在很多兼容性问题

- OS 版本碎片化：Android 的碎片化版本，导致其自带浏览器内核差异，iOS在这方面要好很多，但仍然存在兼容的问题。
- 国内的特殊情况：国内手机厂商以及浏览器厂商，随大部分使用WebKit内核，但相关兼容问题仍大量存在，并且没有方便查询的资料库，处理起来非常棘手。
- WebView：WebView提供了大量的API，可以由开发者控制某些特性的开关，这就导致某些部分特性在自带浏览器下可用而在WebView下不可用。
- 更多工具：
  - html5test.com：可以检测当前浏览器对HTML5的支持程度。
  - mobilehtml5.com：提供了一个兼容性矩阵，可以更全局直观的查阅兼容性。
  - html5readiness.com：以时间维度展示所有浏览器HTML5特性的可用性。
  - caniuse.com：查看不同浏览器的不同版本的支持程度。
  - modernizr.com：这是一个特性检测库，通过对特性的检测并提供对低版本的优雅降级处理。
- 文档：推荐 https://developer.mozilla.org/ 提供中文版哦


### 三、基准

### 四、检测
#### 1、终端
**分类**：

- 按设备类型划分：目前普遍说的终端为三大类：PC电脑、平板、手机，当然TV 电视也即将成为第四大类
- 按操作系统划分：
  - apple：OS X（桌面系统）、iOS（iPhone和Pad）
  - Google：Android（Phone和Pad）
  - Microsoft：覆盖手机、平板、个人电脑的windows系列

**终端检测**：
- 需要检测的场景：显示或隐藏特定内容////加载特定的静态资源样式、脚本////静态扫描修改文件源////返回指定图片质量、大小的图片
- 检测的原理：用户代理（User Agent---UA）最为常用
- 检测的实现：

**遗留问题**
- 硬件信息：UA 不准（浏览器厂商把UA伪装）
- 更精准的终端检测：引入机器学习，采集一定数量的样本学习后用于终端检测

### 五、接口
#### 1、跨终端流程复用
- 如：购物网站前台页面展示有5种形式（PC、Phone Web、Pad Web、Phone App、Pad App），但后台的逻辑基本一致，则使用一套接口，增加流程的复用性。
- 如：移动优先，优先考虑移动端页面的展示，再开发PC的时候可适当扩展API

#### 2、IF(interFace)
IF 主要包括以下几个部分：
- 接口描述：请求、响应数据格式
- 接口文档：由接口描述生成接口文档
- 接口Mock：由接口描述生成接口 Mock 数据
- 接口校验：提供校验服务（HTTP）和校验工具包，支持多重格式的接口校验

**缘由：来自于一次重构**

### 六、定位
#### 1、定位：
- hash：不利于SEO
- history API：可结合ajax通过pjax的方式实现修改路由同时不刷新页面，只刷新部分内容
  - history.pushState
  - history.replaceState
  - window.onpopstate：页面前进后退的时候触发
- 视图定位：


#### 2、数据：

### 七、预览
#### 1、客户端：

#### 2、服务端：

### 八、Hybrid App
> Native App 和Mobile Web 二者混合开发的产物被称为Hybrid App。

#### 1、Hybrid 简史
- 背景：既利用了Native App 丰富的设备API（Device API），又能拥有Mobile Web 的跨平台、高效开发、快速发布的能力，对于相当庞大的应用场景而言都是适用的。
- 优势：跨平台（开发一次，所有平台生效）、高效开发、快速发布、丰富的Device API

#### 2、Hybrid 技术
- Mobole Web开发基础：HTML、CSS、Javascript
- Native App 开发基础：Android、iOS
- Native 与 Web 双向通信机制

##### Native 调用 Web：本质是Javascript脚本的动态执行
- Android 调用 Javascript：webview.loadUrl("javascipt:(function(){alert('ok');})()");
- iOS 调用 Javascript：[webview stringByEvaluatingJavasciptFromStrng:@"alert('ok')"];

##### Web 调用 Native

Android 常见的有三种方式：
- 重写 WebViewClient.shouldOverrideUrlLoading
```Javascript
webView.setWebViewClient(new WebViewClient(){
  @override
  public boolean shouldOverrideUrlLoading(WebView view, Stringurl){
    // TODO 解析url并触发Native代码
    return true;
  }
})
```

当页面内的url 发生变化时，就会触发WebViewClient.shouldOverrideUrlLoading，通过将Web调用Native的数据封装在URL，再由Native 解析数据并执行响应Native方法

- 重写 WebChromeClient.onJsPrompt，或onJsAlert，例：

```Javascript
webView.setWebChromeClient(new WebChromeClient(){
  public boolean onJsPrompt(WebView view, String url, String message, String defaultValue, JsPromptResult result){
    // TODO 解析 message 并触发 Native 代码
    result.confirm("");
    return true;
  }
})
```

当执行"window.prompt("{}")" 这样的js代码时，将会触发WebChromeClient.onJsPrompt

- WebView.addJavascriptInterface，这种方式和前面不同，通过将 JavaObject(A) 映射为 JavaObject(B)，从而调用B.func1 时将会自动触发A.func1，通过这种原生的方式实现了 "web调用Native"

```javascript
webView.addJavascriptInterface(new Object(){
  public void func1(){
  }
  public void func2(){
  }
}, "webViewObj");
```

iOS:可用的方式类似Android 的 WebViewClient.shouldOverrideUrlLoading，通过监控 WebView 的url 变化实现Web 调用Native

```Javascript
-(BOOL)webView:(UIWebView *) webView shouldStartLoadWithRequest:(NSURLRequest *) request navigationType: (UIWebNavigationType) navigationType{}
```

##### Bridge

#### 3、Hybrid 框架
- PhoneGap：一处编写，多处运行
- Titanium

#### 4、Device API
| 设备功能 | 标识 | 核心数据 | 典型应用场景 | Web标准 | Hybrid支持案例 |
|:-------|:------|:----|:------|:------|:------|
| GPS| Geolocation| 经纬度| 搜索 地图/导航 社交 电商| W3C Geolocation API | PhoneGap Geolocation  |
| 加速度计| Accelerometer | xyz轴加速度 | 摇一摇（shake） 导航 游戏| W3C Motion API| PhoneGap Accelerometer PhoneGap Compass |
| 陀螺仪| Gyroscope| xyz轴角速度及偏移角| 指南针、地图/导航、塞车类游戏、增强现实 | W3C Motion API | |
| 磁力计| Magenetometer | xyz轴磁场强度| 指南针、导航 | W3C Motion API | PhoneGap Compass|
| 距离传感器 | Proximity | 距离| 通话过程解锁    | W3C Proximity Events | |
| 传声器| Microphone | 音频数据| 咻一咻、语音录制、语音识别（输入）| W3C Audio API| PhoneGap Capture|
| 扬声器| Speaker || 音频播放  | W3C Audio API| - |
| 摄像头| Camera| 拍照、视频录制、二维码、图像识别（增强现实） | W3C Video API| PhoneGap Camera、PhoneGap Capture | |
| 视频播放 | Video || 视频播放  | W3C Video API| - |
| 光线传感器 | Light | 照度 | 游戏、环境适配    | W3C Light Events、W3C MQ Luminosity  | |
| 气压传感器 | Pressure| 气压 | 监控气压、测量海拔| W3C Pressure Events  | |
| 气温传感器 | Temperature   | 气温 | 监控气温  | W3C Temperature Events | |
| 湿度传感器 | Humidity| 湿度 | 监控相对/绝对湿度 | W3C Humidity Events  | |
| 振动器| Vibrator| | 提醒功能 | W3C Vibration API、支持列表| |
| 近场通信 | NFC |  | 支付、门禁|  |  |
| 设备事件 | Events|| page、visibility、battery、online/offline | W3C Network Information API、W3C Page Visibility API | Phonegap Events |
| 网络类型 | Connection | 网络类型| 大数据下载提醒 | W3C Network Information API | |
| 通信录| Contacts||   || PhoneGap Contacts |
| 文件 | File  || 访问文件系统| W3C File API | PhoneGap File |
| 应用内浏览 | InAppBrowser  ||   || PhoneGap File |
| 通知 | Notification | | 通知| W3C Web Notification | PhoneGap Notification |
| 设备标识 | Device| | | | PhoneGap Device |

### 九、存储
storage 是一个跨终端、跨域的存储组件
- 十亿级日调用次数的考验，稳定可靠
- 兼容IE6+、chrome、firefox、safari
- 不使用flash方案，完美支持移动浏览器
- 跨子域、主域的数据存取，且不改写docuent.domain
- 支持Object、Array 等复杂对象存取

#### 1、状态持久化
- 海量的状态信息给服务器带来了更大的考验，前端存储的天然优势在于利用亿级客户端设备存储状态信息，几乎无网络开销（会有同步）。
- Cookie 可以存储的数据很少（4KB），并且考虑到Cookie 数据在于HTTP 请求和响应Header 中会加重网络开销，falsh storage 和 userData 都属于外挂资源
- localStorage 现在几乎兼容所有浏览器（除IE6/7）
- localStorage 不能跨子域访问


#### 2、技术方案
- 整体方案：存储方案和跨域方案
  - 存储方案：localStorage + userData
  - 跨域方案：使用iframe加载代理页，数据存储在代理页所在的域下，需要实现宿主页和代理页之间的通信，postMessage + window.name
- 跨终端存储方案
- 跨域通信方案
- 安全性
- 遗留问题

#### 3、使用
- 方法如下：

| 方法名 | 方法参数 | 描述 |
|:-------|:---------|:----------|
| length | 属性| 获取存储数据的条数   |
| key(n) | n:索引值 | 根据索引值，返回键名 |
| getItem(key) | key:键名 | 根据键名，获取数据值 |
| setItem(key,value) | key:键名 value:键值 | 根据键名和键值设置数据项，如果键名已经存在，则覆盖值 |
| removeItem(key) | key:键名 | 根据键名删除一个数据项 |
| clear() | 无 | 清空当前的Storage对象|

所有支持web Storage的浏览器均实现了以上标准方法，另外IE8还自己实现了remainingSpace用于查看剩余的存储空间

- 事件如下：
onstorage，当发生存储相关操作的时候触发

标准中事件对象的属性：

| 事件属性    | 描述|
|:--------|:----------|
| key | 返回发生改变的数据项的键名 默认空字符串   |
| oldValue | 返回发生改变的数据项的旧值  默认null |
| newValue | 返回发生改变的数据项的新值  默认null |
| url | 返回发生改变的数据的页面所对应的url  默认空字符串 |
| storageArea | 返回代表所属的storage对象  默认null |

其中，webkit内核的浏览器（Chrome、Safari）以及Opera是完全遵循标准的，IE8则只实现了url，Firefox下则均未实现。

各个浏览器对于事件注册的对象也不一致。其中IE和FF是document对象，chrome和opera是window对象，safari是body。

- local storage的渐进设计方案
> 对于不支持的浏览器，可以做渐进设计，考虑的顺序如下：

  - localStorage
  - globalStorage
  - userdata
  - Cookie

- session storage 的会话
> session storage主要存储会话级别的数据，会话结束后，数据自动销毁。Â

- web storage的安全注意事项：
  - 明文存储，不要存敏感信息
  - 不能抵御xss漏洞攻击
  - 对于存储的数据要严格过滤，防止自身产生存储型xss攻击
  - 容易遭受跨目录攻击
  - 容易遭受DNS欺骗攻击

### 十、动作同步
#### 1、原理
![动作同步原理](http://imgchr.com/images/action_tongbu_bg.png)
