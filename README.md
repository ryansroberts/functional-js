# functional.js (λ) [![Build Status](https://travis-ci.org/leecrossley/functional-js.png?branch=master)](https://travis-ci.org/leecrossley/functional-js) [![devDependency Status](https://david-dm.org/leecrossley/functional-js/dev-status.png)](https://david-dm.org/leecrossley/functional-js#info=devDependencies)

functional.js is (go on, guess) a functional js library. It facilitates [currying](http://en.wikipedia.org/wiki/Currying) and [point-free / tacit](http://en.wikipedia.org/wiki/Tacit_programming) programming in JavaScript.


## Getting started

### Using npm

```
npm install functional.js
```

To then include functional.min.js in your app:

```
var λ = require("functional.js");
```

### Direct dependency

Download the minified version [here](http://bit.ly/funcmin), reference the js file and λ will become a global variable.

## Examples

### Basic λ.curry example

```javascript
var concatenate = λ.curry(function(word1, word2) {
    return word1 + " " + word2;
});

var concatenateHello = concatenate("Hello");
var result = concatenateHello("World");

expect(result).toEqual("Hello World");
```

### Another λ.curry example

```javascript
var add = λ.curry(function(arg1, arg2, arg3) {
    return arg1 + arg2 + arg3;
}); 

var add3 = add(3),
    add5 = add3(2);

expect(add(3)(2)(1)).toEqual(6);
expect(add3(2, 1)).toEqual(6);
expect(add3(2)(1)).toEqual(6);
expect(add5(1)).toEqual(6);
```

### Extending arity with λ.curry example

```javascript
var add = λ.curry(function(arg1, arg2) {
    return arg1 + arg2;
});

var add3 = add(3);

expect(add(1, 2, 3)).toEqual(6);
expect(add3(1, 2, 3, 4, 5)).toEqual(18);
```

### Curried λ.each example

```javascript
var result = [],
    items = ["f", "u", "n", "c"];

var addTo = function (item) {
    return result.push(item);
};

var addToResult = λ.each(addTo);
expect(typeof (addToResult)).toEqual("function");

addToResult(items);
expect(result).toEqual(["f", "u", "n", "c"]);
```

### Curried λ.map example

```javascript
var items = [1, 2, 3];

var doubleUp = function (number) {
    return number * 2;
};

var doubleMap = λ.map(doubleUp);
expect(typeof (doubleMap)).toEqual("function");

var result = doubleMap(items);
expect(result).toEqual([2, 4, 6]);
```

### Curried λ.reduce example

```javascript
var items = [1, 2, 3];

var multiply = function (arg1, arg2) {
    return arg1 * arg2;
};

var multiplyReduceFrom1 = λ.reduce(multiply, 1);
expect(typeof (multiplyReduceFrom1)).toEqual("function");

var result = multiplyReduceFrom1(items);
expect(result).toEqual(6);
```

### Curried λ.any example

```javascript
var items1 = [1, 2, 3],
    items2 = [1, 3, 5];

var even = function (item) {
    return item % 2 === 0;
};

var anyEven = λ.any(even);

expect(anyEven(items1)).toBeTruthy();
expect(anyEven(items2)).not.toBeTruthy();
```

### Curried λ.select example

```javascript
var items = [1, 2, 3, 4, 5];

var even = function (item) {
    return item % 2 === 0;
};
var odd = function (item) {
    return item % 2 !== 0;
};

var selectEven = λ.select(even);
var selectOdd = λ.select(odd);

expect(selectEven(items)).toEqual([2, 4]);
expect(selectOdd(items)).toEqual([1, 3, 5]);
```

### Multiple λ.compose example

```javascript
var e = function (a) {
    return "hello " + a;
};
var f = function (a) {
    return a + 1;
};
var g = function (a) {
    return a * 100;
};
var composed = λ.compose(e, f, g);

expect(composed(2)).toEqual("hello 201");
```

### Curried λ.partition example

```javascript
var items = [7, 6, 5, 4, 3, 2, 1];

var even = function (item) {
    return item % 2 === 0;
};

var partitionEven = λ.partition(even);

var result = partitionEven(items);

expect(result).toEqual([[6, 4, 2], [7, 5, 3, 1]]);
```