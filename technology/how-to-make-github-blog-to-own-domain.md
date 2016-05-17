~<{
    "title": "如何将github上面搭建的博客放到自己的域名下",
    "auther": "liucui",
    "mark": "web,github,前端",
    "create_time": "2015-06-10",
    "cat": "fe",
    "introduction": "最近这段时间折腾了下github，以前都是在上面找一些开源代码来看，基本上没有在上面写过代码，作为一个前端开发工程师来说，有点不道德哈，最近研究了下 hexo ，搭建了一个博客系统，但使用的是github的二级域名，着实不太方便，于是就想着把这个博客系统搬到我自己的域名下，开始还费了不少功夫，弄好后发现其实步骤非常简单。",
    "thumb_img": "http://imgchr.com/images/github_blog.jpg"
}>~


# 如何将github上面搭建的博客放到自己的域名下

最近这段时间折腾了下github，以前都是在上面找一些开源代码来看，基本上没有在上面写过代码，作为一个前端开发工程师来说，有点不道德哈，最近研究了下 hexo ，搭建了一个博客系统，但使用的是github的二级域名，着实不太方便，于是就想着把这个博客系统搬到我自己的域名下，开始还费了不少功夫，弄好后发现其实步骤非常简单。

### 1、你需要有一个可以配置的域名，当然你还要有一个github的帐号

### 2、使用hexo搭建一个基于 github 的博客

- hexo 本身有比较完善的 [开发文档](http://hexo.io/) 使用起来非常方便。
> hexo 配置文件比较麻烦，使用的时候仔细阅读官方文档，避免出错。

- 在本地安装好 hexo 环境后，就可以开始折腾了

```shell
- npm install hexo-cli -g  // 安装hexo 环境
- hexo init blog   // 在本地实例化一个hexo项目
- cd blog  // 进入到项目文件夹
- npm install		// 实例化的项目里面有个package.json 文件，这一步是威力安装json文件里面定义过的那些包
- hexo server		// 运行起来喽
```

- 为github帐号添加SSH keys
> - 创建SSH key 命令：ssh-keygen
> - 然后系统提示输入文件保存位置等信息，连续敲三次回车即可，生成的SSH key文件保存在中～/.ssh/id_rsa.pub
> - 然后用文本编辑工具打开该文件，命令是：
vim ~/.ssh/id_rsa.pub
> - 拷贝.ssh/id_rsa.pub文件内的所以内容，将它粘帖到github帐号管理中的添加SSH key界面中
> - 打开 github-->settins-->ssh key 里面增加一个key，这个key值便是你刚刚拷贝的那个key值
> - 添加过程github会提示你输入一次你的github密码
> - 添加完成后就可以再你的电脑上面clone你在github上面的代码了。


### 3、接下来就是配置域名

- 在你的域名里面添加一个 A 记录，记录值填写你的 github 博客的域名，这样就可以了，一般要等几分钟才会生效，不要心急哦。
- 同样你也可以把它作为你的一个耳机域名来管理，这里我们通过CNAME 的形式来设置。记录类型为 CNAME ，主机记录就是你要写的二级域名的名字（如：aa.bb.com，这里就填aa），记录值同样是你 github 博客的域名。
- 设置二级域名还有个地方需要改，在 github 上，你的博客内容的根目录，添加一个文件，叫做 CNAME，没有后缀名哦，内容就是你的 二级域名的完整地址，即 aa.bb.com ，这里不需要加 http 或 https，结尾不需要加 「/」。

至此，我们可以轻松的将一个github 的博客放到我们自己的域名下面了，由于国内各大服务器提供商目前都不提供免费的服务器（有些短期免费，到期后搬迁太麻烦），github作为全球炙手可热的开源产品，实在是各位猿媛的首选啊！

### 4、hexo 提供markdown格式写文档内容

对于我这个markdown的重度使用者来说，hexo 无疑更是一大利器，简直喜欢到不能再喜欢

以前用过很多 免费的markdown 编辑器，每一款都有各自的侧重点，寻觅了好久，终于找到了一个特别适合自己的编辑器，介绍给大家。[LightPaper
](http://www.ashokgelal.com/) 不过目前貌似只提供mac 版本。喜欢这个编辑器主要是因为 它可以添加目录，还可以时时预览，主题还比较丰富，下面是编辑器的截图。

![LightPaper---markdown编辑利器](http://imgchr.com/lightPaper.png)

### 5、关于我自己的github
	
由于我的博客是基于node自己开发的，因此我把github搭建的博客写为了二级域名的格式，[点击可查看](http://hexo.iqianduan.net) 这里还没有添加任何内容，完全是一个hexo初始的博客样子，小伙伴们，根据自己需要赶紧折腾起来把！