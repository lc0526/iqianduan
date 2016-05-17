~<{
    "title": "css圆角进化论",
    "auther": "liucui",
    "mark": "web,html,css,前端",
    "create_time": "2014-11-02",
    "cat": "fe",
    "introduction": "CSS圆角的实现，经历了三大发展阶段：背景图片（贴图）方式、CSS2.0+HTML标签模拟、CSS3.0圆角属性（border-radius）。这篇文章讲解每一种的实现方式，并对实现的优缺点进行对比分析。",
    "thumb_img": "http://imgchr.com/images/css_radius_bg.jpg"
}>~

# css圆角进化论

![css圆角进化论](http://imgchr.com/images/css_radius_bg.jpg)

###   一、CSS圆角发展过程
- 背景图片实现圆角
- CSS2.0+标签模拟圆角
- CSS3.0圆角属性（border-radius属性)实现圆角

###  二、背景图片实现圆角
- 宽度固定，高度自适应
- 宽度和高度均自适应

#### 1.​宽度固定，高度自适应
实现关键点，4个块级标签构成
- 圆角矩形容器(box)—设置固定宽度，同圆角宽度
- 顶部圆角(radius-top)—使用背景图片实现顶部圆角
- 内容（ content ）—放置主体内容
- 底部圆角（ radius-bottom )—使用背景图片实现顶部圆角

#### 2.宽度和高度均自适应
 实现关键点，5个标签构成
- 圆角矩形容器(box)—1.上下内边距大小至少设置为圆角高度；2.相对定位；3.放置内容
- 4个圆角—4个标签，1.分别设置各个圆角背景图片；2.绝对定位于box的4个角

> 优势和劣势

> - 优势：无需过多无意义标签，能够实现个性化圆角
> - 劣势：增加了HTTP请求和页面字节数

### 三、CSS2.0+标签模拟圆角
- border属性实现圆角颜色
- 标签模拟圆角弧度
- 圆角像素越大，所需标签越多

``` html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title></title>
    <style type="text/css" media="screen">
        *{padding: 0; margin: 0;}
        .box{
            width: 300px;
            margin: 20px auto;
        }
        .radius_border_1{
            height: 1px;
            margin: 0 3px;
            background: lightblue;
            border-left: 1px solid #acc3e3;
            border-right: 1px solid #acc3e3;
        }
        .radius_border_2{
            height: 1px;
            margin: 0 2px;
            background: lightblue;
            border-left: 1px solid #acc3e3;
            border-right: 1px solid #acc3e3;
        }
        .radius_border_2{
            height: 1px;
            margin: 0 1px;
            background: lightblue;
            border-left: 1px solid #acc3e3;
            border-right: 1px solid #acc3e3;
        }
        .loginbox{
            background: lightblue;
            border-left: 1px solid #acc3e3;
            border-right: 1px solid #acc3e3;
            height: 200px;
        }
    </style>
</head>
<body>
    <div class="box">
        <div class="radius_border_1"></div>
        <div class="radius_border_2"></div>
        <div class="radius_border_3"></div>
        <div class="loginbox"></div>
        <div class="radius_border_3"></div>
        <div class="radius_border_2"></div>
        <div class="radius_border_1"></div>
    </div>
</body>
</html>
```
实现的界面是这样的

![表单提示信息](http://imgchr.com/images/css-border-radius.png)

是不是很神奇呢~~~

> 优势和劣势
> - 优势：纯CSS代码，易于维护，体积小
> - 劣势：圆角像素越大，无意义标签越多数，圆角越发呆板，只能实现纯色圆角，局限性大

### 四、CSS3.0圆角属性实现圆角
border属性设置边框样式（颜色、粗细、样式）
border-radius属性实现圆角

> 优势和劣势
> - 优势：专用CSS代码，易于维护，体积小，圆角自然圆滑，适合扁平化圆角实现
> - 劣势：IE8及以下版本不支持CSS3.0，存在兼容性问题，对于个性化圆角实现上存在局限性


以上内容总结自慕课网，视频可见： [CSS圆角进化论](http://www.imooc.com/view/118)
