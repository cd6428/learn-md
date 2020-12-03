# js基础 day_02





# 数据类型转换

## 其它类型 转 String类型

- 其他类型：数字类型、boolean类型、null（值）、undefined类型（值undefined）

### String()

- 转化特点：有引号就行了；
- 语法：转呗；
- 总结：反正最后就是用单双引号包起来了；

```js
var res1 = String(123);
console.log(res1);  // 输出字符串的 123
console.log(typeof res1); // 输出 string

var res2 = String(true);
console.log(res2); // 输出字符串的 true
console.log(typeof res2); // 输出 string

var res3 = String(undefined);
console.log(res3); // 输出 字符串 undefined
console.log(typeof res3);// 输出 string

var res4 = String(null);
console.log(res4); // 输出 字符串null
console.log(typeof res4); // 输出 string
```

### .toString()

- 语法：undefined和null不能使用这个方式变成字符串；

```js
var res1 = (123).toString();
console.log(res1); // 输出字符串123
console.log(typeof res1); // 输出string

var res2 = true.toString();
console.log(res2); // 输出字符串true
console.log(typeof res2); // 输出string

var res3 = undefined.toString();
console.log(res3); // 报错：Cannot read property 'toString' of undefined

var res4 = null.toString();
console.log(res4); //报错： Cannot read property 'toString' of null
```







## 其它类型 转 Boolean类型

- 其他类型：字符串类型、数字类型、null（值）、undefined类型（值）
- 特点：返回一个布尔值；true、false；

### Boolean()

- 语法：

```js
var res1 = Boolean(123);
console.log(res1);// 输出true
console.log(typeof res1); // 输出 boolean

var res2 = Boolean('abc');
console.log(res2);// 输出true
console.log(typeof res2); // 输出 boolean

var res3 = Boolean(undefined);
console.log(res3);// 输出false
console.log(typeof res3); // 输出 boolean

var res4 = Boolean(null);
console.log(res4);// 输出false
console.log(typeof res4); // 输出 boolean
```

- 在js里面，我们在转换其它类型为布尔类型的时候，只有6个情况是false

```js
var res1 = Boolean(0);
console.log(res1); //输出false

var res3 = Boolean(NaN);
console.log(res3); //输出false


var res2 = Boolean('');// 空字符，里面啥没有，空格也没有；
console.log(res2); //输出false


var res6 = Boolean(false);
console.log(res6); //输出false


var res5 = Boolean(null);
console.log(res5); //输出false

var res4 = Boolean(undefined); 
console.log(res4); //输出false
```



# 操作符

- 数据与数据运算；
- 数字运算：数据参加比较、运算；
- 不同的数据类型参加运算，会有问题；比如上面的： 字符串+非字符串；
- **关注：常规需要什么；返回什么；**



## 算术操作符

- 常规：Number类型参加运算；
- 返回：就是Number类型计算的结果；

```js
// +  -  *  /  10%3 取余
// ++ --
```

### 字符串+

- **字符串+**：与字符串临近的类型，转为字符串；里面存在一个**隐式转化**；看不到的转化；
- 隐式转化：在字符串+情况下，数字隐转为字符串；
- 情况：
  - 字符串 + ；
  - +字符串；

```js
// 字符串 +
// 从左到右执行，数字相加，字符串拼接
var res3 = 10+10+"abc"+"def";
console.log(res3);  //输出 20abcdef
```

### 字符串 其他

- 字符串遇见 * / -  %；
- 隐式转化：字符串会隐式转化转为Number，再次参加运算；

```
var res3 = '456' - 123; 
console.log(res3); // 输出 数字 333

// 'abc' 隐式转化为NaN，所有输出NaN；
var res4 = 'abc' - 123;
console.log(res4); // 输出NaN
```

- 其实字符串遇见 * / % 一样的结果；
- 自己去试：其它的类型：null（值）、undefined、Boolean自己去体验；
  
  

### 自增++、自减--

- `++` 自增操作符的作用是让一个数字在原来的基础上自增1

```js
  // ++  --：
  // 作用：在自己的基础上进行自增1，或自减1；
  // 演示：
  // var a = 10;
  // 一元运算：
  // a++;
  // ++a;
  // console.log(a);
```

- 区别：同理 **--**

```js
  // 参加其他运算的时候：
  // var a = 10;
  // var b = a++ + 1;
  // 先算右侧：
  // + 会使两个位置上提供一个数据参加运算；
  // 规则：如果遇见++写在a的后面，先把自己的数推到位置上，在进行a++运算（运算后结果不推到位置上）
  // 10(此时a变为11)   +  1;
  // console.log(b, a);

  // var a = 10;
  // var b = ++a + 1;
  // 先算右侧：
  // + 会使两个位置上提供一个数据参加运算；
  // 规则：如果遇见++写在a前面，++a先算，计算后的结果，再往位置上提供数据；
  // 11 + 1
  // console.log(b, a);


  var a = 10;
  // 先算右侧：
  // 每个位置上绝对有个数据参加运算；
  // 10(++写在a后面，先把自己数据推到位置，在进行自己计算a:11，计算后的结果和这个位置上10没有关系) + 12（++a：先运算，看此时a:11,计算完后 a:12,把计算结果推到位置上）
  var b = a++ + ++a;
  console.log(b);
```

- 用处：这个自增操作符会在后面学习`循环语法for`的时候会遇到；

  



## 比较操作符

- 需要：**常规：Number类型参与比较；**
- 语法：比较两个值的大小，**常规比较就是数字**
- 返回：**比较后的结果，对或错，Boolean值；标示状态成立与否；**

```js
// 语法：>  <  >=  <=   
// 常规操作
4 > 5 // 输出Boolean值  

// 非常规操作：非Number类型要和Number类型比较的话，非Number类型就要隐式转换为数字；
// 非常规：自己去试 null 、undefined、boolean；还是会隐式转化为数字；
console.log( "abc" < 5); // 输出 false
```

------

- `==` 和 `===` 是用来比较两个数据是否相等的;
- 需要：所有类型都可以；
- 返回：Boolean值；标示状态成立与否；

```js
// 语法：== 	!=  ===  !==
```

- 区别：
  - `==` 
    - **同类型：比较值是否一样；特别NaN==NaN  false**
    - **不同类型：转为Number类型，看值是否一样；**
  - `===` 
    - **同类型：再看值；**
    - **不同类型：false**;

```js
// 同类型：比值；返回都是true
console.log(11 == 11);
console.log("abc" == "abc");
console.log(null == null);
console.log(undefined == undefined);

// 同类型：特别的NaN，返回false
console.log(NaN==NaN)  

// 不同类型：非数字类转数字，
console.log("11" == 11);  // true，所以为true;


// 下面的为了解：有精力的同学可以啃下；目前不是我们的重点；
// 不同类型：特别的null 、undefined
// undefined和null与其他Number类型在进行相等判断时不进行类型转换。
console.log(null==0)         //false
console.log(0 == undefined); //false

// ECMAScript认为undefined是从null派生出来的，所以把它们定义为相等的;
console.log(null==undefined)  // true
```

- 拓展：[JS中Null与Undefined的区别](https://www.cnblogs.com/dyh-air/articles/7943295.html)
- `!=` 和`!==` 是比较两个数据是否不相等的；

```js
// 输出 false ,比较两个数据的值是否不相等, 此时两个数据的 值 都 4 ，相等，结果是 false
console.log('4'!= 4); 

// 输出 true ，比较两个数据的类型和值是否不相等，此时两个数据的类型不相等，结果是 true
console.log('4'!== 4); 
```



## 逻辑操作符

- 语法：&&  ||  ！
- 需要：
  - 常规：左右两边需要 true 或 false进行比较，**布尔类型的值进行逻辑判断，**
  - 非常规：需要转Boolean值；
- **返回：用Boolean值进行逻辑判断后，把最后一个成立或不成立的结果返回；**
- `&&` 且：所有条件都要满足的情况下；

```js
true&&true  //true;
true&&false    //false;

1&&2   // 2;


console.log("abc"&&1);  
console.log(null&&0);
```

- 特点：遇见有一个false，那么就直接返回false;

```js
// 用户在登录的时候要用户名和密码同时正确才能登录
var userName = prompt('请输入用户名');
var password = prompt('请输出密码');
console.log(userName === 'admin' && password === '123456');
// 只有 && 两边的 结果都是 true ，最终结果返回最后一个成立的结果；
```

------

- `||` 或：只要你有满足的条件就行；
- 特点：只有有一个true，那么就直接返回是true的这个结果;

```js
// 只要年龄小5岁 或者 身高小于120cm 就可以免费乘坐
var age = parseInt(prompt('请输入你的年龄'));
var height = parseFloat(prompt('请输入你的身高'));
console.log(age < 5 || height < 120);
// || 或者：两边的结果有一个是true，最终结果就是true
```

- `!` ：取反；Boolean值取反；

```js
var res = true;  
console.log(!res);
```





## 赋值运算符

- 语法：给变量赋值；

```js
var a = 1;

// 配合算术运算符在里面；
+=  -=  *=  /=  %=
```

- `+=` 的作用是简写加法，有**运算**在里面的赋值；

```js
// = 的作用就是把右边的结果赋值(存储)给左边的变量之类的容器
var a = 10;

// 相当于是 a = a + 2; 就是一个简写的语法
// -=   *=   /=   %= 除了运算规则不同，作用是一样的，都是简写
a += 2; 
console.log(a); // 输出12

// 非常规
var a = 'cc';
a +=2;
```





## 优先级

```
1. 第一优先级： ()
2. 第二优先级： ++ -- !
3. 第三优先级： *  /  %
4. 第四优先级： +  -
5. 第五优先级： >   >=   <   <=
6. 第六优先级： ==   !=    ===    !==  
7. 第七优先级： &&
8. 第八优先级： || 
9. 第九优先级： = += -= *= /= %=  
```

- 观察代码

```javascript
var a = 200 === (10 + 10) * 10 > 1;

// 先算括号
200===20*10>1

// 在算计算
200===200>1

// 算右侧；
200===true;

// false
console.log(a); 
```





# 流程控制

* 流程控制：我们想要实现一个复杂的效果，只简单的代码是肯定不行的，还要实现代码执行过程的控制；
* 生活：这种情况下，要做这件事；那种情况下，要做那件事；

## 表达式

* 特点：在js代码中，只要可以返回一个**结果**的，都可以称为一个表达式；

```js
// 下面都可以称为表达式
a++; //   a = a+1 ,
5 > 6; // 结果是 false
1+1；
只有结果返回就是表达式！

 10 + 10;

var a;
a = 10;  // 本身这个式子 结果返回的！结果是啥？最终赋值的那个数据！
```

* **技巧：在浏览器后台可以直接敲JS代码，回车返回的就是该表达式的结果；**
* 我们昨天学习的各种数据类型的转化，各种数据参与的运算符，最后都会返回一个结果（不算这个结果是多少），都可以称为一个表达式；



## 结构

* 写程序，就是写各种**语句的组织**，归根到底，就是各种表达式参与我们的思维的体现；在写代码的结构表现上分为下面三种：
  * 顺序结构：从上到下执行的代码就是顺序结构，**程序默认就是由上到下顺序执行的**；
  * 分支结构：**不同的情况下，走不同的分支；**
  * 循环结构：**重复**做一件事情，其作用就是用来重复执行代码的；
    * 特点：**重复，有规律的变化；**
* **程序的世界中大量业务的逻辑就是 分支和循环 相互套用；**





# 分支结构

* 作用：不同的条件，采取不同的行为；

## if 结构   !!!

* **if结构**：单个if结构，解决的一个分支的判断问题；

```js
// if语句：条件表达式的结果成立时，会怎么样；
// 条件表达式：需要返回Boolean值；如果返回的不是Boolean值，就隐式转化为Boolean值；
if(条件表达式) {
   // 当 条件表达式 的结果是 true 时 执行的代码
}

// 例如：判断一下一个人的性别是不是男的
var gender = prompt('请输入性别');
if(gender === '男'){
	console.log('这是一个男人');   
}
// 当输入的结果是 '男' 的时候，就会在控制台中输出消息，否则没有消息输出
```

* **if-else**：解决两个分支的判断问题

```js
if(条件表达式){
   //当条件表达式的结果是 true 时执行的代码
}
else {
  //当条件表达式的结果是 false 时执行的代码
}


//例如： 判断一下一个人的性别是不是男的,如果是男的，让他去男厕所，否则去女厕所
// 当输入的结果是 '男' ,输出 男厕所，否则输出 女厕所

var gender = prompt('请输入性别');
if(gender === '男'){
  console.log('请去男厕所');   
}
else {
  console.log('请去女厕所');
}
```

* **if-else-if**：解决多分支的判断问题，最后一个else可以省略；

```js
// 当满足这个
if(条件表达式1){
   //当条件表达式1的结果是 true 时执行的代码
}
else if(条件表达式2){
  //当条件表达式2的结果是 true 时执行的代码
}
else if(条件表达式3){
  //当条件表达式3的结果是 true 时执行的代码
}
// 中间可以继续写多个判断 ...
else {
  // 多个条件表达式的结果都是 false 的时候执行的代码
}


//例如: 判断一下一个人的性别是不是男的,如果是男的，让他去男厕所，如果是女的，让他去女厕所，否则不让他上厕所
var gender = prompt('请输入性别');
if(gender === '男'){
	console.log('请去男厕所');   
}
else if(gender === '女') {
  console.log('请去女厕所');   
}
else {
  console.log('你个不男不女的家伙，我们这里没有你能上的厕所，去别处吧');
}
```

* 注意上面为一组分支，里面有多个分支；
* 案例：求两个数的最大值；

```js
var num1 = prompt('请输入第一个数字');
var num2 = prompt('请输入第二个数字');

num1 = parseFloat(num1);
num2 = parseFloat(num2);

if(num1 < num2){
    console.log('第一个数字比较大，他是：' + num1);
}
else if ( num1 === num2 ){
    console.log('两个数字一样大');
}
else {
    // 如果以上两个条件都不成立，就必然是num1 < num2了
    console.log('第二个数字比较大，他是：' + num2);
}
```

* **看代码执行到哪？学会用调试；也可以用console.log();**



* **检验值3**



## switch-case结构

* 特点：用于多个**固定值**之间的判断，只能做固定值的判断

```js
switch （数据）{
  case 固定值1: 
    // 当 数据 === 固定值1 时执行的代码; 先看类型，再看值；
        
    break; // 表示当前 情况结束；
        
  case 固定值2: 
    // 背后：数据 === 固定值2 时执行的代码;
        
    break;

  case 固定值3: 
    // 当数据 === 固定值3时执行的代码;
        
    break;
        
        
  // ...中间还可以写多个判断
  
  default : 
    // 当数据和上面的所有固定值都不相等的时候执行的代码
    break;
}

```

* 了解：这个结构里面的break并不是必须的，如果两个 case 之间没有break ，执行完了第一个break 之后，会继续执行下面的case的代码；但是一般情况都是带着break的；
* 案例：输入星期几，看要做什么事情；

```js
switch (xq) {
    case '星期一':
        alert('今天上课');
        break;
    case '星期二':
        alert('健身');
        break;
    case '星期三':
        alert('休息');
        break;
    case '星期四':
        alert('吃饭');
        break;
    case '星期五':
        alert('上班');
        break;
    case '星期六':
        alert(123);
    case '星期日':
        alert('睡觉');
        break;
        // 可以加一个default，当我们的输入错误的时候，可以提示用户
    default :
        // 说明输入的不是星期1-星期日，提示用户输入有误
        alert('请输入星期一到星期日之间的星期数，您的输入有误');
        break;
}
```





## 三元表达式

* 表达式：**有值会返回**

* 语法：if else 两个分支的 简写；有返回值；

```js
// 表达式1 ? 表达式2 : 表达式3;

// 首先 要知道 表达式 会返回结果；
// 过程：先执行表达式1，判断其结果是true还是false，
// 如果是true，则执行表达式2，然后将 表达式2的执行结果 作为整个三元表达式的结果进行返回，
// 如果是false，则执行表达式3，并将 表达式3的结果 作为整个三元表达式的结果

//例如： 求二个数字中谁更大
var a = 10; var b = 20;
var max = a > b ? a : b;
console.log(max);
```

## 小结

* if else 多用于判断一个区间、不固定值的判断：灵活
* switch-case：多用于固定值的判断；比较限制；



