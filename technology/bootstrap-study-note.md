~<{
    "title": "bootstrap学习笔记",
    "auther": "liucui",
    "mark": "web,html,css,框架,前端",
    "create_time": "2014-11-01",
    "cat": "fe",
    "introduction": "Bootstrap 是目前最受欢迎的 HTML、CSS 和 JS 框架，用于开发响应式布局、移动设备优先的 WEB 项目。为了不让自己和时代脱轨，也为了更好的实现前端界面，提高开发过程的速度，把bootstrap学习了一番，记录以下笔记",
    "thumb_img": "http://imgchr.com/images/bootstrap_study_bg.jpg"
}>~

# bootstrap学习笔记
![bootstrap](http://imgchr.com/images/bootstrap_study_bg.jpg)

### 排版
- 1、基础排版：12列
- 2、标题（一）：h1-h6  主标题用h标签，副标题可在h标签里面嵌套small标签，small标签的大小是h标签的65%
- 3、段落（正文文本）：p标签
- 4、强调内容：strong 标签
- 5、粗体：b 标签
- 6、斜体：em 和 i
- 7、强调相关的类
- 8、文本对齐风格：left、right等类名
- 9、列表
    - 1、普通列表
    ``` html
    <ul>
        <li></li>
        <li></li>
    </ul>
    ```
    - 2、有序列表
    ``` html
    <ol>
        <li></li>
        <li></li>
    </ol>
    ```
    - 3、去点列表 class="list-unstyled"
    - 4、内联列表 class="list-inline"
    - 5、定义列表
    ``` html
    <dl>
        <dt></dt>
        <dd></dd>
    </dl>
    ```
        dt、dd各占一行
    - 水平定义列表 class="dl-horizontal" dt、dd在一行

- 10、代码
    - 使用`<code></code>`来显示单行内联代码
    - 使用`<pre></pre>`来显示多行块代码
    - 使用`<kbd></kbd>`来显示用户输入代码
- 11、表格
    - 基础表格   .table
    - 斑马线表格   .table-striped
    - 带边框的表格  .table-bordered
    - 鼠标悬浮高亮的表格   .table-hover
    - 紧凑型表格   .table-condensed
    - 响应式表格   .table-responsive
- 12、表格行的类：table增加table-hover 类名，bootstrap还做了特殊处理。

| 类名 | 描述  | 对应的颜色 |
| :-----| :------| :----------|
| .active| 表示当前活动的信息 | #f5f5f5 |
| .success | 表示成功或者正确的行为 | #dff0d8 |
| .info | 表示中立的信息或行为 | #d9edf7 |
| .warning | 表示警告，需要特别注意 | #fcf8e3 |
| .danger | 表示危险或者可能是错误的行为 | #f2dede|

### 表单
> 要使用bootstrap的样式的所有表单，必须是写在role属性是"form"的form标签里面

- 1、基础表单
> input、select、textarea等元素，在Bootstrap框架中，通过定制了一个类名`form-control`，也就是说，如果这几个元素使用了类名“form-control”，将会实现一些设计上的定制效果

- 2、水平表单
``` html
<form class="form-horizontal" role="form">
  <div class="form-group">
    <label for="inputEmail3" class="col-sm-2 control-label">邮箱</label>
    <div class="col-sm-10">
      <input type="email" class="form-control" id="inputEmail3" placeholder="请输入您的邮箱地址">
    </div>
  </div>
  <div class="form-group ">
    <label for="inputPassword3" class="col-sm-2 control-label">密码</label>
    <div class="col-sm-10">
      <input type="password" class="form-control" id="inputPassword3" placeholder="请输入您的邮箱密码">
    </div>
  </div>
  <div class="form-group">
    <div class="col-sm-offset-2 col-sm-10">
      <div class="checkbox">
        <label>
          <input type="checkbox"> 记住密码
        </label>
      </div>
    </div>
  </div>
  <div class="form-group">
    <div class="col-sm-offset-2 col-sm-10">
      <button type="submit" class="btn btn-default">进入邮箱</button>
    </div>
  </div>
</form>
```

写出来的表单样子

![水平表单](http://imgchr.com/images/bootstrap-1.png)

- 3、内联表单
> 为form表单添加 form-inline 类名，表单则在一行显示
- 4、表单控件(输入框input)
- 5、表单控件(下拉选择框select)
- 6、表单控件(文本域textarea)
- 7、表单控件(复选框checkbox和单选择按钮radio)
- 8、表单控件(复选框和单选按钮水平排列)
> 增加类名 checkbox-inline、radio-inline
- 9、表单控件(按钮)
实现的标签可以是以下四类：
input[type=“submit”]
input[type=“button”]
input[type=“reset”]
&lt;button&gt;

![表单控件(按钮)](http://imgchr.com/images/bootstrap-2.png)
- 10、表单控件大小
    - input-sm:让控件比正常大小更小
    - input-lg:让控件比正常大小更大
    - 这两个类适用于表单中的input，textarea和select控件
- 11、表单控件状态(焦点状态)
- 12、表单控件状态(禁用状态)

![表单控件状态(禁用状态)](http://imgchr.com/images/bootstrap-3.png)
- 13、表单控件状态(验证状态)
    - .has-warning:警告状态（黄色）
    - .has-error：错误状态（红色）
    - .has-success：成功状态（绿色）

![表单控件状态(验证状态)](http://imgchr.com/images/bootstrap-4.png)
- 14、表单提示信息
    - help-block：将提示信息以块状显示，并且显示在控件底部

    ![表单提示信息](http://imgchr.com/images/bootstrap-5.png)

    - help-inline：让提示信息显示在控件的后面，也就是同一水平显示

    ![表单提示信息](http://imgchr.com/images/bootstrap-6.png)
### 按钮与图像
#### 一、按钮
- 基础类名为 btn，通过“.btn-default”定义了一个默认的按钮风格。
- 多标签支持，随意那个标签都可以作为按钮来使用。

**注意：虽然在Bootstrap框架中使用任何标签元素都可以实现按钮风格，但个人并不建议这样使用，为了避免浏览器兼容性问题，个人强烈建议使用button或a标签来制作按钮。**

- 定制风格

![定制风格](http://imgchr.com/images/bootstrap-7.jpg)

- 按钮大小

![按钮大小](http://imgchr.com/images/bootstrap-8.jpg)

- 块状按钮：btn-block 宽度继承父元素，且为块状元素
- 按钮状态——活动状态
    :hover   :active    :focus

- 按钮状态——禁用状态：增加类名disabled

#### 二、图像：
在<img>标签上添加对应的类名，样式没有对图片做大小上的样式限制，所以在实际使用的时候，需要通过其他的方式来处理图片大小。比如说修改控制图片容器大小。（注意不可以通过css样式直接修改img图片的大小，这样操作就不响应了）

- 1、img-responsive：响应式图片，主要针对于响应式设计
- 2、img-rounded：圆角图片
- 3、img-circle：圆形图片
- 4、img-thumbnail：缩略图片

#### 三、图标
所有icon都是以”glyphicon-”前缀的类名开始，然后后缀表示图标的名称images
