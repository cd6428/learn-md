# webAPI day02



# 案例：选择框

## 前置：checked

- 属性：开关属性 checked/selected/disabled ，这种只有两种状态的属性；
- `<input type="checkbox" name="check" id="ck"  checked />`
- 获取：DOM.checked
- 设置：`ck.checked = true;` 两个状态的值，布尔类型；

```js
var ck = document.getElementById('ck');

ck.checked = true;
ck.checked = false;
```





## 实现：全选

* 业务
  * 点全选 选择 ，下面所有盒子都选择；
  * 点全选 取消，下面所有盒子都取消；
  * 下面盒子点选择，全部都选择后，全选按钮会自动选择；
  * 下面盒子点选择，只要有一个没有选择，全选按钮就不会选择；

* 全选：
  * 获取元素：全选盒子、下面的子盒子
  * 注册事件：全选盒子click
  * 点击之后：点全选 选择 ，
    - 拿到全选后的状态；
    - 循环遍历给子元素 赋值状态；

```js
  var ckAll = document.getElementById('checkAll');
  // 伪数组
  var cks = document.getElementsByClassName('ck');

  // 2 给全选注册点击事件
  ckAll.onclick = function() {
    // 3 获取当前是否勾选
    var status = ckAll.checked;

    for (var i = 0; i < cks.length; i++) {
      cks[i].checked = status;
    }
  }
```

## 实现：子选

- 获取元素：全选盒子、下面的子盒子；
- 注册事件：子盒子注册click（循环）；
- 点击之后：
  - 假设现在是子选项全部选中，标示key=true;
  - 循环遍历，看子选项有没有 无选中的盒子
    - 有：key=false;终止循环
    - 无：key仍然还是true；
  - 判断key
    - true：全部选中，父选项 变为选中；
    - false：有没有选中的子选项，父选项 不选中；

```js
  for (var i = 0; i < cks.length; i++) {
    cks[i].onclick = function() {
      // 使用反证法实现判断是否全选
      // 3.1 假设全都选中了
      var flag = true;
        
      // 3.2 循环的去找反例，只要有一个没勾选，就推翻假设
      for (var j = 0; j < cks.length; j++) {
        if (cks[j].checked != true) {
          // 至少有一个没有勾选，推翻假设
          flag = false;
          break;
        }
      }
        
        
      // 3.3 再次判断假设是否成立
      if (flag) {
        // 如果是true，证明全都勾选，设置全选是选中的
        ckAll.checked = true;
      } else {
        // 证明没有全都勾选，设置全选是取消选中的
        ckAll.checked = false;
      }
    }
  }
```



# 案例：tab栏

## 前置：querySelector

* 对象：万物皆对象；（属性和方法的集合体的表述）

* 要点：该选择器输入的值，主要为CSS选择器的写法，获取元素；

```js

// 作用： 根据指定的选择器获取从上到下的第一个元素，获取不到返回个null对象；
// media query   Selector
document.querySelector(css选择器);

// 作用：根据选择器获取所有满足条件的元素，这个使用的比较多；
// 参数：多个css选择器，以逗号隔开，都是字符串
// 返回值：伪数组；for，但是这个伪数组上面有forEach方法；
document.querySelectorAll(css选择器1,css选择器2...);
```

 

## 前置：setAttribute

* 自定义属性的：

* 语法：这个操作属性更为灵活。一般情况下是操作自定义属性多一些；

```js
  // DOM节点上方法：
  var div = document.querySelector("#box");

  // 自定义属性：
  //    HTML ： data-zhangsan
  //    JS   ： dom.dataset.zhangsan
  //    自定义属性：abc="123" index="5"  没有格式的

  // 获取：
  // 场景：获取自定义属性
  // 参数：字符串 属性名（标准、自定义）
  // 返回：属性值；
  //  div.id; var aa = div.getAttribute("id");
  // var bb = div.getAttribute("abc");
  // console.log(bb);


  // 设置：
  // 参数：字符串属性名，属性值；
  div.setAttribute("abc", "*******");
  div.setAttribute("index", "4444");
  div.setAttribute("aa", "新的自定义属性");
```

* 自定义属性：往DOM节点标签内设置自己需要的属性；



## 实现

```js
//  步骤：
//     1.所有按钮获取到,伪数组；
var btns = document.querySelectorAll("input");
var img = document.querySelector("#img");

//     2.注册事件：遍历
for (var i = 0; i < btns.length; i++) {
    btns[i].onclick = function() {
        // 3.点击后：获取自己身上 一一对应关系 自定义属性；
        //           设置给图片？
        img.src = this.getAttribute("guanxi");
    }
}
```





# 知识：事件相关

## 注册事件

* on事件名：
  * **本质相当于是把一个函数存储到 了 on 这个属性里面 ， 后面被重复赋值**
  * 无法多次注册；团队协作时，有可能别人写的代码，会把你的代码覆盖了。
* addEventListener：添加事件监听，可以多次注册事件；
  * 单独注册一个事件，后面可以不写函数名字；
  * 多次注册不同的函数时，最好写上函数的名字；

```js
  // 给按钮注册事件，点击的时候，输出 123
  var btn = document.querySelector("#btn");

  // 本质上：onclick 名字，往这个对象的属性名上 存了方法；
  // btn.onclick = function() {
  //   alert(1);
  // }
  // btn.onclick = function() {
  //   alert(2);
  // }
  // 问题:被重复覆盖


  // 注册事件
  // add:添加
  // Event：事件
  // Listener：监听器
  // 参数：两个，
  //      第一个：字符串里事件类型  click focus blur   注意没有on
  //      第二个：执行函数，只是注册，不执行！


  // 多次注册：不会覆盖
  //      如果是多次注册，执行函数带一个名字；意味着注册的fn1  fn2 函数都生效；
  btn.addEventListener("click", function fn1() {
    console.log(1);
  });
  btn.addEventListener("click", function fn2() {
    console.log(2);
  });
```



## 事件执行

### 三个阶段

* 事件发生的时候，存在这三个阶段：**捕获、到达目标、冒泡；**

* **客观：需要记住**
  * **捕获**：从根部节点往目标DOM节点上，一层一层的找，捕获到用户点击了那个DOM节点；
  * 冒泡：从目标节点到根节点；



### 事件默认在冒泡阶段执行

* **事件默认是在冒泡阶段执行语：JS控制事件的执行阶段：**

* **规则：需要记住**：大白话理解：
  * 点击某个节点后，想象拿针扎了下（用户点击），信号顺着 冒泡 的方向传递回去；
  * 在传递的过程从，如果 冒泡 阶段的节点 注册了同样的事件，会被触发；

```js
  // 捕获阶段执行
  yeye.addEventListener('click', function() {
    console.log('我是你爷爷');
  }, true);
  baba.addEventListener('click', function() {
    console.log('我是你爸爸');
  }, true);

  erzi.addEventListener('click', function() {
    console.log('我是你儿子');
  }, true);


  // 冒泡阶段执行：默认值第三参数是false;
  yeye.addEventListener('click', function() {
    console.log('我是你爷爷');
  }, false);
  baba.addEventListener('click', function() {
    console.log('我是你爸爸');
  }, false);
  erzi.addEventListener('click', function() {
    console.log('我是你儿子');
  }, false);
```



### 阻止冒泡

![1576814669814](assets/1576814669814.png)

* 问题出现：
  * 在写代码的时候，你给子元素注册了事件，
  * 也有可能给父级也注册了点击事件；
  * 那么你现在点击 子元素时 会有问题；

* 解决问题：
  * **当父亲们辈的同样注册了相同的事件，事件默认是在冒泡阶段执行；**
  * 所有注册的相同的事件都会执行；
  * 但是，**用户只想点击当前的有反应就行，上面的不需要再执行了。**
* 你希望在哪里阻止，就在哪个事件处理程序里面调用即可；
  * **在函数里面的前后位置无所谓；**
  * Propagation：传播；阻止冒泡是阻止父亲们辈的事件执行，不是阻止自己执行；

```javascript

  // 问题：
  //    点击子元素，执行代码
  //    父亲同样注册的事件也会执行；

  // 为什么会出现问题？事件默认是在冒泡阶段执行；

  // 解决：
  var left = document.querySelector(".left");
  left.onclick = function(e) {
    alert("用户信息");
    // 事件对象：把用户的一次点击行为，看成一个对象，JS万物皆对象；
    // 方法：
    // Propagation:传播，冒泡阶段；
    e.stopPropagation();
  };

  var right = document.querySelector(".right");
  right.onclick = function(e) {
    alert("配置信息");
    // 阻止传播；
    e.stopPropagation();
  };

  // 
  var father = document.querySelector(".father");
  father.onclick = function() {
    alert(Math.random());
  }
```



### 事件委托

- 情况：当父亲下面有很多子DOM节点，随时可能会新加入一些子DOM节点，子DOM都要注册同一个事件的话；每个事件执行函数内部都不一样，注册多次！

![1576816327190](assets/1576816327190-1598522343478.png)

```js
  // 优化写法：事件只注册一次；
  //    1.注册事件：给父亲；
  //    2.需要知道点击到底 谁？e：事件对象？把用户点击的一次行为看成一个对象；
  var father = document.querySelector(".father");
  father.addEventListener("click", function(e) {
    // target属性名：DOM节点；

    var dom = e.target;
    // console.log(dom);
    // DOM 前面所有学习的属性
    // console.log(dom.className);

    // 点击就是左侧
    if (dom.className == "left") {
      alert("用户信息")
    }
    // 
    else if (dom.className == "mid_1") {
      alert("mid_1 info")
    }
    // 
    else if (dom.className == "mid_2") {
      alert("mid_2 信息")
    }
    // 
    else if (dom.className == "mid_3") {
      alert("mid_3 信息")
    }
    // 
    else if (dom.className == "right") {
      alert("配置信息")
    }
  });
```

- 事件委托：
  - 事件：注册给父亲；
  - 委托：注册事件给父亲，事件的执行委托给儿子！





* 作业：tab按钮切换图片使用事件委托进行实现



