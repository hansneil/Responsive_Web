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

# 3.HTML5［响应式设计］
 - 3.1 polyfill和Modernizr
       
       针对不支持HTML5的旧式浏览器[如ie6等]，polyfill和Modernizr提供了js脚本用于弥补这方面的缺陷。相对于polyfill，Modernizr更值得令人关注，因为它除了让IE支持html5的新元素，还能够基于一系列特性测试来有条件的加载更高级的polyfill，css和额外的js文件。
 - 3.2 关于HTML5
  - 新的文档类型声明: <!DOCTYPE html> / <!doctype html> | 告诉浏览器用标准模式渲染
  - 新建html元素，可以设置语言类型: <‘html lang="en"> / <’html lang="cn">
  - 设置字符编码: <meta charset=utf-8> | 通常都是utf-8编码，除非有特殊需要
  - 精简之处：
    
    引用外部CSS和JS文件时，不再需要声明类型，添加引号，不区分大小写等，如'<'link rel=stylesheet href=css/main.css'>'是一个完全正确的标签。这种精简不局限于引用外部文件，在其他元素中也同样适用。例如下面的代码完全正确:
<pre>
  ‘<’div id=wrapper>
    ‘<’img SRC=img/1.png>
  ‘<’/div>
</pre>
  - <'a>标签：可以在标签中嵌套多个元素
    
    这里需要注意一点，不能在标签中嵌套标签，也不能在标签中嵌套表单
  - html废弃零件: strike enter font frame frameset等等
 - 3.3 HTML5的全新语义元素
  - <'section> 定义文档或者应用程序的区域
  - <'nav> 定义文档的主导航区
  - <'article> 用来包裹独立的内容片段，这部分片段复制到另外一个网站上也能保持完整的意义。或者说该片段能否独立为一篇博客或者文章
  - <'aside> 定义与页面主内容松散相关的内容，可用作侧边栏，引用，广告或导航元素
  - <'hgroup> 如果页面中有<'h1> <'h2> <'h3>等一组元素，可考虑用<'hgroup>将它们包装起来
  - <'head> 不计入大纲结构，不能用它来划分结构，用它来包含对区域内容的说明
  - <'footer> 同header一样，但它用来包含区域内容的辅助信息
  - <'address> 标准离其最近的<'article>或<'body>元素的联系信息
 - 3.4 文本级语义元素
  - <'b> <'em> <'i>
 - 3.5 WAI-ARIA 无障碍网页应用技术
  - 地标角色, role:[application, banner, complementary, contentinfo, form, main, navigation, search]
 - 3.6 关于html5的video等媒体元素
  - <'video>: <'video width height controls autoplay loop poster src><'source><'/source><'/video>
  - 响应式video, 只要去掉width height，之后再设置video {width: height:}即可
  - 对于iframe插入的视频，无法通过上述方法实现响应式，必须借助于插件[FitVids](http://fitvidsjs.com/)
 - 3.7 html让离线web变得可能
   
   - 优点：设置和使用非常简单
   - 机制：每个需要离线的网页都需要指定一个.manifest的文本文件，该文本文件罗列了离线所需的所有资源文件
   - 使用： <'html lang='en' manifest='/offline.manifest'>
   <pre>
     CACHE MANIFEST
       #v1
      CACHE:
       basic_page_layout_ch4.html
       css/main.css
       img/atwiNavBg.png
       img/kingHong.jpg
       img/midnightRun.jpg
       img/moulinRouge.jpg
       img/oscar.png
       img/wyattEarp.jpg
       img/buntingSlice3Invert.png
       img/buntingSlice3.png
     NETWORK: *
     FALLBACK:
       //offline.html
   </pre>

# 4.解决跨浏览器问题
 - 4.1 渐进增强和优雅降级
   
   优雅降级：在现代浏览器中制作网站，然后会老版浏览器提供基本功能。新特性在老版浏览器中会降级。
   
   渐进增强：恪守web标准为基础，在所有浏览器中均可用，然后通过css和js来为新浏览器提供渐进式的功能
 - 4.2 Modernizr
   
   用于检测浏览器功能的开源js库，除了让ie8及一下版本的浏览器支持html5元素，主要做的是浏览器功能检测。至于如何处理之后的事，就是开发人员的事了。
   - 使用modernizr辅助修正样式问题
     
     在不支持3d变换的浏览器上，使用.no-csstransforms3d .note{display:block} .note{display:none}
   - 使用modernizr让老版本ie支持HTML5
   - 使用respond.js让ie支持minx/max媒体查询功能
   - 使用modernizr按需加载资源
     加载方法很简单：
 <pre>
    Modernizr.load({
        test: Modernizr.mq('only all');
        nope: 'js/respond.js'
    })
    Modernizr.load({
        test: Modernizr.mq('only all');
        yep: 'js/pass.js';
        nope: ['js/respond.min.js', 'fail-polyfill.js', 'fail.js'],
        both: 'js/for-all.js'
    })
 </pre>
 - 4.3 必要时将导航链接变为下拉菜单［渐进增强的典型代表］
       
       需要jquery的一个插件，jquery.mobilemenu.js，然后按需加载
 <pre>
    Modernizr.load(
     {
        test: Modernizr.mq('only all'),
        nope: 'js/respond.min.js'
     },
     {
        test: Modernizr.mq('only screen and (max-width: 600px)'),
        yep: ['js/jquery-1.7.1.js', 'js/jquery.mobilemenu.js'],
        complete: function() {
            $document.ready(function(){
                $("#mainnav").mobileMenu({
                    switchWidth: 600,
                    topOptionText: 'Select a Page',
                    indentString: '&nbsp;&nbsp;&nbsp'
                });
            })
        }
     }
    )
 </pre>
