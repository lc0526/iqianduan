~<{
    "title": "Swig 使用指南",
    "auther": "liucui",
    "mark": "web,html5,nodejs,前端",
    "create_time": "2015-12-11",
    "cat": "fe",
    "introduction": "前后端分离已经是目前大部分项目的开发模式，分离带来的首要问题就是前端模板的问题，swig是一个可在客户端也可在服务端使用的模板引擎，语法简单，非常好用，，这篇文章就简单介绍下如何使用swig",
    "thumb_img": "http://imgchr.com/images/how_to_use_swig8f86f.jpg"
}>~

# Swig 使用指南
### 一、如何使用
#### 1、API
```javascript
swig.init({
    allowErrors: false,
    autoescape: true,
    cache: true,
    encoding: 'utf8',
    filters: {},
    root: '/',
    tags: {},
    extensions: {},
    tzOffset: 0
});
```

options:
- **allowErrors**: 默认值为 false。将所有模板解析和编译错误直接输出到模板。如果为 true，则将引发错误，抛出到 Node.js 进程中，可能会使您的应用程序崩溃。
- **autoescape**:  默认true，强烈建议保持。字符转换表请参阅转义过滤器。
 - true: HTML安全转义
 - false: 不转义，除非使用转义过滤器或者转义标签
 - 'js': js安全转义
- **cache**: 更改为 false 将重新编译每个请求的模板的文件。正式环境建议保持true。
- **encoding**: 模板文件编码
- **root**: 需要搜索模板的目录。如果模板传递给 swig.compileFile 绝对路径(以/开头)，Swig不会在模板root中搜索。如果传递一个数组，使用第一个匹配成功的数组项。
- **tzOffset**: 设置默认时区偏移量。此设置会使转换日期过滤器会自动的修正相应时区偏移量。
- **filters**:自定义过滤器或者重写默认过滤器，参见自定义过滤器指南。
- **tags**: 自定义标签或者重写默认标签，参见自定义标签指南。
- **extensions**: 添加第三方库，可以在编译模板时使用，参见参见自定义标签指南。

#### 2、nodejs

```javascript
var tpl = swig.compileFile("path/to/template/file.html"); 
var renderedHtml = tpl.render({ vars: 'to be inserted in template' });
```

或者

```javascript
var tpl = swig.compile("Template string here"); 
var renderedHtml = tpl({ vars: 'to be inserted in template' });
```

#### 3、结合Express
```shell
npm install express
npm install consolidate
```

然后

```javascript
app.engine('.html', cons.swig);
app.set('view engine', 'html');
```

#### 4、浏览器
Swig浏览器版本的api基本与nodejs版相同，不同点如下：
- 不能使用swig.compileFile，浏览器没有文件系统
- 你必须提前使用swig.compile编译好模板
- 按顺序使用extends, import, and include，同时在swig.compile里使用参数templateKey来查找模板
```javascript
var template = swig.compile('<p>{% block content %}{% endblock %}</p>', { filename: 'main' });
var mypage = swig.compile('{% extends "main" %}{% block content %}Oh hey there!{% endblock %}', { filename: 'mypage' });
```

### 二、基础
#### 1、变量
```javascript
{{ foo.bar }}
{{ foo['bar'] }}
```

如果变量未定义，输出空字符。

变量可以通过过滤器来修改：

```javascript
{{ name|title }} was born on {{ birthday|date('F jS, Y') }}
// Jane was born on July 6th, 1985
```

#### 2、逻辑标签
参见标签部分。

#### 3、注释
#### 4、空白
模板里的空白在最终输出时默认保留，如果需要去掉空白，可以在逻辑标签前后加上空白控制服-：

```javascript
{% for item in seq -%}
    {{ item }}
{%- endfor %}
```

### 三、模板继承
Swig 使用 extends 和 block 来实现模板继承
**layout.html**
```html
<!doctype html>
<html>
<head>
    <meta charset="utf-8">
    <title>{% block title %}My Site{% endblock %}</title>
    {% block head %}
        <link rel="stylesheet" href="main.css">
    {% endblock %}
</head>
<body>
    {% block content %}{% endblock %}
</body>
</html>
```

**index.html**
```html
{% extends 'layout.html' %}
{% block title %}My Page{% endblock %}
{% block head %}
{% parent %}
    <link rel="stylesheet" href="custom.css">
{% endblock %}
{% block content %}
    <p>This is just an awesome page.</p>
{% endblock %}
```

### 四、变量过滤器
用于修改变量。变量名称后用 | 字符分隔添加过滤器。您可以添加多个过滤器。
#### 1、例子
```html
{{ name|title }} was born on {{ birthday|date('F jS, Y') }}
and has {{ bikes|length|default("zero") }} bikes.
```

也可以使用 filter 标签来为块内容添加过滤器

```html
{% filter upper %}oh hi, paul{% endfilter %}
```

#### 2、内置过滤器
- **add(value)**：使变量与value相加，可以转换为数值字符串会自动转换为数值。
- **addslashes**：用 \ 转义字符串
- **capitalize**：大写首字母
- **date(format[, tzOffset])**：转换日期为指定格式
- **format**：格式
- **tzOffset**：时区
- **default(value)**：默认值（如果变量为undefined，null，false）
- **escape([type])**：转义字符
 - 默认： &, <, >, ", '
 - js: &, <, >, ", ', =, -, ;
- **first**：返回数组第一个值
- **join(glue)**：同[].join
- **json_encode([indent])**：类似JSON.stringify, indent为缩进空格数
- **last**：返回数组最后一个值
- **length**：返回变量的length，如果是object，返回key的数量
- **lower**：同''.toLowerCase()
- **raw**：指定输入不会被转义
- **replace(search, replace[, flags])**：同''.replace
- **reverse**：翻转数组
- **striptags**：去除html/xml标签
- **title**：大写首字母
- **uniq**：数组去重
- **upper**：同''.toUpperCase
- **url_encode**：同encodeURIComponent
- **url_decode**：同decodeURIComponemt

#### 3、自定义过滤器
创建一个 myfilter.js 然后引入到 Swig 的初始化函数中
```javascript
swig.init({ filters: require('myfilters') });
```

在 myfilter.js 里，每一个 filter 方法都是一个简单的 js 方法，下例是一个翻转字符串的 filter：
```javascript
exports.myfilter = function (input) {
    return input.toString().split('').reverse().join('');
};
```

你的 filter 一旦被引入，你就可以向下面一样使用：
```html
{{ name|myfilter }}
     {% filter myfilter %}
    I shall be filtered
{% endfilter %}
```

你也可以像下面一样给 filter 传参数：
```javascript
exports.prefix = function(input, prefix) {
    return prefix.toString() + input.toString();
};
{{ name|prefix('my prefix') }}
{% filter prefix 'my prefix' %I will be prefixed with "my prefix".{% endfilter %}
{% filter prefix foo %}I will be prefixed with the value stored to `foo`.{% endfilter %}
```

### 五、标签
#### 1、内置标签
**extends**：使当前模板继承父模板，必须在文件最前
- 参数file：父模板相对模板 root 的相对路径
**block**：定义一个块，使之可以被继承的模板重写，或者重写父模板的同名块
- 参数name：块的名字，必须以字母数字下划线开头
**parent**：将父模板中同名块注入当前块中
**include**：包含一个模板到当前位置，这个模板将使用当前上下文
- 参数file: 包含模板相对模板 root 的相对路径
- 参数ignore missing：包含模板不存在也不会报错
- 参数with x：设置 x 至根上下文对象以传递给模板生成。必须是一个键值对
- 参数only：限制模板上下文中用 with x 定义的参数

```html
{% include template_path %}
{% include "path/to/template.js" %}
```

你可以标记 ignore missing，这样如果模板不存在，也不会抛出错误

```html
{% include "foobar.html" ignore missing %}
```

本地声明的上下文变量，默认情况不会传递给包含的模板。例如以下情况，inc.html 无法得到 foo 和 bar

```html
{% set foo = "bar" %}
{% include "inc.html" %}
{% for bar in thing %}
    {% include "inc.html" %}
{% endfor %}
```

如果想把本地声明的变量引入到包含的模板种，可以使用 with 参数来把后面的对象创建到包含模板的上下文中
```html
{% set foo = { bar: "baz" } %}
{% include "inc.html" with foo %}
{% for bar in thing %}
    {% include "inc.html" with bar %}
{% endfor %}
```

如果当前上下文中 foo 和 bar 可用，下面的情况中，只有 foo 会被 inc.html 定义
```html
{% include "inc.html" with foo only %}
```

only 必须作为最后一个参数，放在其他位置会被忽略

**raw**：停止解析标记中任何内容，所有内容都将输出
- 参数file: 父模板相对模板 root 的相对路径
**for**：遍历对象和数组
- 参数x：当前循环迭代名
- 参数in：语法标记
- 参数y：可迭代对象。可以使用过滤器修改

```html
{% for x in y %}
    {% if loop.first %}<ul>{% endif %}
    	<li>{{ loop.index }} - {{ loop.key }}: {{ x }}</li>
    {% if loop.last %}</ul>{% endif %}
{% endfor %}
```

> 特殊循环变量
> - loop.index：当前循环的索引（1开始）
> - loop.index0：当前循环的索引（0开始）
> - loop.revindex：当前循环从结尾开始的索引（1开始）
> - loop.revindex0：当前循环从结尾开始的索引（0开始）
> - loop.key：如果迭代是对象，是当前循环的键，否则同 loop.index
> - loop.first：如果是第一个值返回 true
> - loop.last：如果是最后一个值返回 true
> - loop.cycle：一个帮助函数，以指定的参数作为周期
```

```html
{% for item in items %}
    <li class="{{ loop.cycle('odd', 'even') }}">{{ item }}</li>
{% endfor %}
```

在 for 标签里使用 else
```html
{% for person in people %}
    {{ person }}
{% else %}
    There are no people yet!
{% endfor %}
```

**if**：条件语句
- 参数：接受任何有效的 JavaScript 条件语句，以及一些其他人类可读语法

```javascript
{% if x %}{% endif %}
{% if !x %}{% endif %}
{% if not x %}{% endif %}
{% if x and y %}{% endif %}
{% if x && y %}{% endif %}
{% if x or y %}{% endif %}
{% if x || y %}{% endif %}
{% if x || (y && z) %}{% endif %}
{% if x [operator] y %}
    Operators: ==, !=, <, <=, >, >=, ===, !==
{% endif %}
{% if x == 'five' %}
    The operands can be also be string or number literals
{% endif %}
{% if x|length === 3 %}
    You can use filters on any operand in the statement.
{% endif %}
{% if x in y %}
    If x is a value that is present in y, this will return true.
{% endif %}
```

else 和 else if

```html
{% if foo %}
    Some content.
{% else if "foo" in bar %}
    Content if the array `bar` has "foo" in it.
{% else %}
    Fallback content.
{% endif %}
```

**autoescape**：改变当前变量的自动转义行为
- 参数on：当前内容是否转义
- 参数type：转义类型，js 或者 html，默认 html

假设

```html
some_html_output = '<p>Hello "you" & \'them\'</p>';
```

然后

```html
{% autoescape false %}
    {{ some_html_output }}
{% endautoescape %}
{% autoescape true %}
    {{ some_html_output }}
{% endautoescape %}
{% autoescape true "js" %}
    {{ some_html_output }}
{% endautoescape %}
```

将会输出

```html
<p>Hello "you" & 'them'</p>
 &lt;p&gt;Hello &quot;you&quot; &amp; &#39;them&#39; &lt;/p&gt;
 \u003Cp\u003EHello \u0022you\u0022 & \u0027them\u0027\u003C\u005Cp\u003E
```

**set**：设置一个变量，在当前上下文中复用
- 参数name：变量名
- 参数=：语法标记
- 参数value：变量值

```html
{% set foo = [0, 1, 2, 3, 4, 5] %} {% for num in foo %}
    <li>{{ num }}</li>
{% endfor %}
```

**macro**：创建自定义可服用的代码段
- 参数...: 用户定义

```html
{% macro input type name id label value error %}
 <label for="{{ name }}">{{ label }}</label>
 <input type="{{ type }}" name="{{ name }}" id="{{ id }}" value="{{ value }}"{% if error %} class="error"{% endif %}>
{% endmacro %}
```

然后像下面使用

```html
<div>
    {{ input("text", "fname", "fname", "First Name", fname.value, fname.errors) }}
</div>
<div>
    {{ input("text", "lname", "lname", "Last Name", lname.value, lname.errors) }}
</div>
```

输出如下

```html
<div>
    <label for="fname">First Name</label>
    <input type="text" name="fname" id="fname" value="Paul">
</div>
<div>
    <label for="lname">Last Name</label>
    <input type="text" name="lname" id="lname" value="" class="error">
</div>
```

**import**：允许引入另一个模板的宏进入当前上下文
- 参数file：引入模板相对模板 root 的相对路径
- 参数as：语法标记 var: 分配给宏的可访问上下文对象

```html
{% import 'formmacros.html' as form %}
{# this will run the input macro #}
    {{ form.input("text", "name") }}
    {# this, however, will NOT output anything because the macro is scoped to the "form"     object: #}
{{ input("text", "name") }}
```

**filter**：对整个块应用过滤器
- 参数filter_name: 过滤器名字
- 参数... : 若干传给过滤器的参数 父模板相对模板 root 的相对路径

```html
{% filter uppercase %}
    oh hi, {{ name }}
{% endfilter %}
{% filter replace "." "!" "g" %}
    Hi. My name is Paul.
{% endfilter %}
```

输出

```console
OH HI, PAUL Hi! My name is Paul!
```

**spaceless**：尝试移除html标签间的空格

```html
{% spaceless %}
    {% for num in foo %}
        <li>{{ loop.index }}</li>
    {% endfor %}
{% endspaceless %}
```

输出

```html
<li>1</li><li>2</li><li>3</li>
```
