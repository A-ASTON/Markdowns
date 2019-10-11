# React-Native
使用JavaScript和React编写原生移动程序

## 环境的搭建 
详细查看[搭建开发环境](https://reactnative.cn/docs/getting-started.html)   
十分蛋疼！需要搭建Android的开发环境啦，jdk用的是1.8版本啦，SDK要翻墙啦，还是看上面的文档吧。    

## 进行开发
主要记录一下用到的东西，还有一些坑：    
连接手机进行开发：开启USB调试是必须的，命令行：`adb devices`可查看是否成功连接该设备，连接成功后，使用`react-natvie run-android`可以在安卓机上跑了，IOS还没试过，摇晃手机可以选择RELOAD，实时加载更新后的代码。     
使用模拟器（和安卓开发时差不多），连接后的操作同上。


一边食用文档，一边开发更佳[React Native 中文网](https://reactnative.cn/docs/getting-started.html)   

开始开发时记得，js文件要引入react相关资源（基本操作了）   
`import React, { Component } from 'react';`

使用组件记得引入！！！`import { View } from 'react-native'`

触摸事件：可用组件Touchable、Button、View(用View结合手势响应系统)  
## 样式 
基本遵循css样式的编写，名字用驼峰式，编写规范和React一样   
建议采用如下方式整合，
```js
const styles = StyleSheet.create({
    Button: {
        color: 'red'
    }
});
```
需要注意的是：    
- textAlign,要用在Text组件上
- position：absolute浮动且相对于父组件定位，relative不浮动且相对于自身定位 没有fixed
- flex布局基本没啥不一样，只是flex的值只有number
- 任何属性都没有单位



## 手势响应系统  
文档异常难看！基本的手势响应系统，还没搞懂怎么用。用着[PanResponder](https://reactnative.cn/docs/panresponder/)先，一个更高级的手势功能：    
样板： 
```js
componentWillMount: function() {
    this._panResponder = PanResponder.create({
      // 要求成为响应者：
      onStartShouldSetPanResponder: (evt, gestureState) => true,
      onStartShouldSetPanResponderCapture: (evt, gestureState) => true,
      onMoveShouldSetPanResponder: (evt, gestureState) => true,
      onMoveShouldSetPanResponderCapture: (evt, gestureState) => true,

      onPanResponderGrant: (evt, gestureState) => {
        // 开始手势操作。给用户一些视觉反馈，让他们知道发生了什么事情！

        // gestureState.{x,y} 现在会被设置为0
      },
      onPanResponderMove: (evt, gestureState) => {
        // 最近一次的移动距离为gestureState.move{X,Y}

        // 从成为响应者开始时的累计手势移动距离为gestureState.d{x,y}
      },
      onPanResponderTerminationRequest: (evt, gestureState) => true,
      onPanResponderRelease: (evt, gestureState) => {
        // 用户放开了所有的触摸点，且此时视图已经成为了响应者。
        // 一般来说这意味着一个手势操作已经成功完成。
      },
      onPanResponderTerminate: (evt, gestureState) => {
        // 另一个组件已经成为了新的响应者，所以当前手势将被取消。
      },
      onShouldBlockNativeResponder: (evt, gestureState) => {
        // 返回一个布尔值，决定当前组件是否应该阻止原生组件成为JS响应者
        // 默认返回true。目前暂时只支持android。
        return true;
      },
    });
  },

  render: function() {
    return (
      <View {...this._panResponder.panHandlers} />
    );
  },
```


