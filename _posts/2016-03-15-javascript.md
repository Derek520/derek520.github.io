---
layout: post
title:  Web前端笔记（3)
categories: Web
description: web前端
keywords: Web
comments: true
---

# Javascript



### Javascript笔记：

js作用：

```js
1、制作页面的行为或者特殊效果

2、表单验证；
```

js三种书写方式：

```js
外链式、内链式、行内式
```

&lt;!-- 标签 == 标记 == 元素 &lt; 节点（标记、标记的属性、标记的内容） --&gt;

&lt;!-- DOM 通过自己的倒置的树状结构表现方法，实现目标：针对性的找到页面中的目标节点，从而去控制他 --&gt;

&lt;!-- 可以控制css、html内容、html属性 --&gt;

innerHTML控制内容

```js
oBox.innerHTML = 'js的内容';

oBox.innerHTML = '<p>pppppppp</p>'

oBox.innerHTML = ''; 清空内容

控制html的属性，只有class在js中是className，其他的js和html写法相同
```

js数据类型：

```js
js中数据类型：数值型 字符串'' 布尔型True和false 对象型（空对象 对象） 未定义（排错）
alert( typeof(ob) ) 监测数据类型 typeof()
```

js自定义函数：

```js
function 函数名称(){

命令

} js中大括号写命令；小括号一般都是参数或条件

调用：函数名()

js函数预解析

变量不支持预解析
```

js条件判断：

```js
if(){} else if(){} else if(){} else{}
```

js运算符：

```js
|| == or, && == and,! == not
```

js事件：

```js
<语法：事件源.事件类型 = function(){命令}>
事件源：操作谁
事件类型：操作方法
匿名函数：function(){}
三个事件：
oLi01.onclick = function(){
alert('单击成功');
}
oLi02.onmouseover = function(){
alert('鼠标滑过');
}
oLi03.onmouseout = function(){
alert('鼠标离开');
}
事件源.事件类型 = 匿名函数
onmouseover / onmouseout / onclick
```

js数组：

```js
数组：容器，都是存储数据，变量只能存储一个数据，数组是存储多个数据的容器
var arr1 = new Array(1, 2, 3, 'abc');
var arr2 = [1, 2, 3, 'jqk']; //工作中常用
alert(arr2) 查看数组数据
alert(arr2[3]); 查看单个元素
alert( arr2.length ); 查看数组长度
arr2.jion(',') jion将数组分割成字符串
arr2.push('abc') push 在数据结尾添加数据
arr2.pop() pop在数据结尾处删除数据
arr2.splice(位置，删除数量，添加数据)
arr2.splice(1,2,'xy')
arr2.splice(1) 这个1代表位置，后面没有其他的参数，表示从这个位置删除后面的数据，不添加数据
arr2.reverse() 反转，调头
arr2.indexof(3) 检查某数据在数组出现的第一次索引
```

字符串操作方法：

```
parseInt(str1) 将字符串转换成整数，取掉小数，
parseFoat(str1) 将字符串转成浮点型整数值，保留小数；
str2.split('-') 将字符串分割数组
str3.substring(开始,结束)
//alert(str3.substring(2,4)) //不包含结束
//alert(str3.substring(2)) //从开始到最后所有
// 字符串没有反转方法，但是数组有，把字符串转成数组，数组可以反转reverse，join将数组转成字符串
alert(str3.split('').reverse().join(''));
```

js循环：

```js
// for(初始值;条件;增量){命令}
for(var i=0;i<3;i++)
{
alert('ok');
}
// 工作中常用
```

例子：去重

```js
// 需求：把arr的重复数据去除，剩下的数据放到一个新的数组里面newArr
var arr = [1,2,3,4,1,2,3,4,5,3,6];
var newArr = []; //为了保存将来不重复保留的数据
for(var i=0;i<arr.length;i++)
{
//如果检测到的各个数据的索引值 等于 数组里面的数据的索引值（保留 -- 将这个数据放到newArr），其他就丢弃
//arr.indexOf(arr[i]) == i
if(arr.indexOf(arr[i]) == i)
{
newArr.push(arr[i]);
}
}
alert(newArr);
```

js 定时器：

```js
var oTimer = null; //设置成一个空对象

//按钮单击事件，使用定时器的形式alert（）

// setTimeout(参数1,参数2) 参数1执行的命令：1、匿名函数2、自定义函数（***写函数名）；参数2：延迟时间:毫秒；1000毫秒=1秒

//停止上面的定时器

// clearInterval(目标定时器的名称)

clearInterval(oTimer);

oTimer = null; //为了释放浏览器资源
```

js 封闭函数：

```js
3种封装方式:
;;;;;(function(){
function fn1(){
    alert(2);
}
    fn1()
})();


!function(){
    alert(3)
}()

~function(){
    alert(4)
}()
```


