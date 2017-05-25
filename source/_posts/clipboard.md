---
title: clipboard.js实现复制粘贴
categories: "前端技术"
date: 2017-05-25 09:34:09
---
最近要做一个功能："js自动选择文本并复制到剪切板",发现除了IE，其他浏览器都禁止了js对剪切板的直接操作。然而网上的点击按钮复制一段代码或文本是怎么做到的呢？仔细研究了下，发现是使用了flash技术去实现的，然而手机端浏览器对flash并不友好,所以并不适用于手机端。仅仅是复制文本不应该用太过复杂的方式去实现，这样得到的结果与付出的成本并不成正比，最后终于找到一个技术clipboard.js实现复制粘贴，无需Flash无需依赖任何JS库实现文本复制与剪切。

<!--more-->
复制文本到剪切板不再那么复杂，也不需要繁琐的配置或者加载臃肿的插件；最重要的，不再依赖Flash或者庞大的组件。  
这就是clipboard.js存在的意义。  
官方地址：[https://clipboardjs.com/](https://clipboardjs.com/ "clipboardjs官方网址")  
中文网：[http://clipboardjs.52fhy.com/](http://clipboardjs.52fhy.com/ "clipboardjs中文网")

### 引入clipboard

```	

	<script src="dist/clipboard.min.js"></script>
```

### Html部分
将要复制的元素，绑定到按钮上（按钮也可以替换成div）。

```	

	<span id="demo" oncopy="copySucceed(this)">要复制的内容</span>
	<button id="copyBtn" data-clipboard-action="copy" data-clipboard-target="#demo">点击复制</button>
```

1. 通过data-clipboard-action 属性来指定是 复制(copy) 还是 剪切(cut) 操作。    
注意：剪切(cut) 操作仅适用 `<input>` 或 `<textarea>` 元素，默认是 复制(copy)。
2. 使用 `data-clipboard-target` 属性指定被复制的内容

### js部分
绑定按钮，实例化Clipboard对象

```	

	new Clipboard('#copyBtn');
```

### 成功
这时点击按钮已经可以选中文本并复制了！