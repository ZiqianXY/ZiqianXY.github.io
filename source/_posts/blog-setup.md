---
title: 用Hexo搭建个人博客
date: 2015-12-15
tags: [app, blog, dev, hexo, next]
categories: [dev, blog]
---


本博客是由hexo驱动，使用hexo搭建静态博客，然后添加挂件丰富博客配置是一种快捷简单的方法，让博主只需关注于记录文字本身，无需繁杂的技术细节。这里就介绍一下如何一步一步轻松搞定个人博客的搭建。搭建过程中参考的一系列资料会附在文末，方便问题溯源。

<!--more-->

<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=0 height=0 src="//music.163.com/outchain/player?type=2&id=459148032&auto=1&height=32"></iframe>

---
# 博客基础搭建

## Hexo环境搭建

- node.js，git安装。傻瓜式安装，参考hexo官方文档即可

- hexo安装。安装完以上依赖之后，使用npm安装hexo，一行命令搞定

```
npm install hexo-cli -g
```

## git使用和配置
- 关于git的具体使用方法，参考[廖雪峰的git指南](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)
- 常见问题解决参考[github官方指南](https://help.github.com/)

以下附上git的public-key的配置，参考常见问题。具体步骤为`查看本地是否存在public-key`->`如果没有则生成pub`->`将已有或者生成的pub添加至git的.ssh文件夹下`->`添加至github并连接`

- 查看本地[已有SSH keys](https://help.github.com/articles/checking-for-existing-ssh-keys)
- 如果没有，则[生成SSH key， 并添加SSH key到本地ssh-agent](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)
- [添加SSH key至GitHub账户](https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account)
- [测试SSH连接](https://help.github.com/articles/testing-your-ssh-connection)

## Hexo基本指令
```
hexo g	# 生成博客内容，位于public文件夹下
hexo s	# 开启本地测试服务
hexo d	# 部署至配置服务器
hexo clean	# 清除所有配置及本地生成的public文件
```
至此，一个基本博客框架已搭建完毕，可在本地运行

## 部署至github
Hexo 提供了快速方便的一键部署功能，
```
hexo d	# hexo deploy
```
不过需要首先安装 `hexo-deployer-git`，
```
npm install hexo-deployer-git --save
```
然后修改配置。
```
deploy:
  type: git
  message: notes-to-commit
  repo: git@github.com:username/username.github.io.git
  branch: master
```


---
# 挂件配置及优化

## 基本配置
`站点配置文件`，即`root`下的`_config.yml`文件，参考[hexo官方配置教程](https://hexo.io/zh-cn/docs/configuration.html)

```
# Hexo Configuration
## Docs: https://hexo.io/docs/configuration.html
## Source: https://github.com/hexojs/hexo/

# Site
title: Hexo            # 网站标题
subtitle:              # 网站副标题
description:           # 网站描述
author: 		       # 昵称
language:              # 语言(简体中文:zh-Hans)
timezone:              # 时区，默认使用电脑时区，不用改

# URL
## If your site is put in a subdirectory, set url as 'http://yoursite.com/child' and root as '/child/'
url: http://yoursite.com  # 站点网址
root: /                   # 网站根目录
permalink: :year/:month/:day/:title/ #文单的永久链接格式
permalink_defaults:       # 永久链接中各部分的默认值


# Directory
source_dir: source
public_dir: public
tag_dir: tags
archive_dir: archives
category_dir: categories
code_dir: downloads/code
i18n_dir: :lang
skip_render:

# Writing
new_post_name: :title.md # File name of new posts
default_layout: post
auto_spacing: true
titlecase: false # Transform title into titlecase
external_link: true # Open external links in new tab
filename_case: 0
render_drafts: false
post_asset_folder: true
relative_link: false
future: false
highlight:
  enable: true
  line_number: true
  auto_detect: true
  tab_replace:

# Category & Tag
default_category: uncategorized
category_map: 
tag_map: 

# Date / Time format
## Hexo uses Moment.js to parse and display date
## You can customize the date format as defined in
## http://momentjs.com/docs/#/displaying/format/
date_format: YYYY-MM-DD
time_format: HH:mm:ss

# Pagination
## Set per_page to 0 to disable pagination
per_page: 10
pagination_dir: page

# Extensions
## Plugins: https://hexo.io/plugins/
## Themes: https://hexo.io/themes/
theme: landscape

# Deployment
## Docs: https://hexo.io/docs/deployment.html
deploy:
  type: git
  message: git commit message
  repo: git@github.com:`yourname`/`yourname`.github.io.git
  branch: master
```

## 主题
主题的安装，比较推荐的有jacman、next, 到hexo官方主题区或者github搜索即可，相应安装只需git clone到博客目录下themes文件夹下。hexo主题配置，同样的`_config.yml`文件操作，只不过位于`主题文件夹`下，具体参考相应主题文档。（附第三方参考文档：[Hexo博客搭建全攻略：NexT主题配置](http://www.jianshu.com/p/d95cff938277)）

```
cd your-hexo-site
git clone https://github.com/iissnan/hexo-theme-next themes/next
```


## 侧栏

```
sidebar:
  # Sidebar Position, available value: left | right
  position: right

  # Sidebar Display, available value:
  #  - post    expand on posts automatically. Default.
  #  - always  expand for all pages automatically
  #  - hide    expand only when click on the sidebar toggle icon.
  #  - remove  Totally remove sidebar including sidebar toggler.
  display: post

```

### menu

```
menu:
  home: /
  archives: /archives
  about: /about			#需要自行新建页面，见下文
  categories: /categories	#需要自行新建页面，见下文
  tags: /tags			#需要自行新建页面，见下文
  #commonweal: /404.html
```

### 圆形头像

将以下代码覆盖主题目录下 `source/css/_common/components/sidebar/sidebar-author.styl `

```
.site-author-image {
  display: block;
  margin: 0 auto;
  padding: $site-author-image-padding;
  max-width: $site-author-image-width;
  height: $site-author-image-height;
  border: $site-author-image-border-width solid $site-author-image-border-color;

  /* 头像圆形 */
  border-radius: 80px;
  -webkit-border-radius: 80px;
  -moz-border-radius: 80px;
  box-shadow: inset 0 -1px 0 #333sf;
}


.site-author-name {
  margin: $site-author-name-margin;
  text-align: $site-author-name-align;
  color: $site-author-name-color;
  font-weight: $site-author-name-weight;
}

.site-description {
  margin-top: $site-description-margin-top;
  text-align: $site-description-align;
  font-size: $site-description-font-size;
  color: $site-description-color;
}
```

### toc
```
toc:
  # Table Of Contents in the Sidebar
  enable: true
  
  # Automatically add list number to toc.
  number: true
```

### rss
自动生成订阅页



## 导航栏
导航栏是网站提供的主要功能索引，主要包含以下几项

### tags
标签页默认未自动生成，需要新建
- 新建页面

```
hexo new page tags	
```
- 修改站点目录下 source/tags 的 index.md 文如下：

```
---
title: categories
type: "categories"
comments: false
---
```

### categories
默认未自动生成，新建如tags

### about
默认未自动生成，新建如tags

### search
建议直接使用 `Local Search `, 它是 Hexo 的一个插件服务，避免了三方平台的注册配置过程。

- 安装 hexo-generator-searchdb，在站点的根目录下执行以下命令：
```
npm install hexo-generator-searchdb --save
```
- 在`站点配置文件`添加以下内容，重启服务即可看到
```
search:
 path: search.xml
 field: post
 format: html
 limit: 10000
```

## 底栏

### 评论
此处采用duoshuo
```
duoshuo_shortname: your-duoshuo-shortname
```

### 分享
此处采用duoshuo
```
duoshuo_share: true
```

# 写作

## [front-matter](https://hexo.io/docs/front-matter.html)
其中tags不分先后，categories分先后级关系，示例：
```
---
title: build blog
date: 2015-12-15
type: "tags"
tags: [app, blog, dev, hexo, next]
categories: [dev, blog]
---
```

## [资源文件夹](https://hexo.io/zh-cn/docs/asset-folders.html#%E6%96%87%E7%AB%A0%E8%B5%84%E6%BA%90%E6%96%87%E4%BB%B6%E5%A4%B9)

此功能默认是关闭的，可以通过`站点配置文件_config.yml`打开。
```
post_asset_folder: true
```
开启功能后，Hexo会在每次执行 hexo new [layout] <title> 命令时自动创建一个与之对应的文件夹，此文件夹拥有与对应的md文件名一样的名字，所有与文章对应用的资源都可以放在此文件夹中。

**为此，必须在`站点配置文件_config.yml`将`permalink`的最后设置成文件夹形式，即以斜杠/结尾。**
```
permalink: art/:year-:month/:title/
```

Hexo 专门引入了特定标签来解决，语法如下：
```
{% asset_path slug %}
{% asset_img slug [title] %}
{% asset_link slug [title] %}
```

举列来说，资源文件夹中example.jpg的正确引用方式如下：
```
{% asset_img example.jpg This is an example image %}
```



---
# 参考链接
OK, here, I collect some useful hyperlinks for your building up a new static blog. Here we go: 

- [Hexo](https://hexo.io/zh-cn)
- [MarkDown](https://daringfireball.net/projects/markdown/), a `text-to-HTML` conversion tool for web writers. 
- [GitHUb](https://github.com), a web server to locate the blog source files, so that you can easily get a self-website without purchase for anything, just directly go to `username.github.io`. 


---
# 更新记录
- 2016-03-01，添加`搜索`，`资源文件夹`
- 2015-12-15，新建
