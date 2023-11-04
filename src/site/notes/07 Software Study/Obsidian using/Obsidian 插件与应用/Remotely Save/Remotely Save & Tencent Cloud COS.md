---
{"dg-publish":true,"permalink":"/07-software-study/obsidian-using/obsidian/remotely-save/remotely-save-and-tencent-cloud-cos/","tags":["Obsidian","Tech/Obsidian","clipping"],"noteIcon":""}
---


喜欢英语的小伙伴，可以看看我新写的小软件~

[小狸猫英语播放器-为看视频练听力设计的播放器 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/634267378)

## 数据先做好备份！

数据先做好备份！

数据先做好备份！

数据先做好备份！

## remotely save

目前来说，obsidian的ios用户，基本都是靠icloud做同步的，用过都知道多坑了，我原来都是靠FreeFileSync中转同步勉强使用的。

总之，现在有了更好的选择，那就是 remotely save 插件，支持以下同步方案

1.  dropbox
2.  onedrive
3.  webdav(包括坚果云)
4.  s3(cos/oss)

对于大众用户来说，以上最简单且实用的方案应该是使用坚果云的webdav了，不过目前（2022年3月12日）坚果云还不支持cors配置，移动端ob暂不能使用remotely+坚果云的方法同步，所以本篇先来讲讲remotely+cos的方案。

鉴于现在已经有一些配置教程了，但是我认为对于非技术人员来说，还是过于零散，所以会踩一些坑，本篇文章会尽量把每一个步骤都给还原出来，让不懂技术的同学也能跟着进行配置，保姆级教程。

## 安装Remotely Save插件

安装插件这一步就真的不说明了哈哈哈，相信大家都懂，可以直接从插件市场安装，或者从github下载也行

[GitHub - fyears/remotely-save](https://link.zhihu.com/?target=https%3A//github.com/fyears/remotely-save)

cos新用户比较便宜，这也是我推荐大家去尝试cos的原因，1块钱买不了上当，买不了吃亏，1块钱就能可以50gb的存储容量用一年，顺便还能用来做图床他不香吗，可惜腾讯没有给我打钱哈哈。

打开这个链接，然后选择1块钱的那个套餐，点击立即抢购就完事了。当然了新用户如果没实名还是要按照说明实名验证一下的。

[对象存储特惠-对象存储优惠-对象存储活动 - 腾讯云](https://link.zhihu.com/?target=https%3A//cloud.tencent.com/act/pro/cos)

![](https://pic3.zhimg.com/v2-93f82ae705cd0058f4b5e007210506de_b.jpg)

### 关于流量价格

以上1块钱50GB的是存储价格，访问文件还会产生额外的流量费用，按照以往图床用户的经验，单纯用来自己做笔记的话，一年可能也就十来块钱，很少超过50的，图片使用多的就会花费多一点，总之相比付费网盘或者官方同步，肯定还是有价格优势的，具体收费细节可以参考cos的说明。

## cos配置

确认购买完成以后，下一步来进行cos的配置。

### 进入控制台

如果你购买付款完以后找不到怎么进入控制台，可以回到腾讯云的主页[https://cloud.tencent.com/](https://link.zhihu.com/?target=https%3A//cloud.tencent.com/)，

然后点击右上角的控制台

![](https://pic4.zhimg.com/v2-97758c55095265703126cf2ad2d8b737_b.jpg)

### 进入对象存储

![](https://pic4.zhimg.com/v2-bcc29e074b89358fc4da6f6c110eda57_b.jpg)

此刻你该会看到这个页面

![](https://pic2.zhimg.com/v2-55e91d66b3c91a3e05ac3b490205b869_b.jpg)

### 创建存储桶

点击存储桶列表（默认列表是空的），然后点击创建存储桶

![](https://pic2.zhimg.com/v2-c90023afb5de8f0fae423358f2e03cd5_b.jpg)

地域随便选，选一个离你近的即可

名称也是可以随意的，我这里就写obsidian作为例子

访问权限选择私有读写

![](https://pic4.zhimg.com/v2-540cec51bd17a6fa119dc4420ef3603b_b.jpg)

然后点击「下一步」

这一页默认配置即可，什么都不用修改

![](https://pic1.zhimg.com/v2-7e1633af51f28ed5c28ebbdb769dab20_b.jpg)

点击「下一步」

![](https://pic4.zhimg.com/v2-d180e1d53ec4c1b7e3cefd0d5a521593_b.jpg)

确认配置，点击「创建」

正常情况下你会进入这个页面（如果不小心退了找不到也没关系，在存储桶列表可以找到刚刚创建的obsidian-xxxxxxx的存储桶，点击一下就可以进来了）

![](https://pic1.zhimg.com/v2-6012bc3bb22be20d77a4485e1d6d6290_b.jpg)

存储桶可以理解为一个私有的网盘空间，因为是刚刚创建的，所以没有文件~

至此，存储桶创建完毕，下一步是配置子账号访问权限。

## 创建子账户

我们刚刚的操作都是使用主账户，权限很大，我们给其他程序使用并不需要这么大的权限，所以接下来创建一个子账号专门用于给obsidian同步使用。

点击右上角的「账号信息」

![](https://pic4.zhimg.com/v2-67d1e12d8e6ad28e41d0c0b013108ea3_b.jpg)

点击「快速进入CAM」

![](https://pic2.zhimg.com/v2-ac01a92b73b66eecedfdf1a9d4800441_b.jpg)

点击「用户列表」

![](https://pic1.zhimg.com/v2-3d9cec83be0138982d8451775b85583c_b.jpg)

点击「新建用户」

![](https://pic4.zhimg.com/v2-70f3f587644bdd8dcd1d2d07a67f7dd7_b.jpg)

选择「自定义创建」

![](https://pic1.zhimg.com/v2-1d897f722abdb6d8b2d71b79619e81f4_b.jpg)

选择「可访问资源并接受信息」

![](https://pic3.zhimg.com/v2-bdbab1559b9611226f65306be4394cde_b.jpg)

填上用户名，勾选「编程访问」，手机号最好也填上且验证

![](https://pic3.zhimg.com/v2-cbc3dc9ae46041c797f767d8a4502f72_b.jpg)

下一步，这些权限全部不用勾，直接点「下一步」

![](https://pic3.zhimg.com/v2-30d188e6e20343baa75786f5eceb1312_b.jpg)

这个页面点击完成即可

![](https://pic4.zhimg.com/v2-fdecd24473932e5ff1773deab3ddc123_b.jpg)

把密钥（SecretId+SecretKey）复制保存下来，待会要用到

把密钥（SecretId+SecretKey）复制保存下来，待会要用到

把密钥（SecretId+SecretKey）复制保存下来，待会要用到

![](https://pic4.zhimg.com/v2-b2ba578d09c0b6f2d1dcdd124b45ca83_b.jpg)

至此，子账号创建完成，现在回去继续配置cos

## 给子账号开通存储桶访问权限

回到刚刚操作过的「对象存储」

![](https://pic2.zhimg.com/v2-bc2e3acb14aa4be6a3db04a5d92e36d1_b.jpg)

「存储桶列表」，找到刚刚新建的存储桶，点击配置管理

![](https://pic2.zhimg.com/v2-39e5941cdf5c9bf597cf8758aa2d6985_b.jpg)

「权限管理」-「存储桶访问权限」-添加用户

![](https://pic1.zhimg.com/v2-f83226cf3bbb847f47f72986a64ee7d8_b.jpg)

选择「子账号」，选择刚刚创建的obsidian子账号，权限勾选如图三个，然后记得点「保存」

![](https://pic3.zhimg.com/v2-5533569f35dc991767de024a4906f08e_b.jpg)

## 设置跨域权限

这一步骤，可能以后不再需要，但是目前（2022年3月12日）还是需要设置的。

在上一步的页面基础上，选择「安全管理」-「跨域访问CORS设置」-添加规则

![](https://pic3.zhimg.com/v2-f09d606bca07b2ba94656bc61e78ff0a_b.jpg)

来源origin填上这三行配置

```
app://obsidian.md
capacitor://localhost
http://localhost
```

操作methods全部勾上，其他默认即可，然后点「保存」

![](https://pic1.zhimg.com/v2-d67d9ca1381fb3b6565113d8b9ed8928_b.jpg)

至此，腾讯云的网页端已经配置完毕，接下来去配置电脑客户端。

## 电脑端remotely save 插件配置

打开remotely save的插件配置，选择S3 or compatible方式，一共有5个选项需要配置，我们填好这5个配置就可以了，我稍微说明一下怎么填。我们先打开存储桶的概况页面，找到访问域名的url，把他复制出来

![](https://pic4.zhimg.com/v2-becfe6aceedb023fa09c02b9a54cd03b_b.jpg)

比如地址是 https://obsidian-123456789.cos.ap-guangzhou.myqcloud.com

那么remotely save里面就该这样填

| s3Endpoint | [http://cos.ap-guangzhou.myqcloud.com](https://link.zhihu.com/?target=http%3A//cos.ap-guangzhou.myqcloud.com) |
| --- | --- |
| s3Region | ap-guangzhou |
| s3AccessKeyID | 前文中保存的SercretId |
| s3SecretAccessKey | 前文中保存的AccessKey |
| s3BucketName | obsidian-123456789 |

填好信息以后，点击check,出现右上角的提示，则证明是配置成功了，如果没有，重新检查以上的配置。

![](https://pic3.zhimg.com/v2-3a86d04b0df09f15c6811acaa4acc3a2_b.jpg)

## 同步到存储桶（云端）测试

点击同步按钮，如果出现了这8个提示，证明同步到云存储桶已经成功了

![](https://pic3.zhimg.com/v2-799b92da1727f388c336d715232b5776_b.jpg)

然后我们去存储桶的文件列表再次确认一下，看看文件是不是真的上传成功了。

如果您跟我一样，发现笔记文件已经出现在了文件列表，那就是确认成功配置PC端的同步了。

![](https://pic2.zhimg.com/v2-0712c3cbf51e3f6870c71c4b33270ecd_b.jpg)

## ios端配置

方式1：

如果您已经在使用icloud同步方案（废话了，没用官方同步的都在用icloud），把.obsidian文件给同步到icloud上，那么remotely save 插件的配置也是同步到手机或者ipad了，可以直接使用remotely save 插件了。

方式2：

如果您的ios端是空库，可以在pc端使用export-get QR code 生成一个二维码，在iphone或者ipad用相机扫描就可以打开ob并导入配置了

![](https://pic2.zhimg.com/v2-5e80167404849210ac0855d6532d8961_b.jpg)

ios的插件配置好以后，点同步，就可以把文件给同步过来了（正常情况下）

## remotely save 的其他配置说明

![](https://pic2.zhimg.com/v2-03c2e597625a95a09bb91257314f4d55_b.jpg)

## 注意事项

操作前备份好数据！

鉴于remotely save也是新出的第三方同步插件，亦可能存在未知的风险，对于自己的笔记库，即使用上了remotely save，还是保持git定时备份或者其他备份方案为妙！

总之还是要养成备份的习惯，已经发生了很多使用icloud丢数据的案例了。

最后就是建议用了remotely save同步以后就不要使用icloud的同步了，以免冲突。（把pc上的库从icloud上移出来或者复制多一份在icloud外面用就好了，有用FreeFileSync之类的软件做中转同步的同学本来就是这么操作的你肯定懂的）