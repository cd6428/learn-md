

# 小程序 day_05



## 表单

### 组件

* 密码：设置password属性；
* 单选多选都是专门的组件；

```html
<form >
  <view class="item">
    <label >name:</label>
    <input type="text" />
  </view>
  <view class="item">
    <label>密码:</label>
    <input type="text"  password/>
  </view>
  <!-- 单选 -->
  <view class="item">
    <label>性别:</label>
    <radio-group>
      <radio  checked /> 男
      <radio  /> 女
    </radio-group>
  </view>
  <!-- 多选 -->
  <view class="item">
    <label>爱好:</label>
    <checkbox-group>
      <checkbox  checked />代码
      <checkbox  checked />睡觉
    </checkbox-group>
  </view>

  <button type="primary">提交</button>

</form>
```

### 数据

* wxml表单属性设置：
  * input 有`name`属性，用于提交；单选多选没有`name`属性
  * form组件绑定 submit事件，同时 button按钮 设置`form-type="submit"`用于submit或者`reset`

```html
<!-- 监听表单提交 -->
<form bind:submit="send">
  <view class="item">
    <label for="">姓名: </label>
    <input type="text"  name="username" />
  </view>
  <view class="item">
    <label for="">密码:</label>
    <input type="text" name="password" password />
  </view>
  <view class="item">
    <!-- 指定 form-type -->
    <button type="primary" form-type="submit">保存</button>
  </view>
    
    
   <!-- 单选 -->
  <view class="item">
    <label>性别:</label>
    <radio-group>
      <radio  checked /> 男
      <radio  /> 女
    </radio-group>
  </view>
  <!-- 多选 -->
  <view class="item">
    <label>爱好:</label>
    <checkbox-group>
      <checkbox  checked />代码
      <checkbox  checked />睡觉
    </checkbox-group>
  </view>
    

  <button type="primary" >提交</button>
</form>
```

* 获取数据：事件对象获取数据

```js
Page({
  data: {},
  send: function (ev) {
    // 通过 ev.detail 获取 input 组件中的数据
    console.log(ev.detail.value);
  }
})
```

![1580803853229](assets/1580803853229.png)

* 单选多选获取数据：
  * 绑定change事件，**通过事件对象获取；**
  * 只要一改变，就可以获取数据：

![1580804605204](assets/1580804605204.png)

* 点击提交按钮时：

![1580804994859](assets/1580804994859.png)



## 文档梳理及小结

* 梳理

![1580805774956](assets/1580805774956.png)

* 小结
  * tab:
    * 配置的tabBar
    * 自己写选项卡
  * 数据渲染：
    * wx:for
    * wx:if
    * hidden
  * 组件
    * 适配：rpx；
    * 常用：
      * view
      * navigator url="" ,可以带参数；
    * 声明周期：
      * onLoad：获取传入的参数；
    * 获取表单数据；
  * API
    * wx.request()
    * ...
  * 复用：
    * 组件
    * 模板
  * sitemap.json：用于被搜索规则的设置；



## 框架

### 介绍

* 用原生的小程序写的代码不够高效优雅：
  * 一个组件：有多个文件
  * 获取数据 `this.data.xx`    
  * 设置数据 `this.setData({...})` 
  * API大部分为异步，回调黑洞；
  * wxss语法比较低效；不执行less
* 市场大框架：wepy、mpvue、taro(基于react)、**uni-app**
* `uni-app` 是一个使用 [Vue.js](https://vuejs.org/) 开发所有前端应用的框架，开发者编写一套代码，可发布到iOS、Android、H5、以及各种小程序（微信/支付宝/百度/头条/QQ/钉钉）等多个平台。
* 我们要写一套代码：
  * VUE：v-指令 数据双向绑定
  * 通过一个工具 ：打包变为为 wx小程序可以识别的代码
  * 什么工具？一个封装的非常牛的webpack.js 基于nodejs文件；uni-app
  * nodejs:  fileSystem 
* vue：
  * 本身：用户界面的库，以组件的形式存在；
  * vue框架：vue+axios+vueRouter+vuex；
  * UI框架：Element、Vant；

![1580817119579](assets/1580817119579.png)

### 创建项目

* 全局安装vue-cli：node在8.9版本以上；这个步骤大家前面就已经操作了。不需要再操作了。

```bash
npm install -g @vue/cli
```

* 创建

```bash
vue create -p dcloudio/uni-preset-vue my-project
```

* 选择模板：选择默认

![1601278583830](assets/1601278583830.png)

* 运行并发布uni-app

```bash
npm run dev:%PLATFORM%
npm run build:%PLATFORM%
```

* `%PLATFORM%` 可取值如下：

  | 值            | 平台         |
  | ------------- | ------------ |
  | h5            | H5           |
  | mp-alipay     | 支付宝小程序 |
  | mp-baidu      | 百度小程序   |
  | **mp-weixin** | 微信小程序   |
  | mp-toutiao    | 头条小程序   |
  | mp-qq         | qq 小程序    |

* `npm run dev:mp-weixin`：生成dist目录下，dev文件夹，mp-weixin：

  * 监听模式：有文件变化，就把变化的文件实时编译到mp-weixin下；

![1580863804661](assets/1580863804661.png)

![1580863821585](assets/1580863821585.png)

* 微信小程序开发工具打开编译后的目录：

![1580864052168](assets/1580864052168.png)

* vue文件写代码，预览区实时更新：

![1580864331229](assets/1580864331229.png)



### 窗口配置

* 全局配置：

![1580864607157](assets/1580864607157.png)

* 页面局部配置：且优先于全局配置

![1580864753531](assets/1580864753531.png)



### 基本语法

![1580865109509](assets/1580865109509.png)



## Ugo-初始化

* 注意：
  * 真实UI给我们应该是750px的PSD图或者sketch
  * 如果不是750px，打回重写做；
* 配置less：
  * 1.安装：`npm i less less-loader -D`
  * 2.配置：`<style lang="less">`
* 布局：

![1580866748998](assets/1580866748998.png)





## Ugo-tabBar

- list：配置每项
  - text：文字
  - iconPath：图标路径，相对路径
  - selectedIconPath: 当前选择项的图标路径
  - pagePath：选项卡点击后的页面地址
- 文字颜色：
  - color：选项卡字体颜色
  - selectedColor:被选择中的字体颜色
  - 大小和字号：固定设置；

- 顶部线：
  - borderStyle：顶部线颜色，没有样式和宽度设置；只能为white或者black；
- 位置：
  - position：默认bottom;当设置top时，图标没有，下横线没有；

![1580919463393](assets/1580919463393.png)





## Ugo-首页布局

- 搜索区及轮播图

![1580879742512](assets/1580879742512.png)

- 导航区

![1580879801582](assets/1580879801582.png)

- 公共楼层

![1580881978079](assets/1580881978079.png)

- 第一楼层

![1580882088224](assets/1580882088224.png)









## Ugo-搜索组件

### 需求：封装组件

- 把搜索区封装为组件：
  - 一般在src/目录下新建components文件夹，创建组件

![1580885236293](assets/1580885236293.png)

- 在页面中使用：

![1580885270869](assets/1580885270869.png)

### 需求：分类页中使用

- 新建 分类 category页：

![1580885523622](assets/1580885523622.png)

- 配置分类页：
  - 配置单独的配置项；
  - 配置tabBar的指向；

![1580885633268](assets/1580885633268.png)



### 需求：点击搜索框，添加类名

- 需求：
  - 给input注册focus事件，
  - 聚焦后：给input的父级 添加一个设置好类名；(背景色、显示取消)
- 初始化准备：
  - 类名 focus
  - 取消盒子

![1580904065700](assets/1580904065700.png)

- 聚焦后：添加类名

![1580904139925](assets/1580904139925.png)



### 需求：点击取消，不添加类名

- 需求：
  - 给 取消 注册点击事件
  - 点击后：给input的父级 取消 设置好的灰色的类名；

![1580904204115](assets/1580904204115.png)



### 需求：取消按钮样式

- 需求：美化取消按钮，聚焦状态采用flex布局，初始化设置添加类名；

![1580904300630](assets/1580904300630.png)



### 需求：默认和聚焦状态的图标

- 默认状态、和聚焦状态有显示图标：

![1580891227777](assets/1580891227777.png)

- 经验：两个图标，两个盒子，分别在默认状态和聚焦状态控制其显示隐藏；

![1580891287351](assets/1580891287351.png)

- 背景图：使用网络图或者base64；

![1580891559029](assets/1580891559029.png)



### 需求：输入框的引导信息

- 需求：
  - 默认状态没有文字提示；
  - 聚焦状态有文字提示；

![1580892662714](assets/1580892662714.png)

- 聚焦状态的输入框样式优化：

![1580904387049](assets/1580904387049.png)



### 需求：历史搜索内容

- 聚焦状态的历史搜索内容的布局：

![1580904511396](assets/1580904511396.png)

- 通过v-show控制 历史搜索区显示或隐藏

![1580900719661](assets/1580900719661.png)



### 需求：首页中历史搜索的问题

- 问题：首页会出现滚动条，因为首页的盒子太多；

- 解决：

  - 聚焦：
    - 1.点击子组件的搜索区，触发事件，回调函数内部获取窗口高度；
    - 2.把获取窗口高度通过 **子组件**传递给 index页面的**父组件**;
    - 3.**父组件**拿到数据，设置跟标签高度为窗口高度，设置溢出隐藏；

  ![1580906953507](assets/1580906953507.png)

  - 取消
    - 1.点击子组件的取消，触发事件；
    - 2.把auto通过 **子组件**传递给 index页面的**父组件**;
    - 3.**父组件**拿到数据，设置跟标签高度为窗口高度，设置溢出隐藏；

![1580907120089](assets/1580907120089.png)

- 布局完成：以后不用自己写了，需要替换我给的SRC源码；







