~<{
    "title": "canvas 学习笔记（一）",
    "auther": "liucui",
    "cat": "technical",
    "mark": "html+css",
    "tag": "前端,web",
    "create_time": "2015-11-10",
    "introduction": "一直觉得canvas很神秘，可以做出特别炫酷的东西，于是最近花了点时间来学习了下canvas的部分简单的api，做个笔记，供作以后查看的记录。",
    "thumb_img": "http://imgchr.com/images/canvas_learning_notes_bg.jpg"
}>~

# canvas 学习笔记（一）

随着前端的发展，HTML5和CSS3早已经成为了前端的必备技能，尤其是近一两年，HTML5和CSS3的发展更是迅猛，不会点这些技术都不好意思说自己是个前端，H5的技术平常使用的也很多，尤其是在手机端的web页面上，最近花了点时间研究了下H5的一大特色----canvas，自己写了个简单的小画板，大家可以来体验下。

传送门：[我的小小画板](http://iqianduan.net/static/demo/canvas/index.html)

当然功能还不是很全，需要完善，后续会根据所学习的东西来继续优化，PS：针对手机页面做了适配，在手机上面可以方便的操作，很好玩的哦。

言归正传，下面就来总结下关于canvas的部分知识点

### 一、基础介绍：

#### 1、环境要求：
Google Chrome, Firefox, Safari, Opera, 或者 IE9以上的现代浏览器

#### 2、基础概念：
HTML5中包含一个专门为HTML画布功能设计的标签： canvas ，所以相关的画布功能都是基于这个标签来完成。我们需要将它添加到HTML的body标签中，如下：

```html
<canvas id="myCanvas" width="300" height="300"></canvas>
```

> 小提示：你可以将width和height添加到CSS文件中，但是和直接设置canvas的属性，有一定区别：使用属性来定义canvas，不仅定义的是canvas对象的高宽，同时也定义了可绘制图形区域的高宽。而使用CSS来定义做不到这一点，只能定义Canvas本身的大小，所以推荐使用属性来设置相关高宽


为了能够能够调用HTML5的画布API，我们需要来访问画布的相关上下文（Context），用来访问HTML5画布相关的相关API方法，如下：

```javascript
var canvas = document.getElementById('myCanvas'),     
	context = canvas.getContext('2d');  //使用context可以调用更多方法，绘制直线
```


### 二、绘制直线：

绘制直线会用到以下几个方法

- beginPath() - 开始准备绘制
- moveTo() - 绘制的其实坐标（x, y）
- lineTo() - 绘制结束的坐标（x, y )
- lineWidth - 设置直线的粗细 (20没有单位)
- strokeStyle - 设置直线的颜色
- lineJoin - 设置直线的连接方式
 - miter // 绘制为直角
 - round // 绘制为圆角
 - bevel // 绘制为平角
- lineCap - 设置直线两端的样式 ()
 - 'butt'; //绘制按钮类型
 - 'round'; //绘制圆角类型
 - 'square'; //绘制正方形类型
- stroke() - 立刻开始绘制直线

> 绘制的线的缺省值是分别是：颜色----黑色，粗细----1px，两端样式----butt

> 请在stroke()方法前调用相关的属性设置方法

例：

```javascript
// 这里通过myCanvas获取canvas对象
var canvas = document.getElementById('myCanvas');
// 这里通过 canvas 获取处理API的上下文context
var context = canvas.getContext('2d');

// 绘制第一条直线
context.beginPath();
context.moveTo(100, 70);
context.lineTo(300, 70);
context.lineWidth = 25;
context.strokeStyle = '#DD4814';
context.lineCap = 'butt'; //这里设置直线两端的样式为"buttn"，缺省值
context.stroke();

// 绘制第二条直线
context.beginPath();
context.moveTo(100, 140);
context.lineTo(300, 140);
context.lineWidth = 25;
context.strokeStyle = '#DD4814';
context.lineCap = 'round'; //这里设置直线两端的样式为"圆角"风格
context.stroke();

// 绘制第三条直线
context.beginPath();
context.moveTo(100, 210);
context.lineTo(300, 210);
context.lineWidth = 25;
context.strokeStyle = '#DD4814';
context.lineCap = 'square';
context.stroke();
```
绘制出来的直线如下：

<iframe src="/static/demo/canvas-demo/demo1.html" width="310" height="302" style="border: 1px solid #cdcdcd; overflow: hidden;"></iframe>

### 三、绘制弧形

在HTML5画布中我们使用arc()方法来绘制相关的弧形，相关参数如下：

```javascript
arc( x, // 定义圆心x坐标
	y, // 定义圆心y坐标
	radius, // 半径
	startAngle, // 起始角度
	endAngle, // 结束角度
	counterClockWise // 是否是逆时针方向
);
```

通过下面这个图来理解下以上几个参数分别是什么意思

![绘制弧形](http://imgchr.com/images/canvas_arc.png)

> 通过以上方式画出来的圆弧只是圆弧线（不是实心圆），要画出实心圆可以把画笔的宽度设置成和直径相同


### 四、生成二次曲线
如果需要使用HTML5画布生成二次曲线的话，可以使用如下方法：

```javascript
quadraticCurveTo(
	controllpointX,
	controllpointY,
	endingpointX,
	endingpointY
)
```

二次曲线通过控制两根虚拟的直线来生成对应的图形，请参考如下：

![绘制二次曲线](http://imgchr.com/images/canvas_quadratic.jpg)

### 五、绘制贝塞尔曲线
相对于二次曲线来说， 贝塞尔曲线增加了一个控制点来生成更复杂的曲线样式，其它参数类似，方法及其参数说明如下：

```javascript
bezierCurveTo(
	controllpoint1X,
	controllpoint1Y,
	controllpoint2X,
	controllpoint2Y,
	endingpointX,
	endingpointY
)
```

可以参考下图

![](http://imgchr.com/images/bezierCurve.png)

例：

```javascript
var canvas = document.getElementById('myCanvas'); // 这里通过myCanvas获取canvas对象
var context = canvas.getContext('2d'); // 这里通过canvas获取处理API的上下文context
context.beginPath();
context.moveTo(100, 200);
context.quadraticCurveTo(150, 50, 200, 200);

context.lineWidth = 20;
context.strokeStyle = '#DD4814';
context.stroke();
```

可以得到如下图：
![增加了一个控制点来生成更复杂的曲线类型](http://imgchr.com/images/canvas_bezierCurve572d5.png)



使用HTML5的路经(path)，我们可以连接多个子路经。上一个路经的结束点即成为下一个子路经的起始点。我们可以使用如下的相关方法来构建不同的子路经：

- lineTo
- arcTo
- quadraticCruveTo()
- bezierCurveTo()

> 相关的方法和前面我们介绍的绘制直线及其曲线的方法参数一致

如果你希望重新开始绘制一个路经，可以使用beginPath()方法，下面是生成图形说明：

![使用HTML5的路经生成完整的一条曲线](http://imgchr.com/images/path.jpg)


### HTML5画布添加文字

添加文字会用到下面几个方法

- fillText(textString, x, y); // textString：添加的文字内容 x、y分别是文字开始点的坐标
- font = 'bold 30pt "microsoft yahei"'; // 定义文字属性，例如，样式，字体和大小，用空格来分开
- fillStyle = '#DD4814'; // 用来修改文字颜色
- strokeText('你好，极客标签!', 100, 150); // 设置空心描边字体
- strokeStyle = '#DD4814'; // 设置空心描边字体颜色
- textAlign // 设置文字对齐方式，且定义属性文字对齐都以指定的左边距x为标准
 - center - 居中
 - left - 居左
 - right -   居右
 - start -  文字方向左到右
 - end -  文字方向右到左
- textBaseline // 文字垂直对齐方式
 - top
 - bottom
 - middle
 - hanging
 - alphabetic
 - ideographic
