# vue引入sdk

```
npm install weixin-js-sdk
```

```
import wx from 'weixin-js-sdk';
```

```js
vue每个页面都得调用;

this.axios({
　　method: 'post',
　　url: 'http', //后端地址
　　data:{ url:location.href.split('#')[0] } //当前页面地址向服务端提供授权url参数，并且不需要#后面的部分
}).then((res)=>{  //后端返回签名
　　wx.config({
　　　　debug: true, // 开启调试模式,
　　　　appId: res.appId, // 必填，企业号的唯一标识，此处填写企业号corpid
　　　　timestamp: res.timestamp, // 必填，生成签名的时间戳
　　　　nonceStr: res.nonceStr, // 必填，生成签名的随机串
　　　　signature: res.signature,// 必填，签名，见附录1
　　　　jsApiList: ['scanQRCode'] // 必填，需要使用的JS接口列表，所有JS接口列表见附录2
　　});
})

//安卓手机会自动encodeURIComponent，而ios不会。
```

流程:

1. ​	微信公众后台>公众号设置>功能设置>js接口安全域名;
2. ​    如上引入后,向后端传当前地址;
3.    后端获取jsapi_ticket,和获取access_token;进行签名;返回签名参数;
4.    前端获取签名参数,初始化js-sdk;