title: Hexo，添加返回顶部按钮
date: 2015-08-31 16:03:15
categories:
- hexo学习 
tags:
- Hexo 
- node.js
---
  其实，在hexo中实现这个功能不复杂，结合网上的教程，对相应的模块进行修改就可以了。现给出自己修改的过程...
<!--more-->
## 添加html代码。
打开文件夹/themes/Yilia/layout/_partial在此文件夹下，新建文件totop.ejs，并向其中加入如下代码：
``` bash
<div id="totop" style="position:fixed;bottom:150px;right:50px;cursor: pointer;z-index: 99999;">
<a title="返回顶部"><img src="/img/scrollup.png"/></a>
</div>
```
## 添加js代码。
打开文件夹/themes/Yilia/source/js，新建文件totop.js，将如下代码复制其中：
``` bash
(function($) {
	// When to show the scroll link
	// higher number = scroll link appears further down the page
	var upperLimit = 1000;

	// Our scroll link element
	var scrollElem = $('#totop');

	// Scroll to top speed
	var scrollSpeed = 500;

	// Show and hide the scroll to top link based on scroll position
	scrollElem.hide();
	$(window).scroll(function () {
		var scrollTop = $(document).scrollTop();
		if ( scrollTop > upperLimit ) {
			$(scrollElem).stop().fadeTo(300, 1); // fade back in
		}else{
			$(scrollElem).stop().fadeTo(300, 0); // fade out
		}
	});

	// Scroll to top animation on click
	$(scrollElem).click(function(){
		$('html, body').animate({scrollTop:0}, scrollSpeed); return false;
	});
)(jQuery);
```
可以对upperLimit和scrollSpeed参数进行修改，控制显示位置和回滚速度。
## 添加文件引用。
打开文件/themes/Yilia/layout/_partial/after_footer.ejs，在文件的末尾添加以下两行代码：
``` bash
<%- partial('totop') %>
<script src="<%- config.root %>js/totop.js"></script>
```
## 添加按钮图片
将下面的图片复制到/themes/Yilia/source/img目录下，文件名为scrollup.png，页面足够长时，就看到按钮出现了。
![](http://120.24.60.216:4000/img/scrollup.png)

