# Javascript Promise examples

## callback
```javascript
getAsync("fileA.txt", function(error, result) {
    if (error) { // 실패시
        throw error;
    }
    // 성공시
});
```

## ES5
```javascript
// ES5
'use strict';

function sleep(callback, msec) {
  setTimeout(callback, msec);
}

sleep(function(){
  console.log('wake!')
}, 1000);
```

## ES6
```javascript
// ES6
'use strict';

function sleep(msec) {
  return new Promise(function(resolve, reject){
	setTimeout(resolve, msec);
  });
}

sleep(1000).then(function(){
  console.log('wake!');
});
```

## workflow
```javascript
function asyncFunction() {
    return new Promise(function (resolve, reject) {
        setTimeout(function () {
            resolve('Async Hello world');
        }, 16);
    });
}

asyncFunction().then(function (value) {
    console.log(value); // 'Async Hello world'
}).catch(function (error) {
    console.log(error);
});
```

```javascript
asyncFunction().then(function (value) {
    console.log(value);
}, function (error) {
    console.log(error);
});
```

## getURL function (returns Promise Object)
```javascript
function getURL(URL) {
    return new Promise(function (resolve, reject) {
        var req = new XMLHttpRequest();
      
        req.open('GET', URL, true);
      
        req.onload = function () {
            if (req.status == 200) {
                resolve(req.responseText);
            } else {
                reject(new Error(req.statusText));
            }
        };
      
        req.onerror = function () {
            reject(new Error(req.statusText));
        };
      
        req.send();
    });
}
```

### getURL - get
```javascript
getURL("https://httpbin.org/get").then(function onFulfilled(value) {
    console.log("onFulfilled");
    console.log(value);
}).catch(function onRejected(error){
    console.log("onRejected");
    console.error(error);
});
```

### getURL - 500
```javascript
getURL("https://httpbin.org/status/500").then(function onFulfilled(value) {
    console.log("onFulfilled");
    console.log(value);
}).catch(function onRejected(error){
    console.log("onRejected");
    console.error(error);
});
```

### getURL - 500 (without catch)
```javascript
getURL("https://httpbin.org/status/500").then(function onFulfilled(value) {
    console.log("onFulfilled");
    console.log(value);
}, function onRejected(error) {
    console.log("onRejected");
    console.error(error);
}
```

### Promise.resolve
```javascript
new Promise(function(resolve){
    resolve(42);
}).then(function(value){
    console.log(value);
});

Promise.resolve(42).then(function(value){
    console.log(value);
});
```
### thenable - jQuery
```javascript
var promise = Promise.resolve($.ajax('https://httpbin.org/get'));// promise 객체를 반환한다.

promise.then(function(value){
   console.log(value);
});
```

### thenable - Q
```javascript
var Q = require("Q");
// 이 promise 객체는 ES6 Promises의 인스턴스이다.
var promise = new Promise(function(resolve){
    resolve(1);
});

// Q promise 객체로 변환
Q(promise).then(function(value){
    console.log(value);
}).finally(function(){
    console.log("finally");
});
```

### Promise.reject
```javascript
new Promise(function(resolve, reject){
    reject(new Error('오류'));
}).catch(function(error){
    console.error(error.message); // 오류
});

Promise.reject(new Error('오류')).catch(function(error){
    console.error(error.message); // 오류
});
```

## Promise.prototype.then
```javascript
aPromise.then(function taskA(value){
    // task A
}).then(function taskB(vaue){
    // task B
}).catch(function onRejected(error){
    console.log(error);
});
```

## Quiz

What is the difference between these four promises?

```javascript
doSomething().then(function () {
    return doSomethingElse();
});

doSomething().then(function () {
  doSomethingElse();
});

doSomething().then(doSomethingElse());

doSomething().then(doSomethingElse);
```

```javascript
function doSomething(value) {
    return new Promise(function(resolve, reject){
	    setTimeout(function() { 
            console.log("doSomething : value [" + value + "]");
            resolve("doSomething");
        }, 2000);
    });
}

function doSomethingElse(value) {
    return new Promise(function(resolve, reject){
	    setTimeout(function() { 
            console.log("doSomethingElse : value [" + value + "]");
            resolve("doSomethingElse");
        }, 2000);
    });
}

function finalHandler(value) {
    console.log("finalHandler : value [" + value + "]");
}

doSomething().then(function () {
    return doSomethingElse();
}).then(finalHandler);

doSomething().then(function () {
    doSomethingElse();
}).then(finalHandler);

doSomething().then(doSomethingElse())
    .then(finalHandler);
  
doSomething().then(doSomethingElse)
    .then(finalHandler);
```
