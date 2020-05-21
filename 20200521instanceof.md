

# instanceof

- typeof
- instanceof
- obj.toString

## instanceof

1. 用于class

```js
class Rabbit {}
let rabbit = new Rabbit();
alert(rabbit instanceof Rabbit); // true
```
2. 用于构造函数

```js
function Rabbit() {}
alert(new Rabbit() instanceof Rabbit); // true
```

### 使用静态方法Symbol.hasInstance设置自定义逻辑

```js
// 有canEat属性，则为animal
class Animal {
    static [Symbol.hasInstance](obj) {
        if (obj.canEat) return true;
    }
}

let obj = { canEat: true };
alert(obj instanceof Animal); // true
```
### 检查原型链

```js
class Animal {}

class Rabbit extends Animal {}

let rabbit = new Rabbit();

rabbit instanceof Animal; // true
rabbit.__proto__ === Rabbit.prototype; // true
rabbit.__proto__.__proto__ === Animal.prototype; // true
rabbit.__proto__.__proto__.__proto__ === Object.prototype; // true


rabbit instanceof Animal; // true
rabbit instanceof Object; // true
Animal.prototype.isPrototypeOf(rabbit); // true
Rabbit.prototype.isPrototypeOf(rabbit); // true

// 继承而非实例
Rabbit.prototype.__proto__ === Animal.prototype;  // true
Animal.prototype.isPrototypeOf(Rabbit); //false
Rabbit instanceof Animal; // false
```

### Object.prototype.toString
使用obj.toString()方法

```js
let obj = {}

alert(obj); // [object Object]

alert(obj.toString()); // [object Object]
```


```js
let objectToString = Object.prototype.toString;
let arr = [];
alert(objectToString.call(arr)); // [object Array]

let s = Object.prototype.toString;
s.call(123); // "[object Number]"
s.call(null); // "[object Null]"
s.call(alert); // "[object Function]"
```

#### Symbol.toStringTag

支持自定义
```js
let user = {
    [Symbol.toStringTag]: "User"
};

alert({}.toString.call(user)); // [object User]
```

使用{}toString.call()返回类型值

```js
window[Symbol.toStringTag]; // "Window"

alert({}.toString.call(window)); // [object Window]
```


## 总结


方法	| 用于 |返回值
---|---|---
typeof	| 原始数据类型|	string
{}.toString	| 原始数据类型，内建对象，包含 Symbol.toStringTag 属性的对象|	string
instanceof	|对象	|true/false



## 练习

```js
// 在下面的代码中，为什么 instanceof 会返回 true？我们可以明显看到，a 并不是通过 B() 创建的。

function A() {}
function B() {}

A.prototype = B.prototype = {};

let a = new A();

alert( a instanceof B ); // true
```

我的解决方案
```js
a.__proto__ === B.prototype; // true
```

官网解决方案

> instanceof 并不关心函数，而是关心函数的与原型链匹配的 prototype。
> 
> 并且，这里 a.\_\_proto\_\_ == B.prototype，所以 instanceof 返回 true。
> 
> 总之，根据 instanceof 的逻辑，真正决定类型的是 prototype，而不是构造函数。
