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

# Ex.3

http://codingdojang.com/scode/547

아래와 같은 20×20 격자가 있습니다.

 08 02 22 97 38 15 00 40 00 75 04 05 07 78 52 12 50 77 91 08
 
 49 49 99 40 17 81 18 57 60 87 17 40 98 43 69 48 04 56 62 00
 
 81 49 31 73 55 79 14 29 93 71 40 67 53 88 30 03 49 13 36 65
 
 52 70 95 23 04 60 11 42 69 24 68 56 01 32 56 71 37 02 36 91
 
 22 31 16 71 51 67 63 89 41 92 36 54 22 40 40 28 66 33 13 80
 
 24 47 32 60 99 03 45 02 44 75 33 53 78 36 84 20 35 17 12 50
 
 32 98 81 28 64 23 67 10 26 38 40 67 59 54 70 66 18 38 64 70
 
 67 26 20 68 02 62 12 20 95 63 94 39 63 08 40 91 66 49 94 21
 
 24 55 58 05 66 73 99 26 97 17 78 78 96 83 14 88 34 89 63 72
 
 21 36 23 09 75 00 76 44 20 45 35 14 00 61 33 97 34 31 33 95
 
 78 17 53 28 22 75 31 67 15 94 03 80 04 62 16 14 09 53 56 92
 
 16 39 05 42 96 35 31 47 55 58 88 24 00 17 54 24 36 29 85 57
 
 86 56 00 48 35 71 89 07 05 44 44 37 44 60 21 58 51 54 17 58
 
 19 80 81 68 05 94 47 69 28 73 92 13 86 52 17 77 04 89 55 40
 
 04 52 08 83 97 35 99 16 07 97 57 32 16 26 26 79 33 27 98 66
 
 88 36 68 87 57 62 20 72 03 46 33 67 46 55 12 32 63 93 53 69
 
 04 42 16 73 38 25 39 11 24 94 72 18 08 46 29 32 40 62 76 36
 
 20 69 36 41 72 30 23 88 34 62 99 69 82 67 59 85 74 04 36 16
 
 20 73 35 29 78 31 90 01 74 31 49 71 48 86 81 16 23 57 05 54
 
 01 70 54 71 83 51 54 69 16 92 33 48 61 43 52 01 89 19 67 48 
 
위에서 대각선 방향으로 연속된 붉은 숫자 네 개의 곱은 26 × 63 × 78 × 14 = 1788696 입니다.

그러면 수평, 수직, 또는 대각선 방향으로 연속된 숫자 네 개의 곱 중 최대값은 얼마입니까?

```javascript
String.prototype.stripMargin = function() {
    return this.split("\n").map(line => line.trim()).join("\n");
}

var matrix   = `08 02 22 97 38 15 00 40 00 75 04 05 07 78 52 12 50 77 91 08
                49 49 99 40 17 81 18 57 60 87 17 40 98 43 69 48 04 56 62 00
                81 49 31 73 55 79 14 29 93 71 40 67 53 88 30 03 49 13 36 65
                52 70 95 23 04 60 11 42 69 24 68 56 01 32 56 71 37 02 36 91
                22 31 16 71 51 67 63 89 41 92 36 54 22 40 40 28 66 33 13 80
                24 47 32 60 99 03 45 02 44 75 33 53 78 36 84 20 35 17 12 50
                32 98 81 28 64 23 67 10 26 38 40 67 59 54 70 66 18 38 64 70
                67 26 20 68 02 62 12 20 95 63 94 39 63 08 40 91 66 49 94 21
                24 55 58 05 66 73 99 26 97 17 78 78 96 83 14 88 34 89 63 72
                21 36 23 09 75 00 76 44 20 45 35 14 00 61 33 97 34 31 33 95
                78 17 53 28 22 75 31 67 15 94 03 80 04 62 16 14 09 53 56 92
                16 39 05 42 96 35 31 47 55 58 88 24 00 17 54 24 36 29 85 57
                86 56 00 48 35 71 89 07 05 44 44 37 44 60 21 58 51 54 17 58
                19 80 81 68 05 94 47 69 28 73 92 13 86 52 17 77 04 89 55 40
                04 52 08 83 97 35 99 16 07 97 57 32 16 26 26 79 33 27 98 66
                88 36 68 87 57 62 20 72 03 46 33 67 46 55 12 32 63 93 53 69
                04 42 16 73 38 25 39 11 24 94 72 18 08 46 29 32 40 62 76 36
                20 69 36 41 72 30 23 88 34 62 99 69 82 67 59 85 74 04 36 16
                20 73 35 29 78 31 90 01 74 31 49 71 48 86 81 16 23 57 05 54
                01 70 54 71 83 51 54 69 16 92 33 48 61 43 52 01 89 19 67 48`
    .stripMargin()
    .split("\n").map(line => line.split(" ").map(v => parseInt(v, 10)));

var getTuple = function(matrix, row, col, rowOffset, colOffset) {
    return [
        matrix[row                ][col                ], 
        matrix[row + rowOffset    ][col + colOffset    ], 
        matrix[row + rowOffset * 2][col + colOffset * 2], 
        matrix[row + rowOffset * 3][col + colOffset * 3]
    ];
}

var multiply = (x, y) => x * y;

var max = 0;

for (let i = 0; i < 17; i++) {
    for (let j = 0; j < 17; j++) {
        max = Math.max(max, getTuple(matrix, i, j, 0, 1).reduce(multiply));
        max = Math.max(max, getTuple(matrix, i, j, 1, 0).reduce(multiply));
        max = Math.max(max, getTuple(matrix, i, j, 1, 1).reduce(multiply));
        max = Math.max(max, getTuple(matrix, i, j + 3, 1, -1).reduce(multiply));
    }
}

console.log(max);
```

# Spiral
```javascript
var Matrix = function(rowsize, colsize) {
	return Array.from(Array(rowsize), (v, k) => Array.from(Array(colsize), () => -1));
};

Matrix.prototype.getRowCol = function() {
	return {row : this.length, col : this[0].length};
}

Matrix.prototype.printMatrix = function() {
	var {row, col} = this.getRowCol();
	var maxlength = ("" + (row * col)).length;

	var getspace = function(len, maxlen) {
		return new Array(maxlen - len + 2).join(" ");
	};

	var str = "";
	for (line of this) {
		for (value of line) {
			str += getspace(("" + value).length, maxlength) + value;
		}
		str += "\n";
	}
	console.log(str);
};

Matrix.prototype.makeSpiral = function() {
	var {row, col} = this.getRowCol();
	var [x, y, dx, dy] = [0, 0, 0, 1];

	for (let i = 0; i < row * col; i++) {
		this[x][y] = i;
		[x, y] = [x + dx, y + dy];
		
		if (!this[x] || !this[x][y] || this[x][y] !== -1 ) {
			[x, y] = [x - dx, y - dy];
			[dx, dy] = [dy, -dx];
			[x, y] = [x + dx, y + dy];
		}
	}
	return this;
};

new Matrix(6, 6).makeSpiral().printMatrix();
```

## maze
```javascript
var input1 = `<     >`;

var input2 = `########
              #<     #
              #  ##  #
              #  ##  #
              #     >#
              ########`;

var input3 = `#######
              #<    #
              ##### #
              #     #
              # #####
              # #   #
              # # # #
              #   #>#
              #######`;

var input4 = `<   #   >`;

var input5 = `########
              #<     #
              #     ##
              #    #>#
              ########`;

var input6 = `#< #  #
              #  #  #
              #  # >#`;

var direction = [[1, 0], [-1, 0], [0, -1], [0, 1]];

var canPass = function(input) {
    var start = [], dest = [];
    var maze = input.split("\n").map((line, row) => line.trim().split("").map(function(v, col) {
        (v === "<") ? start = [row, col] : {};
        (v === ">") ? dest  = [row, col] : {};
    }));
    var rowsize = maze.length;
    var colsize = maze[0].length;
    
    console.log(`rowsize  : ${rowsize}, colsize  : ${colsize}` );
    console.log(`start : ${start}, dest : ${dest}`);
//	var [startrow, startcol] = findStart(maze);
};

var findStart = function(maze) {
    var index = maze.reduce((a, b) => a.concat(b)).findIndex(v => v =="<");
    var row = Math.floor(index / maze[0].length);
    var col = index % maze[0].length;
    console.log(`row : ${row}, col : ${col}`);
    return [row, col];
};

var array1 = [1,2,3,4];
var array2 = [5,6,7,8];

var sum = array1.map(function (num, idx) {
  return num + array2[idx];
}); // [6,8,10,12]
```

```javascript
console.log([65,65,133,273,577,3587,577,273,133,65,65].map(v=>(v>>>0).toString(2).slice(1).replace(/0/g," ").replace(/1/g,"*")).join("\n"));

console.log("     *\n     *\n    * *\n   *   *\n  *     *\n**       **\n  *     *\n   *   *\n    * *\n     *\n     *");


console.log([65,65,133,273,577,3587].map(v=>(v>>>0).toString(2).slice(1).replace(/0/g," ").replace(/1/g,"*")).join("\n"));


function b(n){a="";while(--n)a+=" ";return a+"*";}e="\n",c=[b(6),b(6),b(5)+b(2),b(4)+b(4),b(3)+b(6)];alert(c.join(e)+e+"**"+b(8)+"*"+e+c.reverse().join(e))

b=n=>{a="";while(--n)a+=" ";return a+"*";}




[[5],[5],[4,1],[3,3],[2,4],[0,0,7,0],[2,4],[3,3],[4,1],[5,5]].map(v=>v.map(v=>new String(v)

[5,5,41,33,24,"0070",24,33,41,5,5].map(v=>(""+v).split("").map(v=>

[[5],[5],[4,1],[3,3],[2,4],[0,0,7,0],[2,4],[3,3],[4,1],[5,5]].map(v=>v.map(v=>' '.repeat(v)+"*").join("")).join("\n")


     *
     *
    * *
   *   *
  *     *
**       **
  *     *
   *   *
    * *
     *
     *
```
