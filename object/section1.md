## 对象

### 对象的基本概念
- 什么是对象？  
对象是JavaScript的基本数据类型。

- 对象由什么组成？  
对象是一种复合值，它将许多值（原始值或其他对象）聚合在一起，通过名字访问这些值。  
对象也可看作是属性的无序集合，每个属性都是**名/值**对。

- JavaScript中哪些是对象？  
除了字符串、数字、true、false、null和undefined之外，JavaScript中的值都是对象。

- 对象的属性有什么特点？   
属性包含名字和值。  
`属性名`可以是包含**空字符串**在内的任意字符串，但是对象中不能存在两个同名属性。  
`值`是任意JavaScript值，或者（ECMAScript5中）一个getter或setter函数。

- 属性特性（property attribute）是什么？  
属性特性是一些与属性相关的值：  
    - 可写（writable attribute），表明是否可以设置该属性的值。
    - 可枚举（enumerable attribute），表明是否可以通过for/in循环返回该属性。
    - 可配置（configurable attribute），是否可以删除或修改该属性。  

ECMAScript5之前，通过代码给对象创建的所有属性都是可写的、可枚举的和可配置的。ECMAScript5中则可以对这些特性加以配置。    

- 对象特性（object attribute）是什么？
对象除了包含属性，还包含三个相关的对象特性：  
    - 对象的原型（prototype）指向另外一个对象，本对象的属性继承自它的原型对象。
    - 对象的类（class）是一个标识对象类型的字符串。
    - 对象的扩展标记（extensible flag）指明（在ECMAScript5中）是否可以向该对象添加新属性。

- JavaScript的核心特征是什么？  
“原型式继承”（prototypal inheritance）。

- 对象的特点是什么？  
    - 动态。可以随意新增、删除属性。
    - 可变。通过引用而非值来操作对象。

- 对象的基础操作有哪些？  
    - 创建（create）
    - 设置（set）
    - 查找（query）
    - 删除（delete）
    - 检测（test）
    - 枚举（enumerate）

- JavaScript中有哪三类对象？
    - 内置对象（native objet）：例如Date、Math、Array对象。
    - 宿主对象（host object）：由JavaScript解释器所嵌入的宿主环境（如Web浏览器）定义的。例如客户端JavaScript表示网页结构的HTMLElement对象、表示网页文档的Document对象。
    - 自定义对象（user-defined object）：运行中的JavaScript代码创建的对象。

- 对象有哪两类属性？    
    - 自有属性（own property）：直接在对象中定义的属性。
    - 继承属性（inherited property）：在对象的原型对象中定义的属性。