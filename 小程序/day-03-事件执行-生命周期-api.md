

# 小程序 day_03



## 事件的执行

### 为什么

* 必须知道：
  * 1.事件的执行的三个阶段：捕获、到达目标、冒泡：（参考webAPI 捕获与冒泡）
  * 2.事件默认是在冒泡阶段执行；
* 如果不清楚事件的执行，注册事件的时候在用户体验的时候可能会出现问题；



### 冒泡

* 演示：点击儿子时：同时触发了父级的事件；

![1580635101401](assets/1580635101401.png)

![1580635110316](assets/1580635110316.png)

![1580635154868](assets/1580635154868.png)

* **阻止冒泡语法：同时监听用户的触发行为，也阻止冒泡；**
  * catch:事件类型=“事件执行函数”
  * catch事件类型=“事件执行函数”

```html
<view class="p"  catch:tap="parent">
  <view class="s" catch:tap="child"></view>
</view>
```



### 捕获(了解)

* 为什么是了解？因为不这样设置；

* 设置事件在捕获阶段执行：

```html
<view class="p" capture-bind:tap="parent">
  <view class="s" capture-bind:tap="child"></view>
</view>
```

* 阻止捕获阶段的执行

```html
<view class="p" capture-catch::tap="parent">
  <view class="s" capture-catch::tap="child"></view>
</view>
```



### 互斥（了解）

* 基础语法：只要是mut-bind点击的事件，只会执行一个！

![1580636340786](assets/1580636340786.png)

![1580636319724](assets/1580636319724.png)



## 生命周期

* 生命：从生到死，都有特定的时间节点：18岁 大学毕业，结婚，生子，离世；

- **我们可以在特定的时间节点做相应的业务；**  比如：**页面显示后，请求数据；**

- 小程序中将生命周期分成两类，分别是应用级别App和页面级别Page。

- 生命周期函数：

  - **本质：就是内置的一些函数**
  - 时间：**到了特定的节点就会执行；**

- 为什么：

  - 我们写的每个页面都会在不同的时间初始化，出现，隐藏；这些特定的时间节点都可以使用生命周期函数进行监听；

  * **特别参数使用**

### 生命周期-App

* 基础语法：

```js
App({
  // 当第一次启动时，只会执行一次；就是启动了就执行；
  onLaunch: function() {
    console.log(1);
    wx.reques();
  },

  // 前台运行时
  onShow: function() {
    console.log(2);
  },
  // 后台运行时
  onHide: function() {
    console.log(3);
  },

  // 小程序抛出错误时，捕获错误时
  onError: function() {
    console.log("error");
  },

  // 小程序启动时且同时，设置的页面找不到时，
  // 启动后，再次找不到页面，这个函数不执行；
  onPageNotFound: function() {
    console.log("没有找到页面");
  }
})
```

* 点击 关闭按钮：**其实就是切后台，小程序并没有被关闭**

![1580651655444](assets/1580651655444.png)

* 什么时候被关闭：
  * 关机
  * 内存不够用时，微信会自动选择关闭小程序；
  * 或者小程序切后台超过一定的时间；

* 重点
  * onLaunch：在于有些逻辑不能写在onLaunch里面，因为只会在开启的时候才会执行一次！！
  * onShow
  * onHide
  * 编译模式：

![1580649794901](assets/1580649794901.png)



### 生命周期-Page

* 和整个项目一样，每个页面都有自己的生命周期；

* 基础语法

```js
Page({
  // 路径页面加载完时
  onLoad: function() {
    console.log("page-页面加载了");
  },

  // 页面显示时
  onShow: function() {
    console.log("page-页面显示");
  },

  // 页面渲染完成时
  onReady: function() {
    console.log("page-页面渲染完成时");
  },
    
  // 页面隐藏时
  onHide: function() {
    console.log("page-页面被隐藏的时候");
  },
})
```

* 演示：点击navigator
  * 从当前某个路径点击 ，点击navigator 路径转跳，**当前路径只是隐藏；并没有被销毁;**
  * **从其他路径，点击   返回 <  ，返回当前路径  只会执行 onShow，可以理解为页面只是被隐藏了，页面不会重新再次执行加载和渲染完成；**
  * 页面：第一次出现的时候；





### 场景值

* 场景值：小程序处于什么样的场景，会有一个特定的值；比如打开小程序的方式：扫码、转发、搜索
* 语法：

![1580652558726](assets/1580652558726.png)

![1580652388845](assets/1580652388845.png)

* **意义：比如需要统计小程序哪种方式打开的最多？集中更好的方式进行推广；**











### 地址参数

* 基础语法：

![1580653861403](assets/1580653861403.png)

* 把拿到的数据的id放入每个地址上

![1580653732732](assets/1580653732732.png)

* 点击相应的页面：获取参入的参数

![1580653939351](assets/1580653939351.png)

* 意义：可以往页面传入特定的参数，进行相应的数据请求；（商品详情页）



## API

* 应用程序接口：
  * 接口：
    * 给你机会，你可以拿到我身上（后台服务端）的数据，
    * 或者使用我的（前端内置的DOM操作）某些功能
  * 代码：
    * 后台的设计的接口 url地址
    * webAPI：document.qs();
* 小程序：学习API就是方法；顶级对象 `wx`
  * `wx.requset()`
* 文档：https://developers.weixin.qq.com/miniprogram/dev/api/

### wx.showLoading()

* 语法：加载框

```js
wx.showLoading({
  title: '加载中',
})

setTimeout(function () {
  wx.hideLoading()；
}, 2000)
```

### wx.showModal()

* 语法：显示一个弹出框

```js
wx.showModal({
  title: '提示',
  content: '这是一个模态弹窗',
  // 点击按钮的执行函数；
  success (res) {
    if (res.confirm) {
      console.log('用户点击确定')
    } else if (res.cancel) {
      console.log('用户点击取消')
    }
  }
});
```

### wx.showToast()

* 语法：点击后简单的信息提示

```js
wx.showToast({
    title: '成功',
    icon: 'success',
    duration: 2000
});
```



### wx.showActionSheet()

* 语法：显示系统的菜单，菜单项可以进行设置

```js
wx.showActionSheet({
  itemList: ['A', 'B', 'C'],
  success (res) {
    console.log(res.tapIndex)
  },
  fail (res) {
    console.log(res.errMsg)
  }
});
```



### wx.chooseImage()

* 从本地相册选择图片或使用相机拍照。

```js
wx.chooseImage({
 // 选择几张照片
  count: 1,
  // 所选的图片的尺寸：原图，压缩图
  sizeType: ['original', 'compressed'],
  // 来源：相册、相机
  sourceType: ['album', 'camera'],
  // 选择其中一项后的回调
  success (res) {
    // tempFilePath可以作为img标签的src属性显示图片
    const tempFilePaths = res.tempFilePaths;
  }
});
```

### wx.uploadFile()

* 将本地资源上传到服务器。

```js
wx.uploadFile({
    url: 'https://example.weixin.qq.com/upload', //仅为示例，非真实的接口地址
    filePath: "https://xx.com/asd/xxx.png",  //文件地址路径
    name: 'image_file',  // 默认后台接受的字段
    success (res){

    }
});
```









## 案例：测颜值

### 布局

![1580659804650](assets/1580659804650.png)

* wxml：

```html
<view class="box">
  <!-- 预览区 -->
  <view class="img">
    <image mode="aspectFit" src="/imgs/1.jpg" />
  </view>
    
    
  <!-- 信息区 -->
  <view class="infos">
    <view class="item">性别:女</view>
    <view class="item">年龄:26</view>
    <view class="item">颜值:100</view>
  </view>


  <!-- 按钮 -->
  <view class="btn">
    <button type="primary">上传照片</button>
  </view>

</view>
```

* wxss：

  * box：采用定位，相对于找定位的父级，就是窗口，w/h：100% 整个窗口
  * 复习：flex布局的相关属性；
  * 图片展示：mode的选择

  ![1580659963331](assets/1580659963331.png)

```css
.box {
  position: absolute;
  width: 100%;
  height: 100%;
  background-color: #ccc;
  display: flex;
  flex-direction: column;
}


/* 图片展示区 */

.box .img {
  height: 640rpx;
}

.box .img image {
  width: 100%;
  height: 100%;
}

.box .infos {
  flex: 1;
  display: flex;
  flex-direction: column;
  justify-content: center;
  font-size: 60rpx;
  font-weight: 800;
  text-align: center;
}


/* 按钮区 */
.box .btn {
  height: 100rpx;
}
```

### 需求

* 1.点击上传照片。注册点击事件；

* 2.选择照片，显示图片;

![1580662749427](assets/1580662749427.png)

* 3.返回数据，渲染到页面中；
  * https://ai.qq.com/
  * 测颜值API地址：https://ai.qq.com/cgi-bin/appdemo_detectface?g_tk=5381

![1580662940519](assets/1580662940519.png)

* 拿到数据后进行渲染：

![1580663009864](assets/1580663009864.png)

* loading优化

![1580663123852](assets/1580663123852.png)