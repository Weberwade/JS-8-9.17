# BOM

# 1. BOM简介

**浏览器对象模型**

+ BOM为我们提供了一组对象，通过这组对象可以完成对浏览器窗口的各种操作
+ BOM对象：
  + Window - 代表浏览器窗口（全局对象）
  + Navigator - 浏览器的对象（可以用来识别浏览器）
  + Location - 浏览器的地址栏信息
  + History - 浏览器的历史纪录（控制浏览器的前进后退）
    + 只能获取浏览器访问过几个网页，不能获取具体网页信息，如何获取具体网页信息就侵犯了用户的隐私
  + Screen - 用户屏幕的信息
+ BOM对象都是作为window对象的属性保存的，所以可以直接在JS中访问这些对象

# 2.BOM对象

+ BOM对象都是作为window对象的属性保存的，访问就以全局形式访问，或者window属性访问

## 2.1 `Navigator`

**Navigator - 浏览器的对象（可以用来识别浏览器）**

### 2.1.1  `Navigator`属性和方法

+ 查询MDN文档
  + [Navigator - Web API 接口参考 | MDN (mozilla.org)](https://developer.mozilla.org/zh-CN/docs/Web/API/Navigator)

+ `navigator.userAgent`属性
  + 一个用的比例较高的属性
  + 返回一个描述浏览器信息的字符串
  + 代码案例
    + 代码太长查看MDN [例子 #1：检测浏览器并返回浏览器名称字符串](https://developer.mozilla.org/zh-CN/docs/Web/API/Window/navigator#例子_1：检测浏览器并返回浏览器名称字符串)

## 2.2 `Location`

**表示的时浏览器的地址栏信息**

+ 可以直接将location的值修改为一个新的地址，这样会使网页发生跳转

### 2.2.1 `Location`属性和方法

#### 2.2.1.1 `location.href`属性

+ 返回当前网页完整地址

#### 2.2.1.2 `location.protocol`属性

+ 获取当前网页的网络协议 

#### 2.2.1.3 `location.pathname`属性

+ 获取当前网页的后缀

**还有很多地址的细致属性、方法，查询MDN文档**

[Location - Web API 接口参考 | MDN (mozilla.org)](https://developer.mozilla.org/zh-CN/docs/Web/API/Location)

#### 2.2.1.4 `location.assign()`方法

+ 和直接修改window.location一样，使网页发生跳转

+ 参数

  + 新的网址

+ `````javascript
  location.assign('https:/www.baidu.com')
  `````

#### 2.2.1.5 `location.replace()`方法

+ 用新网址替换当前网址，替换后无法通过回退按钮回退

+ 参数

  + 新的网址

+ `````javascript
  location.replace('https:/www.baidu.com')
  `````

#### 2.2.1.6 `location.reload()`方法

+ 刷新页面

+ 参数

  + true 表示强制情况网页缓存

+ ````javascript
  location.reload(true)

## 2.3 `history`

浏览器的历史纪录（控制浏览器的前进后退）

### 2.3.1`history`属性和方法

#### 2.3.1.1 `history.back()`方法

+ 网页回退到下一个页面，作用和回退按钮一样

+ ````javascript
  history.back()
  ````

#### 2.3.1.2 `history.forward()`

+ 网页前进上一个页面，作用和前进按钮一样

+ ````javascript
  history.forward()
  ````

#### 2.3.1.3 ` history.go()`

+ 可以向前后跳转，传递正数前进，负数回退 

  + 正1向前跳转一个，正2向前跳转两个，以此类推负值也是

+ ``````
  history.go(-1)



