---
title: Hello World
date: 2017-04-15 08:34:14
---
Welcome to [Hexo](https://hexo.io/)! This is your very first post. Check [documentation](https://hexo.io/docs/) for more info. If you get any problems when using Hexo, you can find the answer in [troubleshooting](https://hexo.io/docs/troubleshooting.html) or you can ask me on [GitHub](https://github.com/hexojs/hexo/issues).

<!--more-->
## 关于hexo
### 官网
[https://hexo.io/zh-cn/](https://hexo.io/zh-cn/ "hexo官网")

### 主题
[https://hexo.io/themes/ ](https://hexo.io/themes/ "hexo官方主题库")

### 使用的主题
[Next](http://theme-next.iissnan.com/ "Next")

## hexo 代码块语法
hexo配置文件中配置代码识别选项后，可以识别代码块，自动美化并高亮显示代码语法，显示代码行号。（在移动端适配效果不是很好）
### 语法一:
使用如下格式来包裹代码，支持语法高亮和代码行号显示	

	{% codeblock %} 你的代码 {% endcodeblock %}
	

效果:

{% codeblock %}
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
{% endcodeblock %}

### 语法二:
使用三个反引号（英文键盘Esc下面的键）来包裹代码块。这种方式实现的效果与第一种方式相同。

### 语法三：
使用双空格缩进的方式，注意代码块之前要空一行，但这种方式在Hexo中不支持代码高亮和显示行号，你可以引入其他插件来实现高亮语法。

效果：

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