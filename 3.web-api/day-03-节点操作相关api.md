# webApi day_03



## 微博:删除

* 前置

```js
// ********************************************事件对象：
//  1.事件的目标对象，用户触发到谁上面了；用于事件委托；DOM节点  打谁就是谁！
e.target

//  2.事件的绑定对象，就是绑定在哪个DOM节点上 和 this一样 DOM节点
e.currentTarget==this -----> true

// ********************************************根据 子DOM节点 寻找 父亲DOM节点：
DOM节点.parentNode

// ********************************************删除指定的子DOM节点
父亲DOM.removeChild(子DOM节点);
```

* 需求：点击删除，删除一条微博；
* 分析：所有的点击按钮都会有点击事件，里面执行的逻辑一样；事件委托；
* 步骤：
  * 1.注册事件给父级
  * 2.通过事件对象知道现在点击的是谁？

```js
  // 2 使用事件委托实现点击span的效果
  // 把事件委托在ul身上
  ul.addEventListener('click', function(e) {

    // 判断点击的对象，是不是span
    if (e.target.nodeName === 'SPAN') {
      // 通过事件对象.target 得到触发事件的元素
      // 要通过span得到li
      var li = e.target.parentNode;
      // 通过ul把li移除
      ul.removeChild(li);
    }
  })
```



## 微博-添加

* 前置：

```js
// ******************************************创建 添加 节点
//  document.createElement('标签名');
//  参数：要创建的新的标签的标签名
//  返回：一个创建的元素对象


//  父级DOM.appendChild(新的子DOM节点)
//  参数：DOM节点
//  效果：从后添加一个子元素对象

//  父级DOM.insertBefore(新的子DOM节点，参考DOM节点)
//  参数：新的子DOM节点，参考DOM节点
//  效果：在参考DOM之前添加 新的DOM节点


// innerHTML
//   获取：元素的内部的HTML结构；字符串；
//   设置：字符串，把内部的HTML结构覆盖；
//   ul.innerHTML = '<li>狗蛋</li>';
//   注意：新增的话，需要把以前字符串拼接上去；


// ******************************************修改节点内容
// innerHTML：用于获取或者设置某个元素的内部结构  (html结构的字符串)；
// innerText：用于获取或者设置某个元素里面的**文本内容**，不具备解析HTML结构；
```

* 需求：发送一条内容，显示在列表的第一条；
* 步骤：
  - 获取元素：文本域、按钮、ul
  - 注册事件：按钮click
  - 点击之后：
    - 若文本为空时，return结束函数；
    - **1.创建一个DOM节点；创建节点**
    - **2.DOM节点里设置我们新的内容：修改内容**
    - **3.插入到列表最前面；追加节点；**
    - 清空文本域

```js
// 2 注册点击事件
btn.onclick = function() {
    // 3.1 获取内容 - 注意： 表单元素的内容使用value获取
    var content = text.value;
    // console.log(content);
    // 3.2 创建一个新的li，设置它的内容是一个p标签和一个span标签
    var li = document.createElement('li');
    li.innerHTML = '<p>' + content + '</p><span>删除</span>';

    // 3.3 使用insertBefore 把新建的li放到最前面
    var first = document.querySelector('ul > li:first-child');
    ul.insertBefore(li, first);
    
    // 3.4 把文本域的内容清空
    text.value = '';
};
```

* 补充：根据DOM节点寻找DOM节点的属性

```js
// 父元素.children  得到某个元素之下的所有的子元素的集合，一个伪数组

// 子元素.parentNode  获取父元素

// 元素.nextElementSibling  -  得到下一个兄弟元素
// 元素.previousElementSibling - 得到上一个兄弟元素
```

* 添加微博：

```js
// var first = document.querySelector('ul > li:first-child');

var first = ul.children[0];
ul.insertBefore(li, first);
```











## 微博-键盘添加

- 键盘事件：交互；
  - 事件类型 ：keydown  keyup
  - 按下哪个键？
    - 事件对象e.keyCode，这个属性被称为  键盘码 ，每个按键对应的数字是不一样 ，只需要判断数字，就知道按下的按键是哪一个； e.keyCode==13 回车键
    - 按下了ctrl：事件对象里面有一个属性 ctrlKey ；如果是true，按下了ctrl键
- 实现：
  - 获取元素：文本域；
  - 注册事件：keydown；（组合键）
  - 按下键盘：判断e.ctrlKey && e.keyCode === 13全部成立

```js
text.onkeydown = function(e) {
    console.log(e.keyCode, e.ctrlKey);
    // 判断是否同时按下ctrl和回车
    if (e.ctrlKey && e.keyCode === 13) {
        // 在代码中执行；
        btn.onclick();
    }
}
```





## 微博-本地化

### 前置-localStorage

- local：本地；Storage：储存；相当于 浏览器自带的U优盘；
- 以后：学习服务器，把 数据 放在服务器上；
- 核心：
  - 读取：U盘里的数据读取出来；
  - 存入：本地进行修改，完成后，再次放入U盘；

```js
// 存储：保存后为字符串；
/       如果存储的是对象之类的复杂类型，需要先把复杂类型转换为的字符串，再存进去；
//      多次对一个键进行赋值，会把前面的值覆盖；
localStorage.setItem(键,值);

// 读取:我们存入的的数据的值，返回的是字符串；
localStorage.getItem(键);

// 删除:
localStorage.removeItem(键);　　

// 全部清空
localStorage.clear();　
```

- sessionStorage：【大约5M】【sessionStorage 用于临时保存同一窗口(或标签页)的数据，在关闭窗口或标签页之后将会删除这些数据。】

```js
// 存储
sessionStorage.setItem("lastname", "Smith");
// 获取
var lastname = sessionStorage.getItem("key");
// 删除
sessionStorage.removeItem("key");
// 全部清除
sessionStorage.clear();
```

### 前置-JSON  

* 上面的问题：把对象变为字符串！

```js
// 将对象转换为json格式的字符串
JSON.stringify(对象);

// 将json格式的字符串 转换为 对象
JSON.parse(json格式字符串);
```



### 展示

```js
var list = [];


// 展示列表
function getData(){
    // 1.获取
    var str = localStorage.getItem("list")||"[]";

    list = JSON.parse(str);
    
    // 3.循环遍历
    for (var i = 0; i < list.length; i++) {
        var one = list[i]; // {neirong: "3"}
        // 1. 新建li
        var li = document.createElement("li");
        li.innerHTML = `<p>${one.neirong}</p><span >删除</span>`;

        // 2.添加到ul里面：从后添加，因为数组中的第一条数据 是最新数据，永远第一位；
        ul.appendChild(li);
    }
}
// 调用一次；
getData();
```



### 添加

![1576911899995](assets/1576911899995.png)

* 思路转变：操作都是数据，添加是list里面添加一条数据；

```js
// 需求：点击发布，把发布的内容，发布在列表最前面；
  // 分析：
  var btn = document.querySelector(".weibo-btn");
  var text = document.querySelector(".weibo-text");

  var ul = document.querySelector(".weibo-list");
  var list = [];
	
  // 初始化展示数据
  getData();

  // 点击
  btn.onclick = function() {
    // ---------------------------------------------数据操作
    // 列表：[]   一条数据：{ info:456}
    var one = {};
    one.val = text.value;

    // 把one对象集合 放入数组内： push 从后添加   unshift从前添加  
    // 选择 unshift :依据DOM操作，从前添加
    list.unshift(one);

    // 1.转化
    var str = JSON.stringify(list);
    // 2.存入本地
    localStorage.setItem("list", str);
      
     //----------------------------------------------重新刷新列表
     getData();
  }
```

### 删除

* 删除：从上面新增知道，新增的主要是list数组内的 一个成员；那么删除也是删除某个一个成员；
* 知识：删除数组中某一个成员？

* 点击某个删除按钮，我怎么知道点击的是第几个按钮？**在初始化的时候，自定义属性设置下标；**

```js
function getData(){
    // 1.获取
    var str = localStorage.getItem("list");

    // 没有数据
    if (str == null) {
        localStorage.setItem("list","[]");
    }
    // 有数据的时候。
    else {
        // 2.转化
        list = JSON.parse(str);
    }
    // 3.循环遍历
    for (var i = 0; i < list.length; i++) {
        var one = list[i]; // {neirong: "3"}
        // 1. 新建li
        var li = document.createElement("li");
        li.innerHTML = `<p>${one.neirong}</p><span index=${i}>删除</span>`;

        // 2.添加到ul里面：从后添加，因为数组中的第一条数据 是最新数据，永远第一位；
        ul.appendChild(li);
    }
}
```

* 实现删除：

```js
  ul.addEventListener('click', function(e) {

    // 判断点击的对象，是不是span
    if (e.target.nodeName === 'SPAN') {
      
       var i = e.target.getAttribute("index");
       list.splice(i,1);
        
       // 更新本地数据
       var res = JSON.stringify(list);
       localStorage.setItem('list',res);
        
        
	   //----------------------------------------------重新刷新列表
       getData();
    }
  })
```
















