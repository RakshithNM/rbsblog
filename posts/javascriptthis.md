---
title: This in javascript
date: 2021-04-03
published: true
tags: ['js','this']
cover_image: ./images/this/this-obj-method.png
canonical_url: false
description: "Understanding the this keyword once and for all"
layout: layouts/post.njk
---

In this post we will explore what `this` keyword refers under various conditions and there by understand the keyword and how it works in javascript.

The `this` keyword can point to
* The object when referenced within the obejcts method.
* The `window` object - when referenced within a function.
* The instance of the object when the new keyword is used.
* The object when arrow function is used`

## `this` within method of an object - no arrow function

```js
const obj = {
    name: "obj",
    printName() {
        console.log(this.name);
    },
    printObj() {
        console.log(this); // this refers to the object `obj`
    }
}
obj.printName() // obj
obj.printObj() //{name: "obj", printName: ƒ, printObj: ƒ}
```
## `this` within method of an object - arrow function

The value of `this` in an arrow function is always the value of `this` in the parent non arrow function.

```js
const obj = {
    name: "obj",
    printObj: () => {
        console.log(this); // this refers to the window
    }
}
obj.printObj() // Window {window: Window, self: Window, document: document, name: "", location: Location, …}
```

## `this` within function body

```js
function greet() {
    console.log(this);
}
greet(); // Window {window: Window, self: Window, document: document, name: "", location: Location, …}
```
## `this` when `new` keyword is used

```js
function Game(inTitle) {
    this.title = inTitle;
    console.log(this); // Game {title: "pong"}
}

const game = new Game("pong");
```
## `this` within callback in a method of an object - no arrow function

```js
const fruits = {
    name: "fruits",
    fruits: ["apple", "mango", "banana"],
    printFruits() {
        console.log(this); // {name: "fruits", fruits: Array(3), printFruits: ƒ}
        this.fruits.forEach(function(fruit) {
            console.log(this); // Window {window: Window, self: Window, document: document, name: "", location: Location, …} * 3 times
        })
    }
}

fruits.printFruits();
```
## `this` within callback in a method of an object - arrow function

```js
const fruits = {
    name: "fruits",
    fruits: ["apple", "mango", "banana"],
    printFruits() {
        console.log(this); // {name: "fruits", fruits: Array(3), printFruits: ƒ}
        this.fruits.forEach((fruit) => {
            console.log(this); // {name: "fruits", fruits: Array(3), printFruits: ƒ} * 3 times
        })
    }
}

fruits.printFruits();
```
