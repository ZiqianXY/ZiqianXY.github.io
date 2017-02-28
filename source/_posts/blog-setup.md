---
title: 用Hexo搭建个人博客
date: 2015-12-15
type: "tags"
tags: [app, blog, dev, hexo, next]
categories: dev
---
  
本博客是由hexo驱动，使用hexo搭建静态博客，然后添加挂件丰富博客配置是以后总快捷简单的方法，让博主只需关注于记录文字本身，无需繁杂的技术细节。这里就介绍一下如何一步一步轻松搞定个人博客的搭建。

<!--more-->

## Hexo环境搭建

### node.js, git, hexo
node.js, git, hexo的傻瓜式安装，参考hexo官方文档即可
```
npm install hexo-cli -g
```

### public-key
git的public-key的配置，参考常见问题，具体步骤为`查看本地是否存在public-key`->`如果没有则生成pub`->`将已有或者生成的pub添加至git的.ssh文件夹下`->`添加至github并连接`

> [`**查看本地已有的SSH keys**`](https://help.github.com/articles/checking-for-existing-ssh-keys)

Before you generate an SSH key, you can check to see if you have any existing SSH keys. Enter `ls -al ~/.ssh` to see if existing SSH keys are present:
```
ls -al ~/.ssh
# Lists the files in your .ssh directory, if they exist
```
Check the directory listing to see if you already have a public SSH key.

- If you don't have an existing public and private key pair, or don't wish to use any that are available to connect to GitHub, then generate a new SSH key.

- If you see an existing public and private key pair listed (for example id_rsa.pub and id_rsa) that you would like to use to connect to GitHub, you can add your SSH key to the ssh-agent.

> [`**生成SSH key**`](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)

After you've checked for existing SSH keys, you can generate a new SSH key to use for authentication, then add it to the ssh-agent.

> `**添加SSH key到ssh-agent**`, If you have GitHub for Windows installed, you can use it to clone repositories and not deal with SSH keys. It also comes with the Git Bash tool, which is the preferred way of running git commands on Windows.

1. Ensure ssh-agent is enabled: **If you are using Git Bash**, turn on ssh-agent:
```
# start the ssh-agent in the background
eval "$(ssh-agent -s)"
Agent pid 59566
```
2. Add your SSH key to the ssh-agent. If you used an existing SSH key rather than generating a new SSH key, you'll need to replace id_rsa in the command with the name of your existing private key file.
```
ssh-add ~/.ssh/id_rsa	# id_rsa为对应.pub的本地key
```
3. Add the SSH key to your GitHub account.(next)

> [`**添加SSH key至GitHub账户**`](https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account)

To configure your GitHub account to use your new (or existing) SSH key, you'll also need to add it to your GitHub account.

> [`**测试SSH连接**`](https://help.github.com/articles/testing-your-ssh-connection)

After you've set up your SSH key and added it to your GitHub account, you can test your connection.
```
ssh -T git@github.com
# Attempts to ssh to GitHub
```


### 部署至github
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

### hexo设置
`主目录`下的_config.yml文件操作，参考hexo官方配置教程
 

## hexo主题配置

主题的安装，比较推荐的有jacman、next, 到hexo官方主题区或者github搜索即可，相应安装只需git clone到博客目录下themes文件夹下

hexo主题配置，同样的_config.yml文件操作，只不过位于`主题文件夹`下，具体参考相应主题文档



## hexo挂件及优化


## 其他资源

OK, here, I collect some useful hyperlinks for your building up a new static blog. Here we go: 

1. [Jekyll](https://jekyllrb.com/), the core engine to translate a .md file to static webPage.

2. [MarkDown](https://daringfireball.net/projects/markdown/), a `text-to-HTML` conversion tool for web writers. 

3. [GitHUb](https://github.com), a web server to locate the blog source files, so that you can easily get a self-website without purchase for anything, just directly go to `username.github.io`. 


