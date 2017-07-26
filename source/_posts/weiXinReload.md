---
title: 微信reload问题
categories: "前端技术"
date: 2017-06-30 10:02:01
---
页面上有一个按钮，点击的时候执行window.location.reload()，正常情况reload()后会刷新当前页面地址，但在安卓的微信浏览器中reload后，通过fiddler抓包发现，并没有发送请求。应该是微信缓存的问题。

<!--more-->
解决方法就是给url后添加一个随机数变量，常用的是添加一个时间戳变量。    

### 给url添加时间戳变量  
```
    function updateUrl() {
        var url = window.location.href;
        var key = 'refreshTimestamp=';  //默认是"t"
        var reg = new RegExp(key + '\\d+');  //正则：t=1472286066028
        var timestamp = +new Date();
        if (url.indexOf(key) > -1) {
            //有时间戳，直接更新
            return url.replace(reg, key + timestamp);
        } else {
            //没有时间戳，加上时间戳
            if (url.indexOf('\?') > -1) {
                var urlArr = url.split('\?');
                if (urlArr[1]) {
                    return urlArr[0] + '?' + key + timestamp + '&' + urlArr[1];
                } else {
                    return urlArr[0] + '?' + key + timestamp;
                }
            } else {
                if (url.indexOf('#') > -1) {
                    return url.split('#')[0] + '?' + key + timestamp + location.hash;
                } else {
                    return url + '?' + key + timestamp;
                }
            }
        }
    }
```

### 刷新
```
		//window.location.reload();
        window.location.href = updateUrl();
```