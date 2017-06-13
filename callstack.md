### ex.01
```javascript
console.log("This is global context");

function ExContext1() {
    console.log("This is ExContext1");
}

function ExContext2() {
    ExContext1();
    console.log("This is ExContext2");
}

ExContext2();
```

### ex.02
```javascript
var var1 = 1;
var var2 = 2;
console.log(var1);  // 1
console.log(var2);  // 2
```

### ex.03
```javascript
var var1 = 1;
var var2 = 2;
function func() {
    var var1 = 10;
    var var2 = 20;
    console.log(var1); // 10
    console.log(var2); // 20
}
func();
console.log(var1);  // 1
console.log(var2);  // 2
```

### ex.04
```javascript
var value = "value1";
 
function printFunc(func) {
    var value = "value2";
    
    function printValue() {
        return value;
    }
    
    console.log(printValue());
}
 
printFunc();
```

### ex.05
```javascript
var value = "value1";
 
function printValue() {
    return value;
}
function printFunc(func) {
    var value = "value2";
    console.log(func());
}
 
printFunc(printValue);
```

### ex.06
```javascript
var y = { x:5 };
 
function withExamFunc() {
    var x = 10;
    var z;
 
    with(y) {
        z = function() {
            console.log(x);    
        }
    }
    z();
}
withExamFunc();
```

### ex.07
```javascript
function outerFunc(){
    var x = 10;
    var innerFunc = function() { console.log(x); }
    return innerFunc;
}
 
var inner = outerFunc();
inner();
```

### ex.08
```javascript
function outerFunc(arg1, arg2){
    var local = 8;
    function innerFunc(innerArg){
        console.log((arg1 + arg2)/(innerArg + local));
    }
    
    return innerFunc;
}
 
var exam1 = outerFunc(2, 4);
exam1(2);
```

### ex.09
```javascript
function HelloFunc(func) {
    this.greeting = "hello";
}
 
HelloFunc.prototype.call = function(func) {
    func ? func(this.greeting) : this.func(this.greeting);
}    
 
var userFunc = function(greeting) {
    console.log(greeting);
}
 
var objHello = new HelloFunc();
objHello.func = userFunc;
objHello.call();
```

### ex.10
```javascript
function HelloFunc(func) {
    this.greeting = "hello";
}
 
HelloFunc.prototype.call = function(func) {
    func ? func(this.greeting) : this.func(this.greeting);
}    
 
var userFunc = function(greeting) {
    console.log(greeting);
}
 
var objHello = new HelloFunc();
objHello.func = userFunc;
objHello.call();
 
function saySomething(obj, methodName, name) {
    return (function(greeting) {
        return obj[methodName](greeting, name);
    });
}
 
function newObj(obj, name) {
    obj.func = saySomething(this, "who", (name || "everyone"));
 
    return obj;
}
 
newObj.prototype.who = function(greeting, name) {
    console.log(greeting + " "  +  (name || "everyone") );
}
 
var obj1 = new newObj(objHello, "zzoon");
obj1.call();
```

### ex.11
```javascript
var buffAr = [
    'I am ',
    '',
    '. I live in ',
    '',
    '. I\'am ',
    '',
    ' years old.',
];
 
function getCompletedStr(name, city, age) {
    buffAr[1] = name;
    buffAr[3] = city;
    buffAr[5] = age;
 
    return buffAr.join('');
}
 
var str = getCompletedStr('zzoon', 'seoul', 16);
console.log(str);
```

### ex.12
```javascript
var getCompletedStr = (function(){
    var buffAr = [
        'I am ',
        '',
        '. I live in ',
        '',
        '. I\'am ',
        '',
        ' years old.',
    ];
 
    return (function(name, city, age) {
        buffAr[1] = name;
        buffAr[3] = city;
        buffAr[5] = age;
 
        return buffAr.join('');
    });
})();
 
var str = getCompletedStr('zzoon', 'seoul', 16);
console.log(str);
```

### ex.13
```javascript
function callLater(obj, a, b) {
    return (function(){
        obj["sum"] = a + b;
        console.log(obj["sum"]);
    });
}
 
var sumObj = {
    sum : 0
}
 
var func = callLater(sumObj, 1, 2);
setTimeout(func, 500);
```

### ex.14
```javascript
function outerFunc(argNum) {
  var num = argNum;
  return function(x) {
      num += x;
      console.log('num: ' + num );
    }
}
 
 var exam = outerFunc(40);
 
 exam(5);
 exam(-10);
```

### ex.15
```javascript
function func(){
   var x = 1;
   return {
      func1 : function(){ console.log(++x); },
      func2 : function(){ console.log(-x); }
   };
};
 
var exam = func();
exam.func1();
exam.func2();
```

### ex.16
```javascript
function countSeconds(howMany) {
  for (var i = 1; i <= howMany; i++) {
    setTimeout(function () {
      console.log(i);
    }, i * 1000);
  }
};
countSeconds(3);
```

### ex.17
```javascript
function countSeconds(howMany) {
  for (var i = 1; i <= howMany; i++) {
    (function (currentI) {
      setTimeout(function () {
        console.log(currentI);
      }, currentI * 1000);
    }(i));
  }
};
countSeconds(3);
```
