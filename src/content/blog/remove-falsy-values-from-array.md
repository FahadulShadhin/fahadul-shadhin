---
title: Remove Falsy Values from a JavaScript Array
description: How to remove falsy values from a JavaScript array using Array.prototype.filter() and Boolean. The resulting array retains only truthy values.
pubDate: 2026-11-01
tags:
  - JavaScript
  - Interview Question
draft: false
---

Given an array with falsy values. We need to remove the falsy values from the array.

JavaScript has the following falsy values:
1. `false`
2. `0`
3. `''` (blank)
4. `null`
5. `undefined`
6. `NaN`

The task is to remove those from an array:

```JavaScript
let myArr = [0, 1, false, 2, '', 3, null, undefined, NaN, 4, 'hello', true];
let filteredArr = myArr.filter(Boolean);
console.log(filteredArr);

/* 
outputs only the truthy values:
[ 1, 2, 3, 4, 'hello', true ]
*/
```

## How Does This Work?

#### The `Boolean` function:
To understand this we need to understand the `Boolean` function. The `Boolean` function returns `true` or `false` depending on the expression given to it:

```JavaScript
Boolean(5 > 6) // returns: false
Boolean(5 < 6) // returns: true
Boolean('Hello world') // returns: true
Boolean('') // returns: false
Boolean(true) // returns: true
Boolean(false) // returns: false
```

#### The `filter` array method:
The structure of `filter` function is as below:

```JavaScript
someArray.filter(function(element, index, array) {
  // Return a truthy value to keep the element
  return true;
});
```
We need to send a function reference to `filter`. It calls the function for every assigned array element and creates a shallow copy containing only the elements for which the function returns a truthy value. Empty slots in a sparse array are skipped.

An example:

```JavaScript
let arr1 = [1 ,2, 3, 4, 5, 6, 7, 8, 9, 10];
let arr2 = arr1.filter(function isSmallerThanFive(num) {
  return num < 5;
});
/*
returns:
[1, 2, 3, 4]
*/
```
The `isSmallerThanFive` function returns `true` for only the elements in `arr1` that are smaller than number 5. Then `filter` returns a new array containing only those truthy elements.

#### `filter` & `Boolean` combined achieve what we need:

So, when we pass the reference of `Boolean` function to `filter`, `Boolean` evaluates every element of the array and returns `true` for the truthy values and `false` for the falsy values. And this finally gives us the expected array removing all the falsy values! 
