# 学习小程序

## 下拉刷新

*在xx.json下配置`"enablePullDownRefresh": true`
*组件js中的`onPullDownRefresh`为下拉刷新的执行逻辑`wx.showNavigationBarLoading()`//在标题栏中显示加载 `wx.hideNavigationBarLoading()` //完成停止加载 `wx.stopPullDownRefresh()` //停止下拉刷新
