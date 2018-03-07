# 学习小程序
## json文件
> app.json
  + `app.json`文件用来对微信进行全局配置，决定页面文件的路径、窗口表现、设置网络超时时间、设置多tab等
  + 以下是一个包含了所有配置选项的app.json
  ``` javascript
      {
        "pages": [
          "pages/index/index",
          "pages/logs/index"
        ],
        "window": {
          "navigationBarTitleText": "Demo"
        },
        "tabBar": {
          "list": [{
            "pagePath": "pages/index/index",
            "text": "首页"
          }, {
            "pagePath": "pages/logs/logs",
            "text": "日志"
          }]
        },
        "networkTimeout": {
          "request": 10000,
          "downloadFile": 10000
        },
        "debug": true
      }
  ```
> app.json 配置项列表  

| 属性 | 属性 |必填 | 描述 |  
| :--- | :--- | :--- | :---|  
|pages|String Array|是|设置页面路径|  
|window|Object|否|设置默认页面的窗口表现|  
|tabBar|Object|否|设置底部 tab 的表现|  
|networkTimeout|Object|否|设置网络超时时间|  
|debug|Boolean|否|设置是否开启 debug 模式| 

> pages 
  + pages接收的一个数组，每一项都是字符串，来指定小程序由哪些页面组成。每一项代表对应页面的【路径+文件名】信息， <strong> 数组的第一项代表小程序的初十页面。小程序中新增/减少页面，都需要对pages数组进行修改 </strong>  
  + 文件名不需要写文件后缀，因为框架会自动去寻找路径下 .json, .js, .wxml, .wxss 四个文件进行整合。
  + 如开发目录为：
  ```
    pages/
    pages/index/index.wxml
    pages/index/index.js
    pages/index/index.wxss
    pages/logs/logs.wxml
    pages/logs/logs.js
    app.js
    app.json
    app.wxss
  ```
  **则需要在 app.json 中写**
  ```
    {
      "pages":[
        "pages/index/index",
        "pages/logs/logs"
      ]
    }
  ```
## window  
用于设置小程序的状态栏、导航栏、标题窗口背景色。

| 属性 | 类型	|默认值|描述|最低版本|  
| :--- | :--- | :--- | :---|  :--- | 
 |navigationBarBackgroundColor | HexColor | #000000 | 导航栏背景颜色，如"#000000"	| |  


**注：HexColor(十六进制颜色值) ， 如："#FFFFFF"**  
**注：navigationStyle只在app.json中生效。开启 custom 后，低版本客户端需要做好兼容。开发者工具基础库版本切到 1.7.0（不代表最低版本，只供调试用） 可方便切到旧视觉**
## 下拉刷新

* 在xx.json下配置`"enablePullDownRefresh": true`
* 组件js中的`onPullDownRefresh`为下拉刷新的执行逻辑  
`wx.showNavigationBarLoading()`//在标题栏中显示加载   
`wx.hideNavigationBarLoading()` //完成停止加载  
`wx.stopPullDownRefresh()` //停止下拉刷新
## 加载更多
**`bindscrolltolower = moreLoad`滚动到底部或右侧触发事件**
#### 在制作加载更多时会发现不能触发相应事件
* scroll-view不设高度也可以触发
* 不设置高度无法触发`bindscroll`
* scroll-view的滚动方向是否设置
## 配置页面的信息  
`navigationBarTitleText`为标题的title  
`"enablePullDownRefresh": true`  
## 授权获取用户信息  
`getUserInfo(){`    
      `var that = this`     
      `wx.getUserInfo({`    
      `success: function (res) {`    
        `console.log(res.userInfo)`    
      `},`  
      `fail((err)=>{`  
       `console.log(err)`  
      `})`  
    `})`    
  `}`
* 授权成功
 `res.userInfo`为用户的信息
* 授权失败  
`{errMsg: "getUserInfo:fail auth deny"}`
---
获取用户信息在全局存储  
`app.globalData`

## 事件
   `bindtap="tapName"`相当于tap事件  pc的click点击事件  
   在js中写对应的函数  
   `Page({`  
  `tapName: function(event) {`  
    `console.log(event)`  
  `}`  
`})` 


| 类型 | 触发条件 | 
| - | :-: |
| touchstart | 手指触摸动作开始 |
| touchmove | 手指触摸后移动 |
| touchcancel |手指动作被打断，如来电提醒，弹框 |
| touchend | 手指触摸动作结束 |
| tap | 手指触摸后马上离开 |
| longpress | 手指触摸后，超过350ms后离开，入火指定了回调函数并触发这个事件，tap时间将不被触发 |
| longtap | 手指触摸后，超过350ms再离开（推荐使用longpress事件代替） |
| transitionend | 会在 WXSS transition 或 wx.createAnimation 动画结束后触发 |
| animationstart | 会在一个 WXSS animation 动画开始时触发 |
| animationiteration | 会在一个 WXSS animation 一次迭代结束时触发 |
| animationend | 会在一个 WXSS animation 动画完成时触发 |

<strong>注：除上表之外的其他组件自定义事件如无特殊声明都是非冒泡事件，如<form/>的submit事件，<input/>的input事件，<scroll-view/>的scroll事件，(详见各个组件)</strong>

---
### 事件绑定和冒泡
* key 以bind或catch开头，然后跟上事件的类型，如bindtap、catchtouchstart。自基础库版本 1.5.0 起，bind和catch后可以紧跟一个冒号，其含义不变，如* *  bind:tap、、catch:touchstart。
* value 是一个字符串，需要在对应的 Page 中定义同名的函数。不然当触发事件的时候会报错。
<strong>bind事件绑定不会阻止冒泡事件向上冒泡，catch事件绑定可以阻止冒泡事件向上冒泡。</strong>
``` html
<view id="outer" bindtap="handleTap1">
  outer view
  <view id="middle" catchtap="handleTap2">
    middle view
    <view id="inner" bindtap="handleTap3">
      inner view
    </view>
  </view>
</view>
 ```
**更多的事件请参考 [小程序事件](https://mp.weixin.qq.com/debug/wxadoc/dev/framework/view/wxml/event.html)。**
## 数据绑定、列表渲染、条件渲染、模板和vuejs相似 

|模块|小程序|vuejs|
|:---|:---:|:---|
|数据绑定|{{message}}|{{message}}|
|列表渲染|wx:for/wx:for-index="index" wx:for-item="item"|v-for/item,index|
|条件渲染 |wx:if | v-if|
|模板|WXML提供模板（template）|vue注册引用|
|引用|import直接is使用|import compents注册使用|


**注意： 花括号和引号之间如果有空格，将最终被解析成为字符串  
 花括号和引号之间如果有空格，将最终被解析成为字符串  
 name为模板的名字，is引用
 include  可以将目标文件除了 <template/> <wxs/> 外的整个代码引入，相当于是拷贝到 include 位置
 **  
 
 ## WXSS
 用css编写就可以用于描述wxml的组件样式  
 为了适应广大的前端开发者，WXSS 具有 CSS 大部分特性。同时为了更适合开发微信小程序，WXSS 对 CSS 进行了扩充以及修改。
 ### 与css相比 wxss扩展的特性有
 * 尺寸单位
 * 样式导入
 ### 尺寸单位 
 * 相当于rem 在iphone6的屏幕上1rpx = 1物理像素 响应式布局
 
 |设备|	rpx换算px (屏幕宽度/750)|px换算rpx (750/屏幕宽度)|
 |:---|:---:|:---|
 |iPhone5|1rpx = 0.42px|1px = 2.34rpx|
 |iPhone6|1rpx = 0.5px|1px = 2rpx|
 |iPhone6 Plus|1rpx = 0.552px|1px = 1.81rpx|
 ## 内联样式
 `<view style="color:{{color}};" />`
 `<view class="normal_view" />`
 ## 全局样式与局部样式
 * app.wxss 中的样式为全局样式  
 *  page 的 wxss 文件中定义的样式为局部样式 只作用在对应的页面，并会**覆盖 app.wxss** 中相同的选择器

