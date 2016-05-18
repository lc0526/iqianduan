~<{
    "title": "如何制作css3的3d动画",
    "auther": "liucui",
    "mark": "web,html,css3,前端",
    "create_time": "2015-06-05",
    "cat": "fe",
    "introduction": "css3的属性可是实现很多炫酷的动画，这段时间学习了css3的3d动画制作，这篇文章讲仔细描述下3d动画的整个实现过程。",
    "thumb_img": "http://imgchr.com/images/css3_3d_thumb.jpg"
}>~

# 如何制作css3的3d动画

## 首先先来看两个用css3实现的炫酷的3d动画效果

- 动画一

<video height="374" width="100%" src="/static/md-images/video/demo1.mp4" controls="controls"></video>

- 动画二

<iframe width="100%" height="400" style="border: 1px solid #333;" src="/static/demo/css3-demo/css3-3d-square.html" frameborder="0"></iframe>

你没看错，这两个炫酷的效果都是用css3实现的

## 下面是动画实现所需要用到的几个css3属性。

### 1、perspective：用来实现一个3d的场景

写3D效果的第一步是要创建一个3D场景，即索要实现效果的模块。这里用到了 `perspective` 属性和 `perspective-origin` 属性。

- perspective：用来定义3d动画距离浏览器的距离，单位是（px）。
- perspective-origin：效果渲染的视角，告诉浏览器我们观看的角度，一般为 center 或 50% 50%，意为 居中。
- transform-style：preserve-3d 来告诉浏览器之后要进行的transform的操作都是对一个3D的世界进行的。

### 2、transition：用来写动画的过度效果
transition 用来实现过度的效果，使动画不至于太过生硬。这是一个复合属性，分别有以下几个属性：

- `transition-property`：过度或动态模拟的css属性，对应的属性有：宽度（width）、高度（height）、边框（border）、绝对定位的上下左右值、外边距（margin）、内边距（padding）、文字阴影（text-shadow）、z-index等。
- `transition-duration`：完成过度所需的时间
- `transition-timing-function`：指定过度函数，函数包括 ease（默认值，速度由快到慢，主见变慢）、linear（匀速）、ease-in（速度越来越快，加速，渐显效果）、ease-out（速度越来越慢，减速，渐隐效果）、ease-in-out（先加速，再减速，渐显渐隐效果）
- `transition-delay`：指定开始出现的延迟时间，即过渡效果开始执行的时间。

### 3、transform：用来实现翻转、角度的转换
transform 同样是个复合属性，用来实现各种转换效果，分别有以下几个属性：

- translate(x,y)	定义 2D 转换。
- translate3d(x,y,z)	定义 3D 转换。	
- translateX/Y/Z	定义转换，分贝用 X、Y、Z 轴的值。
- scale(x,y)	定义 2D 缩放转换。
- scale3d(x,y,z)	定义 3D 缩放转换。	
- scaleX/Y/Z	通过设置 X、Y、Z 轴的值来定义缩放转换，若为Z轴，则定义的是3D旋转。	
- rotate(angle)	定义 2D 旋转，在参数中规定角度。
- rotate3d(x,y,z,angle)	定义 3D 旋转。
- skew(x-angle,y-angle)	定义沿着 X 和 Y 轴的 2D 倾斜转换。
- skewX/Y	定义沿着 X、Y 轴的 2D 倾斜转换。
- perspective(n)	为 3D 转换元素定义透视视图

## 下面介绍下一个简单的骰子的写法

### 1、创建一个3D场景

- 这里使用了perspective 和perspective-origin 两个属性，定义了3D动画的距离是800px，居中显示的。这里借用一张慕课网的图片，来查看这两个属性的确切含义。
- 我们在3D场景里面定义了一个类名为dice的div，这里是我们写这个骰子的外层包裹的div，我们给他定义好宽和高，并让他居中显示。
- 骰子的六个面我们分别用六个div（其他块级元素也可以）来实现，会用到定位，我们这里给.dice 定义为相对定位。
- 我们给我们这个骰子的包裹div，加上了`transform-style: preserve-3d`这个样式，是要告诉浏览器之后要进行的transform的操作都是对一个3D的世界进行的。

这里是慕课网上面一张讲解的图，很形象的画出来了 [perspective 含义](http://img.mukewang.com/555bf6b90001065712000530-500-284.jpg)

```html
<!DOCTYPE html>
<html>
<head>
    <title>实现一个3D骰子</title>
    <style>
    *{
    	padding: 0;
    	margin: 0;    	
	}
	.block{
		margin-top: 100px;
        -webkit-perspective: 800px;
           -moz-perspective: 800px;
                perspective: 800px;
        -webkit-perspective-orign: 50% 50%;
           -moz-perspective-orign: 50% 50%;
                perspective-orign: 50% 50%;
	}
	.dice{
		width: 300px;
		height: 300px;
		margin: 20px auto;
		position: relative;
		-webkit-transform-style: preserve-3d;
           -moz-transform-style: preserve-3d;
                transform-style: preserve-3d;
	}
</head>
<body>
	<div class="block">
		<div class="dice">
		</div>
	</div>
</body>
</html>
```

### 2、场景布置好了，下面来写骰子的六个面

html 为6个相同的div
```html
<div class="block">
	<div class="dice">
		<div class="page" id="page1">1</div>
		<div class="page" id="page2">2</div>
		<div class="page" id="page3">3</div>
		<div class="page" id="page4">4</div>
		<div class="page" id="page5">5</div>
		<div class="page" id="page6">6</div>
	</div>
</div>
```

定义公共的样式
```css
.page{
	width: 200px;
	height: 200px;
	background: rgba(0,0,0,0.3);
	position: absolute;
	font-size: 200px;
	color: #fff;
	line-height: 200px;
	text-align: center;
	border: 1px solid red;
}	
```


这时我们看到的是一个6个div重叠的块，下面是关键的一步，我们来给每个面定义不同的位置，实现一个正方体的结构。


### 3、给骰子的六个面定义位置

```css
	#page2{
        -webkit-transform: rotateY(-90deg);
           -moz-transform: rotateY(-90deg);
            -ms-transform: rotateY(-90deg);
             -o-transform: rotateY(-90deg);
                transform: rotateY(-90deg);
        -webkit-transform-origin: right;
           -moz-transform-origin: right;
            -ms-transform-origin: right;
             -o-transform-origin: right;
                transform-origin: right;
    }
    #page3{
        -webkit-transform: translateZ(-200px);
           -moz-transform: translateZ(-200px);
            -ms-transform: translateZ(-200px);
             -o-transform: translateZ(-200px);
                transform: translateZ(-200px);
        -webkit-transform-origin: right;
           -moz-transform-origin: right;
            -ms-transform-origin: right;
             -o-transform-origin: right;
    }
    #page4{
        -webkit-transform: rotateY(90deg);
           -moz-transform: rotateY(90deg);
            -ms-transform: rotateY(90deg);
             -o-transform: rotateY(90deg);
                transform: rotateY(90deg);
        -webkit-transform-origin: left;
           -moz-transform-origin: left;
            -ms-transform-origin: left;
             -o-transform-origin: left;
    }
    #page5{
        -webkit-transform: rotateX(-90deg);
           -moz-transform: rotateX(-90deg);
            -ms-transform: rotateX(-90deg);
             -o-transform: rotateX(-90deg);
                transform: rotateX(-90deg);
        -webkit-transform-origin: top;
           -moz-transform-origin: top;
            -ms-transform-origin: top;
             -o-transform-origin: top;
    }
    #page6{
        -webkit-transform: rotateX(90deg);
           -moz-transform: rotateX(90deg);
            -ms-transform: rotateX(90deg);
             -o-transform: rotateX(90deg);
                transform: rotateX(90deg);
        -webkit-transform-origin: bottom;
           -moz-transform-origin: bottom;
            -ms-transform-origin: bottom;
             -o-transform-origin: bottom;       
    }
```

这里用到了transform的两个属性 rotate  和 origin，前者是定义旋转角度，后者是定义旋转的轴。下面的图可以比较明确的看出来这两个属性的用法。

![rotate和origin在transform属性里面的用法](http://imgchr.com/images/transform.png)

[点击这里](/static/demo/css3-demo/css3-transform.html) 可以查看上面图片的代码


按照上述代码来写，我们现在已经可以看见一个正方体了，如图：

![css3实现的正方体](http://imgchr.com/images/css3-3d-demo.png)

现在已经实现了一大部分代码的书写了，我们已经写出了一个静态的正方体，接下来让他实现一个转起来的动画就可以了。

## 下面是动画的部分，实现让这个正方体以随机的角度转动起来。

### 用css3来书写动画
css3里面另一强大的属性就是动画的实现，省去了很多的js代码的计算一级各种动画效果的考虑，拥有css3神器，就可以写出各种炫酷的效果来，赶紧来看看怎么实现。

#### 1、如何旋转
上面我们讲过了他过transform的rotate属性来实现旋转，我们通过对每个面的旋转实现了一个正方体的样子，这里我们把正方体作为一个整体，来实现一整个正方体的旋转。

#### 2、定义动画：
css3 里面写动画分为两步，第一步就是来定义一个动画。通过 `@keyframes` 来实现。

语法如下：

> @keyframes animationname {keyframes-selector {css-styles;}}

- animationname：动画的名字（尽量语意化）
- keyframes-selector：动画时长的百分比。0%-100%（或from、to）
- css-styles：一个或多个合法的 CSS 样式属性

我们这里歹意一个名为 `random-rotate` 的动画，通过transform的rotate属性来实现旋转。
代码如下：

```css
@-webkit-keyframes random-rotate{
    0%{
        -webkit-transform:rotateX(0deg) rotateY(0deg);
           -moz-transform:rotateX(0deg) rotateY(0deg);
        	 -o-transform:rotateX(0deg) rotateY(0deg);
                transform:rotateX(0deg) rotateY(0deg);
    }
    100%{
        -webkit-transform:rotateX(360deg) rotateY(360deg);
           -moz-transform:rotateX(360deg) rotateY(360deg);
        	 -o-transform:rotateX(360deg) rotateY(360deg);
                transform:rotateX(360deg) rotateY(360deg);
    }
}
@-moz-keyframes random-rotate{
    0%{
        -webkit-transform:rotateX(0deg) rotateY(0deg);
           -moz-transform:rotateX(0deg) rotateY(0deg);
        	 -o-transform:rotateX(0deg) rotateY(0deg);
                transform:rotateX(0deg) rotateY(0deg);
    }
    100%{
        -webkit-transform:rotateX(360deg) rotateY(360deg);
           -moz-transform:rotateX(360deg) rotateY(360deg);
        	 -o-transform:rotateX(360deg) rotateY(360deg);
                transform:rotateX(360deg) rotateY(360deg);
    }
}
@-o-keyframes random-rotate{
     0%{
        -webkit-transform:rotateX(0deg) rotateY(0deg);
           -moz-transform:rotateX(0deg) rotateY(0deg);
        	 -o-transform:rotateX(0deg) rotateY(0deg);
                transform:rotateX(0deg) rotateY(0deg);
    }
    100%{
        -webkit-transform:rotateX(360deg) rotateY(360deg);
           -moz-transform:rotateX(360deg) rotateY(360deg);
        	 -o-transform:rotateX(360deg) rotateY(360deg);
                transform:rotateX(360deg) rotateY(360deg);
    }
}
@keyframes random-rotate{
     0%{
        -webkit-transform:rotateX(0deg) rotateY(0deg);
           -moz-transform:rotateX(0deg) rotateY(0deg);
        	 -o-transform:rotateX(0deg) rotateY(0deg);
                transform:rotateX(0deg) rotateY(0deg);
    }
    100%{
        -webkit-transform:rotateX(360deg) rotateY(360deg);
           -moz-transform:rotateX(360deg) rotateY(360deg);
        	 -o-transform:rotateX(360deg) rotateY(360deg);
                transform:rotateX(360deg) rotateY(360deg);
    }
}
```

这里我们要这个动画x、y轴分别从0度 转到 360度。

#### 3、动画的实现
css3 里面的animation 配合 @keyframe 来实现。
animation 是一个复合属性，同样我们来看下这个复合属性的各个属性是如何定义的。
> - animation-name：动画的名字（@keyframe 定义好的）
> - animation-duration：动画执行一次的时间
> - animation-timing-function：动画的速度曲线（ease、linear等，等同于transform的速度曲线用法）
> - animation-delay：动画的延时时间
> - animation-interation-count：动画播放的次数（数字/infinite 无限次）
> - animation-direction：动画播放的方向（normal 正常/alternate 反向）
> - animation-play-state：动画播放状态（running 播放/paused 暂停）
> - animation-fill-mode：动画在开始和结束后发生的操作
>> - none：默认，完成一次动画后回到初始帧
>> - forwards：动画结束的位置作为下一次动画的初始帧
>> - backwards：在向元素应用动画样式时迅速应用动画初始帧
>> - both：动画同事具有 forwards 和 backwards 效果

下面来写下代码，我们这里让这个正方体无限转动，每次动画的时间为5s，速度为匀速，动画不延时。同时我们给动画添加一个过度的效果，使动画看起来更平滑

外层div样式改为如下：

```css
.dice{
	width: 300px;
	height: 300px;
	margin: 20px auto;
	position: relative;
	-webkit-transform-style: preserve-3d;
	   -moz-transform-style: preserve-3d;
	   		 transform-style: preserve-3d;
	-webkit-animation: random-rotate 5s linear 0s infinite;
	   -moz-animation: random-rotate 5s linear 0s infinite;
	    -ms-animation: random-rotate 5s linear 0s infinite;
	     -o-animation: random-rotate 5s linear 0s infinite;
	     	 animation: random-rotate 5s linear 0s infinite;
	-webkit-transition: all 1s ease;
	   -moz-transition: all 1s ease;
	    -ms-transition: all 1s ease;
	     -o-transition: all 1s ease;
	        transition: all 1s ease;
}
```

至此，我们已经完整的实现了一个正方体（类似于一个骰子）的旋转，有几点需要注意的提示如下：

- 1、由于个浏览器对css3的实现不同，记得加浏览器前缀名
- 2、css3动画确实很炫，但还是要根据项目的不同来进行取舍
- 3、css3可以实现的动画还很多，大家可以多开开脑洞，来实现属于你的css3动画
- 3、每个动画有自己的用途，使用时不要混淆

最后附上完整的例子，大家可以参考哦~

[点我查看旋转的正方体](/static/demo/css3-demo/css3-3d-square.html) 
