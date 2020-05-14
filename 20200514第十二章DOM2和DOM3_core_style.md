

# 12 DOM2 和 DOM3

## 12.1 DOM变化

### 12.1.1 XML命名空间的变化

### 12.1.2 其他方面的变化

- document.doctype
- document
    - document.importNode()
    - document.defaultView
    - document.implementation.createHTMLDocument()
- Node
    - isSupported()
    - isSameNode()
    - isEqualNode()
    - getUserData()
- 框架
    - iframe.contentDocument


```js
document.implementation.createHTMLDocument("new Node");

// #document<!doctype html>
// <html>
// <head>
// <title>new Node</title>
// </head>
// <body></body>
// </html>
```

## 12.2 样式

### 12.2.1 访问元素的样式


CSS属性 |  JavaScript属性
---|---
background-image | style.backgroundImage
color | style.color
display | style.display
font-family | style.fontFamily


```js
var react = document.querySelector("#ReactApp");

react.style.backgroundColor = "red";
document.body.style.backgroundColor = "yellow";

react.style.width = "200px";
react.style.width = "50px";

react.style.border = "20px solid black";
```

1. DOM样式属性和方法

- cssText：如前所述，通过它能够访问到style 特性中的CSS 代码。
- length：应用给元素的CSS 属性的数量。
- parentRule：表示CSS 信息的CSSRule 对象。本节后面将讨论CSSRule 类型。
- getPropertyCSSValue(propertyName)：返回包含给定属性值的CSSValue 对象。
- getPropertyPriority(propertyName)：如果给定的属性使用了!important 设置，则返回
"important"；否则，返回空字符串。
- getPropertyValue(propertyName)：返回给定属性的字符串值。
- item(index)：返回给定位置的CSS 属性的名称。
- removeProperty(propertyName)：从样式中删除给定属性。
- setProperty(propertyName,value,priority)：将给定属性设置为相应的值，并加上优先
权标志（"important"或者一个空字符串）。

```js
document.body.style.length;  // 2
document.body.style.cssText;  // "overscroll-behavior-x: none; overflow-y: hidden;"

// 遍历CSS属性
for (var i=0, len = document.body.style.length; i < len; i++) {
    alert(document.body.style[i]);
}
// overscroll-behavior-x
// overflow-y


// 遍历CSS属性和值
for (var i=0, len = document.body.style.length; i<len; i++) {
    prop = document.body.style.item(i);
    value = document.body.style.getPropertyValue(prop);
    alert(prop + ":" + value);
}
// overscroll-behavior-x:none
// overflow-y:hidden
```

2. 计算的样式

- getComputedStyle()


```js
var bodyStyle = document.defaultView.getComputedStyle(document.body, null);

bodyStyle; // CSSStyleDeclaration{0: "animation-delay", 1: "animation-direction", 2: "animation-duration", …}

bodyStyle.alignContent;  // "normal"
```



### 12.2.2 操作样式表

```js
var sheet = null;
for (var i=0, len = document.styleSheets.length; i<len; i++) {
    sheet = document.styleSheets[i].href;
    alert(sheet);
}
```

- css规则
- 创建规则: insertRule()
- 删除规则：deleteRule()


### 12.2.3 元素大小

1. 偏移量 offset dimension
- element.offsetHeight
- element.offsetWidth
- element.offsetTop
- element.offsetLeft


![image](https://cdn.nlark.com/yuque/0/2020/png/419446/1589451968465-368c2fe5-775f-462e-b088-6d9ba07d66b7.png)


2. 客户区大小 client dimension

![image](https://cdn.nlark.com/yuque/0/2020/png/419446/1589452074155-962251a4-05a0-4880-8efa-ea3dda215f15.png)


3. 滚动大小 scroll dimension

- scrollHeight
- scrollWidth
- scrollTop
- scrollLeft


4. 确定元素大小

```js
var react = document.querySelector("#ReactApp");

react.getBoundingClientRect();
// DOMRect {x: 0, y: 0, width: 1296, height: 810, top: 0, …}
// bottom: 810
// height: 810
// left: 0
// right: 1296
// top: 0
// width: 1296
// x: 0
// y: 0
// __proto__: DOMRect
```











