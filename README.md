# 闭包  
	var sagas = [];  
	var hero = aHero();  
	var newSaga = function(){  
	 	var foil = aFoil();  
	 	sagas.push(function(){  
	 		var deed = aDeed();  
	 		console.log(hero+deed+foil)	;  
 		})  
	}  
  
	newSaga();  
	sagas[0]();  
	sagas[0]();  
	newSaga();  
  
**提问,这里的sagas是被push进了什么呢？**  
	1. 一个function object      
	2. 一个词法作用域 	  
	3. 一个执行上下文	  
	4. 一个匿名函数的结果  
  
**这里答案是第一个, 匿名函数后没有括号，所以这个函数还没有执行，并不能够得到函数结果**  
  
# this  
this是一个标识符，它需要和值进行绑定，跟变量差不多。 但是它是自动绑定在对象上。一般来说，this绑定在哪个对象上是由`定位函数参数规则`来决定的。
	<font color="#ff0000">this指向的对象，就是调用时候的点左边的方法(如没有，则默认是指向window)</font>  

# 原型链

# canvas
	加载一个图片
	drawImage(img对象(new Image()), 起始x坐标点, 起始y坐标点)
	获取图片信息(包括每个素材点的红绿蓝透明通道())
	var imgData = ctx.getImageData(起始x坐标点, 起始y坐标点, 目标width, 目标height);
	ctx.putImageData(imgData,0,0);
**例**  

    <script type="text/javascript">  
		var canvas = document.getElementById('c');  
		var ctx = canvas.getContext('2d');  
		var img = new Image();  
		img.src = 'imgs/timg.jpg';  
		img.onload = function(){  
			ctx.drawImage(img, 0, 0);  
			var imgData = ctx.getImageData(0,0,500,500);
			for (var i = 0; i < imgData.data.length; i++) {
					var average=(imgData.data[i*4]+imgData.data[i*4+1]+imgData.data[i*4+2])/3;
					// 这里，imgData.data分别代表R,G,B,A, 以四个为一个循环
					imgData.data[i*4] = average;
					imgData.data[i*4+1] = average;
					imgData.data[i*4+2] = average;
			}  
			// 把修改之后的色值重新赋予图像
			ctx.putImageData(imgData,0,0);  
		}  
		console.log(canvas);  
	</script>  

	# 文档	
	1. 标题，内容简介	
	2. 安装方法		
	3. 模块功能介绍
	4. 使用案例
	5. 可预见bug	
	6. 版本证书声明