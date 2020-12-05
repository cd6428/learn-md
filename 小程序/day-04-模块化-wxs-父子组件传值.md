

# 小程序 day_04



## 模块化

### 基本使用

* 语法：小程序遵循的是类似 CommonJS 的规范。通过 module.exports 或 exports 对外暴露接口，通过 require 导入模块。
* 用处：公用的方法的可以写在一个JS文件内，供每个页面使用；

![1580716593405](assets/1580716593405.png)



### npm模块

* **小程序目前不支持直接引入 node_modules** , 开发者需要使用到 node_modules 时候使用小程序支持的 npm功能。

* 使用步骤：

  * `npm init -y`

  * `npm i mine -S`：随便下载我们需要用到的包

  * 点击微信开发工具 / 工具 / 构建npm：

    ![1580717065354](assets/1580717065354.png)

  * 详情/本地设置：使用npm模块

    ![1580717147899](assets/1580717147899.png)

  * 测试：

    ![1580717283875](assets/1580717283875.png)

* 小程序寻找包的规则：在JS页面中使用`require`
  * 优先：寻找`miniprogram_npm`下的包
  * 如果没有，则找当前路径下，有没有这个名字的JS文件
  * 如果没有，则页面报错找不到；



### getApp()

* 文件作用域：在 JavaScript 文件中声明的变量和函数只在该文件中有效；不同的文件中可以声明相同名字的变量和函数，不会互相影响。
* 定义全局的数据：

![1580718071548](assets/1580718071548.png)

* 在任何页面的JS中使用：

![1580718169881](assets/1580718169881.png)

* 意义：共享数据和方法

![1580718687058](assets/1580718687058.png)

### 需求

* 设置公共函数：可以把每个页面要显示在视图层的数据，两边都加上 `***_ info _***`

* 可以设置在某个JS文件内，或者在App的对象内；

![1580719208469](assets/1580719208469.png)

* 在页面的JS内引入使用：

![1580719351548](assets/1580719351548.png)

* 页面没有显示：

![1580719420042](assets/1580719420042.png)

* 目前解决：但是这样操作其实已经改变JS内置的data的数据了；

![1580719772712](assets/1580719772712.png)



## wxs

### 不显示的原因-了解

* 不显示：

![1580720049000](assets/1580720049000.png)

![1580720091446](assets/1580720091446.png)

* 原因：小程序被设计为渲染层 和逻辑层，且渲染层 和逻辑层是相互孤立的

![1580720298529](assets/1580720298529.png)

### 基本使用

* 渲染层：有三个层：wxml wxss wxs；(可以理解为html css js)

![1580720441000](assets/1580720441000.png)

* wxml 就可以使用 wxs的数据；

* 需知：
  * 1.使用wxs,要通过wxs标签在wxml引入；
  * 2.wxs标签支持模块化：可以使用`module.exports`
  * 3wxs标签 必须 有 module 属性（属性值就是该wxs标签内部作为模块导出的对象名，可以在wxml内使用）

![1580721205800](assets/1580721205800.png)

![1580721229513](assets/1580721229513.png)

![1580721380729](assets/1580721380729.png)

### 公共wxs

* 定义wxs文件：
* 引入，使用

![1580722094928](assets/1580722094928.png)

* 意义：
  * 1.解决模块化的需求
  * 2.可以在wxml标签内直接使用定义的方法，而且和JS的内置的逻辑没有任何关系，非常的方便！

* 语法使用：https://developers.weixin.qq.com/miniprogram/dev/reference/wxs/
  * 变量 不能使用 const
  * 定义变量没有$
  * 其他的使用：按照基础的使用来就行；



### 作用!!!

* 自己的定义的JS文件或者在App内设置的数据，可以作为公共数据分享；
* npm模块：第三方模块包，已经写好得更为丰富的方法；
* wxs：**其实就是在负责渲染层（视图层）的数据展示处理，就是vue中的数据过滤；**



## 组件

### 页面内组件

* 语法：

![1580731906305](assets/1580731906305.png)

* index.js、index.json

![1580732549560](assets/1580732549560.png)

* 小程序自定义组件与页面主要有两点不同：
  * 页面JS调用的函数不同；
  * JSON配置：有标识自己为组件的属性 `*component*`

* 在页面中使用：
  * 在index.json文件中注册
  * 在wxml中使用；单标签双标签都可以

![1580732628863](assets/1580732628863.png)

### 父子组件

* 定义父级组件：

![1580733131885](assets/1580733131885.png)

* 定义子组件：

![1580733203038](assets/1580733203038.png)

* 子组件在父组件内使用：

![1580733263901](assets/1580733263901.png)

### 通信：父级-->子级

* 父级传递数据：传递给子级的属性上：

![1580733643776](assets/1580733643776.png)

* 子级：接受数据，设置属性：

![1580733828085](assets/1580733828085.png)

### 通信：子级-->父级

* 子组件JS：定义自定义事件名称：

![1580734663182](assets/1580734663182.png)

* 子组件wxml：在子组件内调用函数及触发：

![1580734696770](assets/1580734696770.png)

* 父组件wxml：子组件绑定自定义事件及父级的回调函数：

![1580734860464](assets/1580734860464.png)

* 父组件JS：f_send函数内部：

![1580734931978](assets/1580734931978.png)





## Vant Weapp

* Vant Weapp 是移动端 Vue 组件库 [Vant](https://github.com/youzan/vant) 的小程序版本，两者基于相同的视觉规范，提供一致的 API 接口，助力开发者快速搭建小程序应用。 

* 安装：

```bash
# 通过 npm 安装
npm i vant-weapp -S --production
```

* 小程序工具配置：

![1580738251073](assets/1580738251073.png)

* 在app.json或者页面.json 注册组件：

```json
"usingComponents": {
  "van-button": "vant-weapp/button"
}
```

* 按钮：

```
<van-button type="primary">按钮</van-button>
```

* 其他演示：

![1580739086533](assets/1580739086533.png)





## F2

* F2 是一个专注于移动，开箱即用的可视化解决方案，完美支持 H5 环境同时兼容多种环境（Node, 小程序，Weex），完备的图形语法理论，满足你的各种可视化需求，专业的移动设计指引为你带来最佳的移动端图表体验。 
* https://f2.antv.vision/zh：使用文档 针对vue；

* 安装

```bash
npm i @antv/f2-canvas -S
```

* 工具构建配置：

![1580738251073](assets/1580738251073.png)

* 页面中注册：

```json
{
  "usingComponents": {
    "ff-canvas": "@antv/f2-canvas"
  }
}
```

* wxml: 组件的规定
  - 必须有父级盒子：类名为container；
  - ff-canvas：必须必须设置宽高；
* JS初始化：

```html
<view class="container">
  <ff-canvas id="column-dom" canvas-id="column" opts="{{opts}}"></ff-canvas>
</view>
```

- 参考学习地址：https://www.yuque.com/antv/blog/bg9sxf

```js
let chart = null;

function initChart(canvas, width, height, F2) {
  // 图表数据（也可通过请求后端获得）
  const data = [
    { year: '1951 年', sales: 38 },
    { year: '1952 年', sales: 52 },
    { year: '1956 年', sales: 61 },
    { year: '1957 年', sales: 145 },
    { year: '1958 年', sales: 48 },
    { year: '1959 年', sales: 38 },
    { year: '1960 年', sales: 38 },
    { year: '1962 年', sales: 38 },
  ];
  
  // 实例化图表
  chart = new F2.Chart({
    el: canvas,
    width,
    height
  });
	
  // 配置图表数据
  chart.source(data, {
    sales: {
      tickCount: 5
    }
  });
  
  chart.interval().position('year*sales');
  chart.render();
  return chart;
}

Page({
  data: {
    // 图表参数
    opts: {
      onInit: initChart
    }
  }
});
```


## 日历

* github地址：https://github.com/treadpit/wx_calendar   没有npm包可以使用；

* 下载github并解压缩，拷贝 calendar 文件到小程序项目下
* 注册组件：

```json
{
  "usingComponents": {
    "calendar": "/component/calendar/index"
  }
}
```

* wxml：

```wxml
<calendar />
```

