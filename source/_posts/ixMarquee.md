---
title: 横向无缝滚动（跑马灯）
date: 2017-04-21 22:44:14
---
无缝滚动的代码很多，但我想要的一个滚动n条可以停顿一会再开始滚动，而且每条的长度都不一样，同时可以控制是否允许用户自己滑动。于是网上找了一个xMarquee.js然后加以修改，终于达到了我想要的效果。话不多说先贴上代码。

<!--more-->
### CSS部分

```	

	ul,li {
		margin:0;
		padding:0;
		list-style-type:none;
	}
	body {
		background-color:black;
	}
	.scrollleft {
		padding:5px 20px 0px 20px;
		margin:2px auto;
	}
	.scrollleft ul {
		width:100000%
	}
	.scrollleft li {
		float:left;
		display:inline;
		text-align:center;
		line-height:24px;
		color:#FFFFFF;
	}
	.scrollleft li a {
		margin-right:10px;
	}
	.scrollleft li:hover {
		color:red;
	}
```

### html部分

```

	<div class="scrollleft">
	    <ul>
	        <li><a>00000000000</a></li>
	        <li><a>111111111111111</a></li>
	        <li><a>22222222222222222</a></li>
	        <li><a>333333333333333333333</a></li>
	        <li><a>444444444444444</a></li>
	        <li><a>5555555555555555</a></li>
	        <li><a>66666666666666666666</a></li>
	        <li><a>777777777777777</a></li>
	        <li><a>888888888888</a></li>
	        <li><a>99999999999999999</a></li>
	        <li><a>aaaaaaaaaaaa</a></li>
	    </ul>
	</div>
```

### html部分

```

	/**
	 * jquery ixMarquee
	 * 依赖于jquery.js
	 */
	(function($) {
	    $.fn.ixMarquee = function(options) {
	        var del = {
	            temp: -2, //滚动的长度，正整数的时候是向右滚动，负整数的时候是向左滚动（-2/2）
	            speed: 50, //滚动的频率，单位为毫秒,数字越大速度越慢
	            num: 2, //每滚动2条停顿一次
	            delay: 5000, //一次停顿5000毫秒
	            onSlide: false, //是否可以手动滑动，true-是
	            backMarquee: function(id, content) {} //每滑动完一条的回调函数 @param id-li的索引 content-li的html
	        }
	
	        var options = $.extend(del, options);
	        var xM = $(this);
	        var backMarquee = del.backMarquee;
	
	        xM.each(function() {
	            var fontW = 0;
	            var t, o;
	            var $root = $(this);
	            var self = $(this).find("ul:first");
	            var fli = self.find("li:first");
	            var fla = self.find("li:last");
	            var temp = parseInt(del.temp);
	            var speed = parseInt(del.speed);
	            var start = 0;
	            for (var i = 0; i < self.find("li").length; i++) {
	                self.find("li").eq(i).data("index", i);
	                fontW += self.find("li").eq(i).width();
	            }
	            if (fontW < $(this).width()) {
	                return;
	            } //判断如文字的长度小于显示框的长度，则不执行marquee
	            if (temp > 0) {
	                self.css({
	                    marginLeft: -self.find("li:last").width()
	                });
	                self.find("li:last").prependTo(self);
	                start = -self.find("li:first").width();
	            }
	
	            function marquee() {
	                $root.css('overflow', 'hidden');
	                var idex, num = del.num;
	                if (temp < 0) {
	                    if (-start > fli.width()) {
	                        start = 0;
	                        fli.appendTo(self);
	                        idex = self.find("li:first").data("index");
	                        backMarquee(idex, self.find("li:first").html());
	                    }
	                } else {
	                    if (start > 0) {
	                        self.find("li:last").prependTo(self);
	                        start = -self.find("li:first").width();
	                        idex = self.find("li").eq(1).data("index");
	                        backMarquee(idex, self.find("li").eq(1).html());
	                    }
	                }
	                fli = self.find("li:first");
	                self.css({
	                    marginLeft: start
	                });
	                start = start + temp;
	                if (idex % num == 0) {
	                    reStart();
	                } //停顿处
	            }
	            t = setInterval(function() {
	                marquee()
	            }, speed);
	            $root.hover(function() {
	                if (o) {
	                    clearTimeout(o);
	                    o = false;
	                }
	                if (t) {
	                    clearInterval(t);
	                    t = false;
	                }
	                if (del.onSlide) {
	                    $root.css('overflow', 'auto')
	                }
	            }, function() {
	                t = setInterval(function() {
	                    marquee()
	                }, speed);
	            });
	
	            function reStart() { //停顿
	                clearInterval(t);
	                o = setTimeout(function() {
	                    t = setInterval(function() {
	                        marquee()
	                    }, speed);
	                }, del.delay)
	            }
	        })
	    }
	})(jQuery);
	
	/*初始化*/
	$(function() {
	    $(".scrollleft").ixMarquee({
	        backMarquee: function(id, con) {
	            console.log(id + '**' + con);
	        }
	    });
	});
```

### 注意
1. 记得先引入jquery;
2. ul 宽度要设为10000%，要尽可能的大，是为了让所有的li都在一行，而不会排到下一行；
3. 不要给li加左右padding或者margin，否则一个li滑动到下一个li之间会很僵硬，这是宽度计算的问题。如果要使li之间有间隙，给其内部元素添加左右padding或者margin即可。

