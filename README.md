# About javascript prototype
## Example 1
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

## Example 2
```javascript
var C = {};
C.c = function() {
    return "C";
}

var D = function() {};
D.prototype.d = function() {
    return "D";
}

console.log(C.c()); 	  // C
console.log(new C().c()); // Uncaught TypeError: C is not a constructor

console.log(D.d()); 	  // Uncaught TypeError: D.d is not a function
console.log(new D().d()); // D
```

## Example 3
```javascript
var E = {};
E.prototype.e = function () { // Uncaught TypeError: Cannot set property 'e' of undefined
    return null;
}
```
