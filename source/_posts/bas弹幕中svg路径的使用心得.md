---
title: bas弹幕中svg路径的使用心得
date: 2021-10-16 13:07:19
tags:
---
# 一、bas中path对象基本说明
bas弹幕中可以通过path对象来实现图片的展示
```
def path p {
  d = "M 0 0 L 100 0 L 100 100 "
  viewBox="0 0 100 100"
  x = 40%
  y = 15%
  borderWidth = 1
  borderColor = 0xffffff
  borderAlpha = 0.8
  fillColor = 0x00a1d6
  fillAlpha = 0.8
  width = 20%
  duration = 2s
  zIndex = 1
  scale = 0.8
}

```

|属性名|值类型|是否必须|默认值|是否可变|是否渐变|说明|
|-------|-------|-------|-------|-------|-------|-------|
|x|number|否|0|是|是|x坐标，可以为百分比值|
|y|number|否|0|是|是|x坐标，可以为百分比值|
|zIndex|number|否|0|否|否|层次权重，值高的对象在上层|
|scale|number|否|1|否|否|缩放|
|duration|time|否|-|否|否|元素生命周期，有动画时默认为动画总时间，无动画时默认4s|
|d|string|是|""|否|否|svg 路径|
|borderWidth|number|否|0|否|否|描边宽度|
|borderColor|number|否|0|否|否|描边颜色|
|borderAlpha|number|否|1|否|否|描边透明度|
|fillColor|number|否|0xffffff|否|否|填充颜色|
|fillAlpha|number|否|1|否|否|填充透明度|
|viewBox|string|否|-|否|否|svg 画布大小，默认完整显示|
|width|number|否|-|否|否|宽度，可以为百分比值，需要设置 viewBox 才可以生效|
|viewBox|string|否|-|否|否|宽度，可以为百分比值，需要设置 viewBox 才可以生效|
|<font color=#FF0000>parent</font>|string|否|-|否|否|父级|

# 二、bas中path对象进阶说明
基础的path对象只能实现x,y移动的动画效果，但如果给path对象添加parent父级属性，可以在父级上实现透明度、缩放、旋转等功能，从而实现子级效果。

例子：正方形淡入旋转效果
```
def text squareP{
    content = " "
    fontSize = 2%
    x = 50%
    y = 50%
    anchorX = 0.5
    anchorY = 0.5
    scale = 1
    zIndex = 5
    alpha = 0
    rotateZ = 0
}
def path square{
    fillColor = 0xeeeeee
    viewBox = "0 0 400 400"
    anchorX = 0.5
    anchorY = 0.5
    zIndex = 5
    width = 50%
    parent = "squareP"
    d="M 0 0 h 400 v 400 h -400 z"
}
set squareP {} 0ms 
then set squareP{ rotateZ = 360 alpha = 1 } 1s
```
# 三、svg路径
截取于svg之path详解（https://www.jianshu.com/p/c819ae16d29b）

1、直线命令
顾名思义，直线命令就是在两个点之间画直线。首先是“Move to”命令，M，需要两个参数，分别是需要移动到点的x轴和y轴的坐标。在使用M命令移动画笔后，只会移动画笔，但不会在两点之间画线。所以M命令经常出现在路径的开始处，用来指明从何处开始画。

大写字母，表示采用绝对定位。小写字母，表示采用相对定位。

解析：
M
    移动到的点的x轴和y轴的坐标
L
    需要两个参数，分别是一个点的x轴和y轴坐标，L命令将会在当前位置和新位置（L前面画笔所在的点）之间画一条线段。
H
    绘制平行线
V
    绘制垂直线
Z
    从当前点画一条直线到路径的起点

```
绘制正方形 d="M10 10 h 80 v 80 h -80 Z"
```

原理分析：画笔移动到(10,10)点，由此开始，向右移动80像素构成一条水平线，然后向下移动80像素，然后向左移动80像素，最后再回到起点。
