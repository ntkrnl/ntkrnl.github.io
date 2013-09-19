---
author: admin
comments: true
date: 2011-11-06 22:02:14+00:00
layout: post
slug: wordpress-comment-smileys-to-add-replace-and-auto-hide
title: wordpress评论表情添加、替换和自动隐藏
wordpress_id: 518
categories:
- wp
---

### 添加


评论添加表情方法有很多种，可以用插件[wp-smilise](http://wordpress.org/extend/plugins/wp-smilies/)或者[wp-grins](http://wordpress.org/extend/plugins/wp-grins/)，也可以把这个[smiley.php](http://cctvsmg-wordpress.stor.sinaapp.com/uploads/2011/11/smiley.php)放在使用的模板目录下，然后修改模板的comments.php文件，在 textarea之前添加如下一句：


> <div id="smiley"><?php include(TEMPLATEPATH . '/smiley.php'); ?></div>


效果如下：
[![](http://cctvsmg-wordpress.stor.sinaapp.com/uploads/2011/11/添加smile.png)](http://cctvsmg-wordpress.stor.sinaapp.com/uploads/2011/11/添加smile.png)


### 替换


wordpress的默认表情在wp-includesimagessmilies下，下载自定义表情包然后覆盖掉原来的即可，这里有人人表情包[下载](http://cctvsmg-wordpress.stor.sinaapp.com/uploads/2011/11/%E4%BA%BA%E4%BA%BA%E7%BD%91%E7%89%88.zip)。


### 自动隐藏


共需修改2个地方，首先在模板加载的js后面添加这样一段：


> $(document).ready(function(){
/*smilies*/
$("#smiley").hide();
$("#comment").focus(function() {
$("#smiley").animate({opacity: 'show'},{duration: 500} );
}).blur(function() {
$("#smiley").animate({opacity: 'hide'},{duration: 500});
});
});


然后修改模板的header.php文件，在header加载js文件的部分之前添加下面这句，这里调用的google提供的jquery精简库，速度比较快。


> <script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/jquery/1.4/jquery.min.js"></script>


要注意的是，header加载js应该位于<?php wp_head(); ?>之后，最好确保是最后执行。
