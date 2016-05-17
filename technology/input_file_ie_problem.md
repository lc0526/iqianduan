~<{
	"title": "input[type='file']在IE下的问题",
	"author": "liucui",
	"mark": "web,html,前端,兼容性",
	"create_time": "2015-03-24",
	"cat": "fe",
	"introduction": "input上传文件的表单很好用，但在IE浏览器里面问题太多了，虽然IE大势已去，但在天朝这样的国度里面，IE的使用者大有人在，不得不调整兼容问题。",
	"thumb_img": "http://imgchr.com/images/input_file_ie_bg.jpg"
}>~

# input[type='file']在IE下的问题

> input上传文件的表单很好用，但在IE浏览器里面问题太多了，虽然IE大势已去，但在天朝这样的国度里面，IE的使用者大有人在，不得不调整兼容问题。

首先看个demo
```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>demo2</title>
	<style>
	*{
		padding: 0;
		margin: 0;
	}
	.btn{
		width: 100px;
		height: 28px;
		line-height: 28px;
		color: #fff;
		background: #538de3;
		border-radius: 6px;
		margin: 30px auto;
		position: relative;
		text-align: center;
		cursor: pointer;
	}
	.btn input{
		position: absolute;
		left: 0;
		top: 0;
		width: 100%;
		height: 100%;
		opacity: 0;
		filter: alpha(opacity=0);
		cursor: pointer;
	}
	</style>
</head>
<body>
	<div class="btn">
		<input type="file">上传文件
	</div>
</body>
</html>
```


以上的代码理论上应该可以实现一个上传的按钮，现代浏览器里面都支持良好，但在IE浏览器里面的表现着实恶心，点击上传的时候左边需要双击才可以上传，右半边按钮单击就可以上传。

> 几经修改，最终解决了问题，但是还是没弄明白为什么IE会这样显示。

- 为了修改IE里面的bug，在上传input的外层div上面增加 `overflow: hidden;` 的样式。
- 给input 标签增加样式 `left: -150px; width: 250px; font-size: 100px;`

哈哈，问题解决了，妈妈再也不用担心IE上面的bug搞不定了！！！