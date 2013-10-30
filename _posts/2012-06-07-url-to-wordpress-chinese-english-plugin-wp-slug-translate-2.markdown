---
author: admin
comments: true
date: 2012-06-07 09:26:21+00:00
layout: post
slug: url-to-wordpress-chinese-english-plugin-wp-slug-translate-2
title: WordPress 中文URL转为英文插件wp slug translate
wordpress_id: 1000
categories:
- 未分类
tags:
- WordPress
---

文章来源：[http://www.boke8.net/wordpress-wp-slug-translate.html](http://www.boke8.net/wordpress-wp-slug-translate.html)

#####wp slug translate插件介绍

通过该插件，可以让wordpress中文博客的博主使用/%postname%.html形式的固定链接时的文章URL的中文自动翻译为英文显示，英文显示不但较为美观，且对SEO是比较有利的。

#####wp slug translate插件安装使用

1. 下载WordPress博客插件[wp slug translate](http://wordpress.org/extend/plugins/wp-slug/)，并上传至wp-content/plugins/目录下（可以在博客后台的添加插件功能中直接搜索安装）
2. 登陆博客后台，在已安装插件列表中启用wp slug translate插件
3. 在设置选项卡下点击“固定链接”选项，设置自定义结构为/%postname%.html形式。（如果先前已做这一步的不用理会）
4. 添加新文章时，输入文章的标题和输入内容后，点击发布，就会自动把博客标题翻译为英文URL


#####wp slug translate插件说明
1. 如果在标题中设置有slug， 则选用标题中设置的slug作为缩略名， 标题设置的格式： titlｅ@@ Ｓlug
2. 如果标题未设置slug， 但在缩略名的栏目中有缩略名存在， 则选用slug栏目中的slug作为缩略名。
3. 如果以上两处都未设置缩略名（slug）， 则自动换取标题（title）， 然后将标题翻译成英文（如果是非英文的标题）， 翻译来源是谷歌翻译， 然后将翻译得到的英文作为slug设置成缩略名。
4. 如果因为某种原因， 比如网络问题、或者该中文字符无法翻译等等， 就自动会把非英文字符（其实就是汉字）转换成拼音。 转换成拼音的不仅仅是标题， 有可能是已经设置的slug， 如果已经设置的slug中含有中文字符也会翻译成拼音， 不过如果个Google的翻译中含有中文字符就会自动删除而不是翻译成拼音， 因为我觉得这个就没有意思了！


**提醒：**该插件的翻译来源是谷歌在线翻译，翻译后的英文并不一定是百分之百正确。
