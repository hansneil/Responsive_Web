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
