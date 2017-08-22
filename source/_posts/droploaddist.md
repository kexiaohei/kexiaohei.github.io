---
title: 上下拉刷新插件（依赖于jquery或zepto）
categories: "前端技术"
date: 2017-07-29 09:00:01
---

介绍一个html5移动端上下拉刷新插件，依赖于jquery或者zepto。


<!--more-->
 
最近比较懒，就不详细介绍了，大家可以自行百度droploaddist，也可以下载源码和案例。    
传送门：   
[原作者：http://ons.me/526.html](http://ons.me/526.html "原作者")   
[源码和demo：https://github.com/ximan/dropload](https://github.com/ximan/dropload "源码和demo")    

下面是简单代码示例：   
引入文件(依赖库zepto或jquery两者选一)     
```
	<link rel="stylesheet" type="text/css" href="droploaddist/dropload.css">
	<script type="text/javascript" src="js/zepto.min.js"></script>
	<script type="text/javascript" src="droploaddist/dropload.min.js"></script>     
```

html部分    
```
	<div id="listDiv">
		<div class="li">新闻</div>
		<div class="li">新闻</div>
		<div class="li">新闻</div>
		<div class="li">新闻</div>
	</div>
```

js部分    
```
	 	//上下拉刷新的区域
        var $scrollArea = $(window);
        var $dropDiv = $('#listDiv');
        $dropDiv.dropload({
            scrollArea: $scrollArea,//滚动条滑动的区域
            threshold: 50,
            loadUpFn: function (me) {
                //刷新整个页面
                window.location.reload();
                setTimeout(function () {
                    me.resetload();
                }, 500);
            },
            loadDownFn: function (me) {
                var $last = $dropDiv.find(".li").last();//最后一条元素
                var lastId = $last.data("id");//最后一条元素的data-id
                if (!lastId) {
                    //如果不存在last_id
                    me.lock();// 锁定
                    me.noData();// 无数据
                    me.resetload();// 重置页面刷新状态
                    return;
                }
                var url = "";
                $.ajax({
                    type: "post",
                    url: url,
                    data: {
                        last: lastId
                    },
                    dataType: "json",
                    success: function (ret) {
                        var listHtml = ret;//返回的html列表
                        if (listHtml && listHtml.length) {
                            //一定时间显示加载效果
                            setTimeout(function () {
                                // 在页面最后一条之后插入新的html数据
                                $last.after(listHtml);
                                // 每次数据插入，必须重置
                                me.resetload();
                            }, 300);
                        } else {
                            me.lock();// 锁定
                            me.noData();// 无数据
                            me.resetload();// 重置页面刷新状态
                        }
                    },
                    error: function (xhr, type) {
                        me.lock();// 锁定
                        me.Err();// 出错了
                        me.resetload();// 即使加载出错，也得重置
                    }
                });
            }
        });
```

需要说明一下的是，.Err()方法是我修改源码添加的一个方法，源码里并没有，效果就是底部出现“出错了(；′⌒`)！”。和.noData()方法是一个原理，有这个需求的同学模仿源码里.noData()方法来添加一个新的方法即可。