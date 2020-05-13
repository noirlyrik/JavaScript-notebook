
# 8 BOM

## 8.1 核心对象window

### 8.1.1 全局作用域

- 全局环境中的变量和函数会变为window的属性

- 全局变量无法用delete删除，在window上定义的属性可以

```js
var age = 29; // configurable: false,因此无法用delete删除
window.color = "red";

delete window.age;  //false
delete window.color;  //true

window.age;  //29
window.color;  //undefined
```

- 通过查询window对象了解某个变量是否存在

```js
var newValue = oldValue; //Uncaught ReferenceError: oldValue is not defined

var newValue = window.oldValue;  //undefined
window.oldValue;  //undefined
```

### 8.1.2 窗口关系及框架

- top指向最外层的框架，即浏览器窗口

```html
<html>
    <head>
        <title>Frameset Example</title>
    </head>
    <frameset rows="160, *">
        <frame src="frame.htm" name="topFrame">
            <frameset cols = "50%, 50%">
                <frame src="anotherframe.htm" name="leftFrame">
                <frame src="yetanotherframe.htm" name="rightFrame">
            </frameset>
    </frameset>
</html>
```





![image](https://cdn.nlark.com/yuque/0/2020/png/419446/1589264320059-100c01d6-6aa3-4add-8bab-e1298254cd9a.png)

- parent指向当前框架的直接上层框架

```html
<html>
    <head>
        <title>Frameset Example</title>
    </head>
    <frameset rows="160, *">
        <frame src="frame.htm" name="topFrame">
            <frameset cols = "50%, 50%">
                <frame src="anotherframe.htm" name="leftFrame">
                <frame src="anotherframeset.html" name="rightFrame">
            </frameset>
    </frameset>
</html>
```

```html
<html>
    <head>
        <frameset cols="50%, 50%">
            <frame src="red.htm" name="redFrame">
            <frame src="blue.htm" name="blueFrame">
        </frameset>
    </head>
</html>
```

![image](https://cdn.nlark.com/yuque/0/2020/png/419446/1589332763235-95c43774-2cbf-43d0-8ce2-67d8d9d17fa4.png)


### 8.1.3 窗口位置


- screenLeft / screenX
- screenTop / screenY

可能禁用

- moveTo
- moveBy

### 8.1.4 窗口大小

- innerWidth / innerHeight

viewport视口大小

- outerWidth / outerHeight

标准模式

- document.documentElement.clientWidth / document.documentElement.clientHeight


混杂模式

- document.body.clientWidth / document.body.clientHeight

可能禁用

- resizeTo
- resizeBy



### 8.1.5 导航和打开窗口


- window.open()

```js
window.open("http://www.wrox.com/", "wroxWindow", "height=400, width=400, top=10, left=10, resizable=yes");
```

效果图

![image](https://cdn.nlark.com/yuque/0/2020/png/419446/1589270455943-5f05959e-4edf-466f-b61d-480c55ec7233.png)

操作打开的窗口

```js
var wroxWin = window.open("http://wrox.com/", "wroxWindow", "height=400, width=400, top=10, left=10, resizable=yes");

// 关闭窗口
wroxWin.close();
```


- closed属性和opener属性

```js
wroxWin.close();

wroxWin.closed;  // true

var wroxWin = window.open("http://wrox.com/", "wroxWindow", "height=400, width=400, top=10, left=10, resizable=yes");

wroxWin.opener == window;  // true
```

- chrome新标签页opener为null，表示该标签页是一个独立进程，不需要与打开它的标签页进行通信


- 检测弹出窗口是否被屏蔽

```js
var wroxWin = window.open("http://wrox.com/", "_blank");

if (wroxWin == null) {
    alert("The popup was blocked!");
}
```

- 封装在try-catch中

```js
var blocked = false;

try {
    var wroxWin = window.open("http://www.wrox.com", "_blank");
    if (wroxWin == null) {
        blocked = true;
    } 
} catch(ex) {
    blocked = true;
}

if (blocked) {
    alert("The popup was blocked");
}
```


### 8.1.6 超时调用和间歇调用

- 超时调用：setTimeout()
    - 可传递字符串和函数

```js
setTimeout(function() {
    alert("hello world");
}, 3000);
```
- 不推荐传递字符串

```js
setTimeout("alert('hello world')", 1000);
VM3631:1 Refused to evaluate a string as JavaScript because 'unsafe-eval' is not an allowed source of script in the following Content Security Policy directive: "script-src 'strict-dynamic' 'sha256-1+GSDjMMklBjZY0QiWq+tGupCvajw4Xbn46ect2mZgM=' 'sha256-2mX1M62Fd0u8q0dQY2mRsK5S1NS9jJuQAvyE8tD0dkQ=' 'sha256-EtIKSV82ixJHE3AzqhoiVbUGKG+Kd8XS0fFToow29o0=' 'sha256-HqdPsO6hNmT/mfSeGdcX3eEGrZVva7AKD2Z2+1ujCZ8=' 'sha256-VKboFBdOdpwCwCkw/y71xPwtM/YeZSZvOP8Fn2OijOM=' 'sha256-IEF9PjeyU0vsr61C8cm3JQOerOYWdBsaGddCSPp6tZs=' 'sha256-C9ctze2LhHtwL+fcPVPkmVRYjQgXTGs4xfBAzlQwGWk=' 'sha256-uYRyY21O0+cTlqqmpXJY6brg5BX+o5iikh9EsVc30yc='".
```

- 间歇调用：setInterval()
    - 不建议传递字符串


```js
var num = 0;
var max = 10;
var intervalId = null;

function incrementNumber() {
    num++;
    
    if (num == max) {
        clearInterval(intervalId);
        alert("Done");
    }
}

intervalId = setInterval(incrementNumber, 500);
```

- 使用setTimeout超时调用模拟间歇调用

```js
var num = 0;
var max = 10;

function incrementNumber1() {
    num++;
    if(num < max) {
        setTimeout(incrementNumber, 500);
    } else {
        alert("Done");
    }
}

setTimeout(incrementNumber1, 500);
```

### 8.1.7 系统对话框

- alert()
- confirm()
- prompt()
- 打印：window.print();
- 查找：window.find();


