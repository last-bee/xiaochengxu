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
      &nbsp;`var that = this`     
      &nbsp;`wx.getUserInfo({`    
      &nbsp;`success: function (res) {`    
        &nbsp;`console.log(res.userInfo)`    
      &nbsp;`},`  
      &nbsp;`fail((err)=>{`  
       &nbsp;`console.log(err)`  
      &nbsp;`})`  
    &nbsp;`})`    
  `}`
* 授权成功
 `res.userInfo`为用户的信息
* 授权失败  
`{errMsg: "getUserInfo:fail auth deny"}`
