---
title: Base64Image
date: 2018-01-28 15:52:45
tags: javascript base64 image
---

#### 小图标制作小技巧 ####

##### 思路 #####
> 很多图标网上搜不到,或是搜到又不是自己想要的,自己要动手制作,又需要一些图片处理软件,不是很方便,不如换个思路。利用js的canvas画图,画完之后再转为base64,即可在css中直接使用了。很是方便。

#### 实现 ####

``` javascript
1> 打开w3school的在线编辑 `http://www.w3school.com.cn/tiy/t.asp?f=html5_canvas`
2> copy下面代码
<!DOCTYPE HTML>
<html>
<body>

<canvas id="myCanvas" style="border:solid 1px black"></canvas>
<div id="result"></div>
<script type="text/javascript">

var canvas=document.getElementById('myCanvas');
var ctx=canvas.getContext('2d');
ctx.strokeStyle='#fed06a';
ctx.arc(12,12,10,0,2*Math.PI);
ctx.stroke();
ctx.fillStyle="#fed06a";
ctx.fill();
ctx.strokeStyle='white';
ctx.moveTo(7,11);
ctx.lineWidth=2;
ctx.lineTo(12,15);
ctx.lineTo(17,8);
ctx.stroke();

ctx.fillStyle='#fed06a';
ctx.beginPath();
ctx.arc(32,12,9,0,2*Math.PI);
ctx.arc(32,12,7,0,2*Math.PI);
ctx.fill("evenodd");

var result=document.getElementById('result');
result.innerHTML = canvas.toDataURL();
</script>

</body>
</html>
