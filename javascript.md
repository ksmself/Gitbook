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

## Conditional Statements

### Comparison Operators 

* is equal to: **===**
* is not equal to: **!==** 

### Truthy and Falsy

```javascript
let myVariable = 'I Exist!';
if (myVariable) {
   console.log(myVariable)
} else {
   console.log('The variable does not exist.')
}
```

* **if** statement will run because **myVariable** has a **truthy** value.
* even though the value of **myVariable** is not explicitly the value **true**, when used in a boolean or conditional context, it evaluates to **true** because it has been assigned a non-falsy value. 

#### falsy values

* **0**
* empty strings like **""** or **''**
* **null**, represent there is no value at all
* **undefined**, represent when a declared variable lacks a value
* **NaN**

### Truthy and Falsy Assignment

Say you have a website and want to take a user's username to make a personalized greeting. Sometimes, the user does not have an account, making the **username** variable falsy. The code below checks it username is defined and assigns a defalut string if it is not. 

```javascript
let defaultName = username || 'Stranger';
```

**\|\|** checks the **left-hand condition first**, the variable **defaultName** will be assigned the actual value of **username** if is truthy, and it will be assigned the value of **'Stranger'** if _username is falsy_. This concept is also referred to as _short-circuit evaluation_. 

### Ternary Operator

```javascript
isNightTime ? console.log('Turn on the lights!') 
: console.log('Turn off the lights!');
```

* Two expressions follow the **?** and are separated by a **colon**. 
* If the condition evaluates to **true**, the **first** expression executes.
* If the condition evaluates to **false**, the **second** expression executes. 

## Functions

### Function Declarations

One way to create a function is by using a function declaration. 

```javascript
function greetWorld() {
  console.log('Hello, World!');
}
```

* The **function** is a keyword.
* greetWorld is the **name** of the function, followed by parentheses.
* console.log\('Hello, World!'\); is a **function body**, the block of statements required to perform a specific task, enclosed in the function's curly brackets, **{}**. 

### Default Parameters 

One of the features added in ES6 is the ability to use **default parameters**. It allows parameters to have a predetermined value in case there is _no argument passed_ into the function or if the argument is _undefined_ when called. 

```javascript
function greeting (name = 'stranger') {
  console.log(`Hello, ${name}!`)
}

greeting('Nick') // Output: Hello, Nick!
greeting() // Output: Hello, stranger!
```

### Return

When a function is called, the computer will ****_**run through**_ the function's code and _**evaluate the result**_ of calling the function. By default that resulting value is **undefined**. 

```javascript
function rectangleArea(width, height) {
  let area = width * height 
}
console.log(rectangleArea(5, 7)) 
// Prints undefined
```

Did we write our function wrong? No, In fact, the function worked fine, and the computer did calculate the area as 35, but we didn't capture it. We can do that with the keyword **return**! 

### Function Expressions 

Another way to define a function. 

* To define a function inside an expression, we can use the **function** keyword.
* In a function expression, the _function name is usually omitted_. It is called an anonymous function. 
* A function expression is often stored in a **variable in order to refer to it**. 
* Unlike function declarations, function expressions are not hoisted so they cannot be called before they are defined. 

```javascript
const calculateArea = function(width, height){
  const area = width * height;
  return area;
}; 
```

### Arrow Functions

ES6 introduced _arrow function syntax_, a shorter way to write functions by using the special "fat arrow" **\(\) =&gt;** notation. 

* Arrow functions remove the need to type out the keyword **function** every time you need to create a function. 
* Instead, you first include the parameters inside the **\( \)** and then add an arrow **=&gt;** that points to the function body surrounded **{}**.
* It's important to be familiar with the multiple ways of writing functions because you will come across each of these when reading other JavaScript code.  

```javascript
const rectangleArea = (width, height) => {
  let area = width * height;
  return area;
};
```

### Concise Body Arrow Functions

JS also provides several ways to refactor arrow function syntax. 

1. Functions that take **only a single parameter do not need that parameter to be enclosed in parentheses**. However, if a function takes zero or multiple parameters, parentheses are required. 
2. A function body composed of **a sing-line block does not need curly brace**, whatever that line evaluates will be automatically returned. The contents of the block should immediately follow the arrow **=&gt;** and the **return** **keyword can be removed**. This is referred to as implicit return. 

```javascript
//ZERO PARAMETERS
const functionName = () => {};

//ONE PARAMETER
const functionName = paramOne => {};

//TWO OR MORE PARAMETERS
const functionName = (paramOne, paramTwo) => {};
```

```javascript
const squareNum = (num) => {
  return num * num;
};

//We can refactor the function to:
const squareNum = num => num * num;
```

## Scope

where variables can be accessed or referenced. 

### Global Scope

Variables can exist either outside of or within blocks. In **global scope**, variables are _declared outside of blocks_. They can be accessed by any code in the program, including code in blocks. 

```javascript
const color = 'blue'

const returnSkyColor = () => {
  return color; // blue 
};

console.log(returnSkyColor()); // blue
```

* Even though the **color** variable is _defined outside of the block_, it can be accessed in the function block. 

### Block Scope

When a variable is _defined inside a block_, it is only accessible to the code within the curly braces **{ }**. This variable has **block scope**. 

```javascript
const logSkyColor = () => {
  let color = 'blue'; 
  console.log(color); // blue 
};

logSkyColor(); // blue 
console.log(color); // ReferenceError
```

### Scope Pollution 

It may seem like a great idea to always make your variables accessible, but _having too many global variables can cause problems_ in a program. When you declare global variables, they go to the **global namespace**. Global variables _remain there until the program finishes_ which means our global namespace can fill up really quickly. 

**Scope pollution** is when we have too many global variables that exist in the global namespace, or when we reuse variables across different scopes. 

```javascript
let num = 50;

const logNum = () => {
  num = 100; // Take note of this line of code
  console.log(num);
};

logNum(); // Prints 100
console.log(num); // Prints 100
```

* We have a variable **num**.
* Inside the function body of **logNum\(\)**, we want to declare a new variable but forgot to use the **let** keyword. 
* When we call **logNum\(\)**, **num** gets reassigned to **100**. 
* The reassignment inside **logNum\(\)** affects the global variable **num**.
* Even though the reassignment is allowed and we won't get an error, if we decide to use **num** later, we'll unknowingly use the new value of **num**.  
* It's best practice to not define variables in the global scope. 

### Practice Good Scoping 

```javascript
const logSkyColor = () => {
  const dusk = true;
  let color = 'blue'; 
  if (dusk) {
    let color = 'pink';
    console.log(color); // pink
  }
  console.log(color); // blue 
};

console.log(color); // ReferenceError
```

* It's an example of how to use block scope. 
* While we use block scope, we still pollute our namespace by reusing the same variable name twice. A better practice would be to rename the variable inside the block. 
* If a **variable does not need to exist outside a block** =&gt; **It shouldn't!** 

## Arrays

Arrays are JS's way of making lists. It can store any data types\(including strings, numbers, and booleans\). Like lists, arrays are ordered, meaning each item has a numbered position. 

### Create an Array

One way we can create an array is to use an array literal. An array literal creates an array by wrapping items in square brackets **\[ \]**. We can have an array that holds all the same data types or an array that _holds different data types_. We can also _save an array to a variable_. 

```javascript
let newYearsResolutions = ['Keep a journal', 'Take a 
falconry class', 'Learn to juggle'];
```

### Arrays with let and const 

Variables declared with the **const** keyword cannot be reassigned. However, elements in an array declared with **const** remain mutable. Meaning that we _**can change the contents of a const array**_, but ****_**cannot reassign a new array or a different value**_. 

```javascript
const utensils = ['Fork', 'Knife', 'Chopsticks', 'Spork'];
// change the contents of a const array is possible
utensils[3] = 'Spoon';
console.log(utensils);
// cannnot reassign a new array! 
utensils = ['namnam'];
```

### The .push\(\) Method

One of built-in JS methods that make working with arrays easier. **.push\(\)** allows us to **add items to the end of an array**. 

```javascript
const itemTracker = ['item 0', 'item 1', 'item 2'];

itemTracker.push('item 3', 'item 4');

console.log(itemTracker); 
//Output: ['item 0', 'item 1', 'item 2', 'item 3', 'item 4'];
```

### The .pop\(\) Method

Another array method, **.pop\(\)** **removes the last item of an array**. 

```javascript
const newItemTracker = ['item 0', 'item 1', 'item 2'];

const removed = newItemTracker.pop();

console.log(newItemTracker); 
// Output: [ 'item 0', 'item 1' ]
console.log(removed);
// Output: item 2
```

### More Array Methods 

[https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)

### Arrays and Functions 

```javascript
const flowers = ['peony', 'daffodil', 'marigold'];

function addFlower(arr) {
  arr.push('lily');
}

addFlower(flowers);

console.log(flowers); 
// Output: ['peony', 'daffodil', 'marigold', 'lily']
```

When you pass an array into a function, if the array is mutated inside the function, that **change will be maintained outside the function** as well. 

## Loops 

### When to use a while loop

The syntax of a **for** loop is ideal when we _know how many times the loop should run_, but we don't always know this in advance. In situations when we want a loop to execute an _undetermined number of times_, **while** loops are the best choice.  

### The break keyword

With breaks, we can add _test conditions_ besides the stopping condition, and exit the loop when they're met. 

## Higher-Order Functions 

### Introduction

When we say "bake", it calls to mind a familiar subroutine-- preheating an oven, putting something into an oven for a set amount of time, and finally removing it. This allows us to **abstract** away a lot of the details and communicate key concepts more concisely. 

In programming, we can accomplish "**abstraction**" by writing **functions**. In addition to allowing us to reuse our code, functions help to _make clear, readable programs_. 

**Higher-order functions** are functions that _accept other functions as arguments and/or return functions as output_. This enables us to build abstractions on other abstractions, just like "We hosted a birthday party" is an abstraction that may build on the abstraction "We made a cake."

### Functions as Data 

We can assign functions to variables, and we can reassign them to new variables. Below, we have an annoyingly long function name that hurts the readability of any code in which it's used. 

```javascript
const announceThatIAmDoingImportantWork = () => {
    console.log("I’m doing very important work!");
};
```

What if we wanted to rename this function without sacrificing the source code? 

```javascript
const busy = announceThatIAmDoingImportantWork;

busy(); // This function call barely takes any space!
```

In JS, functions are first class objects. This means that, like other objects you've encountered, Js functions can have properties and methods. 

## Iterators

The built-in JS array methods that help us **iterate** are called iteration methods, at times referred to as **iterators**. _Iterators are methods called on arrays to manipulate elements and return values_. 

### The .forEach\(\) Method

It will **execute the same code for each element of an array**. 

```javascript
const groceries = ['brown sugar', 'salt', 'cranberries', 
'walnuts'];

groceries.forEach(function(groceryItem){
console.log('-' + groceryItem);
}):
```

* .forEach\(\) takes an argument of callback function. 
* .forEach\(\) _loops through the array and executes the callback function for each element_. During each execution, _the current element is passed as an argument to the callback function_. 

Another way to pass a callback for .forEach\(\) is to use **arrow function** syntax. 

```javascript
groceries.forEach(groceryItem => 
console.log(groceryItem));
```

We can also define a function beforehand to be used as the callback function. 

```javascript
function printGrocery(element){
  console.log(element);
}

groceries.forEach(printGrocery);
```

### The .map\(\) Method

When **.map\(\)** is called on an array, it takes an argument of a callback function and **returns a new array**! 

```javascript
const numbers = [1, 2, 3, 4, 5]; 

const bigNumbers = numbers.map(number => {
  return number * 10;
});

console.log(numbers); // Output: [1, 2, 3, 4, 5]
console.log(bigNumbers); // Output: [10, 20, 30, 40, 50]
```

**.map\(\)** works in a similar manner to **.forEach\(\)** - the major difference is that **.map\(\)** returns a new array. Notice that the elements in **numbers** were not altered and **bigNumbers** is a new array. 

### The .filter\(\) Method

Like **.map\(\)**, **.filter\(\)** _returns a new array_. However, **.filter\(\)** returns an array of elements **after filtering out certain elements** from the original array. The callback function for the **.filter\(\)** method should return **true or false** _depending on the element that is passed to it_. The elements that cause the callback function to **return true are added to the new array**. 

```javascript
const words = ['chair', 'music', 'pillow', 'brick', 
'pen', 'door']; 

const shortWords = words.filter(word => {
  return word.length < 6;
});

console.log(words); 
// Output: ['chair', 'music', 'pillow', 'brick', 'pen', 'door']; 
console.log(shortWords); 
// Output: ['chair', 'music', 'brick', 'pen', 'door']
```

### The .findIndex\(\) Method 

We sometimes want to find the location of an element in an array. Calling **.findIndex\(\)** on an array will **return the index of the** _**first element**_ **that evaluates to true** in the callback function. 

```javascript
const jumbledNums = [123, 25, 78, 5, 9]; 

const lessThanTen = jumbledNums.findIndex(num => {
  return num < 10;
});

console.log(lessThanTen); // Output: 3 
```

If _there isn't a single element in the array that satisfies the condition_ in the callback, then **.findIndex\(\) will return -1**.  

### The .reduce\(\) Method 

It _**returns a single value**_ **after iterating** through the elements of an array, thereby **reducing the array**. 

```javascript
const numbers = [1, 2, 4, 10];

const summedNums = numbers.reduce((accumulator, 
currentValue) => {
  return accumulator + currentValue
})

console.log(summedNums) // Output: 17
```

The **.reduce\(\)** method can also _take an optional second parameter to set an initial value for accumulator_\(remember, the first argument is the callback function\). 

```javascript
const numbers = [1, 2, 4, 10];

const summedNums = numbers.reduce((accumulator, 
currentValue) => {
  return accumulator + currentValue
}, 100)  // <- Second argument for .reduce()

//first accumulator is 100! 
console.log(summedNums); // Output: 117
```

### Iterator Documentation 

[https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/Array\#Iteration\_methods](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array#Iteration_methods)

## Objects 

JavaScript objects are containers storing related data and functionality. 

### Creating Object Literals

Objects can be assigned to variables just like any JavaScript type. Using curly braces, **{ }** to designate an _object literal_. 

```javascript
let spaceship = {}; // spaceship is an empty object
```

We fill an object with unordered data. This data is organized into **key-value** pairs. A key is like a variable name that points to a location in memory that holds a value. A key's value can be of any data type in the language including functions or other objects. 

We make a key-value pair by writing the **key's name**, or identifier, followed by a **colon** and then the **value**. We **separate** each key-value pair in an object literal with a **comma**. 

```javascript
// An object literal with two key-value pairs
let spaceship = {
  'Fuel Type': 'diesel',
  color: 'silver'
};
```

The spaceship object has two properties Fuel Type and color. 'Fuel Type' has **quotation marks** because it contains a **space character**. 

### Accessing Properties 

There are two ways we **can access an object's property**. The first way is **dot notation**. We've used dot notation to access the properties and methods of built-in objects and data instances. With property dot notation, we write the **object's name**, followed by the **dot operator** and then the property name\(**key**\). 

```javascript
let spaceship = {
  homePlanet: 'Earth',
  color: 'silver'
};
spaceship.homePlanet; // Returns 'Earth',
spaceship.color; // Returns 'silver',
```

If we try to access **a property that does not exist** on that object, **undefined** will be returned. 

```javascript
spaceship.favoriteIcecream; // Returns undefined
```

### Bracket Notation

The second way to access a key's value is by using bracket notation, **\[ \]**. To use bracket notation to access an object's property, we pass in the property name**\(key\) as a string**. 

We **must use bracket notation** when accessing **keys that have numbers, spaces, or special characters** in them. Without bracket notation in these situations, our code would throw an error. 

```javascript
let spaceship = {
  'Fuel Type': 'Turbo Fuel',
  'Active Duty': true,
  homePlanet: 'Earth',
  numCrew: 5
};
spaceship['Active Duty'];   // Returns true
spaceship['Fuel Type'];   // Returns  'Turbo Fuel'
spaceship['numCrew'];   // Returns 5
spaceship['!!!!!!!!!!!!!!!'];   // Returns undefined
```

With bracket notation you can also use a variable inside the brackets to select the keys of an object. This can be especially helpful when working with functions. If we tried to write our returnAnyProp\(\) function with dot notation\(**objectName.propName**\) the computer would look for **a key of 'propName' on our object** and not the value of the propName parameter. 

```javascript
let returnAnyProp = (objectName, propName) => 
objectName[propName];

returnAnyProp(spaceship, 'homePlanet'); 
// Returns 'Earth'
```

### 

### 

### 

### 

### 

### 

### 

### 

