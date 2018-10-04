---
title: Javascript Tips and Tricks
date: 2018-10-04 23:02:03
tags: [Javascript]
categories: [Javascript]
---

## Tips and Tricks

#### 1) Getting an array from behind to front

Given the array:

```javascript
const animals = ['Otter', 'Badger', 'Alpaca', 'Sloth'];
```

We can get each item in the array from behind to front by doing this:

```javascript
animals.slice(-1); // ['Otter']
animals.slice(-2); // ['Badger']
animals.slice(-3); // ['Alpaca']
animals.slice(-4); // ['Sloth']
```

#### 2) Short-circuit

Instead of doing:

```javascript
if (condition) {
    callMe();
}
```

You can just simply:

```javascript
condition && callMe();
```

#### 3) One liner `if` `else` statement

The long way:

```javascript
const age = 10;
const legalAge = 18;

if (age >= legalAge) {
    console.log('Drink beer!');
} else {
    console.log('Drink milk or something else!');
}
```

The one liner way:

```javascript
console.log(age >= legalAge ? 'Drink beer!' : 'Drink milk or something else!');
```

#### 4) `typeof` in validation

`typeof` can be useful in validation data validation. Let's say you have a simple addition function that takes 2 arguments as addends then returns the sum. You want to make use that the arguments being passed are really numbers and not objects or string. You can do that by using `typeof`.

```javascript
const add = (x, y) => {
    if (typeof x !== 'number' || typeof y !== 'number') return null;
    return x + y;
};

add(1, 1); // 2
add(1, {}); // null
```

By this solution, you can make sure that the addends are number.

#### 5) Assigning alternative value to a falsy variables

Say you a variable `color` which is undefined. You can add an alternative value to it by using the `||` operator.

```javascript
const color = undefined;

const alpacaColor = color || 'green';

console.log('Alpaca color is ' + alpacaColor); // Alpaca color is green
```

> Who wants a green alpaca?

Special thanks to contributor : [Jofferson Ramirez Tiquez](https://github.com/jofftiquez)
