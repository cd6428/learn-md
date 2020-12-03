# js基础-day_05

# 对象

## 介绍

* JS核心概念：**万物皆对象**，我们在编程中，使用对象来描述万事万物。
* 对象：使用`属性`描述事物的`特征`，使用`方法`来描述`功能`， 就是对象。
* 对象**：属性和方法的集合体**；
* 数组：数据集合体；
* 对象 描述  扳手 ：
  - 属性(特征)：名称 金属、银白色，
  - 方法：能拧螺丝、防身等；





## 为什么

* 之前学习过的对象：new Date()--->time；我们发现，只要学习对象的一些属性和方法，直接使用，就可以得到自己想要的效果。
* 著名思想：**面向对象思想、万物皆对象**
* 特点：对于开发人员更友好的开发；
  - **实现高效开发**
  - **便于维护**
* 如何面对：学习一个**对象（工具包）**，**看它身上有什么方法和特点（属性）**，能帮我干什么事；



## 语法

### 创建

* 构造函数：

```javascript
var obj = new Object(); // 这是一个没有属性和方法的对象
console.log(obj);
```

* 字面量：从字面上能看出数据的类型；

```javascript
var obj = {}; // 这也是一个没有属性和方法对象，其本质和构造函数创建的对象是一样的
console.log(obj,typeof obj);
```



### 设置

* 对象：属性和方法的集合体；

* 如： 使用对象描述一个叫`狗蛋`的人，先字面量声明一个对象，再给对象上属性和方法赋值；

```javascript
var obj = {};

// 对象.属性 = 值;
obj.name = '狗蛋';// 名字是一个人的特征

// 对象.方法名 = function(){}
// 注意：这里和函数一样，只是现在属于工具包上面，不会执行；
obj.sayName = function(){
	console.log('你好，我叫' + obj.name);
}
```

* 通过字面量初始化对象时，一个属性和一个值叫**键值对**。多个键值对之间使用逗号分隔

```js
// 描述一个学生
var student = {
  name : '狗蛋',
  age : 12,
  gender : '男',
  sayName : function(){
    console.log(student.name);
  }
}
```

* 键的方式添加属性：


```js
// 对象[属性名]  属性名必须是String类型，里面可以写字符串；
var obj = {};
obj['name'] = '狗蛋';
obj['sayName'] = function(){
  console.log('你好，我叫' + obj['name']);
}
```







### 获取

* 点属性获取

```javascript
// 得到对象的名字,属性可以当成变量使用
console.log(obj.name);
// 调用对象的方法，方法的本质是函数
obj.sayName();

obj.a // undefined
```

* 以键的方式访问属性

```js
console.log(obj['name']);
obj['sayName']();


// 注意：
var key = "name";
obj[key]  
obj.key  
```



* 练习：统计数组中字符出现的次数；

```js
var arr = ["a","b","c","a","a"];

var obj = {};
for(var i = 0;i<arr.length,i++) {
	var key = arr[i];
	if(obj[key]) {
		obj[key] +=1;
	}
	else {
	    obj[key] =1;
	}
}
```



### 遍历

* 对象也可以遍历；

```javascript
// key 就是obj这个对象中的每个键，obj就是要遍历的对象。
for(var key in obj){
}

var obj = {
  name : '狗蛋',
  age : 12,
  gender : '男'
};
for(var key in obj){
  console.log(key);
  // 只能通过键的方式获取值
  console.log(obj[key]);
}
```



## 内置

### Math

* 有关数学计算的对象；

- Math.random()；这个方法的作用是生成一个 [0,1) 之间的随机浮点数

```js
var r = Math.random();
// 每次执行等到的数字都不一样
console.log(r);
```

- Math.floor(x)   把一个浮点数进行向下取整

```js
console.log(Math.floor(3.1));  // 3
console.log(Math.floor(3.9));  // 3
console.log(Math.floor(-3.1)); // -4
console.log(Math.floor(-3.9)); // -4
```

- 案例：刷新页面，随机弹出笑话

```js
var list = [
    "为什么结婚都喜欢选好日子，因为结婚后都没有好日子。",
    "为什么超人都喜欢穿紧身衣，因为救人要紧",
    "火柴有个问题想不懂，然后就挠头，自己燃烧了自己",
    "包子跑步，为什么在路上消失了，因为太饿自己把自己吃了",
    "自己的事情自己做，函数也能调用自己"
];

var index = Math.floor(Math.random()*list.length);
alert(list[index]);
```

- 作业：给Math对象设置新的方法，功能为可以获取n-m之间的随机整数；



- Math.round(x)  把一个浮点数进行四舍五入取整

```js
console.log(Math.round(3.1));  // 3
console.log(Math.round(3.9));  // 4
console.log(Math.round(-3.1)); // -3
console.log(Math.round(-3.9)); // -4
```

- Math.ceil(x)  把一个浮点数进行向上取整

```js
console.log(Math.ceil(3.1));  // 4
console.log(Math.ceil(3.9));  // 4
console.log(Math.ceil(-3.1)); // -3
console.log(Math.ceil(-3.9)); // -3
```

- Math.abs(x)  求一个数的绝对值 正数

```js
console.log(Math.abs(3));  // 3
console.log(Math.abs(-3)); // 3
```

- Math.max(x,y...)  求多个数字中的最大值，同理 Math.min(x,y...);

```js
console.log(Math.max(10,20));  // 20
console.log(Math.max(8,4,5,7,3)); // 8

console.log(Math.max(10,20));  // 10
console.log(Math.max(8,4,5,7,3)); // 3
```



### Date

- 构造函数：可以构造出一个对象；

```js
var date = new Date(); // 得到的是当前时间的日期对象
```

- 获取年月日时分秒

```js
console.log(date.getFullYear());// 年份
console.log(date.getMonth()); // 月份，从0开始

// 当前日 为什么不是getDay() 英语：Sunday 周六；
console.log(date.getDate()); 

console.log(date.getHours()); // 小时，0-23
console.log(date.getMinutes()); // 分钟 ， 0-59
console.log(date.getSeconds()); // 秒数 ， 0-59
console.log(date.getMilliseconds()); // 毫秒 0-999 ， 1秒 = 1000毫秒
```

- 获取从1970年1月1日到现在的总毫秒数，**常说的时间戳**

```js
var date = new Date();

// 获取date的的时间戳
console.log(date.valueOf());
console.log(date.getTime());
console.log(1*date);

// 特别：获取当前时间的时间戳
console.log(Date.now());
```

* 创建一个**指定日期**的对象：那么这些对象也可以使用上面的方法；

```js
// 给一个日期格式字符串
var date = new Date('2019-01-01');

// 分别传入年月日时分秒。注意传入的月份是从0开始算的
var date = new Date(2019,0,1,12,33,12);
```









# 简单与复杂类型

* 规则
  * **JS 数据都是存在内存上的，内存上分为两个地方: 栈  堆；只要var 变量，就要在 栈上开个格子；**
  * 简单类型 存储在内存的**栈空间**中
  * 复杂类型 存储在内存的**堆空间**中

* 简单类型的储存

![1598013619548](assets/1598013619548.png)

* 复杂类型的储存

![1598013662990](assets/1598013662990.png)

* 作业：画图描述

```js
var arr_1 = [10,20,30];
var arr_2 = arr_1;
arr_2[0] = "abc";

console.log(arr_1[0]);
```

