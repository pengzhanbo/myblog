---
title: es6学习笔记（一）
tags: ['笔记','es6']
date: 2016-03-09 16:25:21
---
学习es6也有一段时间，但一直没有去整理成相应的笔记做总结记录，这两天刚好用 `hexo` 搭建了一个个人博客，那么就开始做整理笔记吧！
<!-- more -->
***
### 1. let  命令
##### 基本用法
  ES6新增 `let` 命令，用以声明变量。用法类似于 `var` ，但所声明的变量，仅在 `let` 所在的代码块内有效。
``` javascript
{
   let a = 1;
   var b = 2;
}
console.log(a);   //ReferenceError: a is not defined.
console.log(b);  // 2
```
##### 不存在变量提升
```
console.log(a);  // undefined
console.log(b); //  ReferenceError
var a = 1;
let b = 2; 
```
上面代码中，变量 `a` 用 `var` 声明，会发生变量提升，即在脚本开始运行时，变量 `a`就已经存在了，但是没有值，所以输出`undefined` 。 变量 `b` 用 `let` 声明，不存在变量提升，这表明在变量声明之前，变量 `b` 是不存在的，如果这时调用到变量`b`，则会抛出错误。

##### 暂时性死区
只要块级作用域内存在 `let` 命令，它所声明的变量就“绑定”这个区域，不再受外部的影响。
```  javascript
var a = 1;
if(true){
  a = 2;  // ReferenceError
  let a;
}
```
上面代码中，存在全局变量 `a` ，但是块级作用域内 `let` 又声明了一个局部变量 `a` ，导致后者绑定这个块级作用域，所以在 `let` 声明变量前，对 `a` 赋值会报错。
ES6明确规定，如果区域中存在 `let` 和 `const` 命令，这个区域对这些命令声明的变量，从一开始就形成了封闭作用域。凡是在声明之前就使用这些变量，就会报错。
在代码块内，使用   `let` 命令声明变量之前，该变量都是不可用的。在语法上，称为“暂时性死区（temporal dead zone，简称TDZ）”。
***

ES6规定暂时性死区和不存在变量提升，主要是为了减少运行时错误，防止在变量声明前就使用这个变量，从而导致意料之外的行为。这样的错误在ES5中很常见，现在有了这种规定，避免此类错误就很容易了。

****

#### 不允许重复声明
`let` 不允许在同一作用域内，重复声明同一个变量
``` javascript
//报错
function fn(){
  let a = 0;
  var a = 1;
}

//报错
function fn(){
  let a = 1;
  let a = 2;
}
``` 
因此，不能在函数内部重新声明参数
``` javascript
//报错
function fn(arg){
  let arg;
}
//不会报错
function fn(arg){
  {
    let arg;
  }
}
```

### 2. const 命令
`const` 声明的是常量，一旦声明，常量的值就不可改变
``` javascript
const PI = 3.14;
console.log(PI);  // 3.14

PI=3;  //赋值无效，常规模式下不会报错
```
`const` 声明的变量不得改变值，这意味着，一旦声明变量，就需要立刻给变量赋值
``` javascript
'use strict'
const a;   // SyntaxError: missing = in const declaration
```
`const` 声明的变量，在严格模式下，会报错，在常规模式下虽然不会报错，但之后也无法重新赋值。
****
*****

### 3. 块级作用域

 ******
****