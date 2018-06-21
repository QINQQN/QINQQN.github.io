---
layout: post
title: "iOS 9 变化笔记"
date: 2018-06-21 18:15:06 
description: "iOS9 变化笔记, 以及工作中常遇到的问题"
tag: iOS
---


这里将介绍下Canvas 基本绘图Api记录
     

### 简介

Canvas我们可以称之为画布，能够在上面绘制各种东西，是安卓平台2D图形绘制的基础。绘制东西，需要4个元素协同来完成：

•位图：Bitmap 来保持（hold）那些像素


•画布：Canvas 来响应draw的调用


•画笔：paint 描述画画的颜色和样式等


•绘图基元：矩形、路径、文字、位图等其他元素



Api


drawColor / drawRGB / drawARGB（绘制颜色）
 /**
  * 使用指定的颜色填充整个画布
  */

  public void drawColor(@ColorInt int color)

  public void drawRGB(int r, int g, int b)

  public void drawARGB(int a, int r, int g, int b)1


drawPoint / drawPoints（绘制点）
//绘制单个点
public void drawPoint(float x, float y, @NonNull Paint paint)

public void drawPoints(new float[]{          //绘制一组点，坐标位置由float数组指定
      500,500,
      500,600,
      500,700
},mPaint);1
2
3
4
5
6
7
8


drawLine / drawLines（绘制直线） 
 // 在坐标(startX,startY)(stopX,stopY)之间绘制一条直线
 public void drawLine(float startX, float startY, float stopX, float stopY,Paint paint)

 public void drawLines(new float[]{               // 绘制一组线 每四数字(两个点的坐标)确定一条线
    100,200,200,200,
    100,300,200,300
  },mPaint);1



drawRect（绘制矩形）
// 左上角和右下角的两个点的坐标
public void drawRect(float left, float top, float right, float bottom,Paint paint);

// Rect精度为int
Rect rect = new Rect(100,100,800,400);
public void drawRect(Rect rect, Paint paint) ;

// Rect精度为float
RectF rectF = new RectF(100,100,800,400);
public void drawRect(RectF rectF, Paint paint);1



drawRoundRect（绘制圆角矩形）
//rx,ry是椭圆的两个半径
public void drawRoundRect(RectF rect, float rx, float ry, Paint paint)1



这里写图片描述

drawOval（绘制椭圆）
//绘制椭圆实际上就是绘制一个矩形的内切图形
public void drawOval(RectF oval, Paint paint)

public void drawOval(float left, float top, float right, float bottom, Paint paint) 1



这里写图片描述

drawCircle（绘制圆）
// 绘制一个圆心坐标在(cx,cy)，半径为radius 的圆。
public void drawCircle(float cx, float cy, float radius, Paint paint)  1



drawArc（绘制圆弧）
/**
* @param oval        矩形
* @param startAngle  开始角度
* @param sweepAngle  扫过角度
* @param useCenter   是否使用中心，false 圆弧起始点和结束点之间的连线加上圆弧围成的图形
* @param paint       The paint used to draw the arc
*/
public void drawArc(RectF oval, float startAngle, float sweepAngle, boolean useCenter, Paint paint)

// 第二种
public void drawArc(float left, float top, float right, float bottom, float startAngle,
            float sweepAngle, boolean useCenter, Paint paint) 1

这里写图片描述

drawBitmap（绘制图片）
// 第一种
public void drawBitmap (Bitmap bitmap, Matrix matrix, Paint paint)1


// 第二种 此处指定的是与坐标原点的距离，并非是与屏幕顶部和左侧的距离
public void drawBitmap (Bitmap bitmap, float left, float top, Paint paint)1


/**
*  第三种
*
* @param bitmap The bitmap to draw
* @param src   指定绘制图片的区域
* @param dst   指定图片在屏幕上显示(绘制)的区域
* 
* 图片宽高会根据指定的区域自动进行缩放。
* 
* 将bitmap取下大小为src区域的图片下来，放到dst大小的矩形中显示，取下的图片宽高会根据dst大小自动进行缩放
*/
public void drawBitmap (Bitmap bitmap, Rect src, Rect dst, Paint paint)
public void drawBitmap (Bitmap bitmap, Rect src, RectF dst, Paint paint)1



drawText（绘制文字）
// x,y 文字开始绘制的启示坐标
public void drawText(String text, float x, float y, Paint paint)1


// [start,end)　
public void drawText(String text, int start, int end,float x, float y, Paint paint)1



画布的操作


相关操作

简要介绍


save 保存当前画布状态 
translate 相对于当前位置位移，而不是每次基于原地(0,0)点移动 
rotate 旋转 
scale 缩放，canvas.scale(1,-1); // 翻转y坐标轴 
restore 回滚到上一次save的状态 


save(); //保存状态 
… //具体操作 
restore(); //回滚到之前的状态


canvas.scale(0.5f,0.5f); 
 canvas.scale(0.5f,0.1f);

调用两次缩放则 x轴实际缩放为0.5x0.5=0.25 y轴实际缩放为0.5x0.1=0.05


canvas.rotate(180); 
 canvas.rotate(20);

调用两次旋转，则实际的旋转角度为180+20=200度。
