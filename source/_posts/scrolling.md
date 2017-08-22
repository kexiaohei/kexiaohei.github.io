---
title: 自定义滚动区域在ios上滑动卡顿问题
categories: "前端技术"
date: 2017-07-29 10:19:01
---

我们都知道有一个css属性叫做“overflow: auto;”，通过这个属性我们可以自定义滚动区域，当内容超出这个区域即出现滚动条。然而这个滚动区域过长时，在ios上滑动的时候会出现卡顿问题，滑动效果很差。


<!--more-->
 
解决这个问题很简单，添加一个css属性-webkit-overflow-scrolling即可解决，明显提升滑动效果。代码如下：
          
```
		.u-scroll {
		    overflow: auto;
		    -webkit-overflow-scrolling: touch;
		}    
```

有强迫症的的童鞋可以这样写：   
 
```
		.u-scroll {
		    overflow: auto !important;
		    -webkit-overflow-scrolling: touch !important;
		}    
```