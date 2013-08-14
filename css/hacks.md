
# 浏览器兼容性问题

CSS对浏览器的兼容性有时让人很头疼,或许当你了解当中的技巧跟原理,就会觉得也不是难事,从网上收集了IE7,6与Fireofx的兼容性处理方法并整理了一下.对于web2.0的过度,请尽量用xhtml格式写代码,而且DOCTYPE 影响 CSS 处理,作为W3C的标准,一定要加 DOCTYPE声名. 

# CSS技巧

1.div的垂直居中问题 vertical-align:middle; 将行距增加到和整个DIV一样高 line-height:200px; 然后插入文字，就垂直居中了。缺点是要控制内容不要换行 

2. margin加倍的问题 设置为float的div在ie下设置的margin会加倍。这是一个ie6都存在的bug。解决方案是在这个div里面加上 display:inline; 例如：

 	<#div id=”imfloat”>

相应的css为

    #IamFloat{ float:left; margin:5px;display:inline;} 

3.浮动ie产生的双倍距离

	#box{ float:left; width:100px; margin:0 0 0 100px;
	//这种情况之下IE会产生200px的距离 display:inline; 
	//使浮动忽略}

这里细说一下block与inline两个元素：block元素的特点是,总是在新行上开始,高度,宽度,行高,边距都可以控制(块元素);Inline 元素的特点是,和其他元素在同一行上,不可控制(内嵌元素); 

	#box{ display:block; 
	//可以为内嵌元素模拟为块元素 display:inline; 
	//实现同一行排列的效果 diplay:table; 

4 IE与宽度和高度的问题 IE 不认得min-这个定义，但实际上它把正常的width和height当作有min的情况来使。这样问题就大了，如果只用宽度和高度，正常的浏览器里这两个值就不会变，如果只用min-width和min-height的话，IE下面根本等于没有设置宽度和高度。 比如要设置背景图片，这个宽度是比较重要的。要解决这个问题，可以这样： 

	#box{ width: 80px; height: 35px;}html>body #box{ width: auto; height: auto; min-width: 80px; min-height: 35px;} 

5.页面的最小宽度 min -width是个非常方便的CSS命令，它可以指定元素最小也不能小于某个宽度，这样就能保证排版一直正确。但IE不认得这个，而它实际上把width当做最小宽度来使。为了让这一命令在IE上也能用，可以把一个<div> 放到 <body> 标签下，然后为div指定一个类, 然后CSS这样设计：
 
	#container{ min-width: 600px; width:expression(document.body.clientWidth < 600? "600px": "auto" );}

 第一个min-width是正常的；但第2行的width使用了Javascript，这只有IE才认得，这也会让你的HTML文档不太正规。它实际上通过Javascript的判断来实现最小宽度。 

6.DIV浮动IE文本产生3象素的bug 左边对象浮动，右边采用外补丁的左边距来定位，右边对象内的文本会离左边有3px的间距. 

	#box{ float:left; width:800px;} 

	#left{ float:left; width:50%;} 
	#right{ width:50%;} *html
	#left{ margin-right:-3px; //这句是关键} 

	<div id="box"> <div id="left"></div> <div id="right"></div> </div> 


7.IE捉迷藏的问题 当div应用复杂的时候每个栏中又有一些链接，DIV等这个时候容易发生捉迷藏的问题。 有些内容显示不出来，当鼠标选择这个区域时发现内容确实在页面。 解决办法：对·#layout· 使用 ·line-height· 属性或者给#layout使用固定高和宽。页面结构尽量简单。 

8.float的div闭合;清除浮动;自适应高度; 