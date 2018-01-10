---
title: hexo安装和部署
categories: "前端技术"
date: 2018-01-10 16:02:01
---
因为要换电脑，重新整理了下hexo，顺便写一篇。
<!--more-->
### GitHub账号    
首先，你得有一个github账号，建立一个Repository。注意名字要叫做：账号名.github.io。建好后得到一个地址，这个就是上传本地文件/拉取线上文件的地址。    
### 安装git工具    
网上搜索git，下载安装即可。    
### 安装node    
网上搜索node，下载安装即可。    
### 通过cmd命令安装hexo     
	npm install hexo-cli -g

### 通过cmd命令建立本地博客    
    hexo init blog  //建立文件夹，blog为文件夹名称，可另取   
    cd blog  //进入文件夹
    npm install  //安装 
    hexo server  //运行    
在浏览器地址栏输入：localhost:4000 ，即可访问   
### 写文章
在blog\source\_posts文件夹下，新建md文件，打开并编辑文章（去网上搜索并下载安装一款markdown编辑器，比如MarkdownPad2）    
### 上传
打开blog文件夹下_config.yml文件，找到以下内容并修改     
    deploy:
      type: git
      repo: https://github.com/kexiaohei/kexiaohei.github.io.git
      branch: master
### 通过cmd命令安装部署工具      
    npm install hexo-deployer-git --save
### 通过cmd命令部署    
    hexo clean && hexo g && hexo d    
### 通过cmd命令部署 
访问地址：账号名.github.io。
### 建立git分支   
部署完成后，github已经上有了编译后的文件和代码。为了更换电脑时博客文件的迁移，我们还可以在当前git再建立一个分支，然后将本地整个blog文件夹的内容上传到分支上。这样，当更换电脑，迁移博客文件时，我们只需从git分支上拉取即可。注意修改本地文件时，不仅要通过cmd命令发布，也要通过git工具将修改内容上传到git分支。 
### 迁移到新电脑的操作
1. 确保安装好了git和node     
2. 将git上建立的分支拉取到本地     
3. win+R打开cmd命令安装hexo：`npm install hexo-cli -g`    
4. 通过cmd进入本地博客文件夹（git分支拉取到本地的文件夹），执行：`hexo s`    
5. 通过浏览器访问localhost:4000    
   
### 其他    
基本的建立已经完成了，还有其他主题下载，_config.yml文件的配置，域名的解析等可自行探究。


