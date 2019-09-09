# 微信小程序自定义右上角提示组件
### 1. 目录结构
```
project-name
├── components
│   ├── add-tips            // 提示组件
│   ├── assets              // 资源目录
├── pages
│   ├── index               // demo演示页面
├── app.js                  
├── app.json
├── app.wxss   
└── project.config.json     // 小程序配置文件 
```   
### 2. 引用方式：

a. 在app.json中配置add-tips组件引用；

```
 "usingComponents": {
    "add-tips": "/components/add-tips/index"
 },
```

b. 在wxml页面直接引用。
```
<add-tips></add-tips>
```

### 3.核心代码示例：


```
      // 判断是否已经显示过
      let cacheOne = wx.getStorageSync(STORAGE_KEY_ONE);
      const now = +new Date();
      // 校验缓存数据 以及缓存时间是否过期(关闭后缓存一个月 一个月后重新提示用户)
      if (cacheOne && (now - cacheOne < 30 * 24 * 3600000)) return;
      // 处理根据系统信息处理位移箭头位置（重点）
      let systemInfo = wx.getSystemInfoSync();
      let client = wx.getMenuButtonBoundingClientRect();
      if (systemInfo && client) {
        this.setData({
          marRight: systemInfo.screenWidth - client.left - 28
        });
      }
      // 没显示过，则进行展示
      this.setData({
        SHOW_TOP: true
      });
```


### 4. 效果图：

![](https://github.com/weipoo/add-tips/blob/master/demo.jpg)

