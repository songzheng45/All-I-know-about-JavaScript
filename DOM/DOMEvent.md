## 事件冒泡


### 理解事件流
事件流：描述从页面中接收事件的顺序。有两种事件流：  
1. 事件冒泡流（IE）
2. 事件捕获流（Netscape） 

### 事件冒泡
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

### 事件捕获
事件捕获：不太具体的节点应该更早接收到事件，而最具体的节点最后接收到事件。

