---
layout: post
title: "iOS 9 变化笔记"
date: 2018-06-21 18:15:06 
description: "iOS9 变化笔记, 以及工作中常遇到的问题"
tag: iOS
---
这里将介绍下小程序九：导航&地图&画布
     

### 示例代码：

index.wxss:

[javascript] view plain copy 

1./** 修改默认的navigator点击态 **/  
2..navigator-hover{  
3.    color:blue;  
4.}  
5./** 自定义其他点击态样式类 **/  
6..other-navigator-hover{  
7.    color:red;  
8.}  







index.wxml:

[javascript] view plain copy 

1.<view class="btn-area">  
2.    <navigator url="navigate?title=navigate" hover-class="navigator-hover">跳转到新页面</navigator>  
3.    <navigator url="redirect?title=redirect" redirect hover-class="other-navigator-hover">在当前页打开</navigator>  
4.</view>  
5.</navigator>  
6.<view style="text-align:center"> {{title}} </view>  
7.<view> 点击左上角返回回到之前页面 </view>  
8.  
9.<view style="text-align:center"> {{title}} </view>  
10.<view> 点击左上角返回回到上级页面 </view>  




index.js:

[javascript] view plain copy 

1.Page({  
2.  onLoad: function(options) {  
3.    this.setData({  
4.      title: options.title  
5.    })  
6.  }  
7.})  







map


--------------------------------------------------------------------------------
地图



属性名 

类型 

默认值 

说明 

longitude 
Number 
  
中心经度 

latitude 
Number 
  
中心纬度 

scale 
Number 
1 
缩放级别 

markers 
Array 
  
标记点 

covers 
Array 
  
覆盖物 



标记点

标记点用于在地图上显示标记的位置，不能自定义图标和样式



属性 

说明 

类型 

必填 

备注 

latitude 
纬度 
Number 
是 
浮点数，范围 -90 ~ 90 

longitude 
经度 
Number 
是 
浮点数，范围 -180 ~ 180 

name 
标注点名 
String 
是 
  

desc 
标注点详细描述 
String 
否 
  



覆盖物

覆盖物用于在地图上显示自定义图标，可自定义图标和样式



属性 

说明 

类型 

必填 

备注 

latitude 
纬度 
Number 
是 
浮点数，范围 -90 ~ 90 

longitude 
经度 
Number 
是 
浮点数，范围 -180 ~ 180 

iconPath 
显示的图标 
String 
是 
项目目录下的图片路径，支持相对路径写法 

rotate 
旋转角度 
Number 
否 
顺时针旋转的角度，范围 0 ~ 360，默认为 0 



地图组件的经纬度必填, 如果不填经纬度则默认值是北京的经纬度。

目前测试在正式环境是调用不出来的，不清楚原因。

示例：

index.wxml:

[javascript] view plain copy 

1.<map longitude="23.099994" latitude="113.324520" markers="{{markers}}" covers="{{covers}}" style="width: 375px; height: 200px;"></map>  







index.js:

[javascript] view plain copy 

1.Page({  
2.  data: {  
3.    markers: [{  
4.      latitude: 23.099994,  
5.      longitude: 113.324520,  
6.      name: 'T.I.T 创意园',  
7.      desc: '我现在的位置'  
8.    }],  
9.    covers: [{  
10.      latitude: 23.099794,  
11.      longitude: 113.324520,  
12.      icaonPath: '../images/car.png',  
13.      rotate: 10  
14.    }, {  
15.      latitude: 23.099298,  
16.      longitude: 113.324129,  
17.      iconPath: '../images/car.png',  
18.      rotate: 90  
19.    }]  
20.  }  
21.})<strong>  
22.</strong>  







canvas


--------------------------------------------------------------------------------





属性名 

类型 

默认值 

说明 


hidden 

Boolean 

false 

设置画布的显示/隐藏，hidden值为true表示隐藏，值为false表示显示 


canvas-id 

String 

  

canvas组件的唯一标识符 


binderror 

EventHandle 

  

当发生错误时触发error事件，detail = { errMsg: 'something wrong' } 



注：

1.
canvas标签默认宽度300px、高度225px
2.
同一页面中的canvas-id不可重复，如果使用一个已经出现过的canvas-id，该canvas标签对应的画布将被隐藏并不再正常工作
示例代码：

index.wxml:

[javascript] view plain copy 

1.<canvas style="width: 300px; height: 200px;" canvas-id="firstCanvas"></canvas>  
2.<!-- 当使用绝对定位时，文档流后边的canvas的显示层级高于前边的canvas-->  
3.<canvas style="width: 400px; height: 500px;" canvas-id="secondCanvas"></canvas>  
4.<!-- 因为canvas-id与前一个canvas重复，该canvas不会显示，并会发送一个错误事件到AppService -->  
5.<canvas style="width: 400px; height: 500px;" canvas-id="secondCanvas" binderror="canvasIdErrorCallback"></canvas>  







index.js:

[javascript] view plain copy 

1.Page({  
2.  canvasIdErrorCallback: function (e) {  
3.    console.error(e.detail.errMsg);  
4.  },  
5.  onReady: function (e) {  
6.  
7.    //使用wx.createContext获取绘图上下文context  
8.    var context = wx.createContext();  
9.  
10.    context.setStrokeStyle("#00ff00");  
11.    context.setLineWidth(5);  
12.    context.rect(0,0,200,200);  
13.    context.stroke()  
14.    context.setStrokeStyle ("#ff0000") ;  
15.    context.setLineWidth (2)  
16.    context.moveTo(160,100)  
17.    context.arc(100,100,60,0,2*Math.PI,true);  
18.    context.moveTo(140,100);  
19.    context.arc(100,100,40,0,Math.PI,false);  
20.    context.moveTo(85,80);  
21.    context.arc(80,80,5,0,2*Math.PI,true);  
22.    context.moveTo(125,80);  
23.    context.arc(120,80,5,0,2*Math.PI,true);  
24.    context.stroke();  
25.  
26.    //调用wx.drawCanvas，通过canvasId指定在哪张画布上绘制，通过actions指定绘制行为  
27.    wx.drawCanvas({  
28.      canvasId: 'firstCanvas',  
29.      actions: context.getActions() //获取绘图动作数组  
30.    });  
31.  }  
32.});  


