---
title: 建博相关
---
因为之前服务器快到期了，所以决定换个方式建博客，顺便把博客弄好看点。之前用Hexo建博客看中它是java编写的，想着用熟悉的语言可能会做点二次开发什么的，结果一年了也没做过啥，所以这次就打算找主题多的，不管啥语言，反正都是几条命令能部署。    
最后发现Hexo+github竟然能直接免费搭建博客，真的够方便的。

### 安装nodejs和安装hexo

``` bash
先到nodejs下载node安装，然后安装hexo
$ npm install -g hexo
```
### 初始化Hexo

``` bash
$ hexo init
```
### 安装插件和依赖

``` bash
$ npm install hexo-deployer-git --save
$ npm install --save hexo-renderer-jade hexo-generator-feed hexo-generator-sitemap hexo-browsersync hexo-generator-archive
```
### 获取butterfly主题

``` bash
$ git clone -b master https://github.com/jerryc127/hexo-theme-butterfly.git themes/butterfly
```

### 创建新的博客

``` bash
$ hexo new "我的博客日志" || hexo n "我的博客日志"
```

### 启动服务

``` bash
$ hexo server || hexo s
```

### 编译生成静态文件

``` bash
$ hexo generate || hexo g
```

### 部署到github

``` bash
$ hexo deploy
```

博客地址：https://shiryoushitsu.github.io