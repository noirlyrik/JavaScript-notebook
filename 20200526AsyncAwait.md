

# async/await


```js
async function f() {
    let promise = new Promise((resolve, reject) => {
        setTimeout(() => resolve("done!"), 1000)
    });
    
    let result = await promise; // 等待，直到promise resolve
    alert(result);
}

f(); // done!
```