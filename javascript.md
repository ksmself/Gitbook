---
description: 구문(syntax)과 기본 문법 정리. 내 머릿속에 들어있는지 확인하는 과정.
---

# JavaScript

## Introduction to Javascript

### Data Types

1. Number
2. String
3. Boolean
4. Null: represents the intentional absence of a value. represented by the keyword **null**\(without quotes\).
5. Undefined: also represents the absence of a value though it has a different use than null. denoted by the keyword **undefined**\(without quotes\).
6. Symbol: A newer feature to the language. unique identifiers, useful  in more complelx coding. 
7. Object: Collections of related data. 

### Properties

When you introduce a new piece of data into a JavaScript program, the browser saves it as an **instance** of the data type. Every string instance has a **property** called _length_ that stores the number of characters in that string. 

### Methods

* Methods are actions we can perform. Javascript provides a number of string methods. 
* When we use **console.log\(\)** we're calling the **.log\(\)** method on the **console** object. 
* You can find a list of **built-in-string methods**: [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/String](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)

### Built-in Objects 

To see all of the properties and methods on the **Math object**: [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/Math](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math)

## Variables 

a container for a value. 

### var

* Prior to the ES6, programmers could only use the **var** keyword to declare variables. 
* short for variable. JavaScript keyword that creates, or declares, a new variable. 
* myName is the variable's name. **Capitalizing** in this way is a standard convention in JS. 

### let 

* the **let** keyword was introduced in ES6.
* variable can be **reassigned** a different value. 
* we can declare a variable **without assigning** the variable a value. The variable will be automatically initialized with  a value of **undefined**. \(and even **var**\)

### const

* also introduced in ES6, and is short for the word constant.
* **cannot be reassigned** because it is **constant**. 
* must be assigned a value when declared. 
* If you're trying to decide between which keyword to use, **let or const**, think about whether you'll need to **reassign** the variable later on. 

### String Interpolation

In the ES6 version of JS, we can insert, or interpolate, variables into strings using template literals. 

```javascript
const myPet = 'armadilllo';
console.log(`I own a pet ${myPet}.`);
//Output: I own a pet armadillo.
```

* a **template literal** is wrapped by backticks **\`** \(this key is usually located on the top of your keyboard, left of the 1 key\) 
* Inside the template literal, you'll see a placeholder, **${myPet}**. The value of **myPet** is inserted into the template literal. 
* biggest benefits to using template literals is the **readability** of the code. 

### typeof operator 

* If you need to check the **data type** of a variable's value, use the **typeof** operator.
* typeof operator checks the value to its right and returns, or passes back, a string of the data type.

```javascript
const unknown1 = 'foo';
console.log(typeof unknown1); // Output: string

const unknown2 = 10;
console.log(typeof unknown2); // Output: number

const unknown3 = true; 
console.log(typeof unknown3); // Output: boolean
```

## 

