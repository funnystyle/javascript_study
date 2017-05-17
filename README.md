# javascript_study
## 1. example 1
```javascript
var A = function() {
	this.a = 1;
};
A.prototype.b = 2;
A.c = 3;

var X = new A();

console.log(A.a); // undefined
console.log(A.b); // undefined
console.log(A.c); // 3

console.log(X.a); // 1
console.log(X.b); // 2
console.log(X.c); // undefined
```
