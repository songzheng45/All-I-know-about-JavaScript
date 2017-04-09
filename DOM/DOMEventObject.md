## 事件对象
事件对象：触发DOM上的事件时都会产生一个对象。  
事件对象event：代表事件的状态，比如事件在其中发生的元素、键盘按键的状态、鼠标的位置、鼠标按钮的状态。  

### 1. DOM中的事件对象
标准的Event属性：  
- **type**：返回string值，表示当前event对象表示的事件类型的名称。
- **target**：返回object值，获取事件目标。具有nodeName（元素名称）等属性。
- **bubbles**：返回布尔值，指示事件是否是冒泡事件类型。
- **cancelable** ：bool值，

标准的event方法：  
- **stopPropagation()**：阻止事件冒泡
- **preventDefault()**：阻止事件默认行为

### 2. IE中的事件对象
IE属性：
- **type**：事件类型
- **srcElement**：事件目标。
- **cancleBubble**：Boolean类型，true表示阻止事件冒泡。
- **returnValue**：Boolean类型。true表示阻止事件默认行为


***

参考：  
[W3School:HTML DOM Event 对象](http://www.w3school.com.cn/jsref/dom_obj_event.asp)  
