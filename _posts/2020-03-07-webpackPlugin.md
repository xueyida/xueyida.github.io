---
layout: post
title: 学习写一个webpack插件
categories: [前端, webpack]
description: 平时有用到很多的webpack插件，比如html等；通过写webpack插件，对了解webpack的原理应该也有一定的了解
keywords: webpack 前端 webpackPlugin Node
---

<h3>平时有用到很多的webpack插件，比如html等；通过写webpack插件，对了解webpack的原理应该也有一定的了解；</h3>

## 写插件的步骤

- 初始化package.json文件，使用npm init

- 安装webpack
    
    ```javascript
        yarn add webpack webpack-cli -D
    ```

- 用webpack构建项目

    **目的**
    
    - 使用plugin    
    - 构建插件

- 开始写插件
    
    需要对webpack的原理有一定的了解，具体的了解，异步webpack相关的了解

    compiler

    compilation

    Tapable




## 参考

[webpack官网，如何写一个webpack插件](https://www.webpackjs.com/contribute/writing-a-plugin/)
