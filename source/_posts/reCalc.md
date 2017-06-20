---
title: 移动端实现UI设计稿的等比例适配
categories: "前端技术"
date: 2017-06-20 10:02:01
---
从美工那里拿到UI高保真图之后，前端需要根据这个图编写代码。然而图只是一张图，编写出来的代码却是要在不同设备里展现页面的。怎样让你编写的代码在不同设备里呈现的页面，始终和高保真图保持等比例呢？

<!--more-->
### viewport
首先，为了适配移动端设备，肯定要在head里加上viewport。   
   
```
	<meta name="viewport" content="width=device-width,minimum-scale=1.0,maximum-scale=1.0,user-scalable=no,initial-scale=1.0"/>
```

### 单位（px、em、rem）
其次，我们需要了解几个单位的区别
#### px
px像素（Pixel）。相对长度单位。像素px是相对于显示器屏幕分辨率而言的。    
特点：    
1. IE无法调整那些使用px作为单位的字体大小；    
2. 国外的大部分网站能够调整的原因在于其使用了em或rem作为字体单位；    
3. Firefox能够调整px和em，rem，但是96%以上的中国网民使用IE浏览器(或内核)。 

#### em
em是相对长度单位。相对于当前对象内文本的字体尺寸。如当前对行内文本的字体尺寸未被人为设置，则相对于浏览器的默认字体尺寸。    
特点:    
1. em的值并不是固定的；    
2. em会继承父级元素的字体大小。      

#### rem
rem是CSS3新增的一个相对单位（root em，根em），这个单位引起了广泛关注。这个单位与em有什么区别呢？区别在于使用rem为元素设定字体大小时，仍然是相对大小，但相对的只是HTML根元素。这个单位可谓集相对大小和绝对大小的优点于一身，通过它既可以做到只修改根元素就成比例地调整所有字体大小，又可以避免字体大小逐层复合的连锁反应。目前，除了IE8及更早版本外，所有浏览器均已支持rem。

### js动态计算根节点的font-size
了解了以上三个单位的区别，我们知道应该选择rem，这样只需要动态计算html根元素的大小，就可以改变整个文档内rem的大小，即可实现等比例的缩放。    
假设设计稿是宽750px来做的，书写css方便计算考虑，根节点的font-size假定为100px，得出设备宽为7.5rem。设计稿中标注的任何px数值都可以换算成px/100的rem值。
就是说，每一个设备的宽度都定为7.5个rem，然后宽度非750px的设备里，就需要用JS对font-size做动态计算。
换算关系为：根节点的font-size=设备宽度/7.5。代码如下：    
   
```
	<script>
		(function (doc, win) {
			var docEl = doc.documentElement,
					resizeEvt = 'orientationchange' in window ? 'orientationchange' : 'resize',
					reCalc = function () {
						var clientWidth = docEl.clientWidth;
						if (!clientWidth) return;
						docEl.style.fontSize = 100 * (clientWidth / 750) + 'px';
					};
			if (!doc.addEventListener) return;
			win.addEventListener(resizeEvt, reCalc, false);
			doc.addEventListener('DOMContentLoaded', reCalc, false);
		})(document, window);
	</script>
```
以上代码应在head内，所有css和js之前。