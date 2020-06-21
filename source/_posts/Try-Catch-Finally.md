---
title: Try Catch Finally
---
之前用react做项目的时候有一个场景： 退出系统的时候需要调用logout接口（记录日志），之前做退出登录直接清空本地记录的登录信息，清完之后发现登出接口需要用户的token等信息， 然后使用try catch finally，先调用登出接口然后，不管接口是否调用成功，finally,清除本地登录信息， debug的时候发现对异步操作，try，finally只能用于同步操作，后来用promise, finally 解决，同在try里运用 await

```
try{
    // logout api
    await logoutApi()
} finally {
    // clear local login info
}

//或者

logoutApi().finally(()=>{
    // clear local login info
})
```
await相当于把异步接口请求变为同步，等接口处理完了之后，再去执行finally中的代码

参考[https://javascript.info/try-catch](https://javascript.info/try-catch)

### try..catch只能同步工作
    如果一段代码在类似setTimout的异步代码片段里抛出异常，try..catch无法扑捉到该异常
    ```
try {
  setTimeout(function() {
    noSuchVariable; // script will die here
  }, 1000);
} catch (e) {
  alert( "won't work" );
}
    ```
    这是因为这个方法本身是推迟运行，而引擎已经离开了try..catch结构，
    要在一个异步的方法中捕捉异常，可以把try..catch放在该异步方法中
    ```
setTimeout(function() {
  try {
    noSuchVariable; // try..catch handles the error!
  } catch {
    alert( "error is caught here!" );
  }
}, 1000);
    ```
    