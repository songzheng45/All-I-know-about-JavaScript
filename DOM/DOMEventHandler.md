## 事件处理程序
分为三种：
### 1. HTML事件处理程序
将事件直接加到HTML元素上。如
```html
<input type="button" value="按钮" id="btn" onclick="myFunc('hello')"/>
```  
缺点：HTML和JS代码紧密耦合在一起，已被开发人员摒弃。

### 2. DOM0级事件处理程序
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

### 3. DOM2级事件处理程序
定义了两个方法,用于处理指定和删除事件处理程序的操作：  
``` javascript
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

``` javascript
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

### 4. IE事件处理程序
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

### 跨浏览器的事件处理程序
能力检测。  

``` javascript
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