# 浅谈安卓抖音协议， 抖音设备注册


<br />抖音最近加入了风控，大大限制了数据拉取的成功度，处理这个问题很棘手，具体自己探索。<br />同时抖音加强了对SO的加密，即使修复ida堆栈，也是jumpout，大大提升了代码追踪的繁琐度，所以最新版的SO还没有深入跟进分析。

那么回到今天的话题，抖音的设备如何注册<br />其实网上已经有公开的资料<br />的确可行，咱们老生常谈，简单的聊一下思路逻辑<br />一：首先通过抓包找到接口地址<br />[http://log.snssdk.com/service/2/device_register](http://log.snssdk.com/service/2/device_register)<br />二：通过JDAX对源代码的分析，我们可以发现它<br />![image.png](https://cdn.nlark.com/yuque/0/2020/png/97322/1607304537651-40bd16e4-0a14-4369-9ba4-f168a4364dd2.png#align=left&display=inline&height=195&margin=%5Bobject%20Object%5D&name=image.png&originHeight=390&originWidth=1228&size=126090&status=done&style=none&width=614)<br />先通过GZIP压缩，再TTEncryptUtils加密，最后POST发送出去请求<br />然后X-SS-STUB，发现它只是一个对post的body部分的md5<br />![](https://cdn.nlark.com/yuque/0/2020/png/97322/1607304522293-825c9cd9-b676-4811-a73a-93d81d575280.png#align=left&display=inline&height=65&margin=%5Bobject%20Object%5D&originHeight=65&originWidth=434&size=0&status=done&style=none&width=434)<br />三：最后我们可以拼装属于自己的请求包<br />![](https://cdn.nlark.com/yuque/0/2020/png/97322/1607304522223-2f1048d4-74d1-4589-b923-10389246c253.png#align=left&display=inline&height=172&margin=%5Bobject%20Object%5D&originHeight=172&originWidth=554&size=0&status=done&style=none&width=554)<br />
<br />——————————————————————————————————————————
<a name="9794cc28"></a>
#### TiToData：专业的短视频、直播数据接口服务平台。
<a name="1c5f89ff"></a>
#### 更多信息请联系： [TiToData](https://www.titodata.com?from=douyinarticle)
覆盖主流平台：抖音，快手，小红书，TikTok，YouTube
