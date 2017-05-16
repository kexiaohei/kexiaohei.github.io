---
title: 移动前端手机输入法自带emoji表情字符处理
categories: "前端技术"
date: 2017-05-16 18:00:14
---
遇到一个问题，移动端输入emoji表情无法存储到数据库。手机输入法里自带的emoji表情，应该是某些特殊字符，但是为什么会无法存储到数据库呢？是因为emoji用到的字符是4字节的utf-16（utf-16有2字节和4字节两种编码），而数据库一般是采用的utf-8，并且最大只允许3字节的字符。这样冲突就产生了，导致emoji表情无法存储到数据库。

<!--more-->
如何解决这个问题呢？首先需要对输入的字符进行检测，检测出表情字符，然后将其utf-16编码转换成实体编码，再存入数据库即可。详细原理可参考这篇博客[http://blog.csdn.net/binjly/article/details/47321043](http://blog.csdn.net/binjly/article/details/47321043 "原文链接")（感谢原作者，说的很详细），这里就不多说，直接贴代码。
### 检测并转换

```	
	
	/** 
	 * 用于把用utf16编码的字符转换成实体字符，以供后台存储 
	 * @param  {string} str 将要转换的字符串，其中含有utf16字符将被自动检出 
	 * @return {string} 转换后的字符串，utf16字符将被转换&#xxxx;形式的实体字符 
	 */  
	function utf16toEntities(str) {  
	    var patt=/[\ud800-\udbff][\udc00-\udfff]/g; // 检测utf16字符正则  
	    str = str.replace(patt, function(char){  
	            var H, L, code;  
	            if (char.length===2) {  
	                H = char.charCodeAt(0); // 取出高位  
	                L = char.charCodeAt(1); // 取出低位  
	                code = (H - 0xD800) * 0x400 + 0x10000 + L - 0xDC00; // 转换算法  
	                return "&#" + code + ";";  
	            } else {  
	                return char;  
	            }  
	        });  
	    return str;  
	} 
		function utf16toEntities(str) {  
		    var patt=/[\ud800-\udbff][\udc00-\udfff]/g; // 检测utf16字符正则  
		    str = str.replace(patt, function(char){  
		            var H, L, code;  
		            if (char.length===2) {  
		                H = char.charCodeAt(0); // 取出高位  
		                L = char.charCodeAt(1); // 取出低位  
		                code = (H - 0xD800) * 0x400 + 0x10000 + L - 0xDC00; // 转换算法  
		                return "&#" + code + ";";  
		            } else {  
		                return char;  
		            }  
		        });  
		    return str;  
		} 
```

ok！实际使用时，提交这个方法转换后的字符串即可。

```

	str = utf16toEntities(str);

```