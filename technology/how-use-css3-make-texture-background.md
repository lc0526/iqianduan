~<{
    "title": "如何用css3制作纹理背景",
    "auther": "liucui",
    "mark": "web,html,css,前端",
    "create_time": "2014-11-06",
    "cat": "fe",
    "introduction": "看到题目大家也许会想，这是什么意思，一直想系统一下自己的css3的知识，才发现自己对css3的掌握程度简直不敢直视，很多地方都差了好多，暂且一点点来学吧！",
    "thumb_img": "http://imgchr.com/images/texture_bg.jpg"
}>~

# 如何用css3制作纹理背景
看到题目大家也许会想，这是什么意思，一直想系统一下自己的css3的知识，才发现自己对css3的掌握程度简直不敢直视，很多地方都差了好多，暂且一点点来学吧！

记得有一天在微博上面，看到w3cplus的大漠除了个题目，用css3实现上下两个颜色的锯齿状背景图，完全不敢想像，不用图片要如何实现，可是真的就可以用代码敲出来。随后看了看文章附带的连接，真可谓是大开眼界，膜拜大神啊！

先给大家看几张图
![漂亮的纹理背景](http://imgchr.com/images/texture_bg.jpg)

对，你没看错，这些好看的纹理背景都是用css3实现的，没有图片背景哦！！！

那现在就来看看究竟是如何实现的。

### 一、简单的布局：
html代码很简单，只要一个容器即可
```html
<div class="horizontal stripes"></div>
```

来看一下css代码
``` css
.stripes {
	height: 250px;
	width: 375px;
	float: left;
	margin: 10px;
	-webkit-background-size: 50px 50px;
	-moz-background-size: 50px 50px;
	background-size: 50px 50px;
	-moz-box-shadow: 1px 1px 8px gray;
	-webkit-box-shadow: 1px 1px 8px gray;
	box-shadow: 1px 1px 8px gray;
}
```

样式布局里除了基础布局，用到了两个css3的属性，box-shadow（盒阴影） 和 background-size （规定背景图像的尺寸）
box-shadow 使用方法：
> 语法：**box-shadow**: h-shadow v-shadow blur spread color inset;

> **h-shadow** 必需。水平阴影的位置。允许负值。

> **v-shadow** 必需。垂直阴影的位置。允许负值。

> **blur** 可选。模糊距离。

> **spread** 可选。阴影的尺寸。

> **color** 可选。阴影的颜色。请参阅 CSS 颜色值。

> **inset** 可选。将外部阴影 (outset) 改为内部阴影。

通过上面的语法，我们可以给边框设置多层阴影

> 语法：**background-size**: length|percentage|cover|contain;

> **length** 设置背景图像的高度和宽度。第一个值设置宽度，第二个值设置高度。如果只设置一个值，则第二个值会被设置为 "auto"。

> **percentage** 以父元素的百分比来设置背景图像的宽度和高度。第一个值设置宽度，第二个值设置高度。如果只设置一个值，则第二个值会被设置为 "auto"。

> **cover** 把背景图像扩展至足够大，以使背景图像完全覆盖背景区域。背景图像的某些部分也许无法显示在背景定位区域中。

> **contain** 把图像图像扩展至最大尺寸，以使其宽度和高度完全适应内容区域。


以上的代码实现的就是一个带有阴影的框，下面来实现纹理和颜色部分

``` css
.horizontal{
	background-color: #0ae;
	background-image: -webkit-gradient(linear, 0 0, 0 100%, color-stop(.5, rgba(255, 255, 255, .2)), color-stop(.5, transparent), to(transparent));
	background-image: -webkit-linear-gradient(rgba(255, 255, 255, .2) 50%, transparent 50%, transparent);
	background-image: -moz-linear-gradient(rgba(255, 255, 255, .2) 50%, transparent 50%, transparent);
	background-image: -ms-linear-gradient(rgba(255, 255, 255, .2) 50%, transparent 50%, transparent);
	background-image: -o-linear-gradient(rgba(255, 255, 255, .2) 50%, transparent 50%, transparent);
	background-image: linear-gradient(rgba(255, 255, 255, .2) 50%, transparent 50%, transparent);
}
```

- 1、背景色是#0ae，没有疑问
- 2、纹理使用的是css3的 background-image 属性里面的线性渐变 linear-gradient 的值，不同内核的浏览器的写法不同，所实现的就是一半为白色透明度为 20% ，一半为全透明，其余部分透明
- 3、综合以上实现最后的效果即是在一个背景色为 #0ae 的 div 上面有一个遮罩层。

[查看demo](/fe/css3/css3_texture_background/index.html)