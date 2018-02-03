---
title: vue-demo
date: 2017-12-02 11:25:59
tags: vue nodejs
---

#### 安装 ####
``` javascript
1> 安装nodejs  `brew install node` `npm view vue-cli`
2> 安装vue-cli `nmp install -g vue-cli`
3> 安装webpack `nmp install -g webpack`
4> 创建webpack为模板的项目 `vue init webpack vue-demo`
```

#### 常见问题 ####

1、无法通过ip地址访问
``` javascript
修改config/index.js , host: '0.0.0.0'
```

2、invalid host header
``` javascript
修改webpack.dev.config.js , devServer.disableHostCheck: true
```
3、跨域问题的处理
``` javascript
1> 问题描述: 通常开发阶段,前端页面使用node静态服务器,端口号是 8080。后端接口一般是本地的tomcat,端口号可能是 8081 。登录注册通常会写写cookie，后端response的cookie写在 8081 下，于是 8080 下拿不到 8081 的cookie，登录无效。
2> 解决办法,开启代理服务器。 config/index.js 文件中的proxyTable 。`axios`发起的请求仍然为 8080 ,通过反向代理,把 8080 的请求代理到 8081 上即可。
```
