---
title: css变量的妙用（解决transform多属性变化问题，适用于其它复合属性） 
categories: "前端技术"  
date: 2018-04-11 14:10:01  
---
前面已经介绍了css变量的使用。近期发现一个问题正好用css变量来解决。那就是关于类似transform这种存在多个属性的复合属性样式，如何通过js动态的改变其中某个属性的值，而不影响其它属性的值的问题。

<!--more-->

### 问题难点
transform定义2D/3D转换，可以同时定义多个转换  
 
	<style>
		#test {
		        position: absolute;
		        left: 0;
		        right: 0;
		        top: 0;
		        bottom: 0;
		        margin: auto;
		        width: 50px;
		        height: 50px;
		        background-color: #0c60ee;
		        transform: scale(2) rotate(15deg) rotateX(20deg) rotateY(10deg) rotateZ(13deg);
		    }
	</style>

	<div id="test"></div>
如上，定义了一个小方块，进行了放大/缩小、2D旋转、以及沿着X、Y、Z轴的3D旋转的转换。当我们想通过js动态更改transform其中某个单一属性时，会发现js没有提供这种方法。按照正常的思路，我们只有获取整个transform属性值，然后改变其中我们想改变的值，然后再重新赋值给transform。然而只有当`style`是通过内嵌`<div style=""></div>`的方式写入的时候，我们才能通过`js`的`style`对象获取到`style`里面具体的值。否则我们只能通过`getComputedStyle() //非IE`或`currentStyle //IE`方法，去获得css最终渲染的值，这时我们得到的transform只能是`matrix //2D`或`matrix3d //3D`矩阵。这里介绍一个获取的方法。

	/**
     * 获取元素css最终渲染的值
     * @param element dom元素
     * @param attr 想要获取的属性名称
     * @returns {*}
     */
    function getFinStyle(element, attr) { //
        if (element.currentStyle) { //IE
            return element.currentStyle[attr];
        } else { //非IE
            return window.getComputedStyle(element, null)[attr];
        }
    }

	getFinStyle(document.getElementById("test"), "transform");
然并卵，确实有人写了将矩阵再转换回去的方法，但涉及到的计算、判断、正则等实在太麻烦，并且不能100%匹配。那么，接下来我们可以通过css变量巧妙的解决这个问题。
	
### 解决问题
闲话不多说，这里附上一个<a href="/meSite/multi-transform.html" target="_blank" style="color:red;">demo</a>，详看代码。     
#### css：
	
	#test {
            --scale: 1; /*定义缩放系数*/
            --rotate: 0deg; /*定义2D旋转角度*/
            --rotateX: 0deg; /*定义3D X轴旋转角度*/
            --rotateY: 0deg; /*定义3D Y轴旋转角度*/
            --rotateZ: 0deg; /*定义3D Z轴旋转角度*/
            position: absolute;
            left: 0;
            right: 0;
            top: 0;
            bottom: 0;
            margin: auto;
            width: 50px;
            height: 50px;
            background-color: #0c60ee;
            transform: scale(var(--scale)) rotate(var(--rotate)) rotateX(var(--rotateX)) rotateY(var(--rotateY)) rotateZ(var(--rotateZ));
        }
#### html：

	<input type="range" min="1" max="200" value="100" oninput="scale(this.value)">放大/缩小<br/>
	<input type="range" min="0" max="360" value="0" oninput="rotate(this.value)">2D旋转<br/>
	<input type="range" min="0" max="360" value="0" oninput="rotateX(this.value)">沿着X轴的3D旋转<br/>
	<input type="range" min="0" max="360" value="0" oninput="rotateY(this.value)">沿着Y轴的3D旋转<br/>
	<input type="range" min="0" max="360" value="0" oninput="rotateZ(this.value)">沿着Z轴的3D旋转<br/>
	
	<div id="test"></div>
#### js

	var obj = document.getElementById("test");

    function scale(d) { //改变缩放系数
        d = d / 100;
        obj.style.setProperty("--scale", d);
    }

    function rotate(d) { //改变2D旋转角度
        obj.style.setProperty("--rotate", d + "deg");
    }

    function rotateX(d) { //改变3D X轴旋转角度
        obj.style.setProperty("--rotateX", d + "deg");
    }

    function rotateY(d) { //改变3D Y轴旋转角度
        obj.style.setProperty("--rotateY", d + "deg");
    }

    function rotateZ(d) { //改变3D Z轴旋转角度
        obj.style.setProperty("--rotateZ", d + "deg");
    }
### 总结
ok，原理很简单，只要将每个属性要转换的系数用css变量去定义，当我们想要动态改变时，通过js去改变对应的css变量即可。     
有关于前端技术，其实很多技术并不十分困难，关键在于巧妙的运用。奇思妙想，总能让人有眼前一亮的感觉。