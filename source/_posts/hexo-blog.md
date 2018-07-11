---
title: hexo搭建博客过程（详细）
data: 2018-11-10 13:34:00
tags: 
- hexo
- nodejs
- markdown
categories : c

---
本章节详细介绍hexo搭建博客的过程

<!-- more -->

### 第一步:安装git，并且设置user.name和user.email配置信息：
```html
git config --global user.name "你的GitHub用户名"
git config --global user.email "你的GitHub注册邮箱"
生成ssh密钥文件：
ssh-keygen -t rsa -C "你的GitHub注册邮箱"
```
然后直接三个回车即可，默认不需要设置密码
然后找到生成的.ssh的文件夹中的id_rsa.pub密钥，将内容全部复制
![](/images/git秘钥.png)
打开GitHub_Settings_keys 页面，新建new SSH Key
![](/images/sshkeys.png)
Title为标题，任意填即可，将刚刚复制的id_rsa.pub内容粘贴进去，最后点击Add SSH key。
在Git Bash中检测GitHub公钥设置是否成功，输入 
```html
ssh git@github.com 
```
![](/images/验证秘钥是否成功.png)

### 安装hexo
#### 全局安装hexo
```
npm install -g hexo-cli
```
#### 生成hexo博客站点
安装 Hexo 完成后，请执行下列命令，Hexo 将会在指定文件夹中新建所需要的文件。
```html
$ hexo init <folder>
$ cd <folder>
$ npm install
#hexo的服务启动，命令
hexo server
```
安装完成后，制定文件夹的目录如下：
```html
.
├── _config.yml
├── package.json
├── scaffolds
├── source
|   ├── _drafts
|   └── _posts
└── themes
```
#### hexo常用命令
```html
# 清空缓存
hexo clean
# 生成静态网页
hexo g
# 启动hexo服务，默认端口为4000
hexo s
```
### 安装Next主题
#### 进入hexo官网，找到next主题
![](/images/next主题.png)
windows的主题安装方法如下：
[next主题地址](https://github.com/theme-next/hexo-theme-next）
Windows下下载主题：
```html
#在终端窗口下，定位到 Hexo 站点目录下。使用 Git checkout 代码：
$ cd your-hexo-site
$ git clone https://github.com/iissnan/hexo-theme-next themes/next
```
Linux的主题链接是：https://github.com/iissnan/hexo-theme-next
linux下安装方法是：
```html
$ cd hexo
$ ls
_config.yml  node_modules  package.json  public  scaffolds  source  themes
$ mkdir themes/next
$ curl -s https://api.github.com/repos/iissnan/hexo-theme-next/releases/latest | grep tarball_url | cut -d '"' -f 4 | wget -i - -O- | tar -zx -C themes/next --strip-components=1
```
#### next的相关配置

对于整个项目，有一个站点配置文件_config.yml，该文件位于根目录下，对于每个主题，都有一个主题的配置文件_config.yml，位于每个主题的根目录下，在本项目中位于E:\Blog\themes/next目录下：

##### 启用主题
与所有 Hexo 主题启用的模式一样。 当 克隆/下载 完成后，打开 站点配置文件， 找到 theme 字段，并将其值更改为 next。
```html
theme: next
```
到此，NexT 主题安装完成。下一步我们将验证主题是否正确启用。在切换主题之后、验证之前， 我们最好使用 hexo clean 来清除 Hexo 的缓存。

##### 验证主题
首先启动 Hexo 本地站点，并开启调试模式（即加上 --debug），整个命令是 hexo s --debug。 在服务启动的过程，注意观察命令行输出是否有任何异常信息，如果你碰到问题，这些信息将帮助他人更好的定位错误。 当命令行输出中提示出：
``` html
INFO  Hexo is running at http://0.0.0.0:4000/. Press Ctrl+C to stop.
```
此时即可使用浏览器访问 http://localhost:4000，检查站点是否正确运行,当你看到站点的外观与下图所示类似时即说明你已成功安装 NexT 主题。这是 NexT 默认的 Scheme —— Muse
![](/images/主题验证.png)
现在，你已经成功安装并启用了 NexT 主题。下一步我们将要更改一些主题的设定，包括个性化以及集成第三方服务。
##### 主题设定

在主题配置文件下，找到schemes:
![](/images/主题选择.png)

#### 设置语言
编辑 站点配置文件， 将 language 设置成你所需要的语言。建议明确设置你所需要的语言，例如选用简体中文，配置如下：
```
#相对应的文件在next主题文件夹下面的language文件夹内
language: zh-CN
```
#### 设置菜单
菜单配置包括三个部分，第一是菜单项（名称和链接），第二是菜单项的显示文本，第三是菜单项对应的图标。 NexT 使用的是 Font Awesome 提供的图标， Font Awesome 提供了 600+ 的图标，可以满足绝大的多数的场景，同时无须担心在 Retina 屏幕下 图标模糊的问题。
编辑 主题配置文件，修改以下内容：

##### 设定菜单内容
对应的字段是 menu。 菜单内容的设置格式是：item name: link。其中 item name 是一个名称，这个名称并不直接显示在页面上，她将用于匹配图标以及翻译。
```html
menu:
  home: / || home
  #about: /about/ || user
  #tags: /tags/ || tags
  categories: /categories/ || th
  archives: /archives/ || archive
  #schedule: /schedule/ || calendar
  #sitemap: /sitemap.xml || sitemap
  #commonweal: /404/ || heartbeat
  ```
NexT 默认的菜单项有（标注！的项表示需要手动创建这个页面）：
![](/images/next菜单.png)

###### 设置菜单项的显示文本。
在第一步中设置的菜单的名称并不直接用于界面上的展示。Hexo 在生成的时候将使用 这个名称查找对应的语言翻译，并提取显示文本。这些翻译文本放置在 NexT 主题目录下的 languages/{language}.yml （{language} 为你所使用的语言）。

以简体中文为例，若你需要添加一个菜单项，比如 something。那么就需要修改简体中文对应的翻译文件 languages/zh-Hans.yml，在 menu 字段下添加一项：
```html
menu:
  home: 首页
  archives: 归档
  categories: 分类
  tags: 标签
  about: 关于
  search: 搜索
  commonweal: 公益404
  something: 有料
```
##### 设定菜单项的图标
对应的字段是 menu_icons。 此设定格式是 item name: icon name，其中 item name 与上一步所配置的菜单名字对应，icon name 是 Font Awesome 图标的 名字。而 enable 可用于控制是否显示图标，你可以设置成 false 来去掉图标。
```html
menu_icons:
  enable: true
  # Icon Mapping.
  home: home
  about: user
  categories: th
  tags: tags
  archives: archive
  commonweal: heartbeat
```

#### 设置侧栏 
略：
参考：https://theme-next.iissnan.com/getting-started.html#menu-settings

#### 设置头像
编辑 主题配置文件， 修改字段 avatar， 值设置成头像的链接地址。其中，头像的链接地址可以是：
![](/images/设置头像.png)
```html
avatar: http://example.com/avatar.png
```

#### 设置作者昵称以及站点描述
编辑 站点配置文件， 设置 author 为你的昵称。
编辑 站点配置文件， 设置 description 字段为你的站点描述。站点描述可以是你喜欢的一句签名
```html
title: 改变从现在开始
subtitle: You are clever
description: 热爱生活，勇于前进
keywords: 
author: xliangfchen
language: zh-CN
timezone:
```
#### 添加动态背景
打开 next/layout/_layout.swig
在</body>之前添加代码(注意不要放在</head>的后面)：
```html
{% if theme.canvas_nest %}
<script type="text/javascript" src="//cdn.bootcss.com/canvas-nest.js/1.0.0/canvas-nest.min.js"></script>
{% endif %}
```
修改主题配置文件，将canvas_nest修改为true
```html
canvas_nest: true
```
#### 添加更新时间
修改语言配置文件/themes/next/languages/zh_Hans.yml，在post下添加以下内容：
```html
post:
  updated: 更新于
```
修改主题配置文件/themes/next/_config.yml
```
updated_at: true
```
写文章的时候可以直接在文章开头设置更新时间
```html
modified:
```
#### 启用站点搜索
##### 安装hexo-generator-search
在站点的根目录下执行以下命令：
```html
npm install hexo-generator-search --save
```
##### 安装 hexo-generator-searchdb
在站点的根目录下执行以下命令：
```html
npm install hexo-generator-searchdb --save
```
##### 启用搜索
编辑站点配置文件，新增以下内容到最后：
```html
search:
  path: search.xml
  field: post
  format: html
  limit: 10000
```
编辑主题配置文件，将local_search下的enable改为true：
```html
local_search:
  enable: true
```
### 上传项目至github
做本操作前倾自行注册github账号，并且已经把秘钥生成成功

#### 创建Repository
创建的时候需要注意Repository的名字。例如我的Github账号是xliangfchen，那么应该创建的Repository的名字为：xliangfchen.github.io

#### 修改配置文件
进入刚刚创建的Repository，复制Repository的连接，例如https://github.com/xliangfchen/xliangfchen.github.io.git

修改站点配置文件
```html
deploy:
  type: git
  repo: https://github.com/xliangfchen/xliangfchen.github.io.git
  branch: master
  message: 'updated at:{{now("YYYY-MM-DD HH/mm/ss")}}'
```

#### 提交代码至github上
```html
hexo generate
hexo deploy
```
在提交代码时可能会出现ERROR Deployer not found: git的错误，此时只需要运行以下命令
```html
npm install --save hexo-deployer-git
```

#### 将Hexo的源码备份到Github分支里面
上传到分支里存储，修改本地的时候先上传存储，再发布。更换电脑的时候再下载下来源文件
```html
$ git init
$ git remote add origin git@github.com:username/username.github.io.git
$ git add .
$ git commit -m "blog"
$ git push origin master:Hexo-Blog
```
在本地写好博文后，可以先执行：
```html
$ git add .
$ git commit -m "blog"
$ git push origin master:Hexo-Blog
```
### 对hexo相关命令进行解释
参考：https://hexo.io/zh-cn/docs/commands.html
#### init
```html
$ hexo init [folder]
```
新建一个网站。如果没有设置 folder ，Hexo 默认在目前的文件夹建立网站。

#### new
```html
$ hexo new [layout] <title>
```
新建一篇文章。如果没有设置 layout 的话，默认使用 _config.yml 中的 default_layout 参数代替。如果标题包含空格的话，请使用引号括起来。

#### generate
```html
$ hexo generate
```
生成静态文件。
参数说明：
```html
-d, --deploy	文件生成后立即部署网站
-w, --watch	监视文件变动
该命令可以简写为
$ hexo g
```
#### publish
```html
$ hexo publish [layout] <filename>
发表草稿。
```
#### server
```html
$ hexo server
启动服务器。默认情况下，访问网址为： http://localhost:4000/。
````
参数说明：
```html
-p, --port	重设端口
-s, --static	只使用静态文件
-l, --log	启动日记记录，使用覆盖记录格式
```
#### deploy
```html
$ hexo deploy
部署网站。
```
参数说明：
```html
-g, --generate	部署之前预先生成静态文件
该命令可以简写为：
$ hexo d
```
#### render
```
$ hexo render <file1> [file2] ...
渲染文件。
```
参数说明：
```html
-o, --output	设置输出路径
migrate
$ hexo migrate <type>
从其他博客系统 迁移内容。
```
#### clean
```html
$ hexo clean
清除缓存文件 (db.json) 和已生成的静态文件 (public)。
```
在某些情况（尤其是更换主题后），如果发现您对站点的更改无论如何也不生效，您可能需要运行该命令。

#### list
```html
$ hexo list <type>
列出网站资料。
```

#### version
```html
$ hexo version
显示 Hexo 版本。
```

### 对git相关命令进行解释
参考：https://git-scm.com/book/zh/v2/Git-%E5%9F%BA%E7%A1%80-%E8%8E%B7%E5%8F%96-Git-%E4%BB%93%E5%BA%93
#### 在现有目录中初始化仓库
```html
#如果你打算使用 Git 来对现有的项目进行管理，你只需要进入该项目目录并输入：
$ git init
```
该命令将创建一个名为 .git 的子目录，这个子目录含有你初始化的 Git 仓库中所有的必须文件，这些文件是 Git 仓库的骨干。 但是，在这个时候，我们仅仅是做了一个初始化的操作，你的项目里的文件还没有被跟踪
如果你是在一个已经存在文件的文件夹（而不是空文件夹）中初始化 Git 仓库来进行版本控制的话，你应该开始跟踪这些文件并提交。 你可通过 git add 命令来实现对指定文件的跟踪，然后执行 git commit 提交：
```html
$ git add *.c
$ git add LICENSE
$ git commit -m 'initial project version'
```
稍后我们再逐一解释每一条指令的意思。 现在，你已经得到了一个实际维护（或者说是跟踪）着若干个文件的 Git 仓库。
#### 克隆现有的仓库
如果你想获得一份已经存在了的 Git 仓库的拷贝，比如说，你想为某个开源项目贡献自己的一份力，这时就要用到 git clone 命令。 如果你对其它的 VCS 系统（比如说Subversion）很熟悉，请留心一下你所使用的命令是"clone"而不是"checkout"。 这是 Git 区别于其它版本控制系统的一个重要特性，Git 克隆的是该 Git 仓库服务器上的几乎所有数据，而不是仅仅复制完成你的工作所需要文件。 当你执行 git clone 命令的时候，默认配置下远程 Git 仓库中的每一个文件的每一个版本都将被拉取下来。 事实上，如果你的服务器的磁盘坏掉了，你通常可以使用任何一个克隆下来的用户端来重建服务器上的仓库（虽然可能会丢失某些服务器端的挂钩设置，但是所有版本的数据仍在，详见 在服务器上搭建 Git ）。

克隆仓库的命令格式是 `git clone [url]` 。 比如，要克隆 Git 的可链接库 libgit2，可以用下面的命令：
```html
$ git clone https://github.com/libgit2/libgit2
```
这会在当前目录下创建一个名为 “libgit2” 的目录，并在这个目录下初始化一个 .git 文件夹，从远程仓库拉取下所有数据放入 .git 文件夹，然后从中读取最新版本的文件的拷贝。 如果你进入到这个新建的 `libgit2` 文件夹，你会发现所有的项目文件已经在里面了，准备就绪等待后续的开发和使用。 如果你想在克隆远程仓库的时候，自定义本地仓库的名字，你可以使用如下命令：
```
$ git clone https://github.com/libgit2/libgit2 mylibgit
```
这将执行与上一个命令相同的操作，不过在本地创建的仓库名字变为 ```mylibgit``。

Git 支持多种数据传输协议。 上面的例子使用的是 https:// 协议，不过你也可以使用 git:// 协议或者使用 SSH 传输协议，比如 user@server:path/to/repo.git 。 在服务器上搭建 Git 将会介绍所有这些协议在服务器端如何配置使用，以及各种方式之间的利弊。