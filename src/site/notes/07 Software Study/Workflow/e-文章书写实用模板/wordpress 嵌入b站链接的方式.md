---
{"dg-publish":true,"dg-permalink":"07 Software Study/Workflow/e-articles","permalink":"/07 Software Study/Workflow/e-articles/"}
---

# 第一次尝试 来自 B站
## 1 首先点击复制嵌入代码

```
<iframe src="//player.bilibili.com/player.html?aid=81502772&;amp;cid=139471736&amp;page=1"scrolling=”no” border=”0″ frameborder=”no” framespacing=”0″ allowfullscreen=”true”> </iframe>
```

## 2 再加上【以下内容】到代码内，这里调整的是播放界面在网站中显示的大小，可以更改高度和宽度。

```
style=”width: 100%; height: 500px; max-width: 100%；align:center; padding:20px 0;
```


## 3 结果

```
<iframe src="//player.bilibili.com/player.html?aid=81502772&;amp;cid=139471736&amp;page=1" scrolling=”no” border=”0″ frameborder=”no” framespacing=”0″ allowfullscreen=”true” style=”width: 100%; height: 500px; max-width: 100%；align:center; padding:20px 0;”> </iframe> 
```


## 自己尝试一下！

```
style=”width: 100%; height: 500px; max-width: 100%；align:center; padding:20px 0;”
```


# 第二次尝试 来源 腾讯云
## 前言

很多小伙伴想把B站的视频嵌入到自己的博客或者网站中，但直接使用官方视频下面的嵌入代码，网站用户就看不了高清、发不了弹幕，并且视频排版也很不美观。然后用户点击播放器里各种连接被引入源站，你相当于是无偿给他打广告的。

这里就教大家如何嵌入高质量的B站视频代码

## 代码

首先上代码
```
<iframe src="//player.bilibili.com/player.html?aid=557196521&bvid=BV1Se4y1f7Rs&cid=808139146&p=1" scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true"> </iframe>
```

```
<iframe src="//player.bilibili.com/player.html?aid=557196521&bvid=BV1Se4y1f7Rs&cid=808139146&page=1&high_quality=1&danmaku=0" allowfullscreen="allowfullscreen" width="100%" height="500" scrolling="no" frameborder="0" sandbox="allow-top-navigation allow-same-origin allow-forms allow-scripts"></iframe>
```
可行

```
<iframe src="//player.bilibili.com/player.html?aid=557196521&bvid=BV1Se4y1f7Rs&cid=808139146&high_quality=1&danmaku=0" allowfullscreen="allowfullscreen" width="100%" height="500" scrolling="no" frameborder="0" sandbox="allow-top-navigation allow-same-origin allow-forms allow-scripts"></iframe>
```

1. 修改后代码复制过来
2. 复制网页代码 替换部分代码 原代码的 "aid"(含) 到 "&" (前) 替换复制代码的 "aid" 到 ''& 区间

官方代码：

```javascript
<iframe src="//player.bilibili.com/player.html?aid=375588815&bvid=BV1so4y1m7U5&cid=339262048&page=1" scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true"> </iframe>
```

复制

修改后：

```javascript
<iframe src="//player.bilibili.com/player.html?aid=375588815&bvid=BV1so4y1m7U5&cid=339262048&page=1&high_quality=1&danmaku=0" allowfullscreen="allowfullscreen" width="100%" height="500" scrolling="no" frameborder="0" sandbox="allow-top-navigation allow-same-origin allow-forms allow-scripts"></iframe>

```

复制

## 代码讲解

```javascript
BILIBILI 地址PC端参数
    &high_quality=1   (1=最高画质 0=最低画质)
    &danmaku=0   (1=打开弹幕 0=关闭弹幕)
iframe 参数
    allowfullscreen="allowfullscreen" #移动端全屏
    sandbox="allow-top-navigation allow-same-origin allow-forms allow-scripts" #禁止弹出网页
```

复制

|属性|值|描述|
|---|---|---|
|align|left right top middle bottom|不赞成使用。请使用样式代替。规定如何根据周围的元素来对齐此框架。|
||||
|frameborder|10|规定是否显示框架周围的边框。|
|height|pixels%|规定 iframe 的高度。|
|longdesc|URL|规定一个页面，该页面包含了有关iframe 的较长描述。|
||||
|marginheight|pixels|定义 iframe的顶部和底部的边距。|
||||
|marginwidth|pixels|定义 iframe的左侧和右侧的边距。|
||||
|name|frame_name|规定 iframe 的名称。|
|sandbox|“”allow-formsallow-same-originallow-scriptsallow-top-navigation|启用一系列对 <_iframe> 中内容的额外限制。|
|scrolling|yesnoauto|规定是否在 iframe中显示滚动条。|
||||
|seamless|seamless|规定 <_iframe> 看上去像是包含文档的一部分。|
|src|URL|规定在 iframe中显示的文档的 URL。|
||||
|srcdoc|HTML_code|规定在 <_iframe> 中显示的页面的 HTML 内容。|
|width|pixels%|定义 iframe 的宽度。|