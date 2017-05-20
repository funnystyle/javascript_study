# Javascript Promise

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

### Ex.1
```javascript
getURL("https://httpbin.org/get").then(function onFulfilled(value) {
    console.log("onFulfilled");
    console.log(value);
}).catch(function onRejected(error){
    console.log("onRejected");
    console.error(error);
});
```

### Ex.2
```javascript
getURL("https://httpbin.org/status/500").then(function onFulfilled(value) {
    console.log("onFulfilled");
    console.log(value);
}).catch(function onRejected(error){
    console.log("onRejected");
    console.error(error);
});
```
