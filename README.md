# 学习小程序

## 下拉刷新

* 在xx.json下配置`"enablePullDownRefresh": true`
* 组件js中的`onPullDownRefresh`为下拉刷新的执行逻辑  
`wx.showNavigationBarLoading()`//在标题栏中显示加载   
`wx.hideNavigationBarLoading()` //完成停止加载  
`wx.stopPullDownRefresh()` //停止下拉刷新
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


模块|小程序|vuejs
条件渲染 |wx:if | v-if
