# jQuery基础

## 原生js入口函数与jQuery入口函数的区别

原生js入口函数`window.onload`和jQuery入口函数$(function)的区别主要有两点：

+ 加载模式不同，原生JS会等到DOM元素加载完毕并且图片也加载完毕之后再执行入口函数里面的代码，而jQuery会在DOM元素加载完毕之后，并不会等到图片加载完毕之后就去执行入口函数里面的代码。
+ 原生js如果编写了多个入口函数，后面编写的入口函数会覆盖前面编写的入口函数。而jQuery的入口函数可以有多个而且相互之间不会干扰

## 防止jQuery中'的冲突

+ 在js代码的最前面添加jQuery.noConflict()---------->表示释放掉`'$'`的使用权，释放之后就不可以再使用`'$`'符号，而是要改用jQuery。
+ 如果想用别的符号来代替`'$'`,则使用 `var 符号 = jQuery.noConflict()`。这样，这个符号的作用就和`'$'`一样了

## jquery的若干静态方法

### $.each()

此方法的作用和数组的forEach方法较为类似，但是也有所不同，具体表现在以下两点：

+ forEach只能遍历数组，不能遍历伪数组
+ 调用的形式有所不同

```javascript
<script>
    var array = [1,2,3,4,5];
	var obj = {0:1,1:2,2:3,3:4,4:5,length:5};
	
	//用原生js遍历这两个变量
    array.forEach(function(index,value){
        console.log(index+'-------'+value);
    });
    for(var key in obj){
		console.log(key+'------'+obj[key]);
    }
    
    //用jQuery遍历这两个变量
    $.each(array,function(value,index){
        console.log(value+'-------'+index);
    });
	 $.each(obj,function(value,index){
        console.log(value+'-------'+index);
    });
    
</script>
```

### $.map()

此方法和数组的map方法类似，具体不同之处如下:

+ 数组的map方法的回调函数有三个参数，顺序是index，value，array。第三个参数array就是遍历的数组本身。而jQuery的回调函数的参数只有两个，顺序为value，index。
+ $.map()方法可以用在伪数组上。

```javascript
<script>
    var array = [1,2,3,4,5];
	var obj = {0:1,1:2,2:3,3:4,4:5,length:5};
	
	//用原生js
    array.map(function(index,value,array){
        console.log(index+'-------'+value+'------'+array);
    });
    
    
    //用jQuery
    $.map(array,function(value,index){
        console.log(value+'-------'+index);
    });
	 $.map(obj,function(value,index){
        console.log(value+'-------'+index);
    });
    
</script>
```

#### 与$.each()方法的区别

`$.map()`和`$.each()`方法的区别主要有两点:

+ `$.map()`执行完的返回值是个空的数组，而`$.each()`的返回值是数组本身。
+ `$.each()`可以在回调函数里return来设置自己的返回值，但是`$.map()`的回调函数里没有return。

## $.holdready()

`$.holdready(true)`这个函数主要是用来在阻止写在`$('document').ready(function(){})`里面的代码执行的，当写成`$.holdready(false)`时候就会解除阻止。

#### tips--->webstorm使用技巧

+ 设置代码片段

  ![](E:\学习\jquery\1.PNG)

在活动模板里点击右边的侧边栏里的加号，在模板文本里面写入代码块，缩写里面填入快捷键，下面的Define里面选everywhere。

+ 设置默认浏览器打开快捷键

  ![](E:\学习\jquery\2.PNG)

