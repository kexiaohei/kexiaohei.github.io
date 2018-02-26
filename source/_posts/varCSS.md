---
title: css变量的使用 
categories: "前端技术"  
date: 2018-02-23 14:10:01  
---
在任何语言中，变量的有一点作用都是一样的，那就是可以降低维护成本，附带还有更高性能，文件更高压缩率的好处。在css中我们也可以灵活的使用变量。

<!--more-->

### 语法
CSS中原生的变量定义语法是：`--*`，变量使用语法是：`var(--*)`，其中`*`表示变量名称。
   
### 命名规范
css变量命名稍显宽松，只要不包含`$`，`[`，`^`，`(`，`%`等字符，普通字符局限在只要是“数字[0-9]”“字母[a-z A-Z]”“下划线_”和“短横线-”这些组合，甚至可以是中文，日文或者韩文。

### CSS变量作用域
1. 变量也是跟着CSS选择器走的，如果变量所在的选择器和使用变量的元素没有交集，是没有效果的。如果想全局使用变量，可以设置在`:root`选择器上；    
2. 当存在多个同样名称的变量时候，变量的覆盖规则由CSS选择器的权重决定的，但并无`!important`这种用法，因为没有必要，`!important`设计初衷是干掉JS的`style`设置，但对于变量的定义则没有这样的需求。    
  
		/*在这里申明css全局变量*/
		:root {
			--x: green;
		}
		
		/*使用变量*/
		div {
			--x: red; /*内部，单独声明了变量*/
			color: var(--x); /*red*/
		}
		
		p {
			color: var(--x); /*green*/
		}
		
		a {
			color: var(--x); /*green*/
		}
		
### CSS变量的空格尾随特性
即在使用`var(--*)`，编译出来时，其后是默认尾随一个空格的。     
错误示例：            

	body {
		  --temp: 20;   
		  font-size: var(--temp)px;
		}      

相当于：        

	body {  
		  font-size: 20 px;
		} 
是错误的写法。正确示例如下：    
 
	body {
		  --temp: 20px;   
		  font-size: var(--temp);
		}  
或使用 CSS3 `calc()`计算：   
   
	body {
		--temp: 20;   
		font-size: calc(var(--temp) * 1px);
	} 

### CSS变量的相互传递特性
变量是可以赋值给变量的，就像`a=1,b=a,c=b` =》 `c=1`    

	body {
	  	--a: #4CAF50;   
	  	--b: var(--a);
		color: var(--b)
	}

### css变量使用的完整语法
格式：`var(自定义变量名, 默认值)`如果使用的变量没有定义，则使用后面的值作为元素的属性值。    
！注意：仅限于没有定义，即自定义变量名不存在时，才会启用后面的默认值；若自定义变量名，存在，对于CSS变量，只要语法是正确的，就算变量里面的值是个乱七八糟的东西，也是会作为正常的声明解析，并不会启用后面的默认值，而是使用该属性本身的默认值。   
下面一个问题可以解释css变量完整语法的用法：

	body {
	  --c: 20px;
	  background-color: red;
	  background-color: var(--c, green);
	}
此时<body>的背景色是（）？    

	A. transparent    B. 20px     C. red      D. green
`20px`这个变量值对于`background-color`属性来说，显然是不合法的。    
答案是…………………………`A. transparent`    
所以，为了不自找麻烦，请避免使用不合法的变量值。


附上原文链接：[http://www.zhangxinxu.com/wordpress/2016/11/css-css3-variables-var/](http://www.zhangxinxu.com/wordpress/2016/11/css-css3-variables-var/ "原文链接")