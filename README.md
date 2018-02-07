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

类型|触发条件
touchstart|手指触摸动作开始
touchmove|手指触摸后移动
touchcancel|手指动作被打断，如来电提醒|弹框
touchend|手指触摸动作结束
tap|手指触摸后马上离开
longpress|手指触摸后，超过350ms后离开，入火指定了回调函数并触发这个事件，tap时间将不被触发


