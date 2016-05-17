~<{
    "title": "一个div实现一个圆的关闭按钮",
    "auther": "liucui",
    "mark": "web,html,css3,前端",
    "create_time": "2015-03-26",
    "cat": "fe",
    "introduction": "小僧去面试的时候被问到的一个问题，主要就是考察css3的功底，所谓难者不会，会者不难，我也来试试。",
    "thumb_img": "http://imgchr.com/images/a_div_x_circle_bg.jpg"
}>~

# 一个div实现一个圆的关闭按钮

> 小僧去面试的时候被问到的一个问题，主要就是考察css3的功底，所谓难者不会，会者不难，我也来试试。

### 原理如下

- 利用css3的伪元素 **:before :after**
- 利用css3的转换角度 **transform: rotate(90deg);**

### 代码如下：
#### html代码
``` html
<div class="close"></div>
```
#### css代码
``` css
.close{
    width: 30px;
    height: 30px;
    background: #fff;
    position: relative;
    border-radius: 50%;
    margin: 20px auto;
}
.close:before{
    content: '';
    display: block;
    width: 100%;
    height: 1px;
    background: red;
    -ms-transform:rotate(45deg);
    -moz-transform:rotate(45deg);
    -webkit-transform:rotate(45deg);
    -o-transform:rotate(45deg);
    position: absolute;
    left: 0;
    top: 15px;
}
.close:after{
    content: '';
    display: block;
    width: 100%;
    height: 1px;
    background: red;
    -ms-transform:rotate(135deg);
    -moz-transform:rotate(135deg);
    -webkit-transform:rotate(135deg);
    -o-transform:rotate(135deg);
    position: absolute;
    left: 0;
    top: 15px;
}
```
实现的图片是这样的

![一个div实现关闭按钮](http://imgchr.com/images/a_div_close.png)
