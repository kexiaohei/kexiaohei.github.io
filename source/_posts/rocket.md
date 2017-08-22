---
title: 回到顶部火箭特效
categories: "前端技术"
date: 2017-07-26 15:02:01
---
在页面右下角做一个火箭形状的按钮，只有当页面滚动条不在顶部时才显示，点击要有火箭发射的效果，同时页面滚动到顶部。

<!--more-->
难点就在于火箭特效，上网看了一个例子用css做的，代码多且复杂，效果也不是很完美，索性自己做了一个，动画主要使用CSS3动画去完成，代码简单易懂。   

### html部分代码  
```
    <div id="backTop" onclick="backToTop(this);"></div>
```

### css代码
使用了css3的animation属性，现在应兼容大部分浏览器，如遇不兼容，可自行搜索兼容写法    
```
		#backTop {
		    position: fixed;
		    bottom: 2rem;
		    right: 1rem;
		    display: none;
		    z-index: 99;
		    cursor: pointer;
		    border-radius: .2rem;
		    width: 8rem;
		    height: 15rem;
			/*常态 显示灰色火箭图片*/
		    background: url("../image/rocket/rocket_button_up_01.png") no-repeat 0 0;
		    background-size: contain;
		}
		
		#backTop:hover {
			/*当鼠标移动到火箭按钮上面时，显示亮色火箭图片*/
		    background-image: url("../image/rocket/rocket_button_up_02.png");
		}
		
		#backTop.launch {
		    animation: launch 1s ease-in-out;
		}
		
		@keyframes launch {
		    0% {
				/*火箭发射图片，带火焰1*/
		        background-image: url("../image/rocket/rocket_button_up_03.png");
		        bottom: 2rem;
		    }
		    15% {
				/*火箭发射图片，带火焰2*/
		        background-image: url("../image/rocket/rocket_button_up_04.png");
		        bottom: 2rem;
		    }
		    30% {
				/*火箭发射图片，带火焰3*/
		        background-image: url("../image/rocket/rocket_button_up_05.png");
		        bottom: 2rem;
		    }
		    45% {
				/*火箭发射图片，带火焰4*/
		        background-image: url("../image/rocket/rocket_button_up_06.png");
		        bottom: 2rem;
		    }
		    100% {
				/*火箭发射图片，带火焰4*/
		        background-image: url("../image/rocket/rocket_button_up_06.png");
		        bottom: 1200px;
		    }
		}
```

### js代码
```
		<script type="text/javascript" src="js/jquery-3.1.1.min.js"></script>
		<script type="text/javascript">
			$(document).ready(function () {
				var $container = $(window);
				var topH = 50; //顶部高度
				var $backTop = $("#backTop"); //滚动到顶部的按钮元素
				//监听滚动条，只有当滚动条高度大于设定的顶部高度时才显示按钮
				$container.scroll(function () {
				    var afterScrollTop = $container.scrollTop();
				    if (afterScrollTop >= topH) {
				        $backTop.show();//显示按钮
				    } else {
				        $backTop.hide();//隐藏按钮
				    }
				});
			});
	
			//点击了火箭按钮的回调，触发发射特效，页面滚动回顶部
			function backToTop(ele) {
			    $(ele).addClass("launch");//触发发射特效
			    setTimeout(function () {
			        $('html,body').animate({scrollTop: 0}, 300);
			        $(ele).removeClass("launch");//结束后取消发射特效
			    }, 800);
			}
		</script>
```
<a href="/meSite/rokets/index.html" target="_blank" style="color:red;">点我查看演示</a>
完成了，去试试吧，火箭图片下载地址：[http://pan.baidu.com/s/1qYuhnJ2](http://pan.baidu.com/s/1qYuhnJ2 "火箭图片下载地址")