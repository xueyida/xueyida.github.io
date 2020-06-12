---
layout: post
title: Javascript数据类型
categories: [前端]
description: 解决数据类型类型转换中的问题
keywords: 前端  Javascript
---

<h1 align="center" >数据类型转换</h1>


### 数据类型

- 基本数据类型

  1. Number
  2. String
  3. Boolean
  4. Undefined
  5. Null
  6. Symbol
  7. BigInt(ES2020)

      `不能与Number进行换算`；

- 引用数据类型

  指的是内存中的可以被`标识符`引用的一块区域；除了上面的数据类型，其余的都是引用数据类型；
  
### 内置对象的分类

  - 值属性
    - Infinity (`typeof Infinity` === `number`)
    - NaN (`typeof NaN` === `number`)
    - undefined ( `typeof undefined` === `undefined`)
    - null (`typeof null` === `object`)
    - globalThis 
      提供了标准的方式来获取不同环境下的全局`this`对象

  - 函数属性
  - 基本对象
  - 数字和日期对象
  - 字符串
  - 可索引的集合对象
  - 使用键的集合对象
  - 结构化数据
  - 控制抽象对象
  - 反射
  - 国际化
  - WebAssembly
  - 其他
    arguments  

  


### 类型转换（垃圾转换）

  - 转数字

    - 方法

      1. `Number()`
      2. `parseInt()`
      3. `parseFloat()`

    - 规则
      
      - 数字： 除了NaN转为NaN,其余正常转换

      - 字符串 : 符合规则的转为数字

      - Boolean: `true`->`1`,`false`->`0`

      - null : 0

      - undefined： NaN

      - Symbol： 报错

      - BigInt： 正常转换

      - 数组: `[1]`/`[]`转换成功，转换为1/0；`['a']`/`[1, 2]`转换失败

      - 除数组的引用数据类型: NaN


  - 转字符串

    - 方法

      1. `String()`
      2. `value.toString()`
      3. `""+value`

    - 规则

      1. 布尔： `true`->`'true'`, `false`->`'false'`
      2. 数字： `123`->`'123'`
      3. null: `null` -> `'null'`
      4. undefined: `'undefined'`
      5. Symbol: `'Symbol(1)'`
      6. BigInt: `34n` -> `"34"`
      7. 引用数据类型
          数组：`[2,3]` -> `'2,3'`
          对象：`{a:1}` -> `'[object, object]'` 
          函数：`function a() {}` -> `'function a(){}'`
    
    - 例子

      1. 1 + '2' = 12;
      2. 对象转换为字符串


  - 转布尔

    - 转Boolean的方法

      `Boolean()`

    - 规则

      false: 
        `0`, `-0`, `NaN`（数字类型）, 
        `0n`, `-0n`（BigInt类型）,
        `空字符串`(字符串类型), 
        `false`（布尔类型）, 
        `undefined`, 
        `null`;

      true: 剩余的数据类型，包括Symbol;
      
### 类型判断

#### typeof

1. undefined： `undefined` -> `'undefined'`
2. null: `null` -> `'object'`
3. 数字: `1` -> `'number'`
4. 字符串: `'123'` -> `'string'`
5. BigInt: `2n` -> `'bigint'`
6. Symbol: `Symbol(2)` -> `'symbol'`
7. 引用数据类型

    - 函数：`function a(){}` -> `'function'`
    - 对象： `{}` -> `'object'`
    - 数组： `[]` -> `object`

#### instance

  判断引用数据类型


### 问题

1. 各种引用数据类型之间的区别是什么？

    Object是所有引用数据类型的父元素；试着用instance判断其他的引用类型，比如Json等；

2. 常用的引用类型?
    对象、数组、函数；

3. 本地对象、内置对象、宿主对象分别是什么？

  宿主对象：BOM对象与DOM对象
  内置对象：内置对象属于本地对象，目前规定的内置对象有Math、Global;
  本地对象：除了宿主对象的所有对象；

### 参考

[标准内置对象](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects)

[JavaScript 数据类型和数据结构](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Data_structures)