## 事件冒泡

大纲：
1. 事件流
2. 事件处理程序
3. 事件对象

### 理解事件流
事件流：描述从页面中接收事件的顺序。有两种事件流：  
1. 事件冒泡流（IE）
2. 事件捕获流（Netscape） 

#### 事件冒泡
事件冒泡：即事件最开始由最具体的元素接收，然后逐级向上传播至最不具体的那个节点（Document）。  
看以下示例：
```javascript
<html>
    <head></head>
    <body>
        <div id="box">
            <input type="button" value="按钮" id="btn" />
        </div>
    </body>
</html>
```
点击示例中的按钮，浏览器会认为也点击了父容器box，进而继续向上传播到html节点，最后到Document节点。

#### 事件捕获
事件捕获：不太具体的节点应该更早接收到事件，而最具体的节点最后接收到事件。

### 事件处理程序
分为三种：
1. HTML事件处理程序
将事件直接加到HTML元素上。如
```html
<input type="button" value="按钮" id="btn" onclick="myFunc('hello')"/>
```  
缺点：HTML和JS代码紧密耦合在一起，已被开发人员摒弃。

2. DOM0级事件处理程序
较传统方式：把一个函数赋值给一个元素的事件处理程序属性。  
优势：简单，跨浏览器。  
示例：
``` html
<input type="button" value="按钮2" id="btn2"/>
```
``` javascript
var btn2 = document.getElementById('btn2');
btn2.onclick = function(){
    alert('DOM0级添加的事件');
}

btn2.onclick = null;    // 删除btn2的onclick事件处理程序
```

3. DOM2级事件处理程序
定义了两个方法,用于处理指定和删除事件处理程序的操作：  
```javascript
addEventListener(eventType,listener[,useCapture])
removeEventListener()
```
参数：  
- eventType : string类型。要监听的事件名。
- listener : 作为事件处理程序的函数。
- useCapture : Boolean类型，可选。true表示使用捕获事件流方式传播事件，false表示使用事件冒泡方式。默认false。在冒泡阶段捕获事件，可以兼容各大浏览器，注意推荐设置为false。
``` html
<input type="button" value="按钮3" id="btn3"/>
```
```javascript
function showMessage(){
    alert(this.value);  // this引用被触发事件的节点对象
}
var btn3 = document.getElementById('btn3');
btn3.addEventListener('click',showMessage,false);

// 通过addEventListener添加的事件只能使用removeEventListener来移除事件处理
btn3.removeEventListener('click',showMessage,false);
```
优点：DOM0级和DOM2级都可以给元素增加多个事件处理程序。

IE不支持DOM2级事件处理程序。

#### IE事件处理程序
`attachEvent()` : 添加事件  
`detachEvent()` : 删除事件  
都接收相同的两个参数：**事件名称**和**事件处理程序的函数**。  
没有第三个参数的原因：IE8以及更早的浏览器版本只支持事件冒泡！  
支持IE事件处理程序的浏览器：IE和Opera。  

示例：
``` javascript
btn2.attachEvent('onclick', showMessage);
btn2.detachEvent('onclick', showMessage);
```
#### 跨浏览器的事件处理程序
能力检测。  

```javascript
var eventUtil = {
    addHandler: function (element, type, handler) {
        if (element.addEventListener) { // DOM2 级事件处理程序
            element.addEventListener(type, handler, false);
        } else if (element.attachEvent) { // DOM2 级IE事件处理程序
            element.attachEvent('on' + type, handler);
        } else {    // DOM0 级事件处理程序
            element['on' + type] = handler;
        }
    },
    removeHandler: function (element, type, handler) {
        if (element.removeEventListener) { // DOM2 级事件处理程序
            element.addEventListener(type, handler, false);
        } else if (element.deatachEvent) { // DOM2 级IE事件处理程序
            element.deatachEvent('on' + type, handler);
        } else {    // DOM0 级事件处理程序
            element['on' + type] = null;
        }
    }
};
```

### 事件对象
事件对象：触发DOM上的事件时都会产生一个对象。  
事件对象event
1. DOM中的事件对象  
属性：  
- **type**：string类型，获取事件类型。
- **target**：object类型，获取事件目标。具有nodeName（元素名称）等属性。
- **bubbles**
- **canselable** ：
方法：  
- **stopPropagation()**：阻止事件冒泡
- **preventDefault()**：阻止事件默认行为

2. IE中的事件对象
属性：
- **type**：事件类型
- **srcElement**：事件目标。
- **cancleBubble**：Boolean类型，true表示阻止事件冒泡。
- **returnValue**：Boolean类型。true表示阻止事件默认行为
