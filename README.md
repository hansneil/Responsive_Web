 - 需要那些能够响应各种设备大小的完美设计
 - 响应式设计:
 <pre>
    移动设备优先的原则
    不再使用像素,而使用相对度量单位[em或者percent]
 </pre>

 - HTML5的优秀之处
    <pre>
    强调简化标签
    响应式设计的主要目标:对用户有限的视口作出响应,还要以最快的速度加载网页
    为响应式设计创建更加简洁和快速的代码
    HTML5 文档类型声明
    <!DOCTYPE html>
    链接脚本的正确做法:
    <script src='js/jquery-1.6.2.js'></script>
    [不再需要指定type="text/javascript"]
    [CSS的链接方法类似]

    --------
    新增语义化标签元素
    1.头部和导航
    <header> -- 头部
    <nav> -- 导航
    </pre>

 - CSS3和响应式设计

# 1.关于媒体查询
 - 重置样式: 一组css声明, 用来覆盖各个浏览器的默认样式,一般添加在主样式文件的开头, 用来将各个浏览器自带的默认样式重置成统一表现。比如Eric的[CSS Reset](http://meyerweb.com/eric/tools/css/reset/)。不过在HTML5有更好的解决方法，即[normalize.css](http://necolas.github.com/normalize.css/)
 - 1.1 响应式设计中需要保证图片尽量精简
 
       尽量将重复性的图片仅用一部分图像表示，然后进行水平重复(repeat－x)
 - 1.2 阻止移动浏览器自动调整页面大小
 
       利用viewport meta元素，可以阻止移动浏览器自动缩放页面
   <pre>
   '<'meta name="viewport" content="initial-scale=2.0, width=device-width"'>'
   </pre>
       利用viewport meta元素，可以控制页面的缩放范围，比如最大放大至3倍，最小缩小至0.5倍
   <pre>
   '<'meta name="viewport" content="maximum-scale=2.0, minimum-scale=0.5, width=device-width"'>'
   user-scalable=no，则表示禁止缩放
   </pre>
 - 1.3 始终坚持内容优先
 
       在多屏幕多设备情况下，应该保证用户尽可能多的看到内容，但顺序很重要，希望用户在初始视口中看到主要内容
 - 1.4 媒体查询总结
 
       在已知特定的访问设备尺寸，可以通过媒体查询轻松解决响应式布局。但很显然，它无法适应未来未知的变化。使用媒体查询更像是一个自适应的设计，而不是响应式的设计。要做到真正的响应式布局，需要将呆板的固定式布局改变成流动式布局。

# 2.流式布局
 - 2.1 固定布局经不起未知的考验
 
   那些仅使用媒体查询的设计，仅能从一种的样式突变成另一种样式，无法实现任何平滑渐变。因此需要将固定布局转变为百分比布局。
   
   真正的响应式设计: 流式布局 ＋ 弹性图片 ＋ 媒体查询。
 - 2.2 将固定布局转化为百分比布局
 
   转化公式
<pre>
   百分比宽度 ＝ 目标元素宽度 / 上下文元素宽度
</pre>
   - 设置百分比像素的上下文
     
     找到相对于视口尺寸的元素，将其改为百分比宽度，将其作为其他元素的上下文，之后子元素根据该元素计算相应的百分比。
   - 找到元素正确的上下文
   <pre>
     '<'li'>'<'a'>'...'<'/a'>'<'/li'>'
     此时元素a的上下文元素应该是li，因此需要给li设置一个确定的宽度
     对于li的宽度：可以设置一个固定的宽度值，也可以设置一个相对于li上下文的百分比
   </pre>
   - 用em代替px
     
     为什么使用em：因为em是相对于上下文的字体大小而言的。如果body的文字大小设置为100%，那么其他设置了em的元素都会受到body的初始大小的影响。由于默认的body字体大小为16px，因此font-size: 100% == font-size: 16px == font-size: 1em.

     修改成em时同样需要注意上下文的关系，找到正确的块级元素。
 - 2.3 弹性图片
 
       实现图片和其他媒体元素相对于流式布局缩放也非常简单，只要将max-width: 100%即可。使得图片最大不得超过上下文的宽度，实现了图片随视口缩放。也可以为图片指定特定的规则，比如侧栏的图片需要两张图片并排排列，因此可以将 .sidebar img {max-width: 45%}

       还可以给图片设定阈值，限制图片的最大宽度，即{width: 28.7829% max-width: 202px;}

       存在两个问题：［1］准备足够大的图片以满足大尺寸屏幕的需要 ［2］所有屏幕都要下载最大的图片
       - 解决上述问题的方法：
       
         为不同的屏幕尺寸提供不同大小的图片
 - 2.4 媒体查询和流式布局
 <pre>
 @media screen and (min-width: 1001px) and (max-width: 1080px) {
     #navigation ul li a {font-size: 1.4em}
 }
 @media screen and (min-width: 805px) and (max-width: 1000px) {
     #navigation ul li a {font-size: 1.25em}
 }
 @media screen and (min-width: 769px) and (max-width: 804px) {
     #navigation ul li a {font-size: 1.1em}
 }
 </pre>
 - 2.5 网格系统
