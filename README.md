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

# 优化
* 关键呈现路径  
	关键呈现路径是指浏览器所经历的一系列步骤，从而将html, css, js转换为在屏幕上呈现的像素内容  


* 越具体的css树需要花费的时间越长
	div h1{} > h1{}

* 在外链的tag上添加属于async, 这样浏览器会忽略脚本的请求继续解析dom
  获取JS的三种方式：
  	* 阻塞(<script type="text/javascript" src="***.jx"></script>)
  		* 按顺便渲染dom,请求js及css并解析渲染直到渲染完成再执行下一个
  	* 内联(<script> document.write('now') </script>);
  		* 不需要进行外链请求
  	* 异步(<script type="text/javascript" src="***.js" async></script>)
  		* 按顺序渲染dom并请求js,但是并不解析,不阻止css的解析,dom及css渲染完成之后再进行js的解析

* 浏览器能够同时下载外链文件，最低关键路径来回次数
* 管道
	* 通过css 或 js 做出了改动，浏览器会重新计算受到影响的元素的样式，经历 js->style->layout->paint->composite几个步骤
	* 如果仅更改了绘制属性(背景图片,文本颜色,阴影), 经历js->style->paint->composite几个步骤
	* 如涉及的更改不需要布局, 则经历js->style->composite几个步骤
* 网络应用的生命周期四大领取为LIAR(load, idle, animations, response /加载, 闲置, 动画, 响应)
* 任何涉及动作或屏幕手指操作的互动都需要达到60fps
* 对于任务属性，浏览器都必须运行布局，所以任何涉及位置的更改都有可能会导致强制同步布局
* 在动画的过程中，尽量避免布局和绘制流程
* 新版的chrome中rendering在console面板左边的三个点中, timeline被集成在Performance中
* 使用will-Change: transform/top/left/width/heigh

* bug
	* .htaccess  添加 Vary: Accept-Encoding 标头后项目报500错误
		<IfModule mod_headers.c>
		  <FilesMatch ".(js|css|xml|gz|html)$">
		    Header append Vary: Accept-Encoding
		  </FilesMatch>
		</IfModule>
	* 图片需要指定宽高吗