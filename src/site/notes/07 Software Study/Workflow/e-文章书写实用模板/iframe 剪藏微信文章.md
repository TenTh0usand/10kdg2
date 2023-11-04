---
{"dg-publish":true,"permalink":"/07-software-study/workflow/e/iframe/","tags":["公众号","clipping/methods"],"noteIcon":""}
---

### 写在前面：为什么一定要用flowus剪藏

本身直接复制文章内容保存为html或者markdown，然后粘贴到obsidian之后可以直接浏览图片和文藏，并且观看效果很好。然而，当网页调用图片链接的时候，由于微信图片中url是自带防盗链的，所以会出现这种情况
![image.png|200](https://10kcos1-1306082059.cos.ap-shanghai.myqcloud.com/pic-1/202310212140410.png)
这个解决方案很多，例如最简单的方法是直接复制图片然后一个一个替换...类似的方案也都很鸡肋，于是还是借助flowus这个强大的工具吧

### 第一步：发送到flowus剪藏助手

![image.png](https://10kcos1-1306082059.cos.ap-shanghai.myqcloud.com/pic-1/202310212141670.png)

### 第二步：复制分享链接

![image.png](https://10kcos1-1306082059.cos.ap-shanghai.myqcloud.com/pic-1/202310212137753.png)

### 第三步：把分享链接插入到iframe模板，模板如下

```
<iframe
  id="inlineFrameExample"
  title="Inline Frame Example"
  width="1000"
  height="3000"
  src="网页链接">
</iframe>
```

如果是上传到wordpress文章，就要加入html标签

```
<!-- wp:html -->
<iframe
  id="inlineFrameExample"
  title="Inline Frame Example"
  width="1000"
  height="3000"
  src="网页链接">
</iframe>
<!-- /wp:html -->
```
### 第四步：在obsidian中新建页面，插入iframe，如果需要的话加上标签，上传！

1. 一般选择的目录：
02 Reading/我的剪藏/网络文章/
2. 用template-卡片模板
3. 常用标签`clipping` 
	 -  公众号文章 `clipping/作者姓名` `公众号`
4.上传！(还没结束)
 ![image.png](https://10kcos1-1306082059.cos.ap-shanghai.myqcloud.com/pic-1/202310212148382.png)

5. 上传完效果其实是这样的
 ![image.png](https://10kcos1-1306082059.cos.ap-shanghai.myqcloud.com/pic-1/202310212157564.png)
简单的方式就是复制这段文字然后编辑文章，粘贴替换就好了。
 


