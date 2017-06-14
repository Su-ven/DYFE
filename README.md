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
  
** 这里答案是第一个, 匿名函数后没有括号，所以这个函数还没有执行，并不能够得到函数结果 **  
  
#this  
** this是一个标识符，它需要和值进行绑定，跟变量差不多。 但是它是自动绑定在对象上。一般来说，this绑定在哪个对象上是由定位函数参数规则来决定的。 **  
<font color="#ff0000">this指向的对象，就是调用时候的点左边的方法(如没有，则默认是指向window)</font>  
