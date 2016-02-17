---
title: 利用Hexo在Github上建立个人Blog
date: 2016-02-16 16:09:26
tags:
---

[TOC]
## 描述
本文章主要在于介绍利用github这个平台，通过hexo这个工具进行免费博客的搭建工作。
涉及到的内容较为初浅，还未涉及到高级内容。
git的安装和具体操作命令不再次赘述。

## 创建过程
### Github注册
1. 访问：http://www.github.com/ 进行注册
2. 创建git 仓库。根据github page的介绍，如果是创建组织的站点，那么应该schema命名方式为：
    (username).github.io, 这里会创建一个repository 名称为chrishuihui.github.io
3. 添加SSH Key
    在本地创建一个SSH Key，  然后将创建的Key 添加到github中
```
ssh-keygen -t rsa -C "邮件地址@youremail.com"
```
通过以下命令进行测试：

```
ssh -T git@github.com
```

对于github的操作就可以了。

### 安装hexo
[hexo](https://hexo.io/zh-cn/docs/index.html) 依赖于NodeJS，所以先要安装NodeJS。
NodeJS安装很方便，直接访问https://nodejs.org/en/ 进行下载安装就可以了。
接下来就是安装hexo

``` bash
npm install -g hexo-cli
```
### hexo初体验
很简单，来自于 [Hexo 官网](https://hexo.io/zh-cn/docs/index.html)

``` bash
hexo init blog   #创建一个blog文件夹，并进行初始化，会创建hexo的基本文件
cd blog          
npm install
hexo server      #这个命令就会启动hexo服务
```

启动完成后，直接访问 http://localhost:4000就可以了

### hexo发布到github上
1. 第一步要做的事情是修改 _config.yml 
    修改url 为 http://(username).github.io
    并修改deploy元素：
``` bash
    deploy:
		  type: git
		  repository: https://github.com/chrishuihui/chrishuihui.github.io.git
		  branch: master
```

2. 执行hexo生成和发布命令

``` bash
hexo generate
hexo deploy
可以合并为
hexo d -g
```

3. 随后你就可以访问http://chrishuihui.github.io/查看内容了

### 关于hexo的主题
你可以在https://hexo.io/themes/ 上找寻你要的主题，我用的是[Maupassant](https://github.com/tufu9441/maupassant-hexo)
一般在主题的项目中都会有对主题使用的介绍。

## 关于hexo的使用
### 创建文章
你可以执行下列命令来创建一篇新文章。

``` bash
$ hexo new [layout] \[title\]
```
Hexo 有三种默认布局：post、page 和 draft

布局	路径
post	source/_posts
page	source
draft	source/_drafts
具体参考：https://hexo.io/zh-cn/docs/writing.html

### 删除文章
首先删除目录下的
db.json文件
然后hexo clean
接着hexo g -d


## 常见问题
1. 安装hexo时报错：

``` bash
{ [Error: Cannot find module './build/Release/DTraceProviderBindings'] code: 'MODULE_NOT_FOUND' }
{ [Error: Cannot find module './build/default/DTraceProviderBindings'] code: 'MODULE_NOT_FOUND' }
{ [Error: Cannot find module './build/Debug/DTraceProviderBindings'] code: 'MODULE_NOT_FOUND' }
```

   
   解决办法：

``` java
   $ npm install hexo --no-optional
```

P.S. 但是好像不起作用

2. hexo deploy error:

```
ERROR Deployer not found: git
```

解决办法：

```
安装 npm install hexo-deployer-git --save
将deploy 的 type由github改为git
```

3. Hexo 部署之后，github.io上一直404
    官网上有这样一句话
``` bash
    You must use the username.github.io naming scheme.
   Content from the master branch will be used to build and publish your GitHub Pages site.
```
原因就在于我创建了的repository为blog，不符合github page的规则。

   
#### 参考资料
[Hexo 官网](https://hexo.io/zh-cn/docs/index.html)
[Hexo maupassant主题](https://github.com/tufu9441/maupassant-hexo)
[零基础免费搭建个人博客-hexo+github](http://hifor.net/2015/07/01/%E9%9B%B6%E5%9F%BA%E7%A1%80%E5%85%8D%E8%B4%B9%E6%90%AD%E5%BB%BA%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2-hexo-github/)
[使用七牛为Hexo存储图片](http://blog.shiqichan.com/use-qiniu-store-image-for-hexo/)



