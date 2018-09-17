---
title: Javascript functions
date: 2017-12-12 01:49:27
tags: [javascript, Javascript functions, IIFE, context, scoping, closures]
categories: [javascript]
---

## Javascript functions, closures and scopes

---

### Functions:

##### 1) Function statement:

```
function calcRectArea(width, height) {

	return width * height;

}
 console.log(calcRectArea(5, 6));
```

---

##### 2) Function expression:

```
var getRectArea = function(width, height) {

    return width * height;

}
 console.log(getRectArea(3,4));

// expected output: 12
```

---

##### 2. a) Anonymous methods

var myFunction = function() {
statements
}

---

##### Named function expression

```
var myFunction = function namedFunction(){
    statements
}
```

Benefit of named function expression is that in case we encountered an error,
the stack trace will contain the name of the function, making it easier to find the origin of the error.

---

##### 2. b) IIFE

Normal function, not an IIFE

```
var counter = 0;
var f = function(){
	counter++;
	console.log(counter);
}
f();
counter++;
f();
```

---

Normal function, not an IIFE  
Scope Pollution

```
var counter = 0;
var f = function(){
	var counter = 5;
	console.log(counter);
}
f();
counter++;
f();
```

---

IIFE

```
var counter = 0;
(function(){
	var counter = 5;
	console.log(counter);
})();
counter++;
console.log(counter);
```

---

##### Pros of IIFE:

-   a) Called once, can also be used to initialize variables |
-   b) Improving performance, since javascript first looks upto local scope |
-   c) Simulatting or creating a new scope |
-   d) Avoding scope pollution |

---

##### Arrow functions:

```
([param[, param]]) => {
   statements
}
```

```
param => expression
```

---

##### Context

```
let obj = {
  myVar: 'foo',

  myFunc: function() {
    console.log(this.myVar)
  }
}
obj.myFunc() // foo
```

---

```
let obj = {
  myVar: 'foo',

  myFunc: function() {
    console.log(this.myVar)

    setTimeout(function() {
      console.log(this.myVar)
    }, 1000)
  }
}
obj.myFunc()
```

---

##### Lexical Scope

```
let obj = {
  myVar: 'foo',

  myFunc: function() {
    let self = this
    console.log(this.myVar)

    setTimeout(function() {
      console.log(self.myVar)
    }, 1000)
  }
}
obj.myFunc() // foo ... then... foo
```

---

###### Problem solved with arrow functions:

```
let obj = {
  myVar: 'foo',

  myFunc: function() {
    console.log(this.myVar)

    setTimeout(() => {
      console.log(this.myVar)
    }, 1000)
  }
}
obj.myFunc() // foo ... then... foo
```

---

###### Beware

```
let obj = {
  myVar: 'foo',

  myFunc: () => {
    console.log(this.myVar)
  }
}
obj.myFunc() // undefined
```

---

##### Closures

Created when an inner function tries to access variables and other objects, of the parent function.
Eg.

```
function parent() {
    var name = “John”;
    var child = function () {
        console.log (name); };
    return child;
}
```

## Closures are uni-directional i.e. from parent to child

Each function has a separate scope

```
function parent() {
    var name = “John”;
    var child = function () {
        console.log (name); };
    return child;
}
var child = parent();
child();
// The name would still be accessible, even after exiting parent
```

---

```
function makeCounter {
  var counter = 0; // this variable should normally go away, but it won't!
  return function() {
    counter++;
    return counter;
  }
}
var getCount = makeCounter();
// the function makeCounter has finished, so normally var counter
// would have been forgotten about!
var n1 = getCount(); // n1 now equals 1
var n2 = getCount(); // n2 now equals 2
```

---

IO operations

read file, DB calls,  
In C#, Java multi threaded app  
In nodejs single threaded event loop

callback  
events

---

THANK YOU!
Sources:  
[MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions)  
[Medium](https://medium.com/tfogo/advantages-and-pitfalls-of-arrow-functions-a16f0835799e)  
[Quora](https://www.quora.com/How-do-I-explain-JavaScript-closures-to-a-child)
