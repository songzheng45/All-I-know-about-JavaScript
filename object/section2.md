## 创建对象

创建对象的方式有：`直接量`、关键字`new`和ECMAScript5中的`Object.create()`函数。


### 对象直接量
对象直接量是一个表达式，每次运算都会创建并初始化一个新的对象。
``` javascript
var empty = {};                 // 没有任何属性的对象
var point = {x : 0, y : 0, };   // 
var book = {
    'main title': 'JavaScript',
    'sub-title': 'The definitive Guide',
    'for': 'all audiences'
};
```
属性名字中如果有空格、连字符或者属性名是保留字，必须用用字符串表示。


### 用new创建对象
```javascript
var o = new Object();       // 等价于 {}
var a = new Array();        // 等价于 []
var d = new Date();         // 创建一个表示当前时间的Date对象
var r= new RegExp('js');    // 创建一个进行模式匹配的RegExp对象
```
还可以用自定义构造函数来初始化对象。

### Object.create()
`Object.create()`是ECMAScript5中定义的，是一个静态函数，它创建一个对象。  
``` javascript
Object.create(prototype[,property_desc])
```
第一个参数是这个对象的原型，第二个参数可选，用以对对象的属性进一步描述。  

示例1
``` javascript
var o1 = Object.create({ x : 1, y : 2});    // o1继承了属性x和y
var o2 = Object.create(null);               // 传入null创建没有原型的对象，该对象不包括任何基础方法，如toString()，不能和“+”运算符一起正常工作。
var o3 = Object.create(Object.prototype);   // 创建一个空对象，等价于 {} 或 new Object()
var o4 = Object.create(o3);                 // 创建继承自o3的对象
```
使用`Object.create`可以通过任意原型创建对象，即使任意对象可继承，这是一个强大的特性。  
ECMAScript3中模拟原型继承：
```javascript
/**
 * 返回一个继承自原型对象p的新对象
 * 优先使用Object.create，如果不存在则退化使用其他方法
 */
function inherit(p){
	if (p == null) throw TypeError();
	if (Object.create) {
		return Object.create(p);
	}
	var t = typeof p;
	if (t !== 'object' && t !== 'function') throw TypeError();
	function f() {};    // 定义一个空构造函数
	f.prototype = p;    // 将其原型设置为p
	return new f();     // 使用new f() 创建p的继承对象
}
```
**inherit()**可以防止库函数无意间修改原始对象。
```javascript
var p = { x : "don't change this value"};
library_function(inherit(p));   // 防止对o的意外修改
```