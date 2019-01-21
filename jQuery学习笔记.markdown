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

## jquery内容选择器

#### :empty

找到既没有文本内容也没有子元素的指定元素

```javascript
var $div=$('div:empty')
//用来寻找里面既没有包括子元素也没有文本内容的div
```

#### :parent

找到有子元素或者包括文本内容的指定元素

```javascript
var $div = $('div:parent')
//找到有子元素或者包括文本内容的的div
```

#### :contains(text)

找到包含指定文本内容的指定元素。

```javascript
var $div = $('div:contains("我是div")')
//找到里面包含有(不是只有)文本内容为‘我是div’的div元素。
```

#### :has(selector)

找到包括指定子元素的指定元素

```javascript
var $div = $('div:has("span")')
//找到里面包含有span标签的div标签。
```

### 属性和属性节点

#### 属性：对象身上保存的变量就是属性

#### 属性节点：在编写HTML代码的时候，在HTML标签中添加的属性就是属性节点。DOM元素的属性节点都保存在这个DOM元素的attributes属性中。

#### 区别：任何对象都有属性，但是只有DOM元素才有属性节点。

### 操作属性节点

#### 原生JS操作属性节点

##### DOM元素.setAttribute('属性名称'，‘值’)；-------->用来为DOM元素添加属性节点

##### DOM元素.getAttribute('属性名称')------------->用来获取指定DOM元素的指定属性节点的值

```javascript
document.getElementsByTagName("span")[0].getAttribute('name')
//无论当前页面有多少个div，都只会返回第一个div的name属性的值。
```

```javascript
document.getElementsByTagName("span")[0].setAttribute('name','gouku')
//会把当前页面所有div元素的name属性都设置为gouku
```

#### jQuery操作属性节点的方法-------->attr()

`attr(name|pro|key,val|fn)`作用：用来获取或者设置属性节点

```javascript
$('div').attr('name','gouku')
//将当前页面中所有div标签的name都设置为gouku
$('div').attr('name')
//获取当前页面中第一个div元素的name属性的值。
```

**注意**

+ 该方法既可以设置属性节点的值，也可以获取属性节点的值，如果传入一个参数就是获取属性节点的值，如果是两个参数就是设置属性节点的值。
+ 在获取属性节点的时候，无论找到多少个元素，都只会返回第一个元素指定属性节点的值。
+ 在设置属性节点时，会把找到的所有元素的该属性节点的值都设置成指定的值。

`removeAttr(name)`作用：用来删除指定元素的属性节点

```javascript
$('div').removeAttr('name')
//删除当前页面中所有的div元素的name属性。
```

**注意**

+ 该方法会删除掉当前页面所有的指定元素的指定属性。

### 操作属性

#### jQuery操作属性的方法

##### .prop()方法

特点：与attr()方法一致，传入一个参数表示获取目标属性的值，传入两个参数表示设置目标属性的值。

**注意**

+ .prop()方法不仅能够操作属性，也可以操作属性节点。官方推荐在操作属性节点时,具有 true 和 false 两个属性的属性节点，如 `checked`, `selected` 或者 `disabled` 使用prop()，其他的使用 attr()

##### .removeProp()方法

特点：与removeAttr()方法一致

### jQuery操作类相关的方法

#### .addClass()

**作用**：为标签添加一个或者多个类，如果要添加多个类，类名之间用空格隔开。

**注意**：添加样式的时候，如box样式时，不需要addClass('.box'),只需要addClass('box')。

#### .removeClass()

**作用**：为标签删除一个或者多个类，如果要删除多个类，类名之间用空格隔开。

#### .toggleClass()

**注意**：切换类，即如果当前标签没有这个类就添加，如果有这个类就删除这个类。

### jQuery文本值相关的方法

#### .html()

**作用**：和原生JS的innerHTML一致

#### .text()

**作用**：和原生JS的innerText一致。

#### .val()

**作用**：和原生JS的value一致

### jQuery操作css样式的方法

#### .css()-------->用来设置或者获取指定元素的css样式值。

```javascript
$('div').css('width','200px');
//设置当前页面的所有div的css样式中的width为200px
$('div').css('width');
//获取当前页面的第一个div的css样式中的width值。
$('div').css({
    width:"200px",
    height:"200px",
    background-color:"red"
})
//批量设置
```

### jQuery位置和尺寸操作的方法

#### .width()------->获取或者设置指定元素的width

```javascript
$('div').width()
//获取div元素的width
$('div').width('200px')
//将div元素的width设置为200px
```

#### .offset()--------->获取或者设置元素距离窗口的偏移位

```javascript
$('div').offset().left
//获取div元素距离浏览器窗口左边的距离
$('div').offset({
    left:'10px'
})
//将div元素距离浏览器窗口左边的距离设置为10px
```

**注意**

+ .offset()方法的返回值是一个对象。这个对象里面有两个属性，分别为left和top

#### .position()------->获取元素距离定位元素的偏移位

```javascript
$('div').position().left
//获取当前div距离定位元素的左偏移位
```

**注意**：

+ position方法只能获取，不能设置。
+ position()方法的返回值是一个对象。这个对象里面有两个属性，分别为left和top

### jQuery的scrollTop方法---------->获取或者设置滚动的偏移位

```javascript
设置：

$('div').scrollTop()
//获取当前div元素的向上滚动的距离
为了保证浏览器的兼容, 获取网页滚动的偏移位需要按照如下写法：
$("body").scrollTop()+$("html").scrollTop()

获取：
$('div').scrollTop(200)
//设置当前div元素的向上滚动距离为200px
为了保证浏览器的兼容, 设置网页滚动的偏移位需要按照如下写法：
$("body,html").scrollTop(200)



```

