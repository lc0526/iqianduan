~<{
    "title": "clip 实现圆环进度",
    "auther": "liucui",
    "mark": "web,html,css3,前端",
    "create_time": "2015-09-21",
    "cat": "fe",
    "introduction": "最近公司项目里面用到了圆环进度条，开始计划用图片，后来查了查资料，可以用css实现，于是总结下，仅供参考",
    "thumb_img": "http://imgchr.com/images/clip_to_circle_progress.jpg"
}>~

# clip 实现圆环进度

> 最近公司项目里面用到了圆环进度条，开始计划用图片，后来查了查资料，居然可以用css实现，太神奇了，总结了下用法，仅供参考~

clip 是css2 里面的属性，但一直没用使用过，查了查官方的api，用来属性剪裁绝对定位元素。

当一幅图像的尺寸大于包含它的元素时会发生什么呢？"clip" 属性允许您规定一个元素的可见尺寸，这样此元素就会被修剪并显示为这个形状。

这个属性用于定义一个剪裁矩形。对于一个绝对定义元素，在这个矩形内的内容才可见。出了这个剪裁区域的内容会根据 overflow 的值来处理。剪裁区域可能比元素的内容区大，也可能比内容区小。

取值：
- 默认值：auto
- shape：设置元素的形状。唯一合法的形状值是：rect (top, right, bottom, left)

先来看看 clip 是如何使用的

![clip用法](http://imgchr.com/images/clip_bg.png)

[查看源码](/static/demo/css3-demo/clip_demo.html)

盗用一张 [大漠 w3cPlus](http://www.w3cplus.com/css3/clip.html) 的图片

![clip用法](http://imgchr.com/images/clip_bg1.jpg)
根据这张图片，可以设置clip 的属性值。

由于裁剪是裁剪矩形，所以我们把圆环拆成左右两部分，分别进行裁剪。
下面根据所学到的来实现一个圆环进度

### 一、基础布局
```html
<div class="course_progress">
	<div class="finish_prg">
		<i class="left_prg"></i>
		<i class="right_prg"></i>
	</div>
	<span class="progress_num">50%</span>
</div>
```
基础样式
```css
*{
    padding: 0;
    margin: 0;
}
*,*:before,*:after{
    -webkit-box-sizing: border-box;
       -moz-box-sizing: border-box;
            box-sizing: border-box;
}
.course_progress {
    width: 250px;
    height: 150px;
    display: block;
    position: relative;
    background-color: rgba(0, 0, 0, 0.3);
}
.course_progress .progress_num {
    position: absolute;
    left: 50%;
    top: 50%;
    margin-top: -48px;
    margin-left: -48px;
    width: 96px;
    height: 96px;
    color: #fff;
    font-size: 24px;
    text-shadow: 0 0px 4px rgba(0, 0, 0, 0.8);
    line-height: 82px;
    text-align: center;
    border: 4px solid #fff;
    border-radius: 50%;
}
.course_progress .finish_prg {
    position: absolute;
    left: 50%;
    top: 50%;
    width: 100px;
    height: 100px;
    margin-left: -50px;
    margin-top: -50px;
}
.course_progress .finish_prg i {
    display: block;
    width: 100px;
    height: 100px;
    position: absolute;
    z-index: 1;
    border: 8px solid #3eb97f;
    border-radius: 50px;
}
```
此时我们的得到的是一个完整的圆环，我们在这里没有对left、right两个圆环做处理，两个都是完整的圆环，接下来就到了我们裁剪的步骤了。

### 二、裁剪圆环

根据我们最开始学到的，可以明确:
- 只要右边半圆，左边的裁剪掉，那么需要添加样式 `clip: rect(0px, 100px, 100px, 50px);`
- 只要左边半圆，右边的裁剪掉，那么需要添加样式 `clip: rect(0px, 50px, 100px, 0px);`
- 当然，我们此时看到的圆环还是一个完整的圆环，只不过这个圆环是由两个半圆拼起来的，大家可以在 chrome-developer 里面查看。

### 三、如何让圆环按照我们想要的角度来渲染

圆环得到了，现在我们通过css3 的transform: rotate 属性来实现我们想要的角度

结合外层的裁剪，来实现不同角度的现实

我们来看个例子

![clip结合transform](http://imgchr.com/images/clip_bg2.png)

上面的例子对照不同角度做了demo，[demo可见](/static/demo/css3-demo/clip_demo2.html)

上面是我们写死了角度值，我们可以通过 jquery 来计算需要旋转多少角度

```javascript
var progress = parseInt(30%)/100;
if(progress > 0.5){
	var degree = Math.floor(180/50 * (progress-0.5) * 100 - 180);
	$('.finish_prg').css({
		'clip': 'rect(auto,auto,auto,auto)'
	});
	$('.right_prg').css({
		'-webkit-transform': 'rotate(180deg)',
           '-moz-transform': 'rotate(180deg)',
            '-ms-transform': 'rotate(180deg)',
             '-o-transform': 'rotate(180deg)',
            	'transform': 'rotate(180deg)'
	});
	$('.left_prg').css({
		'-webkit-transform': 'rotate(' + degree + 'deg)',
           '-moz-transform': 'rotate(' + degree + 'deg)',
            '-ms-transform': 'rotate(' + degree + 'deg)',
             '-o-transform': 'rotate(' + degree + 'deg)',
            	'transform': 'rotate(' + degree + 'deg)'
	});
}else{
	var degree = Math.floor(180/50 * progress * 100);
	$('.left_prg').hide();
	$('.right_prg').css({
		'-webkit-transform': 'rotate(' + degree + 'deg)',
           '-moz-transform': 'rotate(' + degree + 'deg)',
            '-ms-transform': 'rotate(' + degree + 'deg)',
             '-o-transform': 'rotate(' + degree + 'deg)',
            	'transform': 'rotate(' + degree + 'deg)'
	})
}
```

一个圆环进度引出了不少知识，技术在于不短的总结和发现，赶紧开动脑筋，来制作更多裁剪的效果吧~~~
