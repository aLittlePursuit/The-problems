## 异步的解决方案async/awaits
> 基本规则
1. async 表示***这是一个async函数***，await只能用在这个函数里面。
2. await 表示在这里***等待promise返回结果***了，再继续执行。
3. await 后面跟着的***应该是一个promise对象***（当然，其他返回值也没关系，只是会立即执行，不过那样就没有意义了…）
> Ajax

```
// 获取产品数据
ajax('products.json', (products) => {
    console.log('AJAX/products >>>', JSON.parse(products));

    // 获取用户数据
    ajax('users.json', (users) => {
        console.log('AJAX/users >>>', JSON.parse(users));

        // 获取评论数据
        ajax('products.json', (comments) => {
            console.log('AJAX/comments >>>', JSON.parse(comments));
        });
    });
});
```
>  Promise

```
// Promise
// 封装 Ajax，返回一个 Promise
function requestP(url) {
    return new Promise(function(resolve, reject) {
        ajax(url, (response) => {
            resolve(JSON.parse(response));
        });
    });
}

// 获取产品数据
requestP('products.json').then((products) => {
    console.log('Promises/products >>>', products);
    // 获取用户数据
    return requestP('users.json');
}).then((users) => {
    console.log('Promises/users >>>', users);
    // 获取评论数据
    return requestP('comments.json');
}).then((comments) => {
    console.log('Promises/comments >>>', comments);
});
```
> Generators

Generators 也是 ES6 一个新的特性，能够 暂停/执行 代码。yield 表示暂停，iterator.next 表示执行下一步，如果你不了解 Generators 也没关系，可以忽略它直接学习 await/async。

```
// Generators
function request(url) {
    ajax(url, (response) => {
        iterator.next(JSON.parse(response));
    });
}

function *main() {
    // 获取产品数据
    let data = yield request('products.json');

    // 获取用户数据
    let users = yield request('users.json');

    // 获取评论数据
    let products = yield request('comments.json');

    console.log('Generator/products >>>', products);
    console.log('Generator/users >>>', users);
    console.log('Generator/comments >>>', comments);
}

var iterator = main();
iterator.next();
```
> await/async

与 Promise 结合使用

```
// 封装 Ajax，返回一个 Promise
function requestP(url) {
    return new Promise(function(resolve, reject) {
        ajax(url, (response) => {
            resolve(JSON.parse(response));
        });
    });
}

(async () => {
    // 获取产品数据
    let data = await requestP('products.json');

     // 获取用户数据
    let users = await requestP('users.json');

     // 获取评论数据
    let products = await requestP('comments.json');

    console.log('ES7 Async/products >>>', products);
    console.log('ES7 Async/users >>>', users);
    console.log('ES7 Async/comments >>>', comments);
}());
```
与 Fetch API 结合使用：

```
(async () => {
// Async/await using the fetch API
    try {

         // 获取产品数据
        let products = await fetch('products.json');

        // Parsing products
        let parsedProducts = await products.json();

        // 获取用户数据
        let users = await fetch('users.json');

        // Parsing users
        let parsedUsers = await users.json();

        // 获取评论数据
        let comments = await fetch('comments.json');

        // Parsing comments
        let parsedComments = await comments.json();


        console.log('ES7 Async+fetch/products >>>', parsedProducts);
        console.log('ES7 Async+fetch/users >>>', parsedUsers);
        console.log('ES7 Async+fetch/comments >>>', parsedComments);


    } catch (error) {
        console.log(error);
    }
}());
```
再次结合 Fetch

```
(async () => {
    let parallelDataFetch = await* [
        (await fetch('products.json')).json(),
        (await fetch('users.json')).json(),
        (await fetch('comments.json')).json()
    ];
    console.log('Async parallel+fetch >>>', parallelDataFetch);
}());
```