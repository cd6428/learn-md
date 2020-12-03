# js基础-day_06



# Array

## 对元素操作

```js
  // push:从后添加；
  // 作用：从数组的后添加一个或者多个元素
  // 参数：一个或者多个元素
  // 返回：数组改变后长度值，注意原来的数组arr已经发生改变！
  // var arr = [1, 2, 3];
  // var res = arr.push(["abc", 4], 5);
  // console.log(res, arr);

  // pop:
  // 作用：数组的后面删除一个元素；
  // 参数：无；
  // 返回：被删除后元素，注意arr原数组已经发生改变！
  // var arr = [1, 2, "abc"];
  // var res = arr.pop();
  // console.log(res, arr);


  // unshift
  // 作用：从数组的前面 添加一个或者多个元素；
  // 参数：一个或者多个元素
  // 返回：数组改变后长度值，注意原来的数组arr已经发生改变！
  // var arr = [1, 2, "abc"];
  // arr.unshift(4, 5);
  // console.log(arr);


  // shift:
  // 作用：从数组的前面 删除一个；
  // 参数：无；
  // 返回：被删除后元素，注意arr原数组已经发生改变！
  // var arr = [1, 2, "abc"];
  // var res = arr.shift();
  // console.log(arr); 
```

* splice：可进行数组任何位置的增删改

```js
  // splice : 原数组arr 会发生改变！
  // 作用1：数组 任意位置 成员删除，一个或者多个！
  // 参数：
  //     参数1：从哪个下标；
  //     参数2：删除几个成员；
  // 返回：被删除元素的数组！（哪怕删除时一个元素）
  // var arr = ['a', 'b', 'c', 'd', 'e', "f", "g"];
  // var res = arr.splice(3, 1);
  // console.log(res); // 删除一个


  // 作用2：数组任意位置是添加成员，一个或者多个！
  // 参数：
  //    参数1：从哪个下标开始；
  //    参数2：0；没有删除的个数；
  //    参数后面：要添加的成员!
  // 返回：[];
  // var arr = ['a', 'b', 'c', 'd', 'e', "f", "g"];
  // var res = arr.splice(3, 0, "666", "777");
  // console.log(arr);


  // 作用3：数组任意位置是替换！
  // 参数：
  //    参数1：从哪个下标开始；
  //    参数2：被删除个数个；
  //    参数后面：要替添加的成员! 
  // var arr = ['a', 'b', 'c', 'd', 'e', "f", "g"];
  // var res = arr.splice(3, 2, "666", "777");
  // console.log(arr);
```

## 与字符串互转

* join 用于将数组中的多元素以指定分隔符连接成一个字符串

```js
var arr = ['刘备','关羽','张飞'];
var str = arr.join('|'); 
console.log(str);  // 刘备|关羽|张飞
```

* split 字符串的方法：转数字，后面为分隔的字符

```js
// 这个方法用于将一个字符串以指定的符号分割成数组
var str = '刘备|关羽|张飞';
var arr = str.split('|');
console.log(arr);
```



## 查找元素

* indexOf：根据元素查找索引，如果这个元素在数组中，返回索引，否则返回-1
* 作用：找元素在不在数组内部

```js
var arr = [10,20,30]
console.log(arr.indexOf(30));  // 2
console.log(arr.indexOf(40));  // -1
```

* findIndex 方法用于查找满足条件的第一个元素的索引，如果没有，则返回-1

```js
var arr = [10, 20, 30];
var res1 = arr.findIndex(function (item) {
  return item >= 20;
});
// 返回 满足条件的第一个元素的的索引
console.log(res1);  


var res2 = arr.findIndex(function (item) {
  return item >= 50;
});
// -1
console.log(res2);
```

## 遍历数组

* for循环：JS语法；不是方法；
* forEach：遍历数组

```js
// 数组的forEach方法用于遍历数组
var arr_1 = [10,20,30,40,50];

// forEach方法需要一个参数是一个函数，这个函数也接收3个参数，
// item是数组中的每个元素，index是item的索引,arr表示当前数组；
arr_1.forEach(function(item,index,arr){
  console.log(item,index);
});
```



## 拼接与截取

* concat 拼接数组，不改变原数组，创建新数组返回

```js
// 数组的concat方法的作用是把多个数组合并成一个新的数组
var arr1 = [1,2,3];
var arr2 = [4,5,6];
var arr3 = [7,8,9];
var res = arr1.concat(arr2,arr3);
console.log(res);

// 复制一个数组
var arr_1 = arr.concat();
```

* slice 截取数组：不对原数组操作，返回的是新的数组；

```js
var arr = ['a','b','c','d','e'];
// 表示 从下标1（包括），截取到下表为4(不包括),
var res = arr.slice(1, 4);

// 如果不给第二个参数，默认就是把从start开始，到length结束的所有的元素截取
var arr_1 = arr_2.slice(1);

// 复制数组：如果省略两个参数，start默认是0，end默认是length
var arr_1 = arr_2.slice();
```









# String

* **不可变特性：多次赋值字符串，内存上不会消失；**

## 查找

* indexOf 字符串中是否存在指定字符 存在就返回找到的下标，没有就-1；

```
// 这个方法用于查找某个字符串是否包含于另一个字符串
var str = '我爱中华人民共和国';
console.log(str.indexOf('中华'));
```

* lastIndexOf  用法和indexOf一样，只不过是从后面开始找，（下标仍在没有变）
* charAt：

```js
// 这个方法用于获取字符串中位于指定位置的字符
var str = '我爱中华人民共和国';
console.log(str.charAt(2));
```

* charCodeAt 了解

```js
// 这个方法用于获取字符串中位于指定位置的字符的ASCII码
var str = 'abcdef'
console.log(str.charCodeAt(0));

// 单个字符
var a = '9'
a.charCodeAt()
```

## 长度

* .length 也有该属性，和数组很像

```js
var str= "aksdjkasjdkasd";
for(var i = 0;i<str.length;i++) {
  console.log(str.charAt(i))
}

```

*  需求：统计字符串中出现次数最多的字符

```js
// 1.准备空对象；
  var obj = {};

  // 2.遍历字符串
  var str = "aaabc";
  for (var i = 0; i < str.length; i++) {
    var key = str.charAt(i);
    if (obj[key]) {
      obj[key] += 1;
    } else {
      obj[key] = 1;
    }
  }

  // 3.统计对象中的最大次数
  var max = 0;
  var info = "";
  for (var key in obj) {
    if (obj[key] > max) {
      max = obj[key];
      info = key;
    }
  }


  console.log(max, info);
```



## 转为数组

* split 字符串转数字，后面的分隔的字符

```javascript
// 这个方法用于将一个字符串以指定的符号分割成数组
var str = '刘备|关羽|张飞';
var arr = str.split('|');
console.log(arr);
```

* 作业：

```js
// 地址栏：http:xxx.xxx.com?name=zs&ps=aaa&info=abc;
// 写JS把地址栏的参数解析出：
var obj = {
	name:"zs",
	ps:"aaa",
	info:"abc"
};
```



## 拼接与截取

* concat 拼接

```js
  // concat  
  // 作用：拼接字符串
  // 参数：一个或者单个字符串；只能是字符串；
  // 返回：新字符串；
  // var str = "abc";
  // var res = str.concat("def", "ghj");
  // console.log(res);

  // + 字符串：
```

* 截取：

```js
  // substring：
  // 作用：字符串截取，不操作原字符串
  // 参数：
  //     位置1：从哪个下标开始  可以省略   
  //     位置2：到哪个下标结束  （包左不包右） 可以省略
  // 返回：截取出来字符串；不操作原字符串
  // var str = '我爱中华人民共和国';
  // var res = str.substring(1, 4);
  // console.log(res, str);


  // slice
  // 作用：字符串截取，不操作原字符串
  // 参数：
  //     位置1：从哪个下标开始  可以省略
  //     位置2：到哪个下标结束  （包左不包右）  可以省略
  // 返回：截取出来字符串；不操作原字符串；

  // var str = '我爱中华人民共和国';
  // var res = str.slice(1, 4);
  // console.log(res, str);

  //      不一样地方：slice参数可以写负数！负数就是从后往前数
  // var res = str.slice(-3);
  // console.log(res);


  // substr:
  // 作用：字符串截取，不操作原字符串
  // 参数：
  //     位置1：从哪个下标开始  可以省略
  //     位置2：截取几个  可以省略
  // 返回：截取出来字符串；不操作原字符串；
  // var str = '我爱中华人民共和国';
  // var res = str.substr(1, 3);
  // console.log(res, str);
```























 