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


- 常用plugin的分析

    - html-webpack-plugin
    
    > 自动生成html

    ```javascript
        new HtmlWebpackPlugin({
            filename: 'index.html', // 生成文件名
            template: path.join(process.cwd(), './index.html') // 模班文件
        })
    ```
    使用了make、emit的事件钩子
    compiler.hooks.make.tapAsync

    compiler.hooks.compilation.tap

   

    - copy-webpack-plugin
   

- 开始写插件

    
    需要对webpack的原理有一定的了解，具体的了解，异步webpack相关的了解
    

    compiler

    > 控制编译的流程

    compilation

    > 控制解析的流程

    Tapable

    > 生产各种钩子



    例子：

    > 函数写法

    ```javascript

        function MyExampleWebpackPlugin() {

        };

        MyExampleWebpackPlugin.prototype.apply = function(compiler{
            
            // plugin写法
            
            compiler.plugin('webpacksEventHook', function(compilation , callback) {
                console.log("This is an example plugin!!!");
                callback();
            });


             // hooks写法

             // webpacksEventHook:emit、complier等
             // TabType: Tab/tabAsync/tabPromise
             complier.hooks.webpacksEventHook.TabType((complication, [callback]) => {
                console.log("This is an example plugin!!!");
                callback();
             })
        };
    ```

    > 类的写法

    ```javascript
        class MyExampleWebpackPluginClassType{
            apply(compiler){

                // plugin写法

                compiler.plugin('webpacksEventHook', function(compilation, callback) {
                    console.log("This is an example plugin!!!");
                    callback();
                });


                // hooks写法

                // webpacksEventHook:emit、complier等
                // TabType: Tab/tabAsync/tabPromise
                complier.hooks.webpacksEventHook.TabType((complication, [callback]) => {

                })
            }
        }
    ```


    方法：

    1. 写一个javascript命名函数
    2. 在命名函数的prototype上面定义apply
    3. 指定一个绑定到webpack的事件钩子函数，使用compiler
    4. 相关的业务的操作，使用的是complication
    5. webpack 提供的回调的调用（哪种类型的回调）

   

## 目标

- 停止服务与开启服务
- 监听文件内容的变化
- 修改一个文件，另一个文件的内容也会变化

tab、tabAsync、tabPromise的区别


> Some plugin hooks are asynchronous. To tap into them, we can use tap method which will behave in synchronous manner or use one of tapAsync method or tapPromise method which are asynchronous methods.

> tapAsync
When we use tapAsync method to tap into plugins, we need to call the callback function which is supplied as the last argument to our function

> tapPromise
When we use tapPromise method to tap into plugins, we need to return a promise which resolves when our asynchronous task is completed



## 阅读文档中的问题

> 不同类型的钩子、不同类型的tap事件之间是如何配合的？

## 参考

[webpack官网，如何写一个webpack插件](https://www.webpackjs.com/contribute/writing-a-plugin/)

[事件钩子的参考](https://www.webpackjs.com/api/compiler-hooks/)

[webpack源码解析](https://juejin.im/post/5c0206626fb9a049bc4c6540)

[tabable解析](https://juejin.im/post/5be90b84e51d457c1c4df852)
