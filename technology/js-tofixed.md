~<{
    "title": "js小数点操作方法(两位小数点)总结",
    "auther": "liucui",
    "mark": "web,js,前端",
    "create_time": "2014-11-04",
    "cat": "fe",
    "introduction": "js小数点操作方法(两位小数点)总结",
    "thumb_img": "http://imgchr.com/images/js_tofixed_bg.jpg"
}>~

# js小数点操作方法(两位小数点)总结
### 用Javascript取float型小数点后两位
例22.127456取成22.13,如何做？
- 1、 最笨的办法:
``` javascript
function get(){
    var s = 22.127456 + "";
    var str = s.substring(0,s.indexOf(".") + 3);
    alert(str);
}
```

- 2、 正则表达式效果不错:
``` javascript
window.onload = function(){
     var a = "23.456322";
    var aNew;
    var re = /([0-9]+\.[0-9]{2})[0-9]*/;
    aNew = a.replace(re,"$1");
    alert(aNew);
}
```

- 3、 他就比较聪明了:
``` javascript
var num = 22.127456;
alert( Math.round(num*100)/100);
```

- 4、会用新鲜东西的朋友....... 但是需要 IE5.5+才支持。
``` javascript
var num = 22.127456;
alert( num.toFixed(2));
```

- 5、 数字舍入toFixed()其中是利用一个函数toFixed 来取小数点几位的!
``` javascript
var a = "0.11";
var b = "0.2801";
var c = "1.002";
var sum1 = parseFloat(a)+parseFloat(b)+parseFloat(c);
var sum2 = (parseFloat(a)+parseFloat(b)+parseFloat(c)).toFixed(4);
document.write("a+b+c="+sum1);
document.write("<br/>");
document.write("a+b+c="+sum2);
```

> a，b，c相加本来为1.3921，但sum1得出的结果为：1.3921000000000001，显然不正确，通过toFixed(n)方法修正后（n是精确的小数点位数），得到正确结果。
> 例如：parseFloat(1.392143).toFixed(3)=1.392;

#### 顺便附上php获取小数点后两位的方法:

``` php
<?php
    echo round(12.566921,2);
    echo '<br />';
    echo round(12.561921,2);
?>
```