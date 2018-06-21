---
layout: post
title: Jekyll搭建个人博客
date: 2016-10-14 
tags: 博客   
---


这里将介绍下微信小程序开发—(八)canvas绘制图形
     

### 步骤


wxml中：

     <canvas canvas-id="myCanvas" class="myCanvas" ></canvas>


     在js文件onLoad: function() {}的方法中开始编写代码




1.创建一个 Canvas 绘图上下文 CanvasContext
     const ctx = wx.createCanvasContext('myCanvas')



2.们来描述要在 Canvas 中绘制什么内容(绘图描述)

①.样式的描述


       ctx.setFillStyle('red')
②形状描述：填充矩形，描边矩形，圆，线段等
       ctx.fillRect(10, 10, 150, 75)



3.绘制
      ctx.draw()

### 效果


wxml中：

     <canvas canvas-id="myCanvas" class="myCanvas" ></canvas>
(1).绘制矩形：参数都是(起点x1,起点y1,宽度，长度)
①填充矩形
填充颜色：setFillStyle('red')


填充矩形:ctx.fillRect(10, 10, 150, 75)或是ctx.rect(10, 10, 150, 75)

如果没有填充颜色，则默认是黑色
js文件中



[html] view plain copy 
1.<span style='color: rgb(51, 51, 51); font-family: "Comic Sans MS"; font-size: 18px;'>const ctx = wx.createCanvasContext('myCanvas')  
2.ctx.setFillStyle('red')  
3.ctx.fillRect(10, 10, 150, 75)  
4.ctx.draw()</span>  

 



②描边矩形

描边颜色:ctx.setStrokeStyle('red')

描边矩形：setFillStroke()




[html] view plain copy 
1.<span style='color: rgb(51, 51, 51); font-family: "Comic Sans MS"; font-size: 18px;'>const ctx = wx.createCanvasContext('myCanvas')  
2.ctx.setStrokeStyle('red')  
3.ctx.strokeRect(10, 10, 150, 75)  
4.ctx.draw()</span>  



③清除画布上的矩形内容：ctx.clearRect(10, 10, 150, 75)

     注意： clearRect 并非画一个白色的矩形在地址区域，而是清空，为了有直观感受，对 canvas 加了一层背景色。

加了一层背景色吐舌头加了一层背景色吐舌头


wxml中：




[html] view plain copy 
1.<span style='color: rgb(51, 51, 51); font-family: "Comic Sans MS"; font-size: 18px;'><canvas canvas-id="myCanvas" style="border: 1px solid; background: #123456;"/></span>  

js中：



[html] view plain copy 
1.<span style='color: rgb(51, 51, 51); font-family: "Comic Sans MS"; font-size: 18px;'>   onLoad: function() {  
2.        const ctx = wx.createCanvasContext('myCanvas');  
3.        ctx.setFillStyle('red');  
4.        ctx.fillRect(0, 0, 150, 200);  
5.        ctx.setFillStyle('blue');  
6.        ctx.fillRect(150, 0, 150, 200);  
7.        ctx.clearRect(10, 10, 150, 75);  
8.        ctx.draw();  
9.    }</span>  



(2).路径

ctx.moveTo(10, 10)：把路径移动到画布中的指定点


ctx.lineTo(110, 60)：增加一个新点，然后创建一条从上次指定点到目标点的线


ctx.fill()：填充


1.填充

对当前路径中的内容进行填充。默认的填充色为黑色。
Tip: 如果当前路径没有闭合，fill() 方法会将起点和终点进行连接，然后填充。




[html] view plain copy 
1.<span style='color: rgb(51, 51, 51); font-family: "Comic Sans MS"; font-size: 18px;'>const ctx = wx.createCanvasContext('myCanvas')  
2.ctx.moveTo(10, 10)  
3.ctx.lineTo(100, 10)  
4.ctx.lineTo(100, 100)  
5.ctx.fill()  
6.ctx.draw()</span>  




Tip: fill() 填充的的路径是从 beginPath() 开始计算，但是不会将 fillRect() 包含进去。





[html] view plain copy 
1.<span style='color: rgb(51, 51, 51); font-family: "Comic Sans MS"; font-size: 18px;'>const ctx = wx.createCanvasContext('myCanvas')  
2.// begin path  
3.ctx.rect(10, 10, 100, 30)  
4.ctx.setFillStyle('yellow')  
5.ctx.fill()  
6.  
7.// begin another path  
8.ctx.beginPath()  
9.ctx.rect(10, 40, 100, 30)  
10.  
11.// only fill this rect, not in current path  
12.ctx.setFillStyle('blue')  
13.ctx.fillRect(10, 70, 100, 30)  
14.  
15.ctx.rect(10, 100, 100, 30)  
16.  
17.// it will fill current path  
18.ctx.setFillStyle('red')  
19.ctx.fill()  
20.ctx.draw()</span>  



### 2.描边

画出当前路径的边框。默认颜色色为黑色。




[html] view plain copy 
1.<span style='color: rgb(51, 51, 51); font-family: "Comic Sans MS"; font-size: 18px;'>const ctx = wx.createCanvasContext('myCanvas')  
2.ctx.moveTo(10, 10)  
3.ctx.lineTo(100, 10)  
4.ctx.lineTo(100, 100)  
5.ctx.stroke()  
6.ctx.draw()</span>  



 Tip: stroke() 描绘的的路径是从 beginPath() 开始计算，但是不会将 strokeRect() 包含进去.




[html] view plain copy 
1.<span style='color: rgb(51, 51, 51); font-family: "Comic Sans MS"; font-size: 18px;'>const ctx = wx.createCanvasContext('myCanvas')  
2.// begin path  
3.ctx.rect(10, 10, 100, 30)  
4.ctx.setStrokeStyle('yellow')  
5.ctx.stroke()  
6.  
7.// begin another path  
8.ctx.beginPath()  
9.ctx.rect(10, 40, 100, 30)  
10.  
11.// only stoke this rect, not in current path  
12.ctx.setStrokeStyle('blue')  
13.ctx.strokeRect(10, 70, 100, 30)  
14.  
15.ctx.rect(10, 100, 100, 30)  
16.  
17.// it will stroke current path  
18.ctx.setStrokeStyle('red')  
19.ctx.stroke()  
20.ctx.draw()</span>  

 



注意：



创建路径：ctx.beginPath()和ctx.closePath()


①.开始创建路径：ctx.beginPath()

开始创建一个路径，需要调用fill或者stroke才会使用路径进行填充或描边。
Tip: 在最开始的时候相当于调用了一次 beginPath()。
Tip: 同一个路径内的多次setFillStyle()、setStrokeStyle()、setLineWidth()等设置，以最后一次设置为准。


②.关闭路径：ctx.closePath()
 Tip: 关闭路径会连接起点和终点。
Tip: 如果关闭路径后没有调用 fill() 或者 stroke() 并开启了新的路径，那之前的路径将不会被渲染。







[html] view plain copy 
1.<span style='color: rgb(51, 51, 51); font-family: "Comic Sans MS"; font-size: 18px;'>const ctx = wx.createCanvasContext('myCanvas')  
2.ctx.moveTo(10, 10)  
3.ctx.lineTo(100, 10)  
4.ctx.lineTo(100, 100)  
5.ctx.closePath()  
6.ctx.stroke()  
7.ctx.draw()</span>  







3.线段：moveTo(10, 10)，lineTo(110, 60)参数都是点的坐标




[html] view plain copy 
1.<span style='color: rgb(51, 51, 51); font-family: "Comic Sans MS"; font-size: 18px;'>const ctx = wx.createCanvasContext('myCanvas')  
2.ctx.moveTo(10, 10)  
3.ctx.rect(10, 10, 100, 50)  
4.ctx.lineTo(110, 60)  
5.ctx.stroke()  
6.ctx.draw()</span>  




ab就是moveTo(10, 10)，lineTo(110, 60)绘制出的线段







4.画一条弧线：

ctx.arc(起点x1,起点y1,半径, 起始弧度,终止弧度,可选 弧度方向<false顺时针，true逆时针，默认是顺时针>)

Tip: 创建一个圆可以用 arc() 方法指定其实弧度为0，终止弧度为 2 * Math.PI。

Tip: 用 stroke() 或者 fill() 方法来在 canvas 中画弧线。





[html] view plain copy 
1.<span style='color: rgb(51, 51, 51); font-family: "Comic Sans MS"; font-size: 18px;'>var app = getApp()    
2.Page({  
3.    onLoad: function() {  
4.        const ctx = wx.createCanvasContext('myCanvas')  
5.        // 绘制一个灰色园  
6.        ctx.arc(100, 75, 50, 0, 2 * Math.PI)  
7.        ctx.setFillStyle('#EEEEEE')  
8.        ctx.fill()  
9.  
10.        //绘制一个坐标系  
11.        ctx.beginPath()  
12.        ctx.moveTo(40, 75)  
13.        ctx.lineTo(160, 75)  
14.        ctx.moveTo(100, 15)  
15.        ctx.lineTo(100, 135)  
16.        ctx.setStrokeStyle('#AAAAAA')  
17.        ctx.stroke()  
18.  
19.        //坐标系4个点的数字  
20.        ctx.setFontSize(12)  
21.        ctx.setFillStyle('black')  
22.        ctx.fillText('0', 165, 78)  
23.        ctx.fillText('0.5*PI', 83, 145)  
24.        ctx.fillText('1*PI', 15, 78)  
25.        ctx.fillText('1.5*PI', 83, 10)  
26.  
27.        // 绘制圆心那个点  
28.        ctx.beginPath()  
29.        ctx.arc(100, 75, 2, 0, 2 * Math.PI)  
30.        ctx.setFillStyle('lightgreen')  
31.        ctx.fill()  
32.  
33.        //绘制1.5*PI的那个点  
34.        ctx.beginPath()  
35.        ctx.arc(100, 25, 2, 0, 2 * Math.PI)  
36.        ctx.setFillStyle('blue')  
37.        ctx.fill()  
38.  
39.        //绘制0的那个点  
40.        ctx.beginPath()  
41.        ctx.arc(150, 75, 2, 0, 2 * Math.PI)  
42.        ctx.setFillStyle('red')  
43.        ctx.fill()  
44.  
45.        // 绘制黑线的弧度  
46.        ctx.beginPath()  
47.        ctx.arc(100, 75, 50, 0, 1.5 * Math.PI)  
48.        ctx.setStrokeStyle('#333333')  
49.        ctx.stroke()  
50.  
51.        ctx.draw()  
52.    }  
53.})</span>  




5.文字

ctx.setFontSize(20):字体的大小


ctx.setTextAlign('left');设置文字的对齐left,right,center


ctx.fillText('文字', 文字在画布中起点x1,起点y1):在画布上绘制被填充的文本。








[html] view plain copy 
1.const ctx = wx.createCanvasContext('myCanvas')  
2.  
3.ctx.setFontSize(20)  
4.ctx.fillText('Hello', 20, 20)  
5.ctx.fillText('MINA', 100, 100)  
6.  
7.ctx.draw()  


 6.渐变
grd.addColorStop(渐变点在起点和终点中的位置<0-1>, '颜色')：颜色渐变
Tip: 小于最小 stop 的部分会按最小 stop 的 color 来渲染，大于最大 stop 的部分会按最大 stop 的 color 来渲染。
Tip: 需要使用 addColorStop() 来指定渐变点，至少要两个。





①线性渐变:ctx.createLinearGradient(起点x1, 起点y1, 终点x2,终点y2)
 Tip: 需要使用 addColorStop() 来指定渐变点，至少要两个




[html] view plain copy 
1.onLoad: function() {  
2.    const ctx = wx.createCanvasContext('myCanvas')  
3.  
4.    // 创建线性渐变  
5.    const grd = ctx.createLinearGradient(0, 0, 200, 0)  
6.    grd.addColorStop(0, 'red')  
7.    grd.addColorStop(1, 'white')  
8.  
9.    // 绘制图形  
10.    ctx.setFillStyle(grd)  
11.    ctx.fillRect(10, 10, 150, 80)  
12.    ctx.draw()  
13.}  





②圆形渐变：ctx.createCircularGradient(圆点x,圆点y,半径)
Tip: 起点在圆心，终点在圆环。
Tip: 需要使用 addColorStop() 来指定渐变点，至少要两个。




[html] view plain copy 
1.onLoad: function() {  
2.    const ctx = wx.createCanvasContext('myCanvas')  
3.    // 创建圆形渐变  
4.    const grd = ctx.createCircularGradient(75, 50, 40)  
5.    grd.addColorStop(0, 'red')  
6.    grd.addColorStop(1, 'white')  
7.  
8.    // 绘制图形  
9.    ctx.setFillStyle(grd)  
10.    ctx.fillRect(10, 10, 150, 100)  
11.    ctx.draw()  
12.}  




7.阴影：ctx.setShadow(阴影x偏移, 阴影y偏移,模糊级别，数值越大越模糊, '颜色')
Tip: 如果没有设置，offsetX 默认值为0， offsetY 默认值为0， blur 默认值为0，color 默认值为 black。




[html] view plain copy 
1.const ctx = wx.createCanvasContext('myCanvas')  
2.ctx.setFillStyle('red')  
3.ctx.setShadow(10, 50, 50, 'blue')  
4.ctx.fillRect(10, 10, 150, 75)  
5.ctx.draw()  




8.旋转

①scale(x,y)方法对横纵坐标进行缩放:多次调用scale，倍数会相乘。




[html] view plain copy 
1.const ctx = wx.createCanvasContext('myCanvas')  
2.  
3.ctx.strokeRect(10, 10, 25, 15)  
4.ctx.scale(2, 2)  
5.ctx.strokeRect(10, 10, 25, 15)  
6.ctx.scale(2, 2)  
7.ctx.strokeRect(10, 10, 25, 15)  
8.  
9.ctx.draw()  




②ctx.rotate(旋转的角度)：对坐标轴进行顺时针旋转.
以弧度计(degrees * Math.PI/180；degrees范围为0~360)
以原点为中心，原点可以用 translate方法修改。顺时针旋转当前坐标轴。多次调用rotate，旋转的角度会叠加。




[html] view plain copy 
1.const ctx = wx.createCanvasContext('myCanvas')  
2.  
3.ctx.strokeRect(100, 10, 150, 100)  
4.ctx.rotate(20 * Math.PI / 180)  
5.ctx.strokeRect(100, 10, 150, 100)  
6.ctx.rotate(20 * Math.PI / 180)  
7.ctx.strokeRect(100, 10, 150, 100)  
8.  
9.ctx.draw()  





③translate(x坐标平移量,y坐标平移量)对坐标原点进行缩放




[html] view plain copy 
1.const ctx = wx.createCanvasContext('myCanvas')  
2.  
3.ctx.strokeRect(10, 10, 150, 100)  
4.ctx.translate(20, 20)  
5.ctx.strokeRect(10, 10, 150, 100)  
6.ctx.translate(20, 20)  
7.ctx.strokeRect(10, 10, 150, 100)  
8.  
9.ctx.draw()  




9.线条样式

①线条的宽度：ctx.setLineWidth(宽度px)
线条的端点样式:ctx.setLineCap('round');   值：'butt'、'round'、'square'





[html] view plain copy 
1.onLoad: function() {  
2.        const ctx = wx.createCanvasContext('myCanvas');  
3.        //绘制线段  
4.        ctx.moveTo(10, 10);  
5.        ctx.lineTo(150, 10);  
6.        ctx.stroke();  
7.  
8.        //线条的端点样式:butt  
9.        ctx.beginPath();  
10.        ctx.setLineCap('butt');  
11.        ctx.setLineWidth(10);  
12.        ctx.moveTo(10, 30);  
13.        ctx.lineTo(150, 30);  
14.        ctx.stroke();  
15.  
16.        //线条的端点样式:round  
17.        ctx.beginPath();  
18.        ctx.setLineCap('round');  
19.        ctx.setLineWidth(10);  
20.        ctx.moveTo(10, 50);  
21.        ctx.lineTo(150, 50);  
22.        ctx.stroke();  
23.  
24.        //线条的端点样式:square  
25.        ctx.beginPath();  
26.        ctx.setLineCap('square');  
27.        ctx.setLineWidth(10);  
28.        ctx.moveTo(10, 70);  
29.        ctx.lineTo(150, 70);  
30.        ctx.stroke();  
31.  
32.        ctx.draw();  
33.    }  




②线条的交点样式:ctx.setLineJoin('bevel')   值：'bevel'、'round'、'miter'
最大斜接长度：ctx.setMiterLimit(2)
斜接长度指的是在两条线交汇处内角和外角之间的距离。

 当 setLineJoin() 为 miter 时才有效。超过最大倾斜长度的，连接处将以 lineJoin 为 bevel 来显示




[html] view plain copy 
1.const ctx = wx.createCanvasContext('myCanvas');  
2.//绘制线段  
3.ctx.beginPath();  
4.ctx.moveTo(10, 10);  
5.ctx.lineTo(100, 50);  
6.ctx.lineTo(10, 90);  
7.ctx.stroke();  
8.  
9.ctx.beginPath();  
10.ctx.setLineJoin('bevel');  
11.ctx.setLineWidth(10);  
12.ctx.moveTo(50, 10);  
13.ctx.lineTo(140, 50);  
14.ctx.lineTo(50, 90);  
15.ctx.stroke();  
16.  
17.ctx.beginPath();  
18.ctx.setLineJoin('round');  
19.ctx.setLineWidth(10);  
20.ctx.moveTo(90, 10);  
21.ctx.lineTo(180, 50);  
22.ctx.lineTo(90, 90);  
23.ctx.stroke();  
24.  
25.ctx.beginPath();  
26.ctx.setLineJoin('miter');  
27.ctx.setLineWidth(10);  
28.ctx.moveTo(130, 10);  
29.ctx.lineTo(220, 50);  
30.ctx.lineTo(130, 90);  
31.ctx.stroke();  
32.  
33.ctx.draw();  





10.全局画笔透明度：ctx.setGlobalAlpha(0.2)

Tip：这个只针对在ctx.setGlobalAlpha(0.2);背后的图形有影响，在它之前的，则没有影响



[html] view plain copy 
1.onLoad: function() {  
2.    const ctx = wx.createCanvasContext('myCanvas');  
3.    ctx.setFillStyle('red');  
4.    ctx.fillRect(10, 10, 150, 100);  
5.    ctx.setGlobalAlpha(0.2);  
6.    ctx.setFillStyle('blue');  
7.    ctx.fillRect(50, 50, 150, 100);  
8.    ctx.setFillStyle('yellow');  
9.    ctx.fillRect(100, 100, 150, 100);  
10.    ctx.draw();  
11.}  




11.保存/恢复

在绘制一个整体的元素，特别是使用了图像变换时头尾必须采用save()，restore()
context.save();//保存
图像变换
设置状态
绘制(填充或是描边)
context.restore();//恢复





[html] view plain copy 
1.const ctx = wx.createCanvasContext('myCanvas')  
2.  
3.// save the default fill style  
4.ctx.save()   
5.ctx.setFillStyle('red')  
6.ctx.fillRect(10, 10, 150, 100)  
7.  
8.// restore to the previous saved state  
9.ctx.restore()  
10.ctx.fillRect(50, 50, 150, 100)  
11.  
12.ctx.draw()  




