---
title: mini-program-login-userinfo
date: 2018-08-13 21:57:53
tags: 微信小程序入门 wx.login wx.getUserInfo
---

### wx.getUserInfo ###
这个接口字面意思很简单，就是取得用户的信息，目前最新版本的接口，已经不会弹出对话框，要用户来授权。所以一般此接口单独使用，毫无效果，示例如下：

``` javascript
//app.js
App({
  onLaunch: function () {
    console.log('App before call wx.getSetting')
    wx.getUserInfo({
      success: res => {
        console.log('success', res)
      },
      fail: res => {
        console.log('fail', res)
      },
      complete: res => {
        console.log('complete', res)
      }
    })
  }
})
```

结果如下
``` javascript
App before call wx.getSetting
fail {errMsg: "getUserInfo:fail auth deny"}
complete {errMsg: "getUserInfo:fail auth deny"}
```
