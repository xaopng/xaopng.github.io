---
title: 'Win10:Hexo+github搭建个人博客'
abbrlink: 6335
date: 2023-06-14 22:06:09
tags:
---

## 写在最前

{% hideToggle 无聊的碎碎念不看也罢 %}

{% note info simple %}
最开始接触博客的契机是我第一次重装Ubuntu的时候。看的是楠皮的博客，之后又重装了7次Ubuntu，每次都去看[楠皮的博客](https://blog.vanxnf.top/)，一个人撑起了他的博客访问量。自此，我终于意识到我也该写个博客了，一开始用到的是csdn，虽然csdn自带的网页markdown非常方便，还有快捷键支持，但是实在是架不住那边烦人的站点广告，之后也试过简书，虽然好看了许多，但是还是没有我当初浏览楠皮博客时那种丝般顺滑的感觉。
{% endnote %}

{% note success simple %}
最后，在无数个下定决心的双休日，我终于在前天，也即是20190407，记牢这个历史性的时刻，搭建成功了我的第一个个人博客，虽然还很简略，没什么文章，但是不急，把我那200多篇个人日记慢慢搬过来就好了。
{% endnote %}

{% endhideToggle %}

## 准备工作

{% hideToggle 安装必要的软件 %}

{% note default simple %}

首先要安装必要的软件
如果下载速度过慢可以参考这篇教程:[基于NDM和TamperMonkey脚本实现高速下载](https://akilar.top/posts/e332c532/)
以下五个软件中，Node.js和git为必要软件，后三者作为之后编写博客的Markdown编辑器，挑选一个使用即可。

{% endnote %}

{% tabs test1, -1 %}

<!-- tab Node.js -->

[Node.js](https://nodejs.org/en/)

{% note danger no-icon simple %}

我下载的是的11.13.0版本。（建议选择左边的稳定版本，右边的最新版本可能会出现莫名bug）
Node.js是基于Chrome的V8 JavaScript引擎构建的运行在服务端的JavaScript开发平台,知道这些就够了。
反正作为一个包管理器，安装以后再也不用去打扰它的具体配置。默默运行就是了。

{% endnote %}

<!-- endtab -->

<!-- tab git -->

[git](https://git-scm.com/)

{% note danger no-icon simple %}

我下载的是2.21.0版本，可以选择安装版，也可以选择绿色版。
绿色版需要加上Git_HOME，%Git_HOME%\bin之类的环境变量，建议下载安装版一路默认安装，安装包会自动添加相应的环境变量。

{% endnote %}

<!-- endtab -->

<!-- tab Atom -->

[Atom](https://github.com/atom/atom/releases)

{% note danger no-icon simple %}

Atom自带markdown渲染，Shift+Ctrl+M即可。而且安装简单。
界面美观，怎么吹都不过分啊。要是没有特殊需求的话这个就足够了。
事实上如果Atom安装了插件之后会很酷炫
插件安装教程和推荐可以参考这篇教程:Atom插件安装和推荐。

{% endnote %}

<!-- endtab -->

<!-- tab Typora -->

[Typora](https://www.typora.io/)

{% note danger no-icon simple %}

typora是一个专业的markdown编辑器，比之atom的最大优势就是同步渲染速度，缺点是对于代码高亮的支持并不是很方便，自带源代码模式 ，拿来看看代码也不错

{% endnote %}

<!-- endtab -->

<!-- tab HexoEditor -->

[HexoEditor](https://github.com/zhuzhuyule/HexoEditor/releases)

{% note danger no-icon simple %}

HexoEditor是我目前一直最喜爱的一款Markdown编辑器，自带图片复制转Markdown链接，同时支持三种图床。具备各种快捷键，还能拖动文本，自带预览，对一些主题渲染有适配，没适配的也能通过导入相应的tags配置进行渲染。
有兴趣的可以看一下我专门为它写的配置教程:[Hexo-editor——Hexo专用的编辑器](https://akilar.top/posts/1da4f99e/)

{% endnote %}

<!-- endtab -->


{% endtabs %}

{% endhideToggle %}

## 安装Hexo

{% hideToggle 点击查看Hexo安装教程 %}

{% note primary simple %}

首先给出官方网址:[Hexo官网](https://hexo.io/zh-cn/)
内容仅供参考，具体搭建可以直接看下面的教程。放官网的目的是在这里可以找到全套的使用文档，而且hexo的作者是个台湾人，对中文的支持很不错。

{% endnote %}

1. 首先需要建立博客文件夹，建议建在非系统盘，例如`~D:/Hexo/`，那么这个目录就是我们博客的根目录了。因为每个人的命名习惯不同，本帖之后会以`[Blogroot]`指代博客根目录。
2. 使用`npm`安装`Hexo`,在`[Blogroot]`路径下{% label 右键 blue %}->{% label "Git Bash Here" blue %},输入
	```bash
	npm config set registry https://registry.npmmirror.com
	#将npm源替换为阿里的镜像。之后的安装就会迅速很多了。
	npm install hexo-cli -g
	# hexo-cli 是 hexo的指令集。
	hexo init
	# 有了指令集以后，使用它的初始化指令来初始化安装Hexo博客。
	```
	
3. 安装插件，依然是在`[Blogroot]`路径下{% label 右键 blue %}->{% label "Git Bash Here"  blue %}，使用`npm`指令挑选需要的插件安装。(请仔细阅读注释，确定你是否需要安装这个插件)。
	```bash
	npm install hexo-generator-index --save
	# 主页插件，最新版Hexo默认安装，可跳过
	npm install hexo-generator-archive --save
	# 归档插件，最新版Hexo默认安装，可跳过
	npm install hexo-generator-category --save
	# 分类插件，最新版Hexo默认安装，可跳过
	npm install hexo-generator-tag --save
	# 标签插件，最新版Hexo默认安装，可跳过
	npm install hexo-server --save
	# 服务插件，最新版Hexo默认安装，可跳过
	npm install hexo-renderer-marked --save
	# markdown渲染支持插件，最新版Hexo默认安装，可跳过
	npm install hexo-renderer-stylus --save
	# nib css支持插件，如无需求，可跳过
	npm install hexo-generator-feed --save
	# RSS订阅支持插件，如无需求，可跳过
	npm install hexo-generator-sitemap --save
	# sitemap生成插件，帮助搜索引擎抓取，如无需求，可跳过
	npm install hexo-admin --save
	# 网页端hexo文档管理插件，如无需求，可跳过
	npm install hexo-deployer-git --save
	# git部署插件，必须安装
	```
4. 常用命令
	{% note   no-icon simple %}
	常用命令在这篇文章中有详细总结:双系统-[Hexo和github的常用命令行归纳](https://akilar.top/posts/803c5fab/)
	{% endnote %}
	
	```bash
	hexo clean
	#清空缓存
	hexo generate
	hexo g #简写
	#重新编译
	hexo server
	hexo s #简写
	#打开本地访问
	hexo new <layout> "文章title"
	#新建文章
	hexo deploy
	hexo d #简写
	#部署到云端
	```
5. 本地预览：在`[Blogroot]`路径下{% label 右键  blue %}->{% label "Git Bash Here" blue %}，输入
	```bash
	hexo server
	```
	然后在浏览器中打开localhost:4000 ,就能看到
	如果你安装了`hexo-admin`插件，就可以通过访问`localhost:4000/admin`来管理你的文章了。并且在可视化界面中操作文章内容。恭喜你，博客的本地部署到这里算是告一段落了。
6. 添加分类页面和标签页面
	- 添加分类页面
		在`[Blogroot]`路径下{% label 右键  blue %}->{% label "Git Bash Here" blue %}，输入
		```bash
		hexo new page categories
		# 创建“分类”页面
		```
		
		打开`[Blogroot]/sources/categories/index.md`
		在它的头部加上`type`属性。
		```diff
		  ---
		  title: categories
		  date: 2017-05-27 13:47:40
		+ type: "categories"
		  ---
		```
		给文章添加分类，例如我要给`Hello-world`这篇文章添加分类，打开
		`[Blogroot]/sources/_posts/Hello-woeld.md`,修改他的头部内容为：
		```diff
		 ---
		 title: Hello-World
		 date: 2019-04-07 00:38:36
		+ categories: 学习笔记
		 tags: [node.js, hexo]
		 ---
		```
	- 添加标签页面
		在`[Blogroot]`路径下{% label 右键  blue %}->{% label "Git Bash Here" blue %}，输入
		
		```bash
		hexo new page tags
		# 创建“标签”页面
		```
		
		打开`[Blogroot]/sources/tags/index.md`
		在它的头部加上`type`属性。
		
		```diff
		 ---
		 title: tags
		 date: 2017-05-27 13:47:40
		+ type: "tags"
		 ---
		```
		给文章添加标签，例如我要给`Hello-world`这篇文章添加标签，打开
		
		`[Blogroot]/sources/_posts/Hello-world.md`,修改他的头部内容为：
		
		```diff
		  ---
		  title: Hello-World
		  date: 2019-04-07 00:38:36
		  categories: 学习笔记
		+ tags: [node.js, hexo]  # 逗号是英文逗号
		  ---
		```
		
		第二种写法是用-短划线列出来
		
		```diff
		  ---
		  title: Hello-World
		  date: 2019-04-07 00:38:36
		  categories: 学习笔记
		+ tags:
		+   - node.js # 注意短线后有空格
		+   - 📁Hexo
		  ---
		```

{% endhideToggle %}



## 部署到GitHub

{% hideToggle 点击查看部署至github的教程 %}

1. 访问官网按照指示注册github账号:[github](https://github.com/)

{% hideToggle 注册过程中可能遇到的bug %}

    有些用户注册github账号时可能会遇到`Unable to verify your captcha response`报错。解决方案：
    
    - 升级浏览器内核：直接下载安装最新版chrome或者Microsoft edge浏览器即可。
    - 把github域名添加到hosts文件中，可以自行百度，也可以参考这篇教程:[访问github或部署在gitpage上的网站过慢的解决方案](https://akilar.top/posts/61b3e163/)

{% endhideToggle %}

   1. 新建`username.github.io`仓库:

      注册成功后，在github首页单击头像->Your repositories

      在自己的 GitHub 账号下创建一个新的仓库，命名为 `username.github.io`（username是你的账号名)。

{% hideToggle 科普：为什么要命名为username.github.io？ %}

{% note warning simple %}


  专门写给老实孩子看的，这段主要是为了解释为啥要按照`username.github.io`这个要求来新建仓库名，不感兴趣的话跳过这段看后面的`配置Git 与 GitHub`就好，不用追根究底。
  在这里，要知道，`GitHub Pages`有两种类型：`User/Organization Pages` 和 `Project Pages`，而我所使用的是 `User Pages`。
  简单来说，`User Pages` 与 `Project Pages` 的区别是：

  - `User Pages` 是用来展示用户的，而 `Project Pages` 是用来展示项目的。
  - 用于存放`User Pages`的仓库必须使用 `username.github.io` 的命名规则，而 `Project Pages`则没有特殊的要求。
  - `User Pages`通过`https://username.github.io`进行访问，而`Projects Pages`通过`https://username.github.io/projectname`进行访问。

{% endnote %}
      

{% note info simple %}
      相关资料:[GitHub Pages Basics / User, Organization, and Project Pages](https://help.github.com/articles/user-organization-and-project-pages/)
{% endnote %}

{% endhideToggle %}

   2. 配置`Git`与`GitHub`:

      - 此处为全局配置，所以可以在任意位置打开git bash,设置用户名称和邮件地址
      
        ```bash
        git config --global user.name "akilarlxh"
        git config --global user.email "akilarlxh@gmail.com"
        ```

      - 设置完成后为了能够在本地使用`git`管理`github`上的项目，需要绑定`SSHkey`。
      
        ```bash
        ssh-keygen -t rsa -C akilarlxh@gmail.com
        # -C后面加你在github的用户名邮箱，这样公钥才会被github认可
        less ~/.ssh/id_rsa.pub
        # 查看公钥内容稍后加入Github账户的sshkey中,
        ```
      
        {% note warning simple %}
        这一步骤推荐在`git bash`中运行指令。若使用`powershell`或`cmd`，`less`指令缺少必要的C语言环境，需要访问`C:\Users\Username\.ssh\id_rsa.pub`复制。
        {% endnote %}

      - 打开[github网页](https://github.com/)

        单击头像->settings,在设置页面找到SSH and GPG keys，单击New SSH key新建`SSH KEY`。

      - 保存后，在git bash测试sshkey是否添加成功，输入
      
        ```bash
        ssh -T git@github.com
        # Attempts to ssh to GitHub
        ```

      - 正常输出是
      
        ```bash
        The authenticity of host 'github.com (207.97.227.239)' can't be established.
        RSA key fingerprint is 16:27:ac:a5:76:28:2d:36:63:1b:56:4d:eb:df:a6:48.
        Are you sure you want to continue connecting (yes/no)?
        # 此处请输入yes
        Hi username! You've successfully authenticated, but GitHub does not
        provide shell access.
        ```

{% hideToggle 配置过程中可能遇到的bug %}

输出报错为

```bash
ssh: connect to host gitee.com port 22: Connection timed out
```

这是由于在当前网络环境中，端口22被占用了，我们改用其他端口再试试

```bash
ssh -T -p 443 git@ssh.github.com
# -p 443表示使用443端口，要是443也被占用，也可以尝试其他端口
```

{% endhideToggle %}

   3. 配置hexo部署插件内容：

      - 确保你安装了`hexo-deployer-git`,如果没有，在`[Blogroot]`路径下右键->"Git Bash Here"，输入：
      
        ```bash
        npm install hexo-deployer-git --save
        ```

      - 打开`[Blogroot]/_config.yml`,修改底部的`deploy`配置项。如果没有找到`deploy`配置项,则自己添加：
      
        {% note info simple %}
        感谢[@姬顶盒](https://musinn.github.io/)的反馈，最新版[hexo-deployer-git](https://www.npmjs.com/package/hexo-deployer-git)的配置项写法已经更新
        {% endnote %}
      
        ```bash
        # 站点部署到github要配置Deployment
        ## Docs: https://zespia.tw/hexo/docs/deploy.html
        deploy:
          type: git
          repo:
            github:
              url: git@github.com:username/username.github.io.git  # 记得把username替换为自己的用户名
              branch: master #2020年10月后github新建仓库默认分支改为main，注意修改
            # 也可以用另一种写法,二选一即可
            github: git@github.com:username/username.github.io.git,master
        ```
      
        {% note warning simple %}
        这里`deploy`前面不要有`空格`，而所有`:`后面都要有空格。对齐缩进情况要严格按照示例来写。`yml`编译对缩进要求很严格，所以格式很重要。
        {% endnote %}

   4. 把本地`hexo`博客内容提交到`git`仓库

      - 若以上内容已经准确配置，在`[Blogroot]`路径下右键->"Git Bash Here"，输入：
      
        ```bash
        hexo clean
        hexo generate
        hexo deploy
        ```

        

      - 不出意外，就可以在浏览器上输入`https://username.github.io`访问你的博客了。

        （记得替换`username`为自己的用户名。

        {% hideToggle 网页部署阶段可能出现的bug %}

        报错`ERROR Deployer not found: git`

        - git用户名和邮箱配置错误，
        
          ```bash
          git config --global user.name%"username"
          git config --global user.email%"username@example.com"
          ```

          这里的`%`，在正确的格式中是一个`空格`，如果你之前没有打空格，那么邮箱和用户名根本就没有记录进去。回退到这一步重新进行。

        - `hexo-deployer-git`插件没有安装正确，重新在`[Blogroot]`路径下右键->"Git Bash Here"，执行：
        
          ```bash
          npm install hexo-deployer-git –save
          # 重新安装之后，再尝试提交
          hexo deploy
          ```
        
        
        {% endhideToggle %}

{% endhideToggle %}

## 主题配置

{% note primary simple %}
本博客主题现已改用[Butterfly](https://butterfly.js.org/)，你可以直接访问[Butterfly主题官方文档](https://butterfly.js.org/)进行主题配置，相比NexT，Butterfly的功能高度集成化，仅仅只需在配置文件中修改true或false即可。本站效果美化方案参考[基于Butterfly主题的美化日记](https://akilar.top/posts/f99b208/)
{% endnote %}



## 版本控制

### 源码存放方案：开源or闭源

{% tabs 源码存放方案, -1 %}
<!-- tab 源码保密，仅开源网页-->
{% note warning simple %}
如果按照我现在的方式进行双分支部署，虽然可以在一个仓库内同时管理博客源码和博客生成的网页文件，但是基于`gitpage`必须是开放的性质，你的博客源码将是完全开源的，任何人都能通过`git clone`拷贝你的博客源码，唯一的区别就是在没有绑定`SSH Key`的情况下他们不可能提交到你的库内。
{% endnote %}

所以，对源码有保密需求的，可以参照以下方式另外新建一个保密仓库作为源码存放库。

1. 创建存放源码的私有仓库

   我们需要创建一个用来存放`Hexo`博客源码的私有仓库`[SourceRepo]`，这点在[Win10](https://akilar.top/posts/6ef63e2d/)的`Hexo`博客搭建教程中有提到。为了保持教程的连贯，此处再写一遍。

   创建完成后，需要把博客的源码`push`到这里。首先获取远程仓库地址，此处虽然`SSH`和`HTTPS`均可。`SSH`在绑定过`ssh key`的设备上无需再输入密码，`HTTPS`则需要输入密码，但是`SSH`偶尔会遇到端口占用的情况。请自主选择。

2. 在`[Blogroot]`路径下右键->"Git Bash Here"，输入

   ```bash
   git init # 初始化git
   ```

   这一步会在你的博客目录下新建一个`.git`文件夹。因为是隐藏文件夹，所以需要你先确保当前目录下隐藏文件夹可见才能看到它。

3. 在远端提交前，我们需要先调整一下屏蔽项，能够使用指令进行安装的内容不包括在需要提交的源码内，这样可以显著减少需要提交的文件量和加快提交速度。打开`[Blogroot]/.gitignore`（也是隐藏文件）,输入以下内容：

   ```bash
   .DS_Store
   Thumbs.db
   db.json
   *.log
   node_modules/
   public/
   .deploy*/
   .deploy_git*/
   .idea
   themes/butterfly/.git
   ```

   如果不是`butterfly`主题，记得替换最后一行内容为你自己当前使用的主题。

4. 然后尝试第一次提交你的目录到远程仓库,依然是在`[Blogroot]`路径下右键->"Git Bash Here"，输入：

   ```bash
   git add . # 添加文件到本地仓库
   git commit -m "自定义内容即可" # 添加文件描述信息
   git remote add origin git@github.com:username/YourRepositoryName.git #链接远程仓库地址，创建主分支
   ```

5. 偶尔会遇到一些与远端内容不一致的问题，一般是因为在创建远程仓库时点选了生成`README.md`或者`license`的选项，输入指令：

   ```bash
   # 要是提示origin已经存在，那么执行
   git remote rm origin
   # 然后再重新尝试
   git remote add origin git@github.com:username/YourRepositoryName.git
   
   git pull origin YourBranchName # 把远程仓库的新增的内容覆盖到本地仓库
   
   git push -u origin YourBranchName -f
   # 把本地仓库的文件推送到远程仓库的主分支，
   #YourBranchName记得替换成分支名，一般是master。
   #2020年10月后github新建仓库默认分支改为main
   # -f 是强制提交，主要是因为前后版本不一致造成的。
   # 然后执行以下指令生成网站并部署到 GitHub 上。
   #(Hexo部署网站是根据_config.yml内的配置，所以不受影响）
   hexo generate
   hexo deploy
   ```

   

<!-- endtab -->

<!-- tab 源码开源，双分支部署 -->

1. 第一次提交git

{% note simple %}

开始准备你的第一次提交`git`
修改博客内容后依次执行以下命令来提交网站相关的文件：

{% endnote %}

   在`[Blogroot]`路径下右键->"Git Bash Here"，输入

   ```bash
   git init
   ```

   这一步会在你的博客目录下新建一个`.git`文件夹。因为是隐藏文件夹，所以需要你先确保当前目录下隐藏文件夹可见才能看到它。

{% note warning simple %}

这句在这里主要是为了在文件夹中`git init`让`git`标记此文件夹为版本库
如果不写这句，不出意外会报错`"fatal: not a git repository (or any of the parent directories): .git"`
和`hexo init`一样，只要第一次时运行一次就好

{% endnote %}

   

2. 在远端提交前，我们需要先调整一下屏蔽项，能够使用指令进行安装的内容不包括在需要提交的源码内，这样可以显著减少需要提交的文件量和加快提交速度。打开`[Blogroot]/.gitignore`（也是隐藏文件）,输入以下内容：

   ```txt
   .DS_Store
   Thumbs.db
   db.json
   *.log
   node_modules/
   public/
   .deploy*/
   .deploy_git*/
   .idea
   themes/butterfly/.git
   ```

   如果不是`butterfly`主题，记得替换最后一行内容为你自己当前使用的主题。

3. 然后尝试第一次提交你的目录到远程仓库,依然是在`[Blogroot]`路径下右键->"Git Bash Here"，输入：

   ```bash
   # 添加文件到本地仓库
   git add .
   # 添加文件描述信息
   git commit -m "自定义内容即可"
   # 添加远程仓库地址,链接远程仓库，创建主分支
   git remote add origin git@github.com:username/username.github.io.git
   # 要是提示origin已经存在，那么执行
   git remote rm origin
   # 然后再次尝试
   git remote add origin git@github.com:username/username.github.io.git
   # 本地新建source分支并切换到source分支
   git checkout -b source
   # 把本地仓库的文件推送到远程仓库
   git push -u origin source -f
   # 强制提交，主要是因为前后版本不一致造成的，
   # 然后执行以下任意一条生成网站并部署到 GitHub 上。
   hexo generate -d
   hexo g -d
   ```

{% note success simple %}

这样一来，在 `GitHub` 上的 `username.github.io` 仓库就有两个分支，
一个 `source` 分支用来存放网站的原始文件，
一个 `master` 分支用来存放生成的静态网页。(2020年10月后github新建仓库默认分支由master改为main)

{% endnote %}

4. 然后把source设置为默认分支。

5. 可能遇到的bug

   - 通过`git clone` 命令下载的`themes`或者`module`文件中可能有`.git文件夹`，会有影响，所以删去，想留着以后方便升级主题也有办法，不过实在太烦，还不如删了痛快，留着教程以后重新配置主题可能还快些。比如我就是在`next`这个主题文件夹里有个`.git`文件夹。

   - 报错`Please make sure you have the correct access rights and the repository exists`
     这个貌似是因为我们新建了分支的关系，反正它的意思就是找不到你的服务器了，如果上面操作都没问题的话建议你删除在`user/username/`下的`.ssh文件夹`，然后重新回到`部署git和github`再配置一下你的`ssh key`。

   - 提示`refusing to merge unrelated histories`意思就是，
     这两个合并的仓库提交历史不一致，所以拒绝合并。
     那么添加`--allow-unrelated-histories`指令表示允许强制合并。

     ```bash
     git pull origin source --allow-unrelated-histories
     ```

<!-- endtab -->
{% endtabs %}



### 博客管理流程

在本地对博客进行修改（添加新博文、修改样式等等）后，通过下面的流程进行管理

1. 依次执行指令
   ```bash
   git add .
   git commit -m "..."
   git push
   # 将改动推送到 GitHub
   ```

2. 然后才执行
   ```bash
   hexo generate -d
   # 或者
   hexo g -d
   ```

   将本地文件发布网站到`master`分支上。(2020年10月后github新建仓库默认分支由master改为main)



### 本地资料丢失或多PC同步

当重装电脑之后，或者想在其他电脑上修改博客，可以使用下列步骤：

1. 使用`git clone git@github.com:Username/[HexoSourceRepo].git`拷贝仓库；
   此处的`[HexoSourceRepo]`指代上述博客源码存放方案中存放源码的仓库名。

2. 在本地新拷贝的`[HexoSourceRepo]`文件夹下通过终端依次执行下列指令：
   ```bash
   npm install -g hexo-cli
   npm install
   ```

   在下一篇的[Ubuntu-Hexo+github搭建个人博客](https://akilar.top/posts/e5502ef6/)中，用这个方法部署文件就会很快。



### 指令脚本

{% tabs 指令脚本, -1 %}
<!-- tab 普通版 -->
每次都要反复敲那么几行指令一定会无聊，那么干脆把指令存在脚本里，每次需要用到的时候双击一下就可以高枕无忧了。

在`[Blogroot]`文件夹下新建三个`txt`文件，分别命名为`git-pull`、`git-push`、`hexo-publish`,打开后依次在里面输入相应的命令。

- git-pull（用来从远程仓库拉取最新更改，适用于多PC或多系统端之间的版本对接）
  ```bash
  git pull
  ```

- git-push（用于提交每次的修改到远程仓库）
  ```bash
  git add .
  git commit -m "deploy from hexo-admin"
  git push
  ```

  

- hexo-publish（清空本地缓存后重新部署博客页面）
  ```bash
  hexo clean
  hexo generate
  hexo depoly
  ```

  之后将`.txt`后缀更改为`.sh`后缀，就是一个可执行脚本了。

<!-- endtab -->

<!-- tab 升级版 -->
在hexo根目录`[blogroot]/`下新建一个脚本文件：`menu.sh`,将以下内容复制进去。

```bash
#!/bin/sh
#本脚本用于群友交流，完全开源，可以随意传阅，不过希望保留出处。
#Author：Akilar
#Modify:Hajeekn(SL)
#Updated: 2021-08-09
echo "=================================================="
echo "              欢迎使用Hexo控制脚本!"
echo "                更方便的魔改版本"
echo "=================================================="
HexoPath=$(cd "$(dirname "$0")"; pwd)
cd ${HexoPath}
printf "\033[32m Blog 根目录："${HexoPath}"\033[0m\n"

printf "\033[32m [0] \033[0m 退出菜单\n"
printf "\033[31m =============以下功能需要在空文件夹内使用========\033[0m\n"
printf "\033[32m [1] \033[0m 初始化安装Hexo（仅在第一次安装时使用）\n"
printf "\033[32m [2] \033[0m 从云端恢复Hexo\n"
printf "\033[31m =============以下功能需要在Hexo文件夹内使用======\033[0m\n"
printf "\033[32m [3] \033[0m 开启本地预览\n"
printf "\033[32m [4] \033[0m 重新编译后开启本地预览\033[33m（修改过_config.yml需使用这个才能看到变化）\033[0m\n"
printf "\033[32m [5] \033[0m 新建博客文章\n"
printf "\033[32m [6] \033[0m 新建博客页面\n"
printf "\033[32m [7] \033[0m 部署页面到博客网站\n"
printf "\033[32m [8] \033[0m 从Github拉取最新版本\n"
printf "\033[32m [9] \033[0m 提交本地修改到GitHub\n"
printf "\033[32m [10] \033[0m 升级Hexo及插件\033[31m（慎用）\033[0m\n"
printf "\033[32m [11] \033[0m 重新安装依赖\n"
printf "\033[32m [12] \033[0m 安装butterfly主题\n"
printf "\033[32m [13] \033[0m 安装volantis主题\n"
printf "\033[32m [14] \033[0m 安装Hexo-Admin \033[33m(用于管理或撰写Hexo博文，适合初学者使用)\033[0m\n"
printf "\033[31m =============以下功能为全局指令==================\033[0m\n"
printf "\033[32m [15] \033[0m 安装ssh密钥\n"
printf "\033[32m [16] \033[0m 验证ssh密钥\n"
printf "\033[32m [17] \033[0m 切换npm源为阿里镜像\033[33m (当使用publish命令时会出现错误,适用于不发布包的人)\033[0m\n"
printf "\033[32m [18] \033[0m 切换npm源为官方源\033[33m (安装慢,但可以使用所有命令)\033[0m\n"
printf "\033[32m [19] \033[0m 安装 Git\n"
printf "\033[32m [20] \033[0m 安装 Node.js\n"
printf "请选择需要的功能，默认选择\033[32m [3] \033[0m开启本地预览\n"
printf "选择：\n"
read answer

if [ "${answer}" = "1" ]; then
printf "\033[32mINFO \033[0m 正在初始化,请坐和放宽...\n"
mkdir Hexo
cd Hexo
npm config set registry https://registry.npmmirror.com
npm install -g hexo-cli
hexo init
npm install --save
npm install hexo-deployer-git --save
printf "\033[32mINFO \033[0m 请查看您当前的Hexo版本...\n"
hexo version
printf "\033[32mINFO \033[0m 安装完成，您可以开始您的Hexo之旅了！\n"
printf "\033[32mINFO \033[0m 请将本脚本文件放入Hexo文件夹以继续使用其他功能！\n"
sleep 5s
printf "\033[32mINFO \033[0m \033[33m请将本脚本文件放入Hexo文件夹以继续使用其他功能！\033[0m\n"
sleep 5s
printf "\033[32mINFO \033[0m \033[31m请将本脚本文件放入Hexo文件夹以继续使用其他功能！\033[0m\n"
sleep 5s
exit 0
else
if [ "${answer}" = "2" ]; then
printf "\033[32mINFO \033[0m 启动拉取器 ...\n"
printf "请输入仓库源码地址: "
read giturl
git clone ${giturl} Hexo
cd Hexo
printf "\033[32mINFO \033[0m 恢复Hexo中...\n"
npm config set registry https://registry.npmmirror.com
npm install -g hexo-cli
# npm install gulp-cli -g #全局安装gulp，未配置不用开启
npm install --save
printf "\033[32mINFO \033[0m 恢复完成，您可以开始您的Hexo之旅了！\n"
printf "\033[32mINFO \033[0m 请将本脚本文件放入Hexo文件夹以继续使用其他功能！\n"
sleep 5s
printf "\033[32mINFO \033[0m \033[33m请将本脚本文件放入Hexo文件夹以继续使用其他功能！\033[0m\n"
sleep 5s
printf "\033[32mINFO \033[0m \033[31m请将本脚本文件放入Hexo文件夹以继续使用其他功能！\033[0m\n"
sleep 5s
exit 0
else
if [ "${answer}" = "3" ] || [ "${answer}" = "" ]; then
printf "\033[32mINFO \033[0m 正在启动本地预览，可以按Ctrl+C退出\n"
hexo s
exec ${HexoPath}/menu.sh
else
if [ "${answer}" = "4" ]; then
printf "\033[32mINFO \033[0m 正在清理本地缓存...\n"
hexo clean
# printf "\033[32mINFO \033[0m 正在更新番剧列表...\n"
# hexo bangumi -u #bilibili追番插件，未配置无需开启
printf "\033[32mINFO \033[0m 正在重新编译静态页面...\n"
hexo generate
# printf "\033[32mINFO \033[0m 正在压缩静态资源...\n"
# gulp #gulp插件，未配置无需开启
printf "\033[32mINFO \033[0m 正在开启本地预览，可以按Ctrl+C退出\n"
hexo server
exec ${HexoPath}/menu.sh
else
if [ "${answer}" = "5" ] || [ "${answer}" = "" ]; then
printf "\033[32mINFO \033[0m 请输入您想要新建的文章标题\n"
printf "\033[32mINFO \033[0m \033[33m标题中的各类标点符号和空格，请用短横\"-\"代替！\033[0m\n"
printf "您的文章标题："
read posttitle
hexo new post ${posttitle}
printf "\033[32mINFO \033[0m 新建完成，正在尝试为您打开文章文件\n"
start ${HexoPath}/source/_posts/${posttitle}.md
exec ${HexoPath}/menu.sh
else
if [ "${answer}" = "6" ] || [ "${answer}" = "" ]; then
printf "\033[32mINFO \033[0m 请输入您想要新建的页面名称\n"
printf "\033[32mINFO \033[0m \033[33m名称中的各类标点符号和空格，请用短横\"-\"代替！\033[0m\n"
printf "您的页面名称："
read pagename
hexo new page ${pagename}
printf "\033[32mINFO \033[0m 新建完成，正在尝试为您打开页面文件\n"
start ${HexoPath}/source/${pagename}/index.md
exec ${HexoPath}/menu.sh
else
if [ "${answer}" = "7" ]; then
printf "\033[32mINFO \033[0m 正在清理本地缓存...\n"
hexo clean
# printf "\033[32mINFO \033[0m 正在更新番剧列表...\n"
# hexo bangumi -u #bilibili追番插件，未配置无需开启
printf "\033[32mINFO \033[0m 正在重新编译静态页面...\n"
hexo generate
# printf "\033[32mINFO \033[0m 正在压缩静态资源...\n"
# gulp #gulp插件，未配置无需开启
printf "\033[32mINFO \033[0m 正在准备将最新修改部署至Hexo...\n"
hexo deploy
printf "\033[32mINFO \033[0m 部署完成，您的网站已经是最新版本！\n"
sleep 1s
exec ${HexoPath}/menu.sh
else
if [ "${answer}" = "8" ]; then
printf "\033[32mINFO \033[0m 正在启动拉取器...\n"
printf "请输入分支名: "
read branch
git pull origin $branch
printf "\033[32mINFO \033[0m 拉取完毕，您的博客已是最新版本！\n"
sleep 1s
exec ${HexoPath}/menu.sh
else
if [ "${answer}" = "9" ]; then
printf "\033[32mINFO \033[0m 正在提交最新修改到GitHub...\n"
git add .
git commit -m "Update posts content"
git push origin $branch
printf "\033[32mINFO \033[0m 提交完毕，您的修改已上传至Github！\n"
sleep 1s
exec ${HexoPath}/menu.sh
else
if [ "${answer}" = "10" ]; then
printf "\033[32mINFO \033[0m 请先确认当前版本 ...\n"
hexo version
sleep 3s
printf "\033[32mINFO \033[0m 即将为您全局升级hexo-cli...\n"
npm install hexo-cli -g
printf "\033[32mINFO \033[0m hexo-cli升级完成，请查看当前版本。\n"
hexo version
sleep 3s
printf "\033[32mINFO \033[0m 即将为您升级npm-check...\n"
npm install -g npm-check
printf "\033[32mINFO \033[0m npm-check升级完成！\n"
printf "\033[32mINFO \033[0m 正在使用npm-check检查系统是否有可升级插件...\n"
npm-check
sleep 3s
printf "\033[32mINFO \033[0m 即将为您升级npm-upgrade...\n"
npm install -g npm-upgrade
printf "\033[32mINFO \033[0m 正在使用npm-upgrade升级插件...\n"
printf "\033[32mINFO \033[0m 您可以在接下来的过程中主动选择是否升级插件\n"
npm-upgrade
sleep 1s
printf "\033[32mINFO \033[0m 正在为您保存升级结果...\n"
npm update -g
npm update --save
printf "\033[32mINFO \033[0m 恭喜您，您的Hexo已经是最新版本\n"
sleep 2s
exec ${HexoPath}/menu.sh
else
if [ "${answer}" = "11" ]; then
printf "\033[32mINFO \033[0m 正在清空当前依赖环境 ...\n"
rm node_modules
printf "\033[32mINFO \033[0m 正在清空当前依赖关系锁定 ...\n"
rm package-lock.json
printf "\033[32mINFO \033[0m 正在清空当前依赖关系缓存 ...\n"
npm cache clean --force
printf "\033[32mINFO \033[0m 正在将npm源替换为阿里云镜像 ...\n"
npm config set registry https://registry.npmmirror.com
printf "\033[32mINFO \033[0m 正在重新安装当前依赖环境 ...\n"
npm install
sleep 2s
exec ${HexoPath}/menu.sh
else
if [ "${answer}" = "12" ]; then
printf "\033[32mINFO \033[0m 正在为您下载最新稳定版butterfly主题 ...\n"
git clone -b master https://gitee.com/iamjerryw/hexo-theme-butterfly.git themes/butterfly
printf "\033[32mINFO \033[0m 正在为您安装必要依赖！\n"
npm install hexo-renderer-pug hexo-renderer-stylus --save
printf "\033[32mINFO \033[0m 安装完成，感谢您对butterfly的支持！\n"
sleep 1s
printf "\033[32mINFO \033[0m 请在/Hexo/_config.yml中将theme修改为butterfly以激活主题！\n"
sleep 3s
exec ${HexoPath}/menu.sh
else
if [ "${answer}" = "13" ]; then
printf "\033[32mINFO \033[0m 正在为您下载最新稳定版volantis主题 ...\n"
git clone https://github.com/volantis-x/hexo-theme-volantis themes/volantis
printf "\033[32mINFO \033[0m 正在安装本地搜索必要依赖！\n"
npm install hexo-generator-search --save
npm install hexo-generator-json-content --save
printf "\033[32mINFO \033[0m 正在安装页面渲染必要依赖！\n"
npm install hexo-renderer-stylus --save
printf "\033[32mINFO \033[0m 安装完成，感谢您对volantis的支持！\n"
sleep 1s
printf "\033[32mINFO \033[0m 请在/Hexo/_config.yml中将theme修改为volantis以激活主题！\n"
sleep 3s
exec ${HexoPath}/menu.sh
else
if [ "${answer}" = "14" ]; then
printf "\033[32mINFO \033[0m 正在为您下载Hexo-Admin插件 ...\n"
npm install hexo-admin --save
printf "\033[32mINFO \033[0m 安装完成，即将为您启动本地预览！\n"
printf "\033[32mINFO \033[0m 请访问 http://localhost:4000/admin/ 进行博文编辑！\n"
sleep 2s
hexo server
sleep 1s
exec ${HexoPath}/menu.sh

else
if [ "${answer}" = "15" ]; then
printf "\033[32mINFO \033[0m 正在启动Git工具...\n"
printf "请输入 GitHub 用户名: "
read githubuser
printf "请输入 GitHub 邮箱: "
read githubemail
git config --global user.name "$githubuser"
git config --global user.email "$githubemail"
ssh-keygen -t rsa -C $githubemail
printf "\033[32mINFO \033[0m 即将打开sshkey，复制后可按 Ctrl+D 返回...\n"
sleep 2s
less ~/.ssh/id_rsa.pub
printf "\033[32mINFO \033[0m 配置完成，请将sshkey添加到Github！\n"
sleep 1s
exec ${HexoPath}/menu.sh
else
if [ "${answer}" = "16" ]; then
printf "\033[32mINFO \033[0m 正在验证SSHkey是否配置成功 ...\n"
ssh -T git@github.com
printf "\033[32mINFO \033[0m 验证完毕，您的SSHkey已成功绑定至Github！\n"
sleep 1s
exec ${HexoPath}/menu.sh
else
if [ "${answer}" = "17" ]; then
printf "\033[32mINFO \033[0m 正在查询当前npm源 ...\n"
npm config get registry
printf "\033[32mINFO \033[0m 正在将npm源替换为阿里云镜像 ...\n"
npm config set registry https://registry.npmmirror.com
sleep 2s
exec ${HexoPath}/menu.sh
else
if [ "${answer}" = "18" ]; then
printf "\033[32mINFO \033[0m 正在查询当前npm源 ...\n"
npm config get registry
printf "\033[32mINFO \033[0m 正在将npm源替换为官方源 ...\n"
npm config set registry https://registry.npmjs.org
sleep 2s
exec ${HexoPath}/menu.sh
else
if [ "${answer}" = "19" ]; then
printf "\033[32mINFO \033[0m 安装 Git 暂不支持linux、macos,如果你是linux或macos用户,请使用系统自带的包管理器安装 ...\n"
printf "\033[32mINFO \033[0m 启动下载器 ...\n"
printf "安装默认使用32包,如果要安装64请更改sh源码或手动将32替换为64 ...\n"
mkdir temp
cd temp
certutil -urlcache -split -f https://npmmirror.com/mirrors/git-for-windows/v2.32.0.windows.2/Git-2.32.0.2-32-bit.exe
./Git-2.32.0.2-32-bit.exe
rm -r temp
printf "安装完成"
sleep 2s
exec ${HexoPath}/menu.sh
else
if [ "${answer}" = "20" ]; then
printf "\033[32mINFO \033[0m 安装 Node.js 暂不支持linux、macos,如果你是linux或macos用户,请使用系统自带的包管理器安装 ...\n"
printf "\033[32mINFO \033[0m 启动下载器 ...\n"
printf "安装默认使用32包,如果要安装64请更改sh源码或手动将32替换为64 ...\n"
mkdir temp
cd temp
certutil -urlcache -split -f https://npmmirror.com/mirrors/node/latest-v12.x/node-v12.22.3-x86.msi
./node-v12.22.3-x86.msi
cd ../
rm -r temp
printf "安装完成"
sleep 2s
exec ${HexoPath}/menu.sh
else
if [ "${answer}" = "0" ]; then
printf "\033[32mINFO \033[0m 欢迎下次光临！\n"
sleep 1s
exit 0
else
printf "\033[31mERROR \033[0m 输入错误，请返回重新选择...\n"
sleep 1s
exec ${HexoPath}/menu.sh
fi
fi
fi
fi
fi
fi
fi
fi
fi
fi
fi
fi
fi
fi
fi
fi
fi
fi
fi
fi
fi
```



<!-- endtab -->
{% endtabs %}


