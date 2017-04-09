## 事件对象
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
