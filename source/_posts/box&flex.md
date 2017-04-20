---
title: box & flex
date: 2017-04-19 18:34:14
---
整理了一下，关于弹性盒子或者叫流布局，box & flex的兼容写法。前者是2009年的语法，已经过时；后者是2012年的语法，也是现在的标准语法。但实际情况下两者有明显的差别，在实际的浏览器测试中，flex并不能完全替代box。在开发过程中遇到很多兼容性方面的坑，因此分别整理了一下两者的兼容写法。以后可能还会有更多的坑，遇到再补充。

<!--more-->
### display：box

```	
	.ub {
	    display: -webkit-box;
	    display: -moz-box;
	    display: -ms-flexbox;
	    display: -o-box;
	    display: box;
	    position: relative;
	}
	
	.ub-ver {
	    -webkit-box-orient: vertical;
	    -moz-box-orient: vertical;
	    -ms-flex-direction: column;
	    -o-box-orient: vertical;
	    box-orient: vertical;
	}
	
	.ub-ac {
	    -webkit-box-align: center;
	    -moz-box-align: center;
	    -ms-flex-align: center;
	    -o-box-align: center;
	    box-align: center;
	}
	
	.ub-ae {
	    -webkit-box-align: end;
	    -moz-box-align: end;
	    -ms-flex-align: end;
	    -o-box-align: end;
	    box-align: end;
	}
	
	.ub-pc {
	    -webkit-box-pack: center;
	    -moz-box-pack: center;
	    -ms-flex-pack: center;
	    -o-box-pack: center;
	    box-pack: center;
	}
	
	.ub-pe {
	    -webkit-box-pack: end;
	    -moz-box-pack: end;
	    -ms-flex-pack: end;
	    -o-box-pack: end;
	    box-pack: end;
	}
	
	.ub-f {
	    position: relative;
	    -webkit-box-flex: 1;
	    -moz-box-flex: 1;
	    -ms-flex: 1;
	    -o-box-flex: 1;
	    box-flex: 1;
	}	
```

### display：flex

```
	.uf {
	    display: -webkit-box;
	    display: -webkit-flex;
	    display: -ms-flexbox;
	    display: flex;
	    position: relative;
	}
	
	.uf-ver {
	    -webkit-box-orient: vertical;
	    -webkit-flex-direction: column;
	    -ms-flex-direction: column;
	    flex-direction: column;
	}
	
	.uf-ac {
	    -webkit-box-align: center;
	    -webkit-align-items: center;
	    -ms-flex-align: center;
	    align-items: center;
	}
	
	.uf-ae {
	    -webkit-box-align: end;
	    -webkit-align-items: flex-end;
	    -ms-flex-align: end;
	    align-items: flex-end;
	}
	
	.uf-pc {
	    -webkit-box-pack: center;
	    -webkit-justify-content: center;
	    -ms-flex-pack: center;
	    justify-content: center;
	}
	
	.uf-pe {
	    -webkit-box-pack: end;
	    -webkit-justify-content: flex-end;
	    -ms-flex-pack: end;
	    justify-content: flex-end;
	}
	
	.uf-pj {
	    -webkit-box-pack: justify;
	    -webkit-justify-content: space-between;
	    -ms-flex-pack: justify;
	    justify-content: space-between;
	}
	
	.uf-pja {
	    -webkit-box-pack: justify;
	    -webkit-justify-content: space-around;
	    -ms-flex-pack: justify;
	    justify-content: space-around;
	}
	
	.uf-f {
	    -webkit-box-flex: 1;
	    -webkit-flex: 1;
	    -ms-flex: 1;
	    flex: 1;
	}
```