## 1125_GitHub Page + Hexo 搭建个人博客

> 主要参考资料：实验楼课程[使用Github Pages和Hexo搭建独立博客]( https://www.shiyanlou.com/courses/700/learning/ ), 作为会员课程质量有点一般，有些步骤显得有点繁琐，可以成功搭建
>
> 在ubuntu虚拟机部署，win10执行特定操作，教程以ubuntu环境为主

### 改进win10环境

> 学习编程是从Ubuntu开始的，命令行和包管理工具很好用，因此安装git bash和chocolatey

#### VS code + bash

> 参考自[Windows下VSCode运行Bash终端]( https://blog.csdn.net/u014291497/article/details/79146099 ) 

Git Bash提供了一种方式可以在Windows下执行Linux命令

两种方式：

1. 将Git bash目录比如C:\Program Files (x86)\Git\bin\bash.exe添加到环境变量中，就可以VSCode终端输入`bash`进入Bash模式了， 同理，输入cmd即可返回默认Cmd模式。
2. 如果想默认设置Bash模式，可以编辑用户设置文件，添加"terminal.integrated.shell.windows": "C:\\Program Files\\Git\\bin\\bash.exe"

> 特别注意：setting.json文件中，只有一对花括号，不同设置以`,`分隔

```
{
    "editor.fontFamily": "Monaco, 'Courier New', monospace",
    "terminal.integrated.shell.windows": "C:\\Program Files\\Git\\bin\\bash.exe" 
}
```

#### chocolatey

[官网安装教程]( https://chocolatey.org/install ) 

按照提示完成安装，后续可以用`choco install`，`choco upgrade`， `choco uninstall`代替相应的Linux命令

### 安装必须工具

#### Node.js

```
sudo apt-get install nodejs
```

##### npm

npm 是 Node包管理器, Node Package Manager 

```
sudo apt-get install npm
```

然后安装 `nrm` ， nrm 是 npm 的资源管理器，借助各个工具可以方便快捷地对 npm 的源进行管理。由于国内网络环境原因在使用 npm 默认下载源的时候不仅速度非常慢而且常常会超时，因此这里还手动指定了从淘宝源下载。

```bash
sudo npm install nrm -g --registry https://registry.npm.taobao.org
```

接下来就可以使用 nrm 对 npm 的资源进行管理了，通过 nrm 我们将 npm 的默认下载源设置为淘宝源。

```bash
nrm use taobao
```

#### Hexo

使用 npm 安装 Hexo 

```
sudo npm install hexo-cli -g
```

### Git

1. git是必备工具，一般都已安装好，配置`user`,`email`，生成`ssh-keygen`，若已做过这些操作，可以略过

```
git config --global user.name "your github account name"
git config --global user.email "your github account email"
```

2. 为了在后续操作中我们能将本地仓库的代码推送至 github 的仓库上，我们需要在本地生成 SSH 秘钥，并将公钥保存到 github 账户信息中，这样我们在本地提交的时候 github 就能通过本地的私钥与公钥进行校验。 

```
ssh-keygen -t rsa -C "your github account email"
```

 生成密钥的过程中会有些提示要求输入，我们一路回车下去即可。 

 在 `/home/.ssh/` 目录底下生成了两个文件，其中 `id_rsa` 是私钥，`id_rsa.pub` 是公钥 

3. 然后将公钥提交到`GitHub -> setting -> SSH adn GPG key`

### 搭建博客

1. 进入目标路径

```
cd Code
$ mkdir Hexo && cd Hexo
```

2. 初始化博客框架

```c
hexo init blog	//该初始化过程可能较慢

cd blog
npm install
```

3. 生成静态网页

```
hexo generate
```

4. 内置服务器可以本地访问 `localhost:4000 `

```
hexo server
```

> 以上命令可以简写做 hexo g, hexo s

#### 模块介绍

`Hexo`初始化完成后，`blog`文件夹内会包含以下内容

- `_config.yml` ：配置文件，可以修改网站的主题、标题、作者等信息。
- `public` ：由 hexo 根据 `source` 文件夹中的资源进行渲染生成的文件夹，里边存储着最终的静态网页文件。
- `scaffolds/` ：模板文件，当要给博客添加新文章的时候，将根据对应的模板进行创建。
- `source/` ：用于存储用户资源，比如文章与新页面等。其中以 `_` 开头的文件夹中除了 `_posts` 文件夹中的 markdown 或 HTML 文件会在执行 `generate` 操作的时候被渲染添加到 `public` 文件夹中之外，其他均被忽略。而且在初始化博客的过程中 `_posts` 目录底会自带一个 `hello-world.md` 的文件。
- `themes/` ：主题文件，自带默认主题 `landscape` 。

#### 七牛图床

静态网页的本质是解析Markdown文件，因此需要稳定的图床使得插入的图片即使在网页上也可以很少地显示

1.  进入[七牛官网](https://portal.qiniu.com/signup/choice)，按流程注册`个人账户`，需要身份证实名认证，支付宝授权
2.  进入个人面板，添加`对象存储`
3.  填写信息之后，创建 空间, 空间名随便，空间属性必须是**公共空间**，否则无法生成外链
4.  进入资源存储列表，点击内容管理 
5.  点击上传文件，按提示完成上传之后就可以从文件列表处获取上传文件的外链了。 

### 发布博客

#### 新建博客

```
hexo new [layout] <filename>
```

其中 `layout` 为可选参数，指定了新创建的文件布局，默认为 `post` 文件。 `filename` 为必填参数，指定了文件名，如果文件名中有空格则需要把文件名用引号`""` 包裹起来

hexo 在 `source/_post` 目录之下创建了一个 `.md` 的文件，该文件即为静态网页文件的待解析文件

```
---
title: hhh
date: 2019-11-28 16:06:01
tags:
---
```

`---`为`hexo n`自动创建文件时根据模板自动添加的信息，包括文章名`title`, 日期`date`，标签`tag`，分类`categories`, 文件夹等等

` <!--more--> `指定摘要，该字段以上的内容为显示内容，全文要点开`Read more`才能阅读

#### 创建标签页与分类页

要创建标签云页面，首先要创建新的页面。

```bash
hexo new page "tags"
```

进入 `source/tags/` 修改 `index.md` 。

```
title: All tags
date: 2016-11-06 14:08:58
type: "tags"
comments: false
```

为了避免将来添加评论功能的时候标签云页面出现评论框，将 `comments` 项设置为 `false` 。当然如果你希望有评论框则不要设置这一项。

同时打开主题配置文件 将`tags` 路径为 `/tags` 

#### 主题配置

##### 下载并更换主题

1. 主题保存地址为`~/Hexo/blog/themes` 
2. 主题名即为主题文件夹名，`next`主题, `material`主题，下载解压后可能需要更改文件夹名字
3. 更换主题需要修改的是`blog`的配置文件`_config.yml`,vs code打开是可以搜索`theme`

```
theme: material
```

> blog 文件夹下的配置文件, #site 下可以改网站名称，作者，语言等信息



#### 部署到GitHub page

> 通常在本地用hexo g, hexo s做完调试，然后通过git提交到GitHub的`username.github.io`仓库来实现网站更新

1. 创建一个新的仓库（如果没有的话），注意仓库名格式必须为 `usrname.github.io` ，这个仓库将作为静态博客文件的存放仓库
2. 进入 `/home/Coder/Hexo/` 目录，将远程的仓库同步到本地

```
cd /home/shiyanlou/Code/Hexo/
git clone [你的仓库的 url]
```

3. 所谓的部署要做的事就是把 `public` 文件目录下的博客文件都复制到你的本地仓库中，并将本地仓库 `push` 到 github 仓库上

```
cp -R public/* [你的仓库名]

cd [你的仓库名]
git add .
git commit -m 'update blog'
git push
```

4. 可以用`hexo d`直接部署

```bash
$ npm install hexo-deployer-git --save
```

修改根目录配置。

```bash
deploy:
  type: git
  repo: io仓库地址
  branch: master
```

#### 绑定域名

在本地博客的 `source` 目录下（例如：`Hexo/blog/source`）创建文件 `CNAME` （这个文件名一定要大写！），使用 vim 或者 gedit 编辑。其中的内容为你的域名。比如你的域名为 `shiyanlou.com` ，那么 `CNAME` 中就填写这个。然后将这个 `CNAME` 文件 push 到 github 的主页仓库当中。

另一方面如果你使用的[阿里云](https://cn.aliyun.com/)购买的域名的话，可以登录阿里云进入控制台为域名添加解析。

记录值中填写你的 github 为你配置的域名，也就是你的 github 仓库名。然后就开始漫长的等待，等到阿里云将你的 DNS 解析规则广播到其他运行商的 DNS 服务器上之后我们才可以开始访问。

如果你选择在其它地方购买域名，可以使用 [DNSPOD](https://www.dnspod.cn/) 设置域名解析。

### Material-X主题

> 参考[Meterial X]( https://xaoxuu.com/wiki/material-x/theme-settings/index.html ) 

#### 根目录配置文件

1. 语言

```
language:- zh-CN- en- zh-HK- zh-TW
```

2. 网站基本信息

```
# 网站标题
title: my blog

# 网站图标
favicon: https://... .ico
# 作者头像，会出现在文章标题下方，不同于侧边栏的大头像
avatar: https:.. .png
```

#### 主题配置文件

1. 修改背景图片、修改头像: 贴七牛云连接即可
2. 修改主题文件内各个`page`文件夹的位置，和自己本地的文件夹目录匹配
3. 修改主题色：`\material\source\less\_color.less`修改
4. 控制侧边栏：主题配置文件`-wiget`关键字

