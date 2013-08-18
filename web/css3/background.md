本文对CSS3中背景的四个新的属性进行了详细介绍。

# Multiple backgrounds

Css3中，对一个元素可以使用`一张以上的背景图片`。除了使用逗号将图片分开以外，其代码与css2相同。第一个声明的图片定位在元素的顶部，接下来的图片层列于下，像这样：

>1.background-image: url(top-image.jpg), url(middle-image.jpg), url(bottom-image.jpg);

#Background Clip

该属确定背景画区，有以下几种可能的属性：

>background-clip: border-box;背景从border开始显示;

>lbackground-clip: padding-box;背景从padding开始显示;

>background-clip: content-box;背景显从content取与开始显示;

>background-clip: no-clip;默认属性，等同于border-box;

# Background Origin

它通常与background-position联合使用，你可以从`border`、`padding`、`content` 来计算background-position（就像background-clip）。

>background-origin: border-box; 从border.开始计算background-position;

>background-origin: padding-box;从padding.开始计算background-position;

>background-origin: content-box;从content.开始计算background-position;


#Background Size

 background-size 常用来调整背景图片的大小，有以下可能的属性：

>background-size: contain; 缩小图片以适合元素（维持像素长宽比）;

>background-size: cover; 扩展元素以填补元素（维持像素长宽比）

>background-size: 100px 100px; 缩小图片至指定的大小.

>background-size: 50% 100%; 缩小图片至指定的大小，百分比是相对包含元素的尺寸.

#Background Break

Css3中，元素可以被分割成单个的盒子（例如，使一个内联的span元素多行排列），
background-break 属性控制背景跨越多个盒子如何显示。

Background-break: continuous；;默认值。盒子之间好像没有空白（好似它们在一个盒子当中，背景图片应用到盒子之上）。
Background-break: bounding-box；将空白考虑进去。
Background-break: each-box；将每个盒子单独处理，对每一个重绘背景。

# background-color

Css3对背景颜色有轻微的加强，除了定义背景颜色之外，你还可以定义一个备用颜色，它在元素最底层的图片不能使用时得以生效。如：

1.background-color: green / blue;
在这个例子中，背景颜色为green。但是，如果最底层的图片不能使用，背景颜色将是blue。如果没有定义颜色，就假定是透明的(transparent)。

#Background Repeat

在css2中，当图片重复时，它经常在元素的底部切断。Css3引入两个新的属性修复它。

space:等量的空白应用到图像块之间直到填满元素。
round:图片缩小直到适合元素。
改变Background Attachment

background-attachment 有一个可能的属性值：local。它通常与能滚动的元素（如：overflow:scroll）一起发挥作用。当background-attachment 为scroll时，元素内容滚动时背景图片不会滚动。background-attachment为local时，元素内容滚动时背景图片会跟着滚动。