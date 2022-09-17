# DOM

# 1.DOM简介

[DOM – 李立超 | lilichao.com](https://www.lilichao.com/index.php/2022/08/09/dom/)

[DOM 概述 - Web API 接口参考 | MDN (mozilla.org)](https://developer.mozilla.org/zh-CN/docs/Web/API/Document_Object_Model/Introduction)

简介就不写笔记了，在MDN和超哥的文档中都可以查询，超哥的说的通俗一点，但是没有那么深，MDN则更传统更深层

**DOM中所有的对象的原型链上一定有Node类**

# 2.如何使用DOM

+ 使用DOM来操作网页，我们需要浏览器至少得先给我一个对象，让我去访问DOM对象才能去完成各种操作
  + 所以浏览器给了我们一个document对象，document代表整个网页所以可以通过document的方法去获取网页中的元素对象等

# 3.document对象

1. document对象代表的是整个网页
2. document对象的原型链
   + HTMLDocument -> Document -> Node -> EventTarget -> Object 
3. 凡是在原型链上存在的对象的属性和方法都可以通过document去调用
4. document对象是全局对象，可以直接调用

# 4.节点

## 4.1 文档节点

### 4.1.1 获取文档节点的属性

+ 一小部分常见的文档节点属性，需要更多查询MDN文档 

1. document.documentElement --> html根元素
2. document.head --> head元素
3. document.title --> title元素
4. document.body --> body元素
5. document.links --> 获取页面中所有的超链接

## 4.2 元素节点（element）

+ 在网页中，每一个标签都是一个元素节点

### 4.2.1 如何获取元素节点对象？

1. 通过document对象来获取已有的元素节点
2. 通过document对象来创建没有的元素节点

### 4.2.2 `document`获取元素节点方法

#### 4.2.2.1 `document.getElementById()`

+ 通过ID属性值获取一个元素对象节点，并将获取到的对象通过返回值返回

+ `````````````````html
  <button id="btn"></button>
  <script>
  const btn = document.getElementById('btn')
  </script>

#### 4.2.2.2 `document.getElementsByClassName()`

+ 根据元素的class属性值获取一组元素节点对象

+ 该方法返回的结果是一个实时的集合，当网页中新添加元素时，集合也会实时的刷新

+ 该方法返回值是一个类数组对象，可以遍历，但是不能使用数组的方法

  + 因为返回的是一个类数组对象，所以也不能直接使用返回的对象，通过索引找到需要修改的class元素进行修改

+ `````````````html
  <button class="b1"></button>
  <button class="b1"></button>
  <button class="b1"></button>
  <button class="b1"></button>
  <script>
       const b1 = document.getElementsByClassName('b1')
       for(let i = 0 ; i < b1.length ;i++){
          b1[i].innerHTML = 'Click Me'
       }
  </script>
  `````````````

#### 4.2.2.3 `document.getElementsByTagName()`

+ 根据标签名获取一组元素节点对象

+ 该方法返回的结果是一个实时的集合，当网页中新添加元素时，集合也会实时的刷新

+ 该方法返回值是一个类数组对象，可以遍历，但是不能使用数组的方法

  + 因为返回的是一个类数组对象，所以也不能直接使用返回的对象，通过索引找到需要修改的class元素进行修改

+ ``````````````````html
  <button id="btn"></button>
  <button class="b1"></button>
  <button class="b1"></button>
  <button class="b1"></button>
  <button class="b1"></button>
  <script>
  const b1 =document.getElementsByTagName('button')
      for(let i = 0 ; i < b1.length ;i++){
          b1[i].innerText = 'Click Me' + i
      }
  </script>
  ``````````````````

+ 该方法的参数还可以传递一个*号，会拿取页面中所有的元素节点

  + `const b1 =document.getElementsByTagName('*')`

#### 4.2.2.4 `document.getElementsByName()`

+ 根据name属性获取一组元素节点对象

+ 主要是用于表单，一般只有表单项才会使用name

+ 该方法返回的结果是一个实时的集合，当网页中新添加元素时，集合也会实时的刷新

+ 该方法返回值是一个类数组对象，可以遍历，但是不能使用数组的方法

  + 因为返回的是一个类数组对象，所以也不能直接使用返回的对象，通过索引找到需要修改的class元素进行修改

+ `````html
  <button name="b1"></button>
  <button name="b1"></button>
  <button name="b1"></button>
  <button name="b1"></button>
  <button name="b1"></button>
  <script>
  const b1 = document.getElementsByName('b1')
  for(let i = 0 ; i < b1.length ;i++){
      b1[i].innerText = 'Click Me' + i
  }

#### 4.2.2.5 `document.querySelectorAll()`

+ 根据CSS选择器去页面中查询元素
+ 不会实时更新！

+ 该方法返回值是一个类数组对象，可以遍历，但是不能使用数组的方法

  + 因为返回的是一个类数组对象，所以也不能直接使用返回的对象，通过索引找到需要修改的class元素进行修改

+ `````````````html
  <div>
    <div></div>
  </div>
  <div>
    <div></div>
  </div>
  <div></div>
  <div></div>
  
  <script>
  const div2 = document.querySelectorAll('div > div')
  for (let i = 0; i < div2.length; i++) {
      div2[i].innerText = 'Click Me' + i
  }
  </script>

#### 4.2.2.6 `document.querySelector()`

+ 根据CSS选择器去页面中查询第一个符合条件的元素 

+ ````````html
  <div>2</div> // 1
  <div>2</div> // 2
  <div>2</div> // 2
  <div>2</div> // 2
  <script>
     const div2 = document.querySelector('div')
     div2.innerText = '1'
  </script>
  ````````

### 4.2.3 创建一个元素节点

#### 4.2.3.1 `document.createElement()`

+ 根据标签名创建一个元素节点对象

+ 创建的元素节点，需要通过添加才能添加到网页中，不会创建就直接添加到网页中

+ ````````````html
  const h2 = document.createElement('h2')
  h2.innerText = '1'
  console.log(h2); // <h2>1</h2>

### 4.2.4 元素节点的原型链

+ 每一种元素标签的第一层元素节点都是不一样的，例如div标签的第一层是HTMLDivElement，所以元素标签用xxx代替
+ xxx元素节点的原型链如下：
  + HTMLxxxElement --> HTMLElement --> Element --> node --> EventTarget --> Object

### 4.2.5 元素节点获取其他节点

+ Document中获取节点的一些方法，在元素节点中也存在此类方法，在元素节点调用就只会在自身的后代中进行查询

  + 如`getElementsByTagName()`等... 这类方法都是存在的，只是缩小了查询范围

#### 4.2.5.1 `element.childNodes`

+ 获取当前元素的**子节点**（会包含文本节点和空白的文本节点）

+ ``````html
  <div id="box1">
    我是box1
    <span class="s1">我是s1</span>
    <span class="s1">我是s1</span>
  </div>
  <script>
  const box1 = document.getElementById('box1')
  const cns = box1.childNodes // NodeList(5) [text, span.s1, text, span.s1, text]
  </script>
  ``````

#### 4.2.5.2 `element.children`

+ 获取当前元素的**子元素**（只会获取元素节点）

+ ```````````html
  <div id="box1">
    我是box1
    <span class="s1">我是s1</span>
    <span class="s1">我是s1</span>
  </div>
  <script>
  const box1 = document.getElementById('box1')    
  const cns = box1.childNodes // HTMLCollection(2) [span.s1, span.s1]
  </script>
  ```````````

#### 4.2.5.3 `element.firstChild`

+ 获取第一个子节点（任何节点都会被获取），会获取空白文本节点所以特别实用！

+ ````````````html
  <div id="box1">
    我是box1
    <span class="s1">我是s1</span>
    <span class="s1">我是s1</span>
  </div>
  <script>
  const box1 = document.getElementById('box1')
  console.log(box1.firstChild); // 空白的文字节点
  </script>
  ````````````

#### 4.2.5.4  `element.firstElementChild`

+ 获取第一个元素节点

+ ```````html
  <div id="box1">
    我是box1
    <span class="s1">我是s1</span>
    <span class="s1">我是s1</span>
  </div>
  <script>
  const box1 = document.getElementById('box1')
  console.log(box1.firstElementChild); // span.s1
  </script>
  ```````

#### 4.2.5.5`element.lastElementChild`

+ 获取最后一个元素节点

+ `````````````html
  <div id="box1">
    我是box1
    <span class="s1">我是s1</span>
    <span class="s1">我是s1</span>
  </div>
  <script>
  const box1 = document.getElementById('box1')
  console.log(box1.lastElementChild); // span.s1
  </script>
  `````````````

#### 4.2.5.6 `element.nextSibling`

+ 获取元素节点的下一个兄弟节点（任何节点包含文本空白节点）不实用

+ ```````````````html
  <div id="box1">
      我是box1
      <span class="s1">我是s1</span>
      <span class="s1">我是s1</span>
  </div>
  <script>
  const box1 = document.getElementById('box1')
  const text = box1.nextSibling
  console.log(text); //#text
  </script>

#### 4.2.5.7 `element.nextElementSibling`

+ 获取元素节点的下一个兄弟元素节点

+ ```````html
  <div id="box1">
      我是box1
      <span class="s1">我是s1</span>
      <span class="s1">我是s1</span>
  </div>
  <script>
  const box1 = document.getElementById('box1')
  const text = box1.nextElementSibling
  console.log(text); // span.s1
  </script>

#### 4.2.5.8 `element.previousSibling`

+ 获取元素节点的上一个兄弟节点（任何节点包含文本空白节点）不实用

+ ``````````````html
  <div id="box1">
      我是box1
      <span class="s1">我是s1</span>
      <span class="s1">我是s1</span>
  </div>
  <script>
  const box1 = document.getElementById('box1')
  const text = box1.previousSibling
  console.log(text); //#text
  </script>

#### 4.2.5.9 `element.previousElementSibling`

+ 获取元素节点的上一个兄弟元素节点

+ ``````````html
  <div id="box1">
      我是box1
      <span class="s1">我是s1</span>
      <span class="s1">我是s1</span>
  </div>
  <script>
  const box1 = document.getElementById('box1')
  const text = box1.previousElementSibling
  console.log(text); // null
  </script>
  ``````````

#### 4.2.5.10 `element.parentNode`

+ 获取该元素节点的父节点（可以获取到document）

+ `````html
  <body>
  <div id="box1">
      我是box1
      <span class="s1">我是s1</span>
      <span class="s1">我是s1</span>
  </div>
  <script>
  const box1 = document.getElementById('box1')
  const text = box1.parentNode
  console.log(text); // body
  </script>
  </body>
  `````

#### 4.2.5.11 `element.parentElement`

+ 获取该元素节点的父元素节点（获取到html为止，再获取返回null）

+ `````````html
  <body>
  <div id="box1">
      我是box1
      <span class="s1">我是s1</span>
      <span class="s1">我是s1</span>
  </div>
  <script>
  const box1 = document.getElementById('box1')
  const text = box1.parentElement
  console.log(text); // body
  </script>
  </body>
  `````````

#### 4.2.5.12 `element.tagName`

+ 获取当前元素的标签名

+ ```````html
  <div id="box1">
      我是box1
      <span class="s1">我是s1</span>
      <span class="s1">我是s1</span>
  </div>
  <script>
  const box1 = document.getElementById('box1')
  const text = box1.tagName
  console.log(text); // DIV
  ```````

### 4.2.6 元素节点添加节点方法

#### 4.2.6.1 `element.appendChild()`

+ 用于给一个节点添加子节点

+ `````````````javascript
  const btn = document.getElementById('btn')
  const list = document.getElementById('list')
  btn.addEventListener('click',function(){
       const li = document.createElement('li')
       li.innerText = '唐僧'
       li.id = 'ts'
       list.appendChild(li)
  })
  `````````````

#### 4.2.6.2 `element.insertAdjacentElement()`

+ 向元素的任意位置添加元素

+ 参数

  1. 添加元素的位置
     1. afterbegin 在开始标签后面添加元素
     2. afterend 在结束标签的后面添加元素 （后面的兄弟元素）
     3. beforebegin 在开始标签的前面添加元素 （前面的兄弟元素）
     4. beforeend 在结束标签前面添加元素
  2. 添加的元素

+ ````````javascript
  const btn = document.getElementById('btn')
  const list = document.getElementById('list')
  btn.addEventListener('click',function(){
      const li = document.createElement('li')
      li.innerText = '唐僧'
      li.id = 'ts'
      list.insertAdjacentElement("beforeend",li)
  })
  ````````

#### 4.2.6.3 `element.insertAdjacentHTML()`

+ 可以直接用来向网页指定位置添加HTML代码

+ 网页中有用户添加的内容，带HTML的方法都不推荐！容易被攻击

+ 参数

  1. 添加元素的位置
     1. afterbegin 在开始标签后面添加元素
     2. afterend 在结束标签的后面添加元素 （后面的兄弟元素）
     3. beforebegin 在开始标签的前面添加元素 （前面的兄弟元素）
     4. beforeend 在结束标签前面添加元素
  2. 添加的元素

+ ````````````````javascript
  const btn = document.getElementById('btn')
  const list = document.getElementById('list')
  btn.addEventListener('click',function(){
  list.insertAdjacentHTML("beforeend","<li id='bgj'>白骨精</li>")
  })
  ````````````````

### 4.2.7 元素节点替换方法

#### 4.2.7.1 `element.replaceWith()`

+ 用一个元素节点替换一个元素节点

+ 参数

  + 新的元素节点

+ ```````````````javascript
  const btn2 = document.getElementById('btn2')
  btn2.onclick = function(){
       //创建一个蜘蛛精替换孙悟空
       const li = document.createElement('li')
       li.innerText = '蜘蛛精'
       li.id = 'zzj'
       // 获取ssw
       const swk = document.getElementById('swk')
       swk.replaceWith(li)
  }
  ```````````````

### 4.2.8 元素节点删除方法

#### 4.2.8.1 `element.remove()`

+ 删除一个元素节点

+ ```````````javascript
  const btn2 = document.getElementById('btn2')
  btn2.onclick = function(){
      //创建一个蜘蛛精替换孙悟空
      const li = document.createElement('li')
      li.innerText = '蜘蛛精'
      li.id = 'zzj'
      // 获取ssw
      const swk = document.getElementById('swk')
      swk.remove()
  }
  ```````````

### 4.2.9 元素节点复制方法

#### 4.2.9.1 `element.cloneNode()`

+ 复制一个元素节点的方法

+ 它会复制节点的所有特点包含属性

+ 这个方法默认只会复制当前节点，而不会复制节点的子节点

+ 参数

  + true 修改默认值使方法深拷贝，会将元素的子节点一起复制返回
  + false 默认值 浅拷贝 只复制当前节点

+ ```````````javascript
  // 点击按钮后， id l1 元素添加到list2中
  const btn1 = document.getElementById('btn1')
  const list2 = document.getElementById('list2')
  const l1 = document.getElementById('l1')
  btn1.onclick = function(){
       const newL1 = l1.cloneNode(true)
       console.log(newL1);
       newL1.id = 'newL1'
  	 list2.appendChild(newL1)
  }

## 4.3 文本节点

+ 在DOM中，网页中所有的文本内容都是文本节点对象，可以通过元素来获取其中的文本节点对象，但是我们通常不会这样做，这样做更麻烦了
  + 我们可以直接通过元素修改其中的文本内容

### 4.3.1 通过元素修改文本

+ 常用的三个通过元素修改文本的三个属性

#### 4.3.1.1 `element.textContent`

+ 获取或修改元素中的文本内容（可以获取到空白文本，读取不到标签）
+ 不赋值可以获取到文本内容
+ 赋值可以修改文本内容（如果将标签当作内容修改进元素，会自动被转义变成文本内容）

+ `````````````html
  <div id="box1">我是div</div>
  <script>
  const box1 = document.getElementById('box1')
  const text = box1.firstChild
  box1.textContent = '123' 
  console.log(text); // '123'
  </script>
  `````````````

+ 注意！textContent获取的是标签中的内容，不会考虑css样式

+ 列如

  + ````````html
    <div id="box1" style="display:none;">我是div</div>
    <script>
    const box1 = document.getElementById('box1')
    console.log(box1.textContent);
    ````````

  + 文字明明被隐藏了，但是通过textContent还是可以获取到内容

#### 4.3.1.2 `element.innerText`

+ 获取或修改元素中的文本内容（不获取空白文本也不读取标签）

+ 不赋值可以获取到文本内容

+ 赋值可以修改文本内容（如果将标签当作内容修改进元素，会自动被转义变成文本内容）

+ ````````````html
  <div id="box1">我是div</div>
  <script>
  const box1 = document.getElementById('box1')
  box1.innerText ='123'
  const text = box1.firstChild
  console.log(text);
  </script>
  ````````````

+ 注意！innerText获取内容时，会考虑css样式

+ 例如

  + ````html
    <div id="box1" style="display:none;">我是div</div>
    <script>
    const box1 = document.getElementById('box1')
    console.log(box1.innerText); // ''
    </script>
    ````

  + 通过innerText去读取css样式，会触发网页的重排（计算css样式）

#### 4.3.1.3 `element.innerHTML`

+ 获取或修改元素中的HTML代码（获取空白也获取标签）

+ 不赋值可以获取到所有内容

+ 赋值会修改元素中的所有内容（标签不会被转义，会成为html标签）

+ 可以理解为innerHTML可以直接向元素中添加HTML代码，而innerText和textContent都不行

+ 注意！用innerHTML插入内容时，有被xss注入的风险

+ ````````html
  <div id="box1">我是div</div>
  <script>
  const box1 = document.getElementById('box1')
  box1.innerHTML='<li>"159"</li>' // 变成li标签159
  </script>
  ````````

## 4.4 属性节点

+ 属性节点（Attr）
  + 在DOM也是一个对象，通常不需要获取对象而是直接通过元素即可完成对其的各种操作

### 4.4.1 如何操作属性节点

1. 通过对象属性的方式（简单且常用）

   1. 先获取到元素，然后通过元素寻找属性

   2. 读取方式：元素.属性名(注意！class属性需要使用className属性来读取)

      + 读取一个布尔值时，会返回true或false

   3. 修改方式：元素.属性名 = 新属性值

   4. `````html
      <input type="text" name="uearname">
      <script>
      const inp = document.querySelector('input')
      console.log(inp.name); // 'uearname'
      inp.name = '159'
      console.log(inp.name); // '159'
      </script>
      `````

2. 通过对象方法的方式

   1. 先获取到元素，然后通过元素寻找属性

   2. 读取方式：元素.getAttribute(’属性名‘)（注意！class在方法中就使用class即可，不需要通过className读取）

   3. 修改方式：元素.setAttribute(属性名,属性值)

   4. ``````html
      <input type="text" name="uearname">
      <script>
      const inp = document.querySelector('input')
      console.log(inp.getAttribute('name')); // 'uearname'
      inp.setAttribute('name','159')
      console.log(inp.getAttribute('name')); // '159'
      </script>
      ``````

      + 注意！setAttribute()方法一定要传两个参数，不然会报错
      + 如果不需要属性可以通过`元素removeAttribut('属性名')`将属性删除

# 5.事件

+ 事件（event）
  + 事件就是用户和页面之间发生的交互行为
    + 如：点击按钮、鼠标移动、双击按钮、敲击键盘、松开按键...
  + 通过为事件绑定响应函数（回调函数），来完成和用户之间的交互

## 5.1 绑定响应函数的方法

+ 在事件的响应函数中，响应函数绑定给谁this就是谁（箭头函数除外）

### 5.1.1 直接在元素标签属性中设置

+ ``````````````html
  <button id="btn" onclick="alert('哎呀你干嘛~~~~~~')">点我！</button>
  ``````````````

### 5.1.2 通过为元素的指定属性设置回调函数绑定事件

+ ```````````javascript
  const btn = document.getElementById('btn')
  btn.onclick = function(){} 
  ```````````

+ 想要触发什么事件，就绑定什么事件，当事件触发以后为事件绑定的函数会调用

  + 这个为事件绑定的函数就是响应函数，事件触发函数调用

+ 元素属性绑定事件的方式同一事件只能绑定一个响应函数，再次绑定响应函数将会覆盖前面的响应函数

### 5.1.3 通过元素对象节点的addEventListener()方法来绑定事件

+ ````````````````javascript
  const btn = document.getElementById('btn')
  btn.addEventListener('click',function(){})
  ````````````````

+ `addEventListener()`方法（推荐方法）

  + 第一个参数是需要绑定的事件
  + 第二个参数是事件触发的响应函数

+ 通过元素对象节点`addEventListener()`方法，可以多次为重复的事件绑定响应函数，每一次绑定的函数都不会被覆盖，会被执行调用

## 5.2 取消事件默认行

### 5.2.1 ` return false`

+ 使用`return`来结束响应函数，告诉事件到这里为止，后面都不要执行了包括默认事件
+ `return false`局限
  + 只能用于xxx.xxx = function(){}的形式的响应函数
  + 对于`addEventListener()`方法绑定的形式不起作用

### 5.2.2 `event.preventDefault()`

+ 取消事件的默认行为
  + 如超链接的跳转等..
+ 与on绑定的事件响应函数中的return false效果一致，但是适用于所有的事件绑定方式

## 5.3 事件冒泡（bubble）

+ 事件的冒泡就是指事件的向上传导，当元素上的某个事件被触发后，其祖先元素上的相同事件也会同时被触发
+ 冒泡的存在大大的简化了代码的编写`，但是在一些场景下我们并不希望冒泡存在
+ 事件的冒泡和元素的样式无关，只和结构相关

### 5.3.1 取消事件冒泡

+ 不希望事件冒泡时，可以通过当前响应函数的事件对象来取消冒泡

+ ``````````html
  <div id="box1">
       <div id="box2"></div>
  </div>
  <script>
  const box1 = document.getElementById('box1')
  const box2 = document.getElementById('box2')
  box1.addEventListener('click', event => {
     event.stopPropagation()
     alert('159')
  })
  box2.addEventListener('click', event => {
      event.stopPropagation()
      alert('159')
  })
  ``````````

## 5.4 事件委派

+ 通过事件冒泡的属性来完成事件的委派

+ 将本该绑定给多个元素的事件，统一绑定给共同父元素（一般绑定给document），再判断触发事件元素是否要进行事件，再通过事件冒泡的属性让元素来完成事件，这样可以降低代码复杂度方便维护

+ `````html
  <button id="btn">点我一下</button>
  <hr>
  <ul id="list">
      <li><a href="javascript:;">连接一</a></li>
      <li><a href="javascript:;">连接二</a></li>
      <li><a href="javascript:;">连接三</a></li>
      <li><a href="javascript:;">连接四</a></li>
  </ul>
  <script>
      const list = document.getElementById('list')
      const btn = document.getElementById('btn')
      const links = list.getElementsByTagName('a')
      // 将事件绑定给document再判断元素是否执行事件
  document.addEventListener("click", function (event) {
      let arrA = [...links]
       if (arrA.includes(event.target)) {
           alert(event.target.innerText);
       }
  })
  btn.addEventListener("click", event => {
       list.insertAdjacentHTML("beforeend",
       "<li><a href='javascript:;'>新超链接</a></li>")
  })
  </script>
  `````

## 5.5 事件捕获（事件传播机制）

事件捕获（事件传播机制）

+ 在DOM中，事件的传播可以分为三个阶段：
  1. 捕获阶段（由祖先元素向目标元素进行事件的捕获）（默认情况下，事件不会在捕获阶段触发）
  2. 目标阶段（事件触发对象）
  3. 冒泡阶段（由目标元素向祖先元素进行事件冒泡）
+ 一般情况下我们不希望事件在捕获阶段触发，所以通常都不需要设置第三个参数
  + 在捕获阶段中如果有停止传导的`event.stopPropagation()`甚至你点的元素对象都没有执行响应函数事件的捕获就结束了

### 5.5.1 事件捕获简介

+ 事件的捕获，指事件从外向内的传导
  + 当前元素触发事件以后，会先从当前元素最大的祖先元素开始向当前元素开始进行事件的捕获
  + 默认情况下，事件不会在捕获阶段触发

### 5.5.2 如何捕获阶段触发事件

**如果希望在捕获阶段触发事件，可以将addEventListener的第三个设置为true**

## 5.6 查询事件触发的阶段

### 5.6.1 `event.eventPhase`属性

+ 表示事件触发的阶段
+ 返回值代表的阶段
  + 1表示捕获阶段
  + 2表示目标阶段
  + 3表示冒泡阶段

# 6.事件对象

## 6.1 事件对象简介

+ 事件对象是由浏览器在事件触发时所创建的对象，这个对象中封装了事件相关的各种信息
+ 通过事件对象可以获取到事件的详细信息
  + 比如：鼠标的坐标、键盘的按钮.....
+ DOM中存在着多种不同类型的事件对象
  + 多种事件对象有一个共同的祖先 Event
+ **主要作用，用来获取事件的详细信息**

## 6.2 如何获取事件对象

+ 浏览器在创建事件对象后，会将事件对象作为响应函数的参数传递，所以我们可以在事件的回调函数中定义一个形参来接受事件对象

+ 任何形式绑定的事件响应函数都可以接收这个参数

+ ````````````javascript
  box1.onmousemove = function(event){
      console.log('159');
  }
  ````````````

## 6.3 事件对象属性

### 6.3.1 `event.clientX`

+ 鼠标移动事件，鼠标的x轴坐标

### 6.3.2 `event.clientY`

+ 鼠标移动事件，鼠标的Y轴坐标

### 6.3.3 `event.target`

+ 事件的响应函数中，`event.target`表示触发事件的对象
+ 此属性会受到事件冒泡的影响，如果没有阻止冒泡子元素的事件传导就会得到触发对象为子元素

### 6.3.4 `event.currentTarget`

+ 事件的响应函数中，`event.currentTarget`表示绑定事件的对象
+ 不受到冒泡影响，始终只会打印绑定事件的对象（同this）

## 6.4 事件对象方法

### 6.3.1 `event.stopPropagation()`

+ 停止事件传导（冒泡）

### 6.3.2 `event.preventDefault()`

+ 取消事件的默认行为
  + 如超链接的跳转等..
+ 与on绑定的事件响应函数中的return false效果一致，但是适用于所有的事件绑定方式

# 7.JSDOM操作CSS

## 7.1 JS修改样式

### 7.1.1 通过操作属性修改内联样式

+ 通过元素对象节点操作属性的方式，添加内联样式

+ 注意！如果样式名中有`-`的样式，需要更改为驼峰命名法进行使用

  + `backgroun-color --> backgroundColor`

+ ``````````````javascript
  // 点击按钮box1变宽
  const btn1 = document.getElementById('btn1')const box1 = document.querySelector('.box1')
              
  btn1.addEventListener('click', function () {
      box1.style.width = '300px'
      box1.style.height = '300px'
      box1.style.backgroundColor = 'red'
  })
  ``````````````

+ 注意！如果是通过计算的到的值直接修改样式。记得在样式后加上字符串单位，不然没有单位无法生效

+ 注意！小量更改可以用，但是还是不推荐，会有耦合问题

  + `box1.style.width = parseInt(stylebox1.width) + 100 + 'px'`

### 7.1.2 通过class修改样式

+ 通过class修改样式的好处
  1. 可以一次性修改多个样式
  2. 对JS和CSS进行一个解耦
+ `element.classList`
  + 不建议使用`box1.className += ' box2'`方式操作class
  + 推荐使用`element.classList`
  + `element.classList`是一个对象，对象中提供对当前元素的类的各种操作方法

+ ``````````html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <meta http-equiv="X-UA-Compatible" content="IE=edge">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <title>Document</title>
      <script>
          window.onload = function(){
              // 点击按钮添加box2 class
              const btn1 = document.getElementById('btn1')
              const box1 = document.querySelector('.box1')
              
              btn1.addEventListener('click', function () {
                  // box1.style.width = '300px'
                  // box1.style.height = '300px'
                  // box1.style.backgroundColor = 'red'
                  box1.classList.add('box2')
              })
          }
      </script>
      <style>
          .box1 {
              width: 200px;
              height: 200px;
              background-color: #bfa;
          }
  
          .box2{
              background-color: yellow;
          }
      </style>
  </head>
  <body>
      <button id="btn1">点我一下 </button>
      <hr>
      <div class="box1"></div>
  </body>
  </html>
  ``````````

#### 7.1.2.1 `element.classList`的一些常用方法

##### 7.1.2.1.1  `element.classList.add()`

+ 向元素中添加一个或多个class
+ `box1.classList.add('box2','box3',...)`
+ 好处：不会重复添加已有的类

##### 7.1.2.1.2 `element.classList.remove()`

+ 删除元素中一个或多个class
+ `box1.classList.remove('box2','box3',...)`

##### 7.1.2.1.3 `element.classList.toggle()`

+ 切换元素中的一个class
  + 如果你有指定class就删除，如果没有就添加
+ `box1.classList.toggle('box2')`

##### 7.1.2.1.4 `element.classList.replace()`

+ 替换class
+ 参数
  1. 被替换的class
  2. 替换的class
+ `box1.classList.replace('box1' ,'box2')`

##### 7.1.2.1.5 `element.classList.contains()`

+ 检查一个元素中是否有检查的class属性
  + 有返回true
  + 没有返回false
+ `box1.classList.contains('box2')`

## 7.2 读取元素样式

### 7.2.1 `getComputedStyle()`函数

+ `getComputedStyle()`window的方法，所以是函数，直接调用即可

+ 它会返回一个实时更新的对象，这个对象中包含了当前元素所有的生效的样式

  + 因为它会返回所有生效的样式对象中有很多属性，不会一眼就能看到自己想要查找的属性，所以想找到自己想要的属性直接使用对象找属性的方法即可，要谁就找谁，如`stylebox1.width`

+ 读取样式的方法都是只读了，只能读取不能修改

+ 参数

  1. 要获取样式的对象
  2. 要获取的伪元素

+ 返回值

  + 返回一个对象，对象中存储了当前元素生效的样式

+ ``````````````javascript
  // 点击按钮读取css样式
  const btn1 = document.getElementById('btn1')
  const box1 = document.querySelector('.box1')
              
  btn1.addEventListener('click', function () {
  	const stylebox1 = getComputedStyle(box1)
  	const beforeStyle = getComputedStyle(box1,'::before')
       console.log(beforeStyle.color);
  })
  ``````````````

+ 注意！如果拿到的值需要计算，那么一定要使用parserInt()函数取整以后才能行，因为拿到的值都是带单位的

  + `const width = parseInt(stylebox1.width) //200 `

+ 注意！使用`getComputedStyle()`去获取一个默认值时最好先查看一眼默认值是什么，例如width默认值是auto但是会传递回一个具体的宽度值，left就会传递回auto，所以有些可以计算有些不行，用前最好查看一下

### 7.2.2  `element.clientHeight`属性

+ 获取元素内部的高度（包含内容区和内边距高度）
+ 获取到值不带单位，是一个数值类型的值，可以直接运算
+ 只读

### 7.2.3 `element.clientWidth`属性

+ 获取元素内部的宽度（包含内容区和内边距宽度）
+ 获取到值不带单位，是一个数值类型的值，可以直接运算
+ 只读

### 7.2.4 `element.offsetHeight`属性

+ 获取元素可见框的高度（包含内容区、内边距、边框）
+ 获取到值不带单位，是一个数值类型的值，可以直接运算
+ 只读

### 7.2.5 `element.offsetWidth`属性

+ 获取元素可见框的宽度（包含内容区、内边距、边框）
+ 获取到值不带单位，是一个数值类型的值，可以直接运算
+ 只读

### 7.2.6 `element.scrollHeight` 属性

+ 获取元素滚动区域的整体高度
+ 获取到值不带单位，是一个数值类型的值，可以直接运算
+ 只读

### 7.2.7 `elment.scrollWidth `属性

+ 获取元素滚动区域的整体宽度
+ 获取到值不带单位，是一个数值类型的值，可以直接运算
+ 只读

### 7.2.8 `element.offsetParent` 属性

+ 获取元素的定位父元素
+ 定位父元素：离当前元素最近的开启了定位的祖先元素，如果所有祖先元素都没有开启定位则返回body
+ 只读

### 7.2.9 `element.offsetTop` 属性

+ 获取元素相对于其定位父元素的上偏移量
+ 获取的是距离定位父元素之间的上偏移量，不一定是top，margin的边距也会被捕捉
+ 只读

### 7.2.10 `element.offsetLeft` 属性

+ 获取元素相对于其定位父元素的左偏移量
+ 获取的是距离定位父元素之间的左偏移量，不一定是left，margin的边距也会被捕捉
+ 只读

### 7.2.11 `element.scrollTop`属性

+ 获取或设置元素滚动条的上偏移量
+ 可读

### 7.2.12 `element.scrollLeft`属性

+ 获取或设置元素滚动条的左偏移量
+ 可读

