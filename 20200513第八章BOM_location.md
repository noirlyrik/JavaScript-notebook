
## 8.2 location


- location既是window属性，也是document属性
- location的属性

![image](https://cdn.nlark.com/yuque/0/2020/png/419446/1589278606453-7d1e8d9e-9c48-41d0-acdb-5358f5ad8944.png)

### 8.2.1 查询字符串参数

- 对location.search得到的内容进行处理


```js

// location.search;
// "?q=3wrnwhufwn&oq=3wrnwhufwn&aqs=chrome..69i57.650j0j7&sourceid=chrome&ie=UTF-8"

function getQueryStringArgs() {
    var qs = (location.search.length > 0 ? location.search.substring(1) : ""),
        args = {},
        items = qs.length ? qs.split("&") : [],
        item = null,
        name = null,
        value = null,
        i = 0,
        len = items.length;
    
    for(i=0; i<len; i++) {
        item = items[i].split("=");
        name = decodeURIComponent(item[0]);
        value = decodeURIComponent(item[1]);
        if(name.length) {
            args[name] = value;
        }
    }
    return args;
}

var args = getQueryStringArgs();

args;  //{q: "3wrnwhufwn", oq: "3wrnwhufwn", aqs: "chrome..69i57.650j0j7", sourceid: "chrome", ie: "UTF-8"}
```


### 8.2.2 位置操作


- location.assign() 打开URL

```js
location.assign("http://www.wrox.com")
// 等价于
window.location = "http://www.wrox.com"
// 等价于 最常用
location.href = "http://www.wrox.com"
```



- location.replace() 打开新URL，并且不能返回之前的页面
- location.reload() 重新加载
- location.reload(true) 从服务器重新加载

![image](https://cdn.nlark.com/yuque/0/2020/png/419446/1589335128344-1910fbab-5b52-4b3e-856e-2c1b87fb52ad.png)


## 8.3 navigator对象

- 检测浏览器类型


![image](https://cdn.nlark.com/yuque/0/2020/png/419446/1589335293891-1e013e9c-a601-420c-b587-2c6cf0fe09eb.png)

![image](https://cdn.nlark.com/yuque/0/2020/png/419446/1589335314771-81df4a2f-f264-4574-949e-bf90ce89e544.png)


## 8.4 screen对象

## 8.5 history对象

- history.go()
- history.back()
- history.forward()
- history.length()