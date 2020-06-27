---
layout: post
title: Javascript数据类型
categories: [前端]
description: 解决数据类型类型转换中的问题
keywords: 前端  Javascript
---

<h1 align="center" >数据类型转换</h1>

运算符与函数会将赋给他们的值，转换为正确的类型；比如

1. `alert`会将任何值转换为字符串

2. 算术运算符会将值转换为数字


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

- null与undefined的区别

  1. `null`代表一个无、空、值未知的`特殊值`;
  2. `undefined`已被声明，但`未赋值`;
  3. 可以为所有变量赋`undefined`,但不建议；
  4. `undefined`用于检验变量是否被赋值
  


### 类型转换（垃圾转换）

  - 转数字

    - 方法

      这里说的是`隐式转换`以及`Number()`

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
      
      2. `""+value....`等其他的隐式转换，比如alert


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
        `空字符串`(字符串类型,剩余的字符串都会转为true,比如`'false'`), 
        `false`（布尔类型）, 
        `undefined`, 
        `null`;

      true: 剩余的数据类型，包括Symbol;

  - 转BigInt

    - 方法

      `BigInt()`
    
    - 规则

      - 数值： `1` -> `1n`

      - 字符串：  符合规则的正常转换 `'11'` -> `11n`;

      - Boolean: `true`->`1n`, `false` -> `0n`

      - undefined: `error`

      - null: `error`

      - Symbol: `error`
          

### 对象的类型转换

  > 规则：

  1. 第一步，obj[Symbol.toPrimitive](hint)

      hint的值：

      1. string
      2. number
      3. default（少数运算符比如`+`, `==`不是`===`）

        当运算符不确定转换为哪种类型时，走default;

      ```javascript

        let user = {
          name: "John",
          money: 1000,

          [Symbol.toPrimitive](hint) {
            alert(`hint: ${hint}`);
            return hint == "string" ? `{name: "${this.name}"}` : this.money;
          }
        };

        // 转换演示：
        alert(user); // hint: string -> {name: "John"}
        alert(+user); // hint: number -> 1000
        alert(user + 500); // hint: default -> 1500
      
      ```

  2. 如果没有`Symbol.toPrimitive`方法，如果hint为`string`(转换为`string`) 
      
      先obj.toString()、后obj.valueOf();
      先在obj上查找toString、valueOf;再去查找`Object.prototype.toString`, `Object.prototype.valueOf`,下面也是一样的

  3. 如果没有`Symbol.toPrimitive`方法，如果hint为`number`或者`default`(除了Date) 
  
      先obj.valueOf()，再obj.toString();
  
  4. 上面是主要的顺序规则，4、5是另外一些转换规则
      
    valueOf、toString返回一个对象，不会报错，会被忽略（就像这种值不存在）；

  5. Symbol.toPrimitive返回对象会报错，只能返回一个`原始值`;

  > 默认转换使用的是Object上的方法：
    
  使用`Object.valueOf`与`Object.toString`，所有对象都会用到Object上的这两个方法；
      
  因为valueOf会返回对象，所以转换的时候一般都是使用的`toString()`,Object.toString()进行兜底-_-!!;

  可以自定义`valueOf`与`toString`进行截取;

  Object.toString: `'[object object]'`;

  Object.valueOf: 指向对象本身


  ```javascript

      let user = {name: "John"};

      alert(user); // [object Object]

      alert(user.valueOf() === user); // true
  
  ```


  > 实际使用

  给对象添加`obj.toString()`给所有的转换,这个方法会截断访问Object上的方法



      
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

    Object是所有引用数据类型的父元素；试着用instance判断其他的引用类型，比如JSON等；

2. 常用的引用类型?
    对象、数组、函数；

3. 本地对象、内置对象、宿主对象分别是什么？

    宿主对象：BOM对象与DOM对象
    内置对象：内置对象属于本地对象，目前规定的内置对象有Math、Global、Date;
    本地对象：除了宿主对象的所有对象；

4. 隐式转换的规则是什么？

### 参考

[标准内置对象](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects)

[JavaScript 数据类型和数据结构](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Data_structures)