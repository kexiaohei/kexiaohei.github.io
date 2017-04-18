---
title: 让你的代码块语法高亮
date: 2017-04-15 09:32:14
---

写技术文档会遇到的问题：如何在一个普通的html里写代码块，并且快速高效地美化代码呢？这里介绍一个highlight插件，可以快速高效地美化你的代码块，自动识别并高亮显示代码语法，完美适配移动端。

<!--more-->

### 在head中添加

	<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/highlight.js/9.10.0/styles/docco.min.css">
	<script src="https://cdnjs.cloudflare.com/ajax/libs/highlight.js/9.10.0/highlight.min.js"></script>
	<script>hljs.initHighlightingOnLoad();</script>

### OK！代码块这样写： 

	<pre>
		<code>
		//...你的代码
		</code>
	</pre>

### 看看效果

	var test = {
        name : function () {
            return 'hello';
        },
        age : function () {
            return 13;
        }
    };
    var name = "张三";
    function printStr(str){
        console.log(str);
    }
    printStr(name);

### 显示行号

	    <style>/*行号样式可以根据情境自己调整*/
	        pre {
	            position: relative;
	            overflow: hidden;
	        }
	
	        code.has-numbering {
	            margin-left: 21px;
	        }
	
	        .pre-numbering {
	            position: absolute;
	            top: 0;
	            left: 0;
	            width: 20px;
	            padding: 7px 0;
				margin: 0;
	            border-right: 1px solid #C3CCD0;
	            border-radius: 3px 0 0 3px;
	            text-align: center;
	            font-family: Menlo, monospace;
	            color: #AAA;
	        }
	    </style>
	<script src="https://cdn.bootcss.com/jquery/3.2.1/jquery.js"></script>
	<script>/*行号显示 依赖jquery*/
	    $(function(){
	        $('pre code').each(function(){
	            var lines = $(this).text().split('\n').length - 1;
	            var $numbering = $('<ul/>').addClass('pre-numbering');
	            $(this)
	                    .addClass('has-numbering')
	                    .parent()
	                    .append($numbering);
	            for(i=1;i<=lines;i++){
	                $numbering.append($('<li/>').text(i));
	            }
	        });
	    });
	</script>


### 主题可以更换，更换不同的css样式表，以展示不同效果

	<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/highlight.js/9.10.0/styles/agate.min.css">

	["agate.css", "androidstudio.css", "arduino-light.css", "arta.css", "ascetic.css", "atelier-cave-dark.css", "atelier-cave-light.css", "atelier-dune-dark.css", "atelier-dune-light.css", "atelier-estuary-dark.css", "atelier-estuary-light.css", "atelier-forest-dark.css", "atelier-forest-light.css", "atelier-heath-dark.css", "atelier-heath-light.css", "atelier-lakeside-dark.css", "atelier-lakeside-light.css", "atelier-plateau-dark.css", "atelier-plateau-light.css", "atelier-savanna-dark.css", "atelier-savanna-light.css", "atelier-seaside-dark.css", "atelier-seaside-light.css", "atelier-sulphurpool-dark.css", "atelier-sulphurpool-light.css", "brown-paper.css", "codepen-embed.css", "color-brewer.css", "dark.css", "darkula.css", "default.css", "docco.css", "dracula.css", "far.css", "foundation.css", "github.css", "github-gist.css", "googlecode.css", "grayscale.css", "gruvbox-dark.css", "gruvbox-light.css", "hopscotch.css", "hybrid.css", "idea.css", "ir-black.css", "kimbie.dark.css", "kimbie.light.css", "magula.css", "mono-blue.css", "monokai.css", "monokai-sublime.css", "obsidian.css", "paraiso-dark.css", "paraiso-light.css", "pojoaque.css", "purebasic.css", "qtcreator_dark.css", "qtcreator_light.css", "railscasts.css", "rainbow.css", "school-book.css", "solarized-dark.css", "solarized-light.css", "sunburst.css", "tomorrow.css", "tomorrow-night.css", "tomorrow-night-blue.css", "tomorrow-night-bright.css", "tomorrow-night-eighties.css", "vs.css", "xcode.css", "xt256.css", "zenburn.css"];

去试试吧。

<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/highlight.js/9.10.0/styles/docco.min.css">
<script src="https://cdnjs.cloudflare.com/ajax/libs/highlight.js/9.10.0/highlight.min.js"></script>
<script>hljs.initHighlightingOnLoad();</script>
    <style>/*行号样式可以根据情境自己调整*/
        pre {
            position: relative;
            overflow: hidden;
        }

        code.has-numbering {
            margin-left: 21px;
        }

        .pre-numbering {
            position: absolute;
            top: 0;
            left: 0;
            width: 20px;
            padding: 7px 0;
			margin: 0;
            border-right: 1px solid #C3CCD0;
            border-radius: 3px 0 0 3px;
            text-align: center;
            font-family: Menlo, monospace;
            color: #AAA;
        }
    </style>
<script src="https://cdn.bootcss.com/jquery/3.2.1/jquery.js"></script>
<script>/*行号显示 依赖jquery*/
    $(function(){
        $('pre code').each(function(){
            var lines = $(this).text().split('\n').length - 1;
            var $numbering = $('<ul/>').addClass('pre-numbering');
            $(this)
                    .addClass('has-numbering')
                    .parent()
                    .append($numbering);
            for(i=1;i<=lines;i++){
                $numbering.append($('<li/>').text(i));
            }
        });
    });
</script>