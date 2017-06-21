---
title: Hexo+GitHub搭建个人博客
date: 2017-06-20 14:56:28
tags: Hexo
---
本文使用Hexo + GitHub Pages建立个人博客。hexo是一款基于Node.js的静态博客框架，可以方便的生成静态网页托管在github上。
可以达到同样目的的还有jekyll,相比hexo而言，jekyll和github更加友好，我们按照jekyll格式写好提交后，github会自动生成静态页面。也就是说，只要交给github托管，本地不需要jekyll环境。但是如果不放在github上托管，环境安装就很麻烦，要安装ruby,python还有一大堆库。这里我们选择使用hexo进行博客搭建。

---
# Hexo环境
安装hexo相当简单，只需要安装 node.js 和 git


## 安装node
直接去官网下载[node.js](https://nodejs.org/en/)


## 安装git

下载Git在win下的安装包，下载地址：[Git-For-Windows](https://git-for-windows.github.io/)
上述官网下载地址可能被墙，下不到的朋友还还可以到这里下载:[Github](https://github.com/waylau/git-for-win)

## 安装hexo
``` bash
$ npm install -g hexo-cli
```

hexo 的环境现在就安装完成了
``` bash
hexo init  
hexo generate
hexo server 
```
可以 hexo s -p 5000 进行本地测试（默认端口4000），如果端口被占用输入ip后页面会一直没反应，需要更换端口。



``` bash
#一些常用命令
hexo new"postName" #新建文章
hexo new page"pageName" #新建页面
hexo generate #生成静态页面至public目录
hexo server #开启预览访问端口（默认端口4000，'ctrl + c'关闭server）
hexo deploy #将.deploy目录部署到GitHub
hexo help # 查看帮助
hexo version #查看Hexo的版本
```
---
# GitHub Pages
hexo生成的页面是在本地的，放在gitHub Pages 托管就可以在服务器上访问你的页面了。
参考 [GitHub Pages](https://pages.github.com/)


1、Create a repository,  settiing 里将项目设置为github pages
2、Clone the repository, 将项目克隆到本地
3、write a html page, 写个静态页 提交

``` bash
$ cd username.github.io
$ echo "hello world" > index.html
$ git add --all
$ git commit -m "first commit"
$ git push -u origin master
```

Fire up a browser and go to https://username.github.io
这样就可以看到你提交的页面了

---
# 整合
hexo里有两个_config.yml配置文件  ，一个在hexo目录下，一个在theme目录下， 前者是站点配置文件，后者是主题配置文件。
站点配置文件中修改deploy如下
``` bash
deploy:
  type: git
  repository: https://github.com/fanfanls/fanfanls.github.io.git
  branch: master     
```

修改后生成的页面就会直接发布到 https://username.github.io 
可以打开网页访问了

---
# 文章托管
现在已经基本实现博客搭建， 然而当你需要再换一台电脑写博客时就会有些犯难。Github上部署的只有生成的静态页，原始文章是在本地的， 怎么解决这个问题呢？ 我们可以使用分支来管理。 
``` bash
新建一个分支hexo
修改hexo分支为默认分支 
将你本地的hexo目录下文件拷贝一份至该分支
站点配置文件中deploy的分支确认为master
提交
```
这样，以后你更换电脑只需要将该分支拉下来写文章 发布一气呵成， 快动手试试吧。



# 问题
``` bash
Q:点击分类标签报404，怎么解决？
```
``` bash
A:终端执行 hexo new page "tags"，自动生成了页面source/index.md；
  修改页面，增加一行 type: "tags"；
  打开主题配置文件，menu 记录中确认  tags: tags 开启。
  重试。

  关于、分类界面同上。
  

```


关于主题优化可以看官网介绍，很详细 http://theme-next.iissnan.com/theme-settings.html










