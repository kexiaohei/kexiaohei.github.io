---
title: MarkdownPad自动生成带有侧边目录的文档
categories: "前端技术"
date: 2017-06-17 10:09:40
---
看了很多markdown生成侧边目录的方法，大多依赖复杂的环境，终于找到一个比较简单的方法。

<!--more-->
我一直使用的MarkdownPad这个Markdown语法编辑器，很实用。就基于这个编辑器来介绍吧。

### 在head里引入文件
打开MarkdownPad，点击 工具 》》选项 》》高级 HTML Head 编辑器 》》粘贴以下代码		   
```
	<!--ztree生成侧边目录-->
	<link rel="stylesheet" type="text/css" href="http://i5ting.github.io/git-quick-start/preview/style/zTreeStyle/zTreeStyle.css">
	<script type="text/javascript" src="http://i5ting.github.io/git-quick-start/preview/js/jquery-1.10.2.min.js"></script>
	<script type="text/javascript"
	        src="http://i5ting.github.io/git-quick-start/preview/js/jquery.ztree.all-3.5.min.js"></script>
	<script type="text/javascript" src="http://i5ting.github.io/git-quick-start/preview/js/jquery.ztree_toc.js"></script>
	<SCRIPT type="text/javascript">
	    $(document).ready(function () {
	        $('#tree').ztree_toc({
	            is_auto_number: true,
	            documment_selector: '.markdown-body',
	            ztreeStyle: {
	                width: '260px',
	                overflow: 'auto',
	                position: 'fixed',
	                'z-index': 2147483647,
	                border: '0px none',
	                left: '0px',
	                top: '0px'
	            }
	        });
	    });
	</SCRIPT>
```
### 编辑markdown文档
在空白的markdown文档中添加一下内容，在中间正常使用Markdown语法，编写内容即可。最后生成的Html会基于文章的标题（H1，H2，H3，H4，H5......）自动生成目录，且会自动生成编号，非常好用。	    
```
	<ul id="tree" class="ztree"></ul>
	<article class='markdown-body'>
	    写markdown内容
	</article>
```