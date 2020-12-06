# webAPI-day04



## 微博-本地化-删除

- 删除：从上面新增知道，新增的主要是arr数组内的 一个成员；那么删除也是删除某个一个成员；
- 点击某个删除按钮，我怎么知道点击的是第几个按钮？
- **在初始化展示的时候，自定义属性设置下标；**

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
    
    // 循环前：ul置空
    ul.innerHTML = "";
    
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

- 实现删除：

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





- BOM： browser object model，是把**browser 浏览器看成是一个对象**，就是学习浏览器对象的各种方法和属性；
- 浏览器对象：**window对象**；



## 案例：获取验证码-倒计时

* BOM：浏览器当做对象；window;

### 前置-BOM-定时器

- setTimeout：一次性定时器；set - 设置；Timeout - 超时

```js
// 作用： 延迟一定的毫秒之后，调用函数一次;
// 返回值： 是该定时器的标识，Number类型，该标识可以用于停止这个定时器
var timer = setTimeout(函数,延迟的毫秒数);

// 停止一次性的定时器：清除后，就不会执行这个定时器；
clearTimeout(timer);
```

- setInterval：永久性的定时器；interval - 间隔

```js
// 作用：阶段的时间执行函数；
// 返回值：就是该定时器的id
var timer = setInterval(函数,间隔毫秒数);

// 清除永久定时器
clearInterval(timer);
```

- 上面两个方法都是window对象下的方法；执行定时器，都是等待自己的间隔才开始执行；

### 实现

- 获取元素：按钮
- 注册事件：click
- 点击之后：
  - 按钮表现为**禁用状态；**
  - 初始化开始计时：显示为5秒；
  - 启动定时器
    - time--：
    - 同时 改变按钮的值；
    - 清除倒计时：time==0时清除定时器；按钮恢复文字和可点击的样式；

```js
// 2. 注册事件 点击之后：
//  2.1 按钮变灰
//  2.2 文字立马显示
//  2.3 开启定时器；文字显示；
//  2.4 判断定时器 是否到达0s；恢复原状；

// 获取按钮
var btn = document.getElementById('getCode');
// 注册点击事件
btn.onclick = function(){
  // 禁用按钮，禁用不能点击了；
  btn.disabled = true;
    
  // 开始倒计时
  var time = 5;
  // 在点击的时候，先改变一次
  btn.value = '获取验证码('+ time +')';
   
  // 设置倒计时
  var timer = setInterval(function(){  
    // 每隔1秒钟，数字要减少1
    time--;  
    // 修改按钮的内容
    btn.value = '获取验证码('+ time +')';   
      
    // 当倒计时到达0的时候，停止定时器
    if(time == 0){
      // 停止的定时器
      clearInterval(timer);
      // 把按钮还原
      // 文字还原
      btn.value = '获取验证码';
      // 可以点击
      btn.disabled = false;
    }
      
  },1000);
}
```

### 补充-BOM

* DOM：document：文档页面；document
* BOM：browser 浏览器   window;

- window 对象特点：
  - 所有window对象的属性和方法，**大部分可以直接省略  `window.`，而直接使用**
  - **顶级对象**：页面中所有的东西都是依赖于这个对象存在的；
  - 变量与函数：**所有的全局变量和全局函数都是window对象的属性和方法**；

```js
// 1.所有window对象的属性和方法，直接省略  `window.`
document.getElementById('xx');
console.log(window.document == document);


// 3.全局变量和函数 都是window上的挂载
var a = 10;
console.log(window.a);
function fn() {
    console.log(1);
}
window.fn();
fn();


// 3.隐式变量：定义变量，变量赋值；在js代码里面，不使用var声明的变量，都是隐式全局变量，这个方式是不推荐的，因为如果不使用var声明，是不会变量提升的；
b = 2;  
console.log(window.b);  //设置到window这个对象上；
```

* onload：页面加载完毕的时候执行（页面加载完毕：**页面所需的静态资源**全部加载完毕；）

```js
window.onload = function(){
    // 1.想要获取图片的宽高，就需要等待图片加载完成后才执行后面的函数；
    // 2.获取DOM节点，等待页面加载完毕！
}
```

* location：负责管理浏览器地址栏相关的行为和信息的对象；

```javascript
// 如果想要使用js进行跳转，只需要 location.href = 新的地址;
location.href = 'https://www.itheima.com';
```



## 案例：手风琴

* 前置：

```
- onmouseover：移入DOM时触发
- onmouseout：移出DOM时触发
```

* 移入实现：
  * 获取元素：所有的li元素
  * 注册事件：鼠标移入
  * 移入之后：排他思想
    * 所有的li变为一个值100；
    * 当前单独变为一个值800；

```js
var lis = document.querySelectorAll('#box li');

for (var i = 0; i < lis.length; i++) {
    // 注册鼠标移入事件
    lis[i].onmouseover = function() {
        // 排他的设置每个li的宽度
        lis.forEach(function(element) {
            element.style.width = 100 + 'px';
        });
        this.style.width = 800 + 'px';
    };
}
```

* 移出：所有的元素回复原来的宽度240

```js
for (var i = 0; i < lis.length; i++) {
    // 注册鼠标的移出事件
    lis[i].onmouseout = function() {
        // 把所有的li恢复原状
        lis.forEach(function(element) {
            element.style.width = 240 + 'px';
        });
    };
}
```





## 案例：tab栏

- 案例：鼠标移入一个选项（选项变为当前选择状态），下面图就会跟着发生变化；
- 步骤：
  - 获取元素：选项、图片；
  - 注册事件：鼠标移入；
  - 移入后的变化：
    - 按钮的状态变化：**排他思想**
      - 先把所有的清除为初始化状态；
      - 给当前DOM节点加当前选择状态；
    - 知道当前的DOM节点，设置图片为对应的地址；

```js
var lis = document.querySelectorAll(".tab-item");
var img = document.querySelector("img");
for (var i = 0; i < lis.length; i++) {

    lis[i].onmouseover = function() {
        // tab项的样式变化
        // 排他思想：
        // 1.先让所有的li 没有 active
        for (var j = 0; j < lis.length; j++) {
            lis[j].classList.remove("active");
        }
        // 2. 当前DOM节点自己 添加 .active
        this.classList.add("active");

        img.src = this.getAttribute("tupian");
    }

}
```







## 案例：360开机动画

### 前置-动画事件

- 动画或者过渡结束事件：专门是指css3里面的  动画或者过渡 结束会触发的事件，css3动画有两种，结束动画事件也有两个；
- **特点：不能使用on的方式注册，只能使用addEventListener的方式注册** 
- transitionend：元素的过渡动画结束的时候触发；

```js
var box = document.querySelector('.box');
box.addEventListener('transitionend',function(){
  console.log(123);
});
```

- animationend：会在帧动画结束的时候触发

```js
var box = document.querySelector('.box');
box.addEventListener('animationend',function(){
  console.log(123);
});
```

- 注意：如果动画是无限次的，不会触发该事件animationend

### 实现

- 核心：分两段**过渡动画**，先让底部的高度逐渐为0，再让整个盒子的宽度为0；

* 步骤：
  * 获取元素：盒子底部，整体盒子
  * 注册事件：盒子底部 transitionend
  * 过度完成：设置整体盒子width

```js
closeButton.onclick = function() {
    // 把下半部分的高度设置为0
    bottomPart.style.height = 0;
}


var box = document.querySelector("#box");
bottomPart.addEventListener('transitionend',function(){
  // 把box盒子的宽度修改为0
  box.style.width = 0;
});
```


