# WebAPI day_01



## 介绍

- API - application   programing   interface 翻译过来叫 `应用编程接口` 
- 万物皆对象：
  - 对象？属性和方法的集合体；
  - 如何学习？看对象上有啥属性？**有什么方法？方法能够做什么？**
- 比如我们学习过的：Math.random()...说到底就是别人已经帮我们**封装好的对象上属性和方法**；
- javascript 组成部分：
  - ECAMAScript：js的语法规范；js基础6天所学es5  
    - 变量：用于储存数据；
    - 数据类型：简单类型（字符串、数字 等）、复杂类型( []、 {} )
    - 方法：字符串方法、**数组的方法；**Date Math
    - **函数：封装一段代码，复用**
    - 结构：if、for  
  - **DOM - document object model - 文档对象模型 -  把整个页面看成一个对象**；
    - document.write();  输出在页面中，可以识别HTML字符串；
  - BOM - browser object model - **浏览器对象模型 - 把浏览器看成一个对象**；
    - 内部存储！
    - 页面地址；
- WebAPI阶段：学习**DOM+BOM**的提供对象上属性和方法，并使用它们实现页面上的效果；





* DOM - **document** object model - 文档对象模型：`document.write()`上方法
* **DOM树**：一个 `树` 形结构 ，把整个树状的模型，这个对象称为**文档对象模型**；
* **节点**：树形结构里面的每个交叉点（HTML标签），在JS被称为 `节点`  ，也叫**DOM节点**；
* **我们现在认知的节点包括**： 标签本身、标签上的属性（src、id、class、style等）、标签内文本；
* **为什么叫文档对象模型**：需要把文档document看成一个对象，**对象封装了好多方法在里面**，学习别人封装了什么方法，怎么用，能帮助我们做什么效果；不考虑内部怎么实现的；更高效的关注于我们的业务；
* **具体学习什么？document上的各种方法**





## 案例：开关灯

### 前置：获取元素

- 作用：**帮助获取页面中已经存在的HTML标签**，获取到了后，在JS层面这叫 DOM节点！
- 元素对象：DOM节点；

```js
// 作用: 获取页面中  已经存在  的HTML标签,DOM节点,元素对象;
// 参数: 字符串，单双引导！ id值；hTML标签上面必须得出现设置id = "xxx"
// 返回: DOM节点（元素对象）;如果页面中没有这个DOM节点，返回null;
//      元素对象---->属性和方法的集合；【返回的DOM节点：是个对象！！！】

// var btn = document.getElementById("btn");

// 特别: 返回body DOM节点
// var body = document.body;
```

- DOM节点，元素对象---->属性和方法的集合；



### 前置：注册事件

- 本质：DOM节点 对象 上的一个**内置方法名**；
- 作用: 用户和指定DOM节点交互; 给DOM节点注册事件：方法名 默认的onclick,用户的点击行为;
- **特别：【!!!方法什么时候被调用？】用户真的去触发点击行为的时候,函数才会执行;(什么时候执行不确定,不是由代码控制) 用户点击一次：代码执行：btn.onclick();**

```js
// 三部分：
// btn 事件源：通过谁要触发这个事件，也就是元素对象 DOM节点；
// click 事件类型：用户通过什么行为,去触发一件事
// 匿名函数 事件处理程序(函数)：用户做了这个行为之后，要做什么事情；

  // 元素对象上有什么方法？
  // 事件：本质上是 DOM节点，元素对象上的一个方法名，很特别，不能自己起，
  //      后面的匿名函数可以我们自己写；
  //      给DOM节点，元素对象上设置方法的 函数；
  //      用人家定好名字onclick有什么特别之处？当用户点击的时候，我们写的函数就会被执行；


  // 设置方法名 onclick 后面的匿名函数
  btn.onclick = function() {
    alert(1);
  };

```

### 前置：改变样式

* DOM节点的属性名：style;

- **style属性：**
  - style属性里面的内容其实是多个**键值对**，js帮我们把它们以对象的方式管理起来；
  - 获取：只需要  `元素对象.style.样式属性名` ；如果样式属性名是多个单词的，需要把样式属性的`-` 去掉，修改为驼峰命名；

```js
// 获取：只能获取行内样式；
div.style.backgroundColor
// 设置：只能获取行内样式；
div.style.backgroundColor = ’#fff‘;
```

- 连起来：点击盒子，变背景色；

```js
var closeBtn = document.getElementById('close');
closeBtn.onclick = function(){
  closeBtn.style.backgroundColor = ’red‘;
}
```

### 实现：两个按钮 

* 业务：点击 关灯按钮，页面变黑；点击 开灯按钮，页面变白；
  
* 步骤：
  * **获取元素**：两个按钮
  * **注册事件**：onclick
  * **在事件处理程序中实现你的效果**

```javascript
// 获取关灯按钮
var closeBtn = document.getElementById('close');

// 注册点击事件
closeBtn.onclick = function(){
    // 修改背景颜色
    document.body.style.backgroundColor = '#000';
};
```

* 经验值：

```js
Uncaught TypeError: Cannot set property 'onclick' of null

// 未捕获的类型错误： 不能  设置  属性 'onclick' 给 null
// 说明你使用了 null 来点了 onclick  ---> 点onclic的那个玩意是null
```



### 显示：一个按钮

* 需求：点击关灯：页面变黑，字变为开灯；点击开灯：页面变白，字变为开灯；
* 步骤：
  - **获取元素**：按钮，body
  - **注册事件**：click
  - **点击之后**：找到当前的显示的值是什么，进行不同的条件的判断；

```js
  //  1.谁？
  var btn = document.getElementById("btn");
  var body = document.body;

  //  2.注册点击事件
  btn.onclick = function() {
    // 看下当前这个按钮是什么字？不同的字，实现不同的效果；
    // btn.value

    // 按钮字是 开灯,点击之后,变白
    if (btn.value == "开灯") {
      body.style.backgroundColor = "#fff";
      // 本身的按钮
      btn.value = "关灯";
    }
    // btn.value == "关灯"
    else {
      // 背景
      body.style.backgroundColor = "#000";
      // 按钮的字发生改变
      btn.value = "开灯";
    }
  };
```





## 案例：搜索区显示隐藏

### 前置：focus、blur

- 注意：
  - 站在对象：内置方法名不能改！**匿名函数什么时候调用？用户触发的时候（代码已经执行完了）才调用，**
  - DOM：新的事件类型；事件类型：focus：聚焦；blur：模糊；
- 注册给谁？DOM节点  有光标的标签 input textarea;
- 事件类型：
  - 有光标时：获得焦点 focus；
  - 无光标时：失去焦点 blur

```js
ipt.onfocus = function(){
  // 光标在输入框里面的时候要做什么事，就使用这个事件即可
}

ipt.onblur =  function(){
  // 光标失去的时候所做的事情，就在这里做
}
```

### 实现

* 业务：有光标时，搜索区显示；无光标时，搜索区隐藏
* 步骤：
  * 获取元素：文本框
  * 注册事件：focus blur
  * 事件后：搜索区的显示隐藏；

```js
// 1 获取元素
var search = document.getElementById('search');
var list = document.getElementById('list');
// 2 注册获得焦点的事件
search.onfocus = function(){
  // 把搜索历史显示 - 通过修改display属性 - 元素.style.display = 'block';
  list.style.display = 'block';
}

// 2 注册失去焦点事件
search.onblur = function(){
  // 把搜索历史隐藏 - 修改display为none
  list.style.display = 'none';
}
```





## 案例：搜索区显示隐藏

### 前置：classList

- classList：DOM元素对象的一个**属性名**；
- 属性值：
  - 是一个对象（有很多方法）；
  - 提供**多个方法**进行操作，操作类名更为简单；**比较好的方式解决上面的2个问题；**
- add：给元素对象添加一个或者多个类名，不会影响原来的类名；

```javascript
// 参数：多个类名，之间用逗号隔开
box.classList.add(类名1,类名2...)；
```

- remove： 给元素删除一个或者多个类名，

```javascript
// 参数：多个类名，可以是多个，多个之间用逗号隔开
box.classList.remove(类名1,类名2...)
```

- toggle：切换类名，

```javascript
// 参数： 要切换的类名
box.classList. (类名)
```

### 实现

```js
// 注册获得焦点事件
search.onfocus = function(){
  // 给搜索历史添加一个类名 （show）
  list.classList.add('show');
}

// 注册焦点的失去事件
search.onblur = function(){
  // 把show这个类名移除
  list.classList.remove('show');
}
```



### 补充：className

* 属性名：是元素对象，DOM节点；
* className：属性，获取和设置DOM节点上的class的值字符串！
* 作用：可以添加或修改我们已经写好CSS的类名（和DOM.style对比）；

```js
console.log(元素.class); // 输出undefined
console.log(元素.className); // 正常输出元素的class属性

// 如果要修改类样式，只需要把className修改一下就行了；
box.className = '新的类名';  // 但是会直接覆盖

// 解决：在原来的基础上进行添加类名
box.className += '新的类名';
```

* 问题：

  * 一直点击按钮，bg-red 一直添加；

  * 如果现有类名："abc aa bb cc dd"，通过className 删除一个 "bb";  非常不好做；









## 案例：点击按钮切换图

### 实现

- 获取元素：按钮、图片
- 注册事件：click
- 点击之后：给图片跟换新的图片地址；

```js
var btn_1 = document.getElementById('btn_1');
var btn_2 = document.getElementById('btn_2');

var img = document.getElementById('img');

// 注册点击事件
btn_1.onclick = function(){
  // 修改图片的src属性
  img.src= './images/01.jpg';
}
btn_2.onclick = function(){
  // 修改图片的src属性
  img.src= './images/02.jpg';
}
```

- 发现一一对应关系；

### 前置：自定义属性

- **标准属性**：html标准中出现的，有**特殊功能的属性** id,class,href,src,title....
- **自定义属性**：
  - 开发者依据自己的需要，把数据存储到对应元素身上时使用的属性，可以自己随便命名的，**没有什么功能，就是自己需要**；
  - 在工作中，一般把和DOM节点相关的数据（有一一对应关系的数据），写在标签内部，以**自定义属性的形式；**
  - 一一对应关系：

![1576653156958](assets/1576653156958.png)

### 实现

```js
  // 标准属性：HTML已经定好属性 id src className alt type value 
  // 自定义属性： 工作：习惯把一一对应关系的数据写在标签内，绑定在一起！【知识点】


  // ------------------------------------------------HTML结构上进行设置
  // 如何写？HTML语法格式：data-自己命名 = 值;
  // 对我们标签有什么影响？没有任何影响，就是为了对应关系；



  // 如何获取？JS语法：DOM节点上有个属性名 dataset
  //                 值    对象   {guanxi: "./images/01.jpg"}


// <input type="button" value="图片1" id="btn_1" data-dizhi="./images/01.jpg">
// <input type="button" value="图片2" id="btn_2" data-dizhi="./images/02.jpg">
// <input type="button" value="图片3" id="btn_3" data-dizhi="./images/03.jpg">

  var img = document.getElementById("img");
  var btn_1 = document.getElementById("btn_1");
  btn_1.onclick = function() {
    img.src = btn_1.dataset.guanxi;
  };
  var btn_2 = document.getElementById("btn_2");
  btn_2.onclick = function() {
    img.src = btn_2.dataset.guanxi;
  };
  var btn_3 = document.getElementById("btn_3");
  btn_3.onclick = function() {
    img.src = btn_3.dataset.guanxi;
  };
```





### 前置：this

- 原有写法：

```js
var btn_3 = document.getElementById("btn_3");
btn_3.onclick = function() {
    img.src = btn_3.dataset.dizhi;
}
```

- **this 规则：谁调用函数，this就指向谁。**

```js
var btn_3 = document.getElementById("btn_3");
btn_3.onclick = function() {
    img.src = this.dataset.dizhi;
}

// 用户触发的时候：点击；btn_3.onclick();
```



### 前置：获取元素

* 根据**标签名**获取元素

```js
// 参数： tagname - 标签名 - 必须是字符串
// 返回值：伪数组 - 里面包含有所有满足条件的元素
// 伪数组：可以遍历；
document.getElementsByTagName(tagname);
```

* 根据元素类名获取元素 ByClassName

```js
// 参数： classname - 类名 - 必须是字符串
// 返回值： 伪数组 - 里面包含有所有满足条件的元素
// 伪数组：可以遍历；
document.getElementsByClassName(classname)
```



### 实现

- 返回：DOM节点的伪数组；

```js
 //  需求：有一万个按钮；

  //  1. 获取所有按钮
  var btns = document.getElementsByTagName("input");
  var img = document.getElementById("img");

  //  2.给每个按钮注册点击事件
  for (var i = 0; i < btns.length; i++) {
    // 设置函数。不执行，什么时候执行？用户点击的时候执行。
    // 当 用户点击的时候执行，for 循环完毕了 
    btns[i].onclick = function() {
      // img.src = btns[i].dataset.guanxi;
      img.src = this.dataset.guanxi;
    }
  }

  // 报错：Uncaught TypeError: Cannot read property 'dataset' of undefined
  // 翻译: undefined.dataset

  // 代码：执行循环for,执行完毕了，此时全局 i : 3

  // 注册函数：什么时候执行？用户点击的时候，用户点击的时候，i:3
  // 执行内部：img.src = btns[i].dataset.guanxi;
  //          btns[3]--->undefined;

  // 解决方案：this
  // 什么时候用this? 找不到当前注册给哪个对象上的时候，就用this;


  // 循环第一次：i:0
  // 立马注册：设置，不执行！！！
  btn[0].onclick = function() {}; // i:1
  // 立马注册：设置，不执行！！！
  btn[1].onclick = function() {
    this
  }; // i:2
  // 立马注册：设置，不执行！！！
  btn[2].onclick = function() {}; // i:3
  // 此时 i:3

  // 用户点击的时候：
  //    执行内部函数 img.src = btns[i].dataset.guanxi;
  //    需要用到全局变量 i
  //    此时全局变量 i:3 
  //    btns[3] 没有这个成员，返回undefined；所以报错；
```

* 经验值：错误解析：

```js

  for (var i = 0; i < btns.length; i++) {
    // 每一个DOM节点：btns[i]  是！！！

    // i:0
    btns[i].onclick = function() {
      // console.log(1);
      img.src = btns[i].dataset.abc;
    }

  }
  // 点击按钮：Cannot read property 'dataset' of undefined
  
  // 分析：
  // 1.循环体内部：只是在注册函数，不是执行函数；
  // 2.那么什么时候会执行？用户触发的时候才会执行  内部的img.src = btns[i].dataset.abc;
  // 3.函数内部找这个 i,这个变量
‘；411是局部变量么？不是；为全局变量；
  // 4.全局变量   i:5
  // 5.找不到 btns[5] 返回undefined
  // 6.所以最终会报错：Cannot read property 'dataset' of undefined


   // 总结：如果找不到当前事件源的DOM节点，使用this;
```

* 作业：点击按钮，弹窗显示当前点击按钮的值；

```js
  <input type="button" value="按钮1">
  <input type="button" value="按钮2">
  <input type="button" value="按钮3">
  <input type="button" value="按钮4">
  <input type="button" value="按钮5">
```









