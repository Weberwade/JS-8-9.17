# JS入门

## 1、编写区域

JS代码需要编写到script中

1. 可以将JS编写在网页内部的script标签中

   + ``````html
     <!DOCTYPE html>
     <html lang="en">
     <head>
         <meta charset="UTF-8">
         <meta http-equiv="X-UA-Compatible" content="IE=edge">
         <meta name="viewport" content="width=device-width, initial-scale=1.0">
         <title>Document</title>
         <script type="text/javascript">
     
             alert('hh')
     
         </script>
     </head>
     <body>
         
         
     </body>
     </html>
     ``````

   + `type="text/javascript"`可以省略不写，这是默认值

2. 可以将js编写到外部JS文件中，然后通过script标签引入，script标签用来引入就不能写内部脚步，写了也无效，要写内部样式重新写一个script标签

   + `````````html
     <script type="text/javascript" src="./script/script.js"></script>
     `````````

3. 可以将JS代码编写到指定属性中

   + `<button onclick="alert('别烦我')">点我！</button>`
   + `<a href="javascript:alert('123');">超链接</a>`

### 1.1 文档的加载

+ 网页是自上向下加载的，如果将JS代码编写到网页的上边

  + JS代码在执行时，网页还没有加载完毕，这时会出现无法获取到DOM对象的情况

+ 解决这个文档加载顺序问题：

  1. 将script标签编写到body标签最后 （优先级最高）

  2. 将代码编写到window.onload事件的回调函数中

     + window.onload属性会在窗口中的内容加载完毕后才触发

     + `````````````javascript
       window.onload = function(){
          const btn = document.getElementById('btn')
          console.log(btn);
       }

  3. 将代码编写到document对象的DOMContentLoaded的回调函数中

     + document的DOMContentLoaded事件会在当前文档加载完毕后触发

     + ````````javascript
       document.addEventListener('DOMContentLoaded',function(){
           const btn = document.getElementById('btn')
           console.log(btn);
       })
       ````````

     + 执行时机更早

  4. 将代码编写到外部的JS文件中，然后以defer的形式进行引入

     + 在标签中加上defer属性，会等当前文档执行完毕以后才加载

     + 执行时机早于（DOMContentLoaded）

     + ````````````html
       <script defer src="./script/script.js"></script>

## 2、基本语法

### 注释

1. 多行注释 Ctrl + /

   + ```````javascript
     /*     123123        */
     ```````

2. .单行注释 Shift + Alt + a

   + `````````````javascript
     // 123123
     `````````````

3. 注释中的内容会被解释器忽略，可以通过注释来对代码进行解释说明，也可以通过注释来注释掉不想执行的代码

### 区分大小写

+ JS严格区分大小写
  + 小写的函数，用大写调用会报错，严格区分！

### 空格

+ JS中多个空格和换行会被忽略
  + 可以利用这个特点来对代码进行格式化

### 结尾分号

+ JS中每条语句都应该以分号结尾
  + JS中具有自动添加分号的机制，如果不写分号解释器会自动添加

## 3、字面量和变量常量

### 字面量

字面量其实就是一个值，它所代表的含义就是它字面的意思

+ 比如 1 2 3 4 100 ‘hello’ true null .....
+ 在JS中所有的字面量都可以直接使用，但是直接使用字面量并不方便

### 变量

变量可以用来“存储”字面量，并且变量中存储的字面量可以随意修改

+ 通过变量名可以对字面量内容进行描述，并且变量比较方便修改

一个变量只有在=左边才是变量，在=右边时它是值

#### 变量的使用

1. 变量声明 --> let 变量名；
   + 可以同时多个用逗号隔开
2. 变量赋值 --> 变量名 = 变量值;
   + 因为JS是一行一行往下执行的所以可以直接使用同样的变量名修改上面变量的值
3. 声明和赋值同时进行 --> let 变量名 = 变量值;

#### 变量的内存结构

+ 变量中并不存储任何值，而是存储值的内存地址；
+ ![变量的内存结构](D:\学习\超哥JS核心基础\学习源码+笔记\01.JS入门\img\变量的内存结构.png)

### 常量

不可改变的变量叫常量

+ 在JS中，使用const来声明常量,常量只能赋值一次，重复赋值会报错
  + 潜规则 常量名 一般用全大写
  + `const X = 1`
+ 在JS中除了常规的常量外，有一些对象类型的数据我们也会声明为常量

## 4、标识符（起名规则）

在JS中，所有可以由我们自主命名的内容，都可以认为是一个标识符

比如：变量名 函数名 类名...

+ 使用标识符需要遵循如下的命名规划：（不遵循则会报错）
  + 标识符只能含有字母、数字、下划线、$,且不能以数字开头
  + 标识符不能是JS中的关键字和保留字，也不建议使用内置的函数或变量名
  + 命名规范
    + 通常会使用驼峰命名法（变量，函数名）
      + 首字母小写，每个单词开头大写
        + 列如：`maxLength`
    + 类名会使用大驼峰命名法
      + 首字母大写，每个单词开头大写
    + 常量的字母会全部大写(常量可以灵活一些规则)
      + 例如`MAX_LENGTH`

## 5、输出语句

### alert

网页中弹出一个提示框

+ 写法
  + `alert('hellow world')`

###  console.log

在控制台输出一个内容

+ 写法
  + `console.log('hello world')`

### document.write

在网页中输出一个内容

+ 写法
  + `document.write('hellow world')`

## 6、声明语句

### let

用来声明一个变量或者一个函数

### var

用来声明一个变量或者一个函数

### let和var的区别

1. let声明的变量具有块作用域，而var没有块作用域，但是var有函数作用域
   + let在代码块中声明的变量无法在代码块外部访问，而var在代码块外也能访问，所以会出现一些意外的差错不严谨，所以尽量使用let
2. 在全局中使用var声明的变量，都会作为window对象的属性保存，而**let不会**使用let在全局声明的变量不会存储在window，而是存在一个秘密的小地方，确实存在但无法访问
   + 注意！特点window和let中有同一个变量时，会使用let中的变量值，let定义的变量优先级高
3. var具有声明提前，let没有
   + 个人认为var的声明提前没有意义，如果我在声明变量前调用，不如严谨一些给我报错

## 7、代码运行模式

### 7.1 正常模式

+ 默认情况下代码都运行在正常模式中
+ 在正常模式中，语法检查并不严格
  + 原则：能不报错地方尽量不报错
+ 这种处理方式导致代码的运行性能较差

### 7.2 严格模式

+ 在严格模式下，语法检查变得严格
  1. 禁止一些语法
  2. 更容易报错
  3. 提升了性能
+ 开启方式
  + 在任何作用域的开头写上字符串`'use strict'`就开启了严格模式
  + 注意！只在当前作用域有效
+ 在开发中，尽量使用严格模式
  + 这样可以将一些隐藏的问题消灭在萌芽阶段，同时提升代码性能

## 8、使用函数

### 8.1 prompt()

获取用户输入的内容

+ 它会将用户输入的内容以字符串的形式返回，可以通过变量来接受

### 8.2 isNaN()

检查函数是否是NaN

