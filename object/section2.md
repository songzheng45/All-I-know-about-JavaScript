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
var a = nwe Array();        // 等价于 []
var d = new Date();         // 创建一个表示当前时间的Date对象
var r= new RegExp('js');    // 创建一个进行模式匹配的RegExp对象
```