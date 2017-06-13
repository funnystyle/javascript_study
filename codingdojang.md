# Ex.1

http://codingdojang.com/scode/548

피보나치 수열의 각 항은 바로 앞의 항 두 개를 더한 것이 됩니다. 1과 2로 시작하는 경우 이 수열은 아래와 같습니다.

1, 2, 3, 5, 8, 13, 21, 34, 55, 89, ...

짝수이면서 4백만 이하인 모든 항을 더하면 얼마가 됩니까?


```javascript
var fibonacci = (function(n) {
	var cache = [0, 1, 2];

	return function fib(i) {
		return cache[i] ? cache[i] : cache[i] = fib(i - 1) + fib(i - 2);
	}
})();

var res = 0,
	sum = 0;

for (let i = 1; (res = fibonacci(i)) <= 4000000; i++) {
	if (res % 2 === 0) {
		sum += res;
	}
}

console.log(sum);
```

# Ex.2

http://codingdojang.com/scode/546

1 ~ 10 사이의 어떤 수로도 나누어 떨어지는 가장 작은 수는 2520입니다.

그러면 1 ~ 20 사이의 어떤 수로도 나누어 떨어지는 가장 작은 수는 얼마입니까?

```javascript
var gcd = function g(x, y) {
	return y ? g(y, x % y) : x;
}

var lcd = function(x, y) {
	return x * y / gcd(x, y);
}

var arr = Array.from({length: 20}, (v, k) => k + 1); // make 1 to 20 array with array-like object and mapFn

var res = arr.reduce(lcd);

console.log(res);
```
