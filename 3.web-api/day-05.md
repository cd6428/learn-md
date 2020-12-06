# webAPI-day05

## 案例：跟随

- 前置-事件：

```js
// 点击：click
// input框：focus  blur；
// 键盘：onkeydown  onkeyup
// 移入移出 mouseover  mouseout
// 动画时间：animationend transitionend;

// 鼠标事件：
// mousedown：当鼠标的按键点下的时候触发  左侧
// mousemove：鼠标在某个元素身上移动的时候触发
// mouseup ：当鼠标的按键被松开的时候触发
```

- 语法：

```js
DOM节点.on+事件类型 = function(e){};
DOM节点.addEventListener(事件类型,function(e){
    // 可视区域坐标系   -   以浏览器的可视区域的左上角为原点的
    e.clientX
    e.clientY

    //  body页面坐标系  -   以body的左上角作为原点
    e.pageX
    e.pageY
});


// 坐标系：定位；
//        页面写一个盒子，绝对定位，参考bodybody的左上角作为原点
//        固定定位的时候  浏览器的可视区域的左上角为原点的  

// 引导：
```

- 案例：盒子跟随鼠标移动
- 步骤：
  - 鼠标移动：给document注册事件，mousemove;
  - 跟着移动：给img盒子设置：pageX,pageY;

```js
document.onmousemove = function(e) {
    // 鼠标在当前窗口的位置
    var x = e.clientX;
    var y = e.clientY;

    // 鼠标相对于 body 左上角的位置；
    // var x = e.pageX;
    // var y = e.pageY;

    img.style.top = y + 'px';
    img.style.left = x + 'px';
};
```







## 案例：拖动

### 前置-DOM位置

- DOM节点-页面中位置 获取：只能获取

```js
// 找到一个有定位的父亲元素，如果上级父亲没有定位，会一直往上找，直到找打有定位的父亲，或者body；
DOM元素.offsetParent

// 得到的是DOM元素距离他的offsetParent元素的水平距离
DOM元素.offsetLeft 

// 得到的是某个元素距离他的offsetParent元素的垂直距离
元素.offsetTop
```

- **设置：DOM.style.top  DOM.style.left**
- **大白话：获取元素的定位距离；**

### 前置-事件解绑

- 需求：希望曾经注册了的事件，在触发之后，无法执行对应的事件处理程序了；想让事件只执行一次！
- 事件解绑：事件注销；

```javascript
var btn = document.getElementById('btn');
btn.onclick = function(){
  btn.onclick = null;
  console.log('谢谢惠顾');
};

var btn = document.getElementById('btn');
btn.addEventListener('click',function fn(){
  // 解绑 当前的函数
  btn.removeEventListener('click',fn);
})

// -------------------------------------------------------练习：
// mousedown mousemove mouseup：
// 需求：左键落下后，页面上移动打印1,
//       弹起的时候，再在页面上移动不会打印1；

// 落下后执行  document.onmousemove  注册；
// 弹起的时候，应该把mousemove注销掉；
document.onmousedown = function() {
    document.onmousemove = function() {
        console.log(1);
    };
}

document.onmouseup = function() {
    document.onmousemove = null;
};
```

### 实现

- 核心：**鼠标落下：盒子跟着移动；鼠标弹起：盒子不跟着动；**

![1599018301513](assets/1599018301513.png)

![1599018317158](assets/1599018317158.png)

```js
  // 分析：鼠标按下的时候，求a，b; 鼠标在盒子内位置；
  //      鼠标移动的时候，鼠标的新位置 - 鼠标在盒子内位置 = 盒子的最终位置；

  // 注册：
  //      1. 鼠标左键落下的时候，在div上落下
  //      2. 鼠标移动的时候，在页面上移动；

  // 步骤：
  //      1.在div注册down事件
  var div = document.querySelector("div");
  div.onmousedown = function(e) {
    //    2.计算鼠标在盒子内位置；
    //      鼠标在页面内位置：e.pageX e.pageY  - 盒子定位位置 offsetLeft/Top
    var a = e.pageX - div.offsetLeft;
    var b = e.pageY - div.offsetTop;

    // console.log(a, b);

    document.onmousemove = function(e) {
      //   4.盒子随着移动过程中新位置 = 鼠标新位置 - 鼠标在盒子内本次固定位置；
      //   x？: e.pageX  -a;
      //   y? : e.pageY - b;
      //   怎么设置？
      div.style.left = e.pageX - a + "px";
      div.style.top = e.pageY - b + "px";
    }

  }


  div.onmouseup = function() {
    document.onmousemove = null;
  }
```









## 案例：放大镜

### 前置-DOM显示宽高

* DOM.style : 100%情况做设置！

```js
// 元素.offsetWidth  元素的实际宽度  border+padding+content
// 元素.offsetHeight 元素的实际高度 

// 元素.clientWidth  - 可视区域的宽度  padding+content
// 元素.clientHeight - 可视区域的高度  
```

### 实现1-遮罩出现及移动

- 需求：鼠标移入，出现黄色的遮罩，和用来放大的盒子！鼠标移出，遮罩和放大的盒子消失
  - 获取元素(box,遮罩，放大用的盒子)
  - 注册事件：移入移出
  - 之后：遮罩和放大盒子显示和隐藏

```js
//
box.onmouseover = function(){
  // 1 控制遮罩和放大的盒子显示
  mask.style.display = 'block';
  big.style.display = 'block';
}
box.onmouseout = function(){
  // 2 控制遮罩和放大的盒子隐藏
  mask.style.display = 'none';
  big.style.display = 'none';
}
```

- 需求：鼠标在小图片上面进行移动的时候，黄色遮罩层会随着鼠标一起移动

![1599030421791](assets/1599030421791.png)

```js
// 需求2：黄色mask 跟着 鼠标 动！
//        鼠标在谁上面移动？不是在mask上移动
// 
box.onmousemove = function(e) {
    // x:?   鼠标位置 - box水平定位距离 - 小盒子border值 - mask宽 / 2
    mask.style.left = e.pageX - box.offsetLeft - 10 - mask.offsetWidth / 2 + "px";
    mask.style.top = e.pageY - box.offsetTop - 10 - mask.offsetHeight / 2 + "px";
}
```

* 了解：只要鼠标在mask上，（mask是属于box一部分），鼠标就不算离开了box;
* 需求：遮罩移动范围  x 最小值和最大值
  * min：0；如果遮罩的位置小于0了，强行设置为0；
  * max： small的无border宽度 - mask的有border宽高；遮罩的位置大于最大值了，强行设置为最大值；

```js
small.onmousemove = function(e){
  // 4 根据鼠标的位置，计算出遮罩应该在哪个位置
  var mx = e.pageX;
  var my = e.pageY;
  
  // 5 遮罩的位置 = 鼠标位置 - box的位置 - 遮罩宽高的一半
  var x = mx - box.offsetLeft - mask.offsetWidth / 2;
  var y = my - box.offsetTop - mask.offsetHeight / 2;
  
  // 6 不让遮罩超出边界,最小值0
  x = x < 0 ? 0 : x;
  y = y < 0 ? 0 : y;
    

  // 算出mask移动的最大距离
  var maxX = small.clientWidth - mask.offsetWidth;
  var maxY = small.clientWidth - mask.offsetHeight;
  x = x > maxX ? maxX : x;
  y = y > maxY ? maxY : y;
    
  // 7 设置给mask
  mask.style.top = y + 'px';
  mask.style.left = x + 'px';
}
```

### 实现2-放大效果

- 获取元素：大图片
- 注册事件：小图片移动
- 移动之后：**鼠标的位置  计算---->出大图应该在的位置，设置给大图**
- 移动比例：

```js
// 我在小图上移动从左到右，移动了  small.clientWidth - mask.offsetWidth，
// 按照道理大图应该移动  bigImg.offsetWidth - big.clientWidth

// 那我在小图上移动了 y 的值
// 大图应该移动多少? 
```

![1593347801923](assets/1593347801923.png)

- 计算大图应该移动的位置：

```js
var bigImgX = x * bigImgMaxX / maxX;
var bigImgY = y * bigImgMaxY / maxY;

// 注意方向是相反的
bigImg.style.top = -bigImgY + 'px';
bigImg.style.left = -bigImgX + 'px';
```



## e-小结

- e：到底是什么神仙？把用户的一次行为也看做对象！万物皆对象！

- 方法：

```js
// ********************阻止冒泡
e.stopPropagation();

// ********************阻止默认行为
// 页面右键事件 查看右键菜单
document.oncontextmenu = function(e){
  e.preventDefault();
}

// 阻止a标签转跳
// 1 把a标签的href属性设置为 javascript:void(0);
// 2 在a标签的点击事件里面，return false;
// 3 使用事件对象.preventDefault();
dom_a.addEventListener('click', function(e) {
    e.preventDefault();
});
```

- 属性：

```js
// 可视区域坐标系 - 以浏览器的可视区域的左上角为原点的
// 可视区域：就是元素用来显示内容的区域
事件对象.clientX
事件对象.clientY

//  页面坐标系  -  以body的左上角作为原点
事件对象.pageX
事件对象.pageY


// 事件的目标对象，用户点击到谁上面了；用于事件委托；
事件对象.target

// 事件的绑定对象，就是是绑定在哪个DOM节点上 和 this一样
// 前面说的事件源，
e.currentTarget==this -----> true
```



## 样式的获取与设置小结

```js
// 参数：DOM节点
// 返回：不管是行内还是行外的样式对象
Window getComputedStyle(DOM节点)
```





