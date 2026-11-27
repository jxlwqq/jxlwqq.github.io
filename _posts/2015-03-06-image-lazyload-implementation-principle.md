---
layout: post
title: "图片延迟加载（lazyload）的实现原理"
date: 2015-03-06 18:17:00 +0800
categories: frontend javascript
---

此前在浏览一些网站的时候，发现他们网站的图片都是你“鼠标”滚到哪，图片才会加载显示。当时觉得好神奇，怎么会这么“跟手”呢。

核心原理是：

1 设置一个定时器，计算每张图片是否会随着滚动条的滚动，而出现在视口（也就是浏览器中的**展现网站的空白部分**）中；

2 为<img>标签设置一个暂存图片URL的自定义属性（例如loadpic），当图片出现在视口时，再将loadpic的值赋给图片的src属性；

最后，贴出分别用原生js和jQuery实现该功能的实现方法：

1 原生JavaScript的实现方法

```
<script>
    var imgs = document.getElementsByTagName('img');
    // 获取视口高度与滚动条的偏移量
    function lazyload(){
        var scrollTop = window.pageYOffset || document.documentElement.scrollTop || document.body.scrollTop;
        var viewportSize = window.innerHeight || document.documentElement.clientHeight || document.body.clientHeight;
        for(var i=0; i<imgs.length; i++) {
            var x =scrollTop+viewportSize-imgs[i].offsetTop;
            if(x>0){
                imgs[i].src = imgs[i].getAttribute('loadpic');   
            }
        }
    }

    setInterval(lazyload,1000);
</script>
```

2 jQuery的实现方法

```
/**
* 图片的src实现原理
*/
$(document).ready(function(){
    // 获取页面视口高度
    var viewportHeight = $(window).height();
    var lazyload = function() {
        // 获取窗口滚动条距离
        var scrollTop = $(window).scrollTop();
        $('img').each(function(){
        // 判断 视口高度+滚动条距离 与 图片元素距离文档原点的高度         
        var x = scrollTop + viewportHeight - $(this).position().top;
        // 如果大于0 即该元素能被浏览者看到，则将暂存于自定义属性loadpic的值赋值给真正的src            
        if (x > 0)
        {
            $(this).attr('src',$(this).attr('loadpic')); 
        }
    })
    }
    // 创建定时器 “实时”计算每个元素的src是否应该被赋值
    setInterval(lazyload,100);
});
```

 当然，上述代码还是很简陋，仅仅说了实现的原理，生产环境推荐使用：[jquery\_lazyload](https://github.com/tuupola/jquery_lazyload "Lazy Load Plugin for jQuery")
