## 原型

所有的JavaScript对象都从原型继承属性。  
通过对象直接量和`new Object()`创建的对象的原型是Object，通过`Object.prototype`获得对原型对象的引用。  
通过new和构造函数创建的对象的原型是构造函数的prototype属性的值。如`Array.prototype`、`Date.prototype`。  

`Object.prototype` 没有原型对象，不继承任何属性。  
普通对象都有原型，而内置构造函数（以及大部分自定义构造函数）都有一个继承自`Object.prototype`的原型。如`new Date()`创建的对象同时继承自`Date.prototype`和`Object.prototype`。这一系列链接的原型对象就是原型链（prototype chain）。  