---
title: Js 新特性
---
以下特性处于ECMAScript标准的state 3或者stage 4，这意味着很快会被浏览器或者其他引擎支持
### 类的私有变量： #符号表示类的私有变量
    `class Couter {
      #n = 0;
      #add() {
        this.#n++;
      }
      onClick() {
        this.#add();
      }
    }
    const c = new Counter();
    c.onClick(); //ok
    c.#add(); //error`
### 可选链操作符： ?.
   使用：可以方便获取嵌套多层的对象属性，表示很激动：
   原用法：`let deepProp = obj && obj.children && obj.label`
   现在可以这么写： `let deepProp = obj?.children?.label;`
   如果obj或者obj.children是null或者undefined，表达式就会短路计算直接返回undefined。
### 空位合并操作符（nullish）： ??
  使用场景：变量如果是空值，就是用默认值。
  原用法：let v = a ? a : b；或者 let v = a|| b;
  弊端： 如果a是 0, '', false这些可能的有效输入，就会被覆盖而取b的值；
  现用法： let n = a ?? b; 表示a为null || undefined时才设置默认值。
  等价于： `let n = a !== undefined && a !== null ? a : b;`
  
### BigInt： 6123n | BigInt(6123 || '6123')
  处理大整数计算时精度丢失的问题
  `BigInt(66) // 66n
  const bi = BigInt(66) 
  typeof(bi) //"bigint"
  typeof 66  //number
  typeof(66n) //"bigint"`
  
  可以比较bigint和number，但不能运算
  `1n < 2  // true
  1n + 2  // Uncaught TypeError: Cannot mix BigInt and other types, use explicit conversions
  1n - 1n  //0n`
  
### static字段，用在Class中表示静态变量
### 顶层await
  ES（2017） ES8用法： aysnc await搭配使用在函数内
  现：允许在顶层使用，简化动态模块加载的过程
   `const data = await import('/remote/module');`
   在浏览器控制台调试异步模块非常方便：
   `res = await fetch('https://github.com') 
   //Response {type: "basic", url: "https://github.com/", redirected: false, status: 200, ok: true, …}`