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
    用到了```javascript compiler.hooks ```，好像是webpack4的写法，之前使用的写法是```javascript compiler.plugin```,使用了make、emit的事件钩子；complier.hooks.emit.tapAsync();

    compiler.hooks.make.tapAsync

    compiler.hooks.compilation.tap


    - copy-webpack-plugin

    > 拷贝资源插件

    ```javascript
        new CopyWebpackPlugin([
            {
                from: path.join(process.cwd(), './vendor/'),
                to: path.join(process.cwd(), './dist/'),
                ignore: ['*.json']
            }
        ])
    ```

- 开始写插件

    
    需要对webpack的原理有一定的了解，具体的了解，异步webpack相关的了解
    

    compiler

    compilation

    Tapable


    例子：

    > 函数写法

    ```javascript
        // 一个 JavaScript 命名函数。
        function MyExampleWebpackPlugin() {

        };

        // 在插件函数的 prototype 上定义一个 `apply` 方法。
        MyExampleWebpackPlugin.prototype.apply = function(compiler{
            // 指定一个挂载到 webpack 自身的事件钩子。
            compiler.plugin('webpacksEventHook', function(compilation /* 处理 webpack 内部实例的特定数据。*/, callback) {
                console.log("This is an example plugin!!!");

                // 功能完成后调用 webpack 提供的回调。
                callback();
            });
        };
    ```

    > 类的写法

    ```javascript
        class MyExampleWebpackPluginClassType{
            apply(compiler){
                 // 指定一个挂载到 webpack 自身的事件钩子。
                compiler.plugin('webpacksEventHook', function(compilation /* 处理 webpack 内部实例的特定数据。*/, callback) {
                    console.log("This is an example plugin!!!");

                    // 功能完成后调用 webpack 提供的回调。
                    callback();
                });
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

tab、tabAsync、tabPromise的区别

Tapable类


## 参考

[webpack官网，如何写一个webpack插件](https://www.webpackjs.com/contribute/writing-a-plugin/)

[事件钩子的参考](https://www.webpackjs.com/api/compiler-hooks/)