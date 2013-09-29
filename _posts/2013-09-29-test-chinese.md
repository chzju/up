---
layout: post
title: javascript中的类型检查
category: posts
---

# 罗列一下js中的类型检查方法： #
1.
	* 原理：typeof检查type。
	* 语法： 
	```
	if(tyeof(value) == "number") {...}
	```
type包括
```
number, string, boolean, undefined, object（typeof(null)返回object）, function
```

1.
	* 原理：instanceof检查私有属性prototype；
	* 语法：
	```
	if(value instanceof Number){...}
	```
可以检测基本数据类型，对于复合数据类型（除了function）通通认作object。 
注意，首字母要大写，如Number,String,Boolean,Object,Function。

1.
	* 原理：检查公有属性constructor；
	* 语法：
	```
	if(var1.constructor == Array){...}
	```
		1. 如果尝试
```
alert(var1.constructor)
```
，你会发现alert窗口的内容是constructor的实现代码。
		1. 当使用iframe时，constructor检查将会失效，因为iframe和父页面使用不同的js引擎实例。
		1. 对于定义形式为
```
function func1(){
	....
}
```
的函数，可以通过
```
func1.constructor.toString().match(/^s*functions*(w+)/)[1];
```
来抽取方法名。而对于形式为
```
func1 = function(){
   ....
}
```
则无法抽取方法名; 
		1. 实例的constructor属性是可以修改的（除了1，true,"ssss"这几类），所以并不可靠。参见[constructor][1]


1. 检查Object.prototype.toString.call(var1)私有属性class；

1. 属性检测法。

[1]: https://developer.mozilla.org/en/Core_JavaScript_1.5_Reference/Global_Objects/Object/constructor "constructor"