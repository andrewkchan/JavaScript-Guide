This repository is a mirror of the full text at GitBook, which you can read [here](https://theandrewchan.gitbooks.io/javascript-crash-course/content/).

# Table of Contents

### Part I: The JavaScript Language

* [Introduction](https://github.com/theandrewchan/JavaScript-Guide#introduction)
1. [Primitives, Expressions](https://github.com/theandrewchan/JavaScript-Guide#1-primitives-expressions)
2. [Functions](https://github.com/theandrewchan/JavaScript-Guide#2-functions)
3. [Arrays](https://github.com/theandrewchan/JavaScript-Guide#3-arrays)
4. [Objects](https://github.com/theandrewchan/JavaScript-Guide#4-objects)

### Part II: Frontend Web Development

* [Overview](https://github.com/theandrewchan/JavaScript-Guide#part-ii---frontend-web-dev-overview)
5. [Basic HTML Review](https://github.com/theandrewchan/JavaScript-Guide#5-review-of-basic-html-tags)
6. [The Document Object Model](https://github.com/theandrewchan/JavaScript-Guide#6-the-document-object-model-dom)
7. [DOM Events and Interactivity](https://github.com/theandrewchan/JavaScript-Guide#7-dom-events-and-interactivity)
8. [Communicating with a Backend](https://github.com/theandrewchan/JavaScript-Guide#8-communicating-with-a-backend)

# JavaScript: Crash Course Part I

## Introduction

JavaScript is the _lingua franca_ of the web - it's used universally by every website out there and has grown from a simple scripting language to a mature programming language with an enormous ecosystem. Today we'll learn basic JavaScript syntax, data types, and functions.

## Getting Started

Getting started with JavaScript is easy - all you need is a web browser. We will be using some particular features that aren't supported by older browsers, so we recommend using the [latest version of Google Chrome](https://www.google.com/chrome/).

Every modern web browser (e.g. Chrome, Firefox, Edge, and Safari) includes something called a **Web Console** which you can use to interactively execute JavaScript in the context of the current page. To open up the Web Console, **right-click** anywhere on the current page and select **Inspect** from the menu (you can also type `Control`+`Shift`+`I` on Windows or `Cmd`+`Option`+`K` on Mac). Then select the **Console** tab in the window that pops up.

You can type any valid JavaScript in this window and press enter to execute it - what's more, you can view variables and objects in the context of the current page. This can be very useful if the current page is running a script that you want to debug!

## 1. Primitives, Expressions

Let's get started and see what primitive data types and operations with them are available in JS. You should be familar with most if not all of these from Python.

### 1.1 Expressions

Basic math is straightforward in JavaScript. The addition (`+`), subtraction (`-`), multiplication (`*`) and division (`/`) operators work as in Python:

```javascript
> 1 + 1 - 1; // semicolons are optional but we will be using them throughout.
1
> 1/2*5+3;
5.5
```

Additionally, we have more advanced operators such as:
* the arithmetic modulus operator (`%`)
* boolean operations like AND (`&&`) and OR (`||`)
* the boolean NOT operator (`!`)

```javascript
> true && false;
false
> true || false;
true
> !true
false
> 17 % 4;
1
```

### 1.2 Variables

We can assign the results of expressions to variables like in Python. The main difference here is that in JavaScript, you must prefix variable declarations with a **`var`** keyword:
```javascript
> var a = 1+1;
> a;
2
> a = 3; // don't need the `var` keyword since `a` has already been declared
> 3
> var b = a = 7; // we can chain assignments and declarations too!
> b;
7
> a;
7
```

Note that you can technically omit the `var` keyword and variable declarations will still work - but this is a bad idea, because it creates the variable in the global rather than local scope! More on that later.

### 1.3 Dynamic Typing and JavaScript Primitives

#### 1.3.1 Primitive Data Types

JavaScript defines six primitive data types. Here are the four most important ones:
* **Boolean** - `true` or `false` (lowercase, not uppercase!)
* **Null** - `null` only. This is similar to `None` in Python.
* **Number** - Like (decimal) numbers in Python. Note that JS has no specific integer type! There are also special Number values like **`NaN`** and **`Infinity`** reserved for values like 1/0.
* **String** - Just like strings in Python, these are immutable. They also support useful operations like slicing, reversing, etc. More on this later.

#### 1.3.2 Dynamic Typing

Like Python, JavaScript is a **loosely typed** or a **dynamic** language. Variables in JavaScript are not directly associated with any particular value type, and any variable can be assigned (and re-assigned) values of all types:

```javascript
> var iAmANumber = 4; // iAmANumber is a Number.
> iAmANumber = true; // iAmANumber now refers to a boolean!
> iAmANumber = "I am not a number"; // iAmANumber is now a string!
```

##### Determining types with `typeof`

You can determine the type of a value in your code using the `typeof` operator, which returns a string corresponding to the type of its argument. [Read the documentation for more.](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/typeof)

#### 1.3.3 Equality Comparisons

Here's where JavaScript and Python (and other languages!) really start to differ: equality comparisons in JavaScript are different in that some values that are different types can still be interpreted as "equal". For example:

```javascript
> 5 == '5';
true
> 5 != '5';
false
```

This is because JavaScript has a concept called **Sameness** that applies across types using the abstract equality operator (`==`). However, we will not be going into the (often complex) rules of sameness. Instead, we will require that you use the **strict equality operator** (`===`) and its counterpart the **strict inequality operator** (`!==`) instead, which only check for equality across identical types:

```javascript
> 5 === '5';
false
> 5 !== '5';
true
> '123' === '123';
true
```

#### 1.3.4 Operations Across Types

As we go deeper into the language we'll see that the main philosophy of JavaScript is essentially to _avoid crashing at all costs_. This means that we can play fast and loose with types, and even perform operations on values of different types! However, some operations aren't defined and will lead to some wonkiness - if in doubt, look up the operation you are applying in the [Mozilla Docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Arithmetic_Operators).

```javascript
> 'my favorite number is ' + 7; // String + Number --> String
"my favorite number is 7"
> 'my favorite value is ' + true; // String + Boolean --> String.
"my favorite value is true"
> 'foo' * 3; // String * Number --> NaN
NaN
> 1/0; // Division by Zero --> Infinity. In Python this would throw an ERROR!
Infinity
```

#### 1.3.5 Truthiness

Like Python, many non-boolean values are interpreted as `true` or `false` for convenience. The following values are **falsy**, e.g. they are interpreted as `false`:

* `false`
* `0`
* `""`, the empty string
* `null`, the null value
* `undefined` for a variable that does not exist. [Read more](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/undefined)
* `NaN` for Number values that do not evaluate to a meaningful number. [Read More](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/NaN)

All other values are **truthy**, e.g. interpreted as `true`.

## 2. Functions

Every function in JavaScript is a [`Function`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function) object. The main point to take away here is that **functions in JavaScript are values themselves and can be manipulated just like values**. This makes JavaScript an incredibly expressive language; here's where the real power is.

### 2.1 Defining and Calling Functions

We can define a function using a _function declaration_. The following function declaration defines a function called `makeSomeNoise` that takes in a single parameter called `yourName`.

```javascript
function makeSomeNoise(yourName) {
  return "Make some noise for " + yourName + "!!";
}
// let's call it now
makeSomeNoise("Sinho Chewi"); // --> "Make some noise for Sinho Chewi!!"
```

We can also use a _function expression_, which is just like a normal expression but returns a **function value**, which can be assigned to a variable or further manipulated:

```javascript
var makeSomeNoise = function(yourName) {
  return "Make some noise for " + yourName + "!!";
}
makeSomeNoise("Anant Sahai"); // --> "Make some noise for Anant Sahai!!"
```

#### 2.1.1 Anatomy of a Function Call

Going back to the philosophy of _avoiding crashing at all costs_, we observe that in JavaScript, functions can be called with less or more arguments than they ask for. Consider the following code:

```javascript
function iWantTwoArguments(a, b) {
  console.log(a, b);
}
// both of the below would throw exceptions in Python!
// but they execute without complaining.
iWantTwoArguments();
iWantTwoArguments(1, 2, 3, 4, 5);
```

There are no errors! But then how do we know if a function was called as intended or with extra/less arguments? We can check if specific parameters were omitted by seeing if they evaluate to `undefined`:

```javascript
function iWantTwoArguments(a, b) {
  if (typeof a === "undefined" || typeof b === "undefined") {
    return console.log("Missing an argument!");
  }
  console.log(a, b);
}
```

We can also check the [**`arguments`**](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/arguments) object, which is an array-like object (more on arrays in the next section):

```javascript
function iWantTwoArguments(a, b) {
  if (arguments.length !== 2) {
    return console.log("Did not receive exactly 2 arguments");
  }
  console.log(a, b);
}
```

Finally, we can combine the arguments object with [**rest parameters**](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/rest_parameters) to let functions accept an _indefinite number of arguments_.

```javascript
function printMyArguments(...args) {
  console.log(args); // prints my arguments in the form of an array.
}
```

### 2.2 Manipulating Functions

#### 2.2.1 Functions as Values

Just like in Python, functions can be passed around as arguments, returned from other functions, or be assigned to variables.

```javascript
function makeAdder(increment) {
  return function(inputNumber) {
    return inputNumber + increment;
  }
}
var incrementByOne = makeAdder(1);
var incrementByTwo = makeAdder(2);
incrementByOne(50); // --> 51
incrementByTwo(50); // --> 52
```

#### 2.2.2 Functional Operations

Since functions are values, we can apply some special operations to them to create new, more complex functions. Here are some such operations:

* [**Function binding**](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/bind) - Create a new function that is bound to a particular scope or is already applied to particular arguments.
* [**Function prototype calling**](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/call) - Call a function within the context of a particular scope with particular arguments.

### 2.3 Control

#### 2.3.1 Conditional Statements

JavaScript's syntax for if-else statements take the following form:

```javascript
if (CONDITION) {
  // STATEMENTS
} else if {
  // ...
} else {
  // ...
}
```

Conditional expressions are surrounded by parentheses and the statements to be executed if the condition is true should be surrounded by curly braces.

```javascript
if (currentClass === "61A") {
  console.log("ez pz lemon sqz");
} else if (currentClass === "61B") {
  console.log("okey dokey lowkey nopey");
} else if (currentClass === "70") {
  console.log("difficult difficult lemon difficult");
} else {
  console.log("???!!???!!???");
}
```

Observe that the above code only really cares about the value of a single expression - the value of the variable `currentClass`. We can make decisions based on different cases for a single expression using the **switch** statement as well, which is essentially syntactic sugar for this special if-else situation. The expression inside `switch (EXPR)` gets evaluated and the result is matched sequentially against each `case VALUE:`. If `EXPR == VALUE` then the code inside that case block is executed. If the `default:` block is reached, then that code will be executed regardless of the expression's value.

```javascript
switch (currentClass) {
  case "61A": {
    console.log("ez pz lemon sqz");
    break;
  }
  case "61B": {
    console.log("okey dokey lowkey nopey");
    break;
  }
  case "70": {
    console.log("difficult difficult lemon difficult");
    break;
  }
  default: {
    console.log("???!!???!!???");
    break;
  }
}
```

Notice the `break` statements at the end of each case block. If `break` is omitted then the program continues matching the expression with cases even after a case block has been executed. Sometimes this is useful but often this will result in the default block always being executed. [Read the documentation on `switch` for more.](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/switch)

So far our conditional controls have taken the form of _statements_ that are _executed_ rather than _evaluated_. But we can also express conditions in the form of _expressions_ that are evaluated to a value using the **conditional (ternary) operator**:

```javascript
var difficulty = (currentClass === "61A") ? "ez pz lemon sqz" : "super difficult";

// the above is equivalent to the following if-else statements::
if (currentClass === "61A") {
  difficulty = "ez pz lemon sqz";
} else {
  difficulty = "super difficult";
}
```

#### 2.3.2 Loops

**While loops** execute the body of the loop as long as a given condition is true:

```javascript
var i = 0;
while (i < 10) {
  console.log("Currently at the " + i + "th iteration of the loop");
  i++;
}
```

Notice in the above code that our loop executes 10 times, and to do this, we needed to do the following:

1. Declare and initialize a "counter variable" **before** our loop begins.
2. Check a **condition** at the start of **each iteration** of the loop.
3. Increment our counter variable at the **end** of each iteration.

We can put all of this code into its own block because all we really care about is the content of the loop. Let's do this using a **for loop**:

```javascript
for (var i = 0; i < 10; i++) {
  console.log("Currently at the " + i + "th iteration of the loop");
}
```

Sometimes when we're in the middle of an iteration of a loop, something happens that makes us want to break out of the loop. We can do this using a **break** statement:

```javascript
for (var i = 0; i < 10; i++) {
  console.log("Currently at the " + i + "th iteration of the loop");
  if (i === 7) {
    break; // this stops the loop at the end of the 7th iteration instead of the 10th
  }
}
```

## 3. Arrays

An _array_ in JavaScript is similar to a Python list: an ordered collection of values of any type that we can add to, delete from, and access by index. They are even created like Python lists:

```javascript
var badProfessors = []; // empty array
var goodProfessors = ["DeNero", "Hug", "Hilfinger"]; // non-empty array
// we can put anything inside arrays, even other arrays!
var dopeStuff = ["Berkeley", 1, ["public", "university"]];
```

We can access and assign to individual indices using square brackets:

```javascript
> var dopeStuff = ["Berkeley", 1, ["public", "university"]];
> dopeStuff[0];
"Berkeley"
> dopeStuff[0] = "UCLA";
> dopeStuff[0];
"UCLA"
```

Unfortunately (unlike Python), we can't use negative indices. To access the last element of an array, we need to use the **length** property of an array:

```javascript
> var dopeStuff = ["Andrew", "is", "GOAT"];
> dopeStuff.length;
3
> dopeStuff[dopeStuff.length - 1];
"GOAT"
```

### 3.1 Array Functions

All arrays are technically instances of the special [`Array`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array) object. This object has some very useful built-in functions.

#### 3.1.1 [`Array.map`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map)

The map function creates a new array with the results of calling a provided function on every element in the calling array. This is a lot like Python list comprehensions, except we are required to provide a function:

```javascript
> var someNumbers = [1, 4, 5, 9];
> var squaredNumbers = someNumbers.map(function(x) { return x*x; });
> squaredNumbers;
[1, 16, 25, 81]
> someNumbers; // original array is not changed
[1, 4, 5, 9]
```

#### 3.1.2 [`Array.forEach`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach)

The forEach function is a lot like the map function, but does **not** create a new array, and does not return anything.

```javascript
> var someNumbers = [1, 4, 5, 9];
> someNumbers.forEach(function(x) { console.log(x*x); });
1
16
25
81
> someNumbers; // original array is not changed
[1, 4, 5, 9]
```

#### 3.1.3 [`Array.push`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/push)

The push function adds one or more elements to the **end** of an array (like the list.append function in Python) and returns the new length of the array.

```javascript
> var someNumbers = [1, 4, 5, 9];
> someNumbers.push(20);
5
> someNumbers;
[1, 4, 5, 9, 20]
```

#### 3.1.4 [`Array.pop`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/pop)

The pop function removes the **last** element from an array and returns that element. This method changes the length of the array. Together with the push function, this is enough to use an array as a stack.

```javascript
> var someNumbers = [1, 4, 5, 9];
> someNumbers.pop();
9
> someNumbers;
[1, 4, 5]
```

#### 3.1.5 [`Array.slice`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/slice)

The slice function returns a shallow copy of a portion of an array into a new array object selected from begin to end (end not included). The original array will not be modified. This is similar to Python's list slices.

```javascript
> var professors = ["DeNero", "Hilfinger", "Hug", "Sahai"];
> var goodProfessors = professors.slice(0, 3);
> goodProfessors;
["DeNero", "Hilfinger", "Hug"]
```

#### 3.1.6 [`Array.indexOf`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/indexOf)

The indexOf() method returns the first index at which a given element can be found in the array, or -1 if it is not present.

```javascript
> var professors = ["DeNero", "Hug", "Hug", "Sahai"];
> professors.indexOf("Hug");
1
> professors.indexOf("Hilfinger");
-1
```

#### 3.1.7 [`Array.join`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/join)

The join() method joins all elements of an array into a string, with an optional `separator` parameter.

```javascript
> var professors = ["DeNero", "Hilfinger", "Hug", "Sahai"];
> professors.join();
"DeNeroHilfingerHugSahai"
> professors.join(" and ");
"DeNero and Hilfinger and Hug and Sahai"
```

## 4. Objects

**Objects** in JavaScript are simply collections of properties, where each property has a string **name** (or _key_) and a **value**, which can also be a function or any other value. You can think of these objects as equivalent to Python dictionaries.

>Note: You may be used to using classes to define objects in Python or Java.
>JavaScript has no direct analog for classes, though a "class" declaration was introduced in the latest version of JavaScript (ES2015), it works rather differently than Python or Java classes. We will not be covering ES2015 classes here, but you can read more about them [here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes) if you are interested.

### 4.1 Defining Objects

Objects in JS are defined just like dictionaries in Python, using curly braces and pairs of keys and values:

```javascript
var mustang = {
  make: "Ford",
  model: "Mustang",
  year: 2009,
  isUsed: true,
  makeNoise: function() {
    return "vroom vroom";
  },
};
```

We can further abstract this away by defining a function to create objects for us (a "constructor"):

```javascript
function createCar(make, model, year) {
  return {
    make: make,
    model: model,
    isUsed: year !== 2018,
    makeNoise: function() {
      return "vroom vroom";
    },
  };
}

// call it to make a mustang
var mustang = createCar("Ford", "Mustang", 2009);
```

This is not the only way to create objects in JavaScript, and indeed there is a whole object-oriented paradigm involving something called **Object Prototypes** that attempts to mimic things like classes and inheritance - things you might be used to if you are coming to JavaScript from a Java/Python/C++ background. We will not cover prototypes, but you can [read the MDN documentation on them if you are interested.](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Inheritance_and_the_prototype_chain)

### 4.2 Object Properties

#### 4.2.1 Accessing and Assigning Properties

We can then access object properties in a couple ways:

```javascript
> mustang.year; // dot notation
2009
> mustang["year"]; // like a dictionary - bracket notation
2009
> var key = "year";
> mustang[key]; // bracket notation again
2009
```

We can assign object properties in the same ways:

```javascript
> mustang["topSpeed"]
undefined // uh oh - the object does not have this property!
> mustang["topSpeed"] = 80;
> mustang.topSpeed;
80 // now it does have the property we want.
```

We can even delete properties from objects using the `delete` operator:

```javascript
> delete mustang.topSpeed;
true // property was successfully deleted.
> mustang.topSpeed;
undefined
```

#### 4.2.2 Iterating Over Properties

There are several ways of iterating over all properties of an object. Starting with the latest version of JavaScript (which all modern browsers should support), we can use the `Object.keys(o)` function to iterate over all of the own properties of an object `o`. This function returns an array of all the keys for the own properties of the argument `o`:

```javascript
> Object.keys(mustang);
["make", "model", "year", "isUsed", "makeNoise"]
```

### 4.3 The `this` Pointer

The `this` pointer in JavaScript is a special pointer that we can use inside functions to refer to the enclosing object. For example, suppose we have a function `canDrive` for our car object that returns whether or not the car can drive at that speed:

```javascript
var car = {
  //...
  topSpeed: 130,
  canDrive: function(speed) {
    return speed > this.topSpeed;
  },
};
car.canDrive(150); // --> will return false
car.topSpeed = 200;
car.canDrive(150); // --> will return true
```

In the example, `this` allows a function defined inside the object to access properties of its enclosing object. It is intended for the same use as the `self` pointer in Python.

#### 4.3.1 The Behavior of `this`

The behavior of the `this` pointer in JavaScript is different than most other programming languages. There are 3 cases that determine what value `this` is bound to:

##### 4.3.1.1 The Global Scope

```javascript
this;
```

When using `this` in the global scope, it will refer to what's known as the _global object_, which is typically the `window` object in web browsers.

##### 4.3.1.2 Calling a Function

```javascript
someFunction();
```

The above code may be executed in any context (within another function, in the global scope, in a loop...) and `this` will still refer to the _global object_ when evaluated inside the body of `someFunction`.

##### 4.3.1.3 Calling an Object Property

```javascript
object.someFunction();
```

In this example, `this` will refer to `object` when evaluated inside the body of `object.someFunction`.

> Note: We do not cover object prototypes in this guide, but the `new` operator also changes the behavior of `this` so that
> it refers to the newly created object.

##### Common Pitfalls

The apparently strange behavior of `this` was designed to allow for more flexibility in the language. Unfortunately, it can be confusing to get and even experienced JavaScript programmers will fall into the trap of binding `this` to the wrong thing.

Consider the following code, in which we define a hero character and a function that makes it take damage:

```javascript
var hero = {
  name: "Gandalf",
  health: 500,
  takeDamage: function(dmg) {
    this.health = Math.max(this.health - dmg, 0);
  },
};

var attacks = [100, 150, 250];
attacks.forEach(hero.takeDamage); // <-- doesn't do what we want!
console.log(hero.health);
```

The above code is intended to make `hero` take a total of 100 + 150 + 250 = 500 damage. Instead, it takes no damage whatsoever after executing the code. This is because when we pass in `hero.takeDamage` as an argument to `forEach`, the function is then executed as a regular function (see 4.3.1.2) rather than as an object property (see 4.3.1.3). There are a couple ways to fix this; one way is to change what we pass into `forEach` so that we explicitly call our function as an object property:

```javascript
attacks.forEach(function(dmg) {
  hero.takeDamage(dmg);
});
```

The above works, but is a little verbose. Here's a better way: we can **[bind](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/bind)** `hero.takeDamage` so that whenever `this` is used inside the function body, it will _always_ refer to what we want it to refer to (the `hero` object).

```javascript
attacks.forEach(hero.takeDamage.bind(hero));
```

The above creates a new function that is identical to `hero.takeDamage`, but is **bound** to the `hero` object permanently. So when we pass it as an argument to `forEach`, even though the function gets executed as a regular function, since we've bound its `this` pointer permanently, it will execute as intended.

### 4.4 Comparing Objects

JS Objects are a reference type. This means that two distinct objects are never equal, even if they have the exact same properties. Only comparing the same object reference with itself returns true.

```javascript
// Two variables, two distinct objects with the same properties
var fruit = {name: 'apple'};
var fruitbear = {name: 'apple'};

fruit === fruitbear; // --> false
apple = fruit; // apple refers to the same object as fruit
fruit === apple; // --> true
```

# Part II - Frontend Web Dev Overview

* Review of basic HTML tags
* Document Object Model (DOM)
* Accessing, manipulating DOM using JavaScript
* Classes, IDs as DOM identifiers
* Styling the DOM using CSS
* CSS Box Model
* The `<div>` tag as a universal tag
* DOM Events and JavaScript

## 5. Review of Basic HTML Tags

Last time, we learned some very basic HTML tags. Let's review them.
_Notation: We will use the terms "element" and "tag" interchangeably, but remember
that tags refer to the text that you write in order to specify an HTML element._

### 5.1 Block Elements

HTML elements are either block-level elements or inline-level elements. A block-level element always starts on a new line and takes up the full width available \(stretches out to the left and right as far as it can\).

The following are the most commonly used block-level elements. For a full list of block-level elements, see [here](https://developer.mozilla.org/en-US/docs/Web/HTML/Block-level_elements).

#### 5.1.1 [`<div>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/div)

The `<div>` tag is short for **Content Division** tag. It is the generic container for any content.

Because `<div>` is meant to enclose content, it is specified using an opening tag and a closing tag:

```html
<div>
I am some text inside of a div element. I love divs!
</div>
```

#### 5.1.2 [`<p>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/p)

The `<p>` tag is short for **Paragraph** tag, and is meant to specifically enclose a single paragraph of text.

It is also specified using an opening tag and a closing tag:

```html
<div>
  <p>
  Here is one paragraph inside of a div element. The only time I use paragraph elements is
  when I want to separate text nicely. However that happens a lot when I'm writing text-only websites.
  </p>
  <p>
  Here is another paragraph still inside of the same div element. All browsers will by default separate
  paragraph elements with a little bit of vertical space so they look nice.
  </p>
</div>
```

#### 5.1.3 List elements - [`<ul>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/ul) and [`<ol>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/ul)

The `<ul>` and `<ol>` tags stand for **unordered lists** and **ordered lists**, respectively. The unordered list is rendered as a list of bullet points, while the ordered list is typically rendered as a numbered list by most browsers.

Additionally, each element of the list must be enclosed by its own tag - `<li>`, the **list element** tag. Note that list tags are also block-level elements.

The full list is therefore specified by an opening tag, a collection of list elements, and a closing tag:

```html
<ul>
  <li>Here is some text inside of the first bullet point.</li>
  <li>
    <p>
    Here is a PARAGRAPH of text inside of the second bullet point.
    </p>
    <p>
    Another paragraph also in the second bullet point!! In fact, since list elements are
    just enumerable block-level elements we can add whatever we want inside of them.
    </p>
  </li>
  <li>
    Here is the third bullet point. Nothing special here.
  </li>
</ul>

<p>My top 5 places to eat in Berkeley:</p>
<ol>
  <li>Thai Noodle</li>
  <li>El Burro Picante</li>
  <li>Thai Basil</li>
  <li>Toss</li>
  <li>Shihlin</li>
</ol>
```

#### 5.1.4 [Heading Elements](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/Heading_Elements) - `<h1>` through `<h6>`

The `<h1>`, `<h2>`, `<h3>`, `<h4>`, `<h5>`, and `<h6>` tags are **section heading** tags that can be used as section titles. `<h1>` is the highest section level \(most important\) and `<h6>` is the lowest section level.

```html
<h1>My very important announcement</h1>

<p>
  I have decided that I have had enough of my roommate's hoverboard. He keeps hoverboarding around everywhere. It's really annoying
  and I wish he would stop.
</p>

<h2>My less important addendum</h2>

<p>
  Also, he hasn't watered the plant in like a month and the plant's leaves are starting to turn brown and fall off. This is not quite as important but I really wish he would start watering the plant like he said he would.
</p>
```

### 5.2 Inline Elements

Inline elements do not start on new lines and only take up as much width as necessary.

The following are some of the most commonly used inline elements. See a full list of inline elements [here](https://developer.mozilla.org/en-US/docs/Web/HTML/Inline_elements).

#### 5.2.1 [`<span>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/span)

The `<span>` tag is a generic inline container for text content. Like the `<div>` tag, it does not inherently represent anything.

```html
<p>
  Here is some text with a <span>text enclosed in a span element</span> in the middle of the sentence.
</p>
```

#### 5.2.2 The Anchor Tag - [`<a>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/a)

The `<a>` tag stands for **anchor** tag, and is used to link to other pages, files, locations in the same page, or any URL.

This tag has an opening tag and a closing tag, and encloses the display text of the link. The link itself is specified by the `href` attribute of the tag. The following HTML code creates a link to google.com, where the display text of the link is "Go to google":

```html
<a href="google.com">Click me to go to google!</a>
```

Additionally, the anchor tag is an inline element, so it can be used within a paragraph of text without disrupting the flow of the page:

```html
<p>
  This is a long paragraph of text. My favorite soda is Sprite.
  Did you know that Sprite is manufactured by <a href="http://www.coca-cola.com/global/">Coca-Cola</a>?
  Wow. Coca-Cola makes a ton of great sodas. Too bad the original Coca-Cola soda tastes like garbage.
</p>
```

Moreover, although it is an inline-tag, we can enclose any type of element using anchor tags:

```html
<a href="berkeley.edu">
  <div>
  This entire section is now a link to Berkeley's website. Wow. It's like a button.
  </div>
</a>
```

##### Link Syntax

There are a couple different ways to specify links using the **href** attribute of the anchor tag.

**Absolute links** are basically just the full URL, e.g. `<a href="https://www.google.com/">Go to google!</a>`. These are most useful for linking to other websites.

However, sometimes we just want to link to another page in the same website that we're currently on. For example, on my personal website at [theandrewchan.github.io](https://theandrewchan.github.io/), I have some links to the about page of my website, [theandrewchan.github.io/about](https://theandrewchan.github.io/about/). Since this page is on the same website, I can just specify a **relative link** with `<a href="/about">Go to about page</a>`, where the link starting with a forward slash \(`/`\) indicates that the remainder of the link is _relative to the root of the website_.

#### 5.2.3 The Image Tag - [`<img>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/img)

The `<img>` tag is used to embed images onto the HTML document. **This element does not enclose any content**, so there is no opening and closing tag - only a single tag. The image to be embedded is specified fully by the tag's `src` attribute, which specifies the URL of the image file:

```html
Say hello to my favorite professor:
<img src="https://people.eecs.berkeley.edu/~sahai/sahai.png">
```

## 6. The Document Object Model (DOM)

Earlier, we learned about basic HTML tags and how they can be used to structure a page. Let's now study how those elements
come together to represent a complex page.

### 6.1 A Web Page as a Tree

Consider the following HTML page:

```html
<div>
  <div id="home">
    <a href="/">Home</a>
  </div>
  <div id="about">
    <a href="/about">About</a>
  </div>
  <div id="projects">
    <a href="/projects">Projects</a>
  </div>
</div>
<div>
  <h1> Welcome to my Website!</h1>
  <p>
    This is my website. My name is Dingleberry Dingus. I know, it's a horrible name.
    I was bullied a lot as a child. I made this website to talk about how I went through life with that name.
  </p>
</div>
```

Let's talk about how some elements enclose other elements. Consider the "home" element with attribute id="home": `<div id="home">`. It is enclosed by a single `<div>` element - call this its **parent** - and it encloses a single `<a>` element - call this element its **child**. Notice how any given element can have any number of children but only a single parent.

We can view the above page, and indeed any such HTML page as a single **tree**, where each node is an HTML element, each node's children are the HTML elements enclosed by that node, and each node's parent is the HTML element that contains it.

Where is the root of this tree? It's actually a hidden node with special tag `<html>`. Most pages will actually make this explicit with the tags `<html>` and `<body>`, where the former is the root of the entire page (including various other hidden nodes), and the latter is the root of the nodes actually being displayed:

```html
<html>
  <body>
    <div>
    <!---->
    </div>
    <div>
    <!---->
    </div>
  </body>
</html>
```

Note that if your HTML source code does not contain these tags, they will be added automatically by the browser.

The entire tree is then called the **Document Object Model (DOM)**, where the document is the name of the tree containing objects specifying the page. You can read more about it in the [official documentation](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model/Introduction).

### 6.2 Accessing the DOM using JavaScript

Trees are super useful because they are easy to understand and manipulate programmatically. Indeed, we can access our web page's DOM tree in JavaScript using the special global variable **`document`**, which is provided by every browser and is technically an instance of the [`Document`](https://developer.mozilla.org/en-US/docs/Web/API/Document) object:

```javascript
> document;
document: { ... }
```

However, the `document` variable by itself does not refer to any node in the tree, but rather contains some functions for manipulating the entire tree. We can access individual nodes of the tree using some of these functions.

_**Notation**_: We will be using the following terms throughout:
* **`document`**: Refers to the global variable with functions to manipulate the entire DOM tree.
* **`element`**: An HTML element and an instance of [`Element`](https://developer.mozilla.org/en-US/docs/Web/API/Element). The nodes of the DOM tree will be of this type.
* **`attribute`**: An attribute of an HTML element. Technically attributes are also nodes in the DOM tree, but we will rarely if ever use them as such.

#### 6.2.1 The Root of the DOM - `<body>`

We can access the root element of our page with [`document.body`](https://developer.mozilla.org/en-US/docs/Web/API/Document/body). This returns the special `<body>` tag that acts as the root node of the HTML elements that are actually displayed. As mentioned above, if your HTML source code does not contain this tag, it will be added automatically by the browser.

#### 6.2.2 Element IDs

You may have noticed in the example code from earlier that some HTML elements had an `id` attribute. This attribute is intended to be the **unique identifier** of the HTML element, and it allows us to access that particular HTML element in our JavaScript code using [`document.getElementById`](https://developer.mozilla.org/en-US/docs/DOM/document.getElementById).

Consider the following web page:

```html
<div>
  <div id="home">
    <a href="/">Home</a>
  </div>
  <div id="about">
    <a href="/about">About</a>
  </div>
  <div id="projects">
    <a href="/projects">Projects</a>
  </div>
</div>
```

We can access the element with ID "home" in our JavaScript code:

```javascript
> document.getElementById("home");
<div id="home">...</div>
```

Note that you can set multiple elements to have the same ID in your HTML code, and the browser won't complain (it's still a bad idea!). However, when you call `document.getElementById`, it will only return the first element with that ID.

#### 6.2.3 Element Tags

Sometimes we would like to access all elements of a particular type. We can do this with [`document.getElementsByTagName`](https://developer.mozilla.org/en-US/docs/Web/API/Element/getElementsByTagName), which returns an HTMLCollection (you can treat this as a read-only array) of all elements of the specified tag name.

For instance, we can access all anchor tags in the following web page:

```html
<div>
  <div id="home">
    <a href="/">Home</a>
  </div>
  <div id="about">
    <a href="/about">About</a>
  </div>
  <div id="projects">
    <a href="/projects">Projects</a>
  </div>
</div>
```

With the code:

```javascript
> var links = document.getElementsByTagName("a");
[a, a, a]
> links[0];
<a href="/">Home</a>
```

Additionally, [`Element.getElementsByTagName`](https://developer.mozilla.org/en-US/docs/Web/API/Element/getElementsByTagName) is also a property of any Element object - the difference is that this function will only look in the _children_ (subtree) of the given object:

```javascript
> var home = document.getElementById("home");
> var homeLinks = home.getElementsByTagName("a");
[a]
> homeLinks[0];
<a href="/">Home</a>
```

#### 6.2.4 Element Classes

There is another type of identifier called **class** that we can use to group HTML elements together. Like IDs, classes are specified as attributes of HTML tags in our web page's source code. Returning to our example web page, let's say we want to group together all the `<div>` elements with anchor tags in them. We can add a class attribute "button" to their tags:

```html
<div>
  <div id="home" class="button">
    <a href="/" class="button-link">Home</a>
  </div>
  <div id="about" class="button">
    <a href="/about" class="button-link">About</a>
  </div>
  <div id="projects" class="button">
    <a href="/projects" class="button-link">Projects</a>
  </div>
</div>
```

In fact, we can associate any element with multiple classes by separating each class with a space:

```html
<div class="button centered jumbo">
  This div is associated with classes "button", "centered", "jumbo".
</div>
```

To access all elements of a particular class, use [`document.getElementsByClassName`](https://developer.mozilla.org/en-US/docs/Web/API/Document/getElementsByClassName), which returns an array-like of all elements with the given class names. If multiple class names (separated by a space) are given, only elements that have ALL the class names are returned.

```javascript
> var buttons = document.getElementsByClassName("button");
[div, div, div]
> buttons[0];
<div id="home" class="button">...</div>
```

[`Element.getElementsByClassName`](https://developer.mozilla.org/en-US/docs/Web/API/Element/getElementsByClassName) is also a property of any Element object - this function will only look in the _children_ (subtree) of the given object:

```javascript
> var home = document.getElementById("home");
> var homeLinks = home.getElementsByClassName("button-link");
[a]
> homeLinks[0];
<a href="/">Home</a>
```

#### 6.2.5 Query Selectors

[`document.querySelectorAll`](https://developer.mozilla.org/en-US/docs/Web/API/Document/querySelectorAll) combines the functionality of `getElementById`, `getElementsByTagName`, and `getElementsByClassName` - we can pass in a single string containing the ID that we want, the tag(s) that we want, and the class(es) that we want. This string is given in [CSS Selector Syntax](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Selectors), and the function returns all elements that satisfy these selectors.

#### 6.2.6 Element Children and Parent

We can access and iterate over an element's direct children in the DOM tree using [`Element.childNodes`](https://developer.mozilla.org/en-US/docs/Web/API/Node/childNodes), which returns a list of all the children of an element in the DOM tree. Additionally, we can access an element's parent node using [`Element.parentNode`](https://developer.mozilla.org/en-US/docs/Web/API/Node/parentNode). Note that both of these properties are read-only properties and not functions.

### 6.3 Manipulating the DOM using JavaScript

So far we've seen how to access nodes in the DOM tree. We can also modify, delete, and even add new nodes to the DOM tree!

#### 6.3.1 Modifying DOM Nodes

##### The [`Element.innerHTML`](https://developer.mozilla.org/en-US/docs/Web/API/Element/innerHTML) Property

Every HTML Element has an `innerHTML` property that specifies the content enclosed by that element as a string. We can get or set this property as we please, and even add in arbitrary HTML in the string.

Consider the following page:

```html
<div id="button">
Stanford sux!!!
</div>
```

We can completely replace or add to the content of the div with the following code:

```javascript
> var btn = document.getElementById("button");
> btn.innerHTML;
"Stanford sux!!!"
> btn.innerHTML = btn.innerHTML + "<p>Go bears!!!</p>";
```

The result will look like this:

```html
<div id="button">
Stanford sux!!!
<p>Go bears!!!</p>
</div>
```

This is one - albeit very jank - method of deleting and adding nodes to the DOM! For the most part you should only use this method to edit text content; use other methods to properly delete and add nodes to the DOM.

##### Setting and Getting Element Attributes

We can also get and set the _attributes_ of an HTML element using the following functions:

* [`Element.setAttribute()`](https://developer.mozilla.org/en-US/docs/DOM/element.setAttribute)
* [`Element.getAttribute()`](https://developer.mozilla.org/en-US/docs/DOM/element.getAttribute)

These functions may be useful for e.g. setting the URL of an anchor tag. You can also use them to get and set the class and ID of an element, but we also have easier-to-use properties for that since it is so common:

* [`Element.id`](https://developer.mozilla.org/en-US/docs/Web/API/Element/id)
* [`Element.className`](https://developer.mozilla.org/en-US/docs/Web/API/Element/className)

#### 6.3.2 Adding DOM Nodes

Adding a node to the DOM takes 2 steps:

1. Create the HTML Element to add.
2. Add the HTML Element to the DOM tree in the right place.

We create elements using the [`document.createElement`](https://developer.mozilla.org/en-US/docs/Web/API/Document/createElement) function; this function takes in a string tag name and creates the corresponding element.

To add an element to the DOM, use [`Element.appendChild`] to add an HTML element as a child of a specific node in the DOM tree. As an example, consider the following web page:

```html
<div id="button">
Stanford sux!!!
</div>
```

Here is a better way of adding a paragraph element to the button above:

```javascript
var newParagraph = document.createElement("p");
newParagraph.innerHTML = "Go bears!!!";

var btn = document.getElementById("button");
btn.appendChild(newParagraph);
```

The end result looks like this:

```html
<div id="button">
Stanford sux!!!
<p>Go bears!!!</p>
</div>
```

#### 6.3.3 Deleting DOM Nodes

Deleting nodes is done by the parent of the node being deleted, using the [`Element.removeChild`](https://developer.mozilla.org/en-US/docs/Web/API/Node/removeChild) function, which takes a reference to the element to remove and returns the element again after it has been deleted from the DOM tree.

Let's go back to our example page:

```html
<div id="button">
Stanford sux!!!
</div>
```

The following code will remove the single div above:

```javascript
> var btn = document.getElementById("button");
> document.body.removeChild(btn);
```

If the specified element does not exist in the DOM or is not a child of the parent node, this function will throw an error.

## 7. DOM Events and Interactivity

We want our website to be _interactive_; essentially, we would like our website to respond to inputs from the user. These inputs - clicking buttons, submitting forms, pressing keys, and even scrolling up or down - are turned into **events** by the browser, which our code can then respond to.

### 7.1 Listening to Events

In order to respond to events, we first listen to an element (an _event target_) for specific events and pass in a function that specifies our response to that event.

As an example, let's consider the task of making a button that creates a pop-up window when the user clicks on it. Starting with the following page:

```html
<div id="button">
Click me!
</div>
```

Let's add a listener to the button to listen for a `click` event. We use the [`Element.addEventListener`](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener) function.

```javascript
var btn = document.getElementById("button");
btn.addEventListener("click", function(e) { alert("Hello!"); });
```

Now when the user clicks the button, they will get a pop-up that says "Hello!". In further detail, when the user clicks the button, a `click` event is fired with the `btn` element as an event target; since we added a function as an **event listener**, this function gets called with the [event object](https://developer.mozilla.org/en-US/docs/Web/API/Event) itself as an argument.

#### 7.1.1 Event Bubbling

By default, events will _bubble up_ (propagate up) the DOM tree when they are fired on a given node in the tree. For example, in the following page, if the user clicks on the innermost div, the `click` event will actually fire for all nodes in the tree!

```html
<div id="grandparent">
  <div id="parent">
    <div id="button">
    Click me!
    </div>
  </div>
</div>
```

Sometimes this is useful (for example, if we want a container to do something based on whether an inner element was clicked). Other times, it's not so useful and can even be annoying. For example, suppose we are designing a game:

HTML:
```html
<div id="danger">
  <div id="goal">
    GOAL ZONE CLICK ME
  </div>
  DANGER ZONE DON'T CLICK ME
</div>
```
JavaScript:
```javascript
document.getElementById("goal").addEventListener("click", function(e) { alert("you win!"); });
document.getElementById("danger").addEventListener("click", function(e) { alert("you lose!"); });
```


Say the user loses if they click in the danger zone and they win if they click in the goal zone. However, a `click` event in the goal zone element will result in the a `click` event also firing for the danger zone element. We can prevent this by calling [`Event.stopPropagation`](https://developer.mozilla.org/en-US/docs/Web/API/Event/stopPropagation) on the click event in our event listener:

```javascript
document.getElementById("goal").addEventListener("click", function(e) {
  alert("you win!");
  e.stopPropagation();
});
document.getElementById("danger").addEventListener("click", function(e) { alert("you lose!"); });
```

#### 7.1.2 Input Events

Events are most useful when combined with [input elements](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input). Let's look at the example of a textbox that responds when the user types something and presses enter:

HTML:
```html
<input type="text" id="namebox" />
<div id="response"></div>
```
JavaScript:
```javascript
document.getElementById("namebox").addEventListener("change", function(e) {
  var responseBox = document.getElementById("response");
  responseBox.innerHTML = "You just typed " + e.target.value;
});
```

The relevant code is the last line; we can access the event target (which in this case is the textbox HTML element) with `e.target` and access the input element's value with `e.target.value`.

#### 7.1.3 Event Defaults

Some events have some special default behavior. For example, a `click` event fired on an anchor tag causes the browser to navigate to whatever URL the anchor tag points to. We can override this behavior in our event listeners by calling [`e.preventDefault`](https://developer.mozilla.org/en-US/docs/Web/API/Event/preventDefault), which also has the added behavior of _canceling the entire event_.

#### 7.1.4 Removing Event Listeners

Just as we can add event listeners, we can also remove event listeners using [`Element.removeEventListener`](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/removeEventListener). This event accepts an event type and a reference to the listener function to be removed and removes the event listener if found. Example:

```javascript
var handleBodyClick = function(e) {
  console.log("document body was clicked!");
}
document.body.addEventListener("click", handleBodyClick);
// we decided it was too annoying so now let's remove it.
// remember that we need to keep a reference to the function to remove!
document.body.removeEventListener("click", handleBodyClick);
```

### 7.2 Types of Events

This is just a small selection of the most common events. See the [official documentation](https://developer.mozilla.org/en-US/docs/Web/Events) for more.

#### 7.2.1 Mouse Events

* [`click`](https://developer.mozilla.org/en-US/docs/Web/Events/click) - The user has tapped or clicked on the element.
* [`mouseover`](https://developer.mozilla.org/en-US/docs/Web/Events/mouseover) - The user is hovering over the element or one of its children with the mouse pointer.
* [`mousedown`](https://developer.mozilla.org/en-US/docs/Web/Events/mousedown) - The user has begun pressing down on their mouse while on the element. This is useful for click-and-hold or long-press events.
* [`mouseup`](https://developer.mozilla.org/en-US/docs/Web/Events/mouseup) - The user has released their mouse over the element.

#### 7.2.2 Keyboard Events

* [`keydown`](https://developer.mozilla.org/en-US/docs/Web/Events/keydown) - ANY key is pressed. The `Event` object passed into the callback function will contain the key code.
* [`keyup`](https://developer.mozilla.org/en-US/docs/Web/Events/keyup) - ANY key is released.

#### 7.2.3 Focus Events

* [`focus`](https://developer.mozilla.org/en-US/docs/Web/Events/focus) - The element has received focus from the user. Typically, this means that they have either clicked on it, or, in the case of a text input, have begun typing in it. (does not bubble)
* [`blur`](https://developer.mozilla.org/en-US/docs/Web/Events/blur) - The element has lost focus. (does not bubble)

#### 7.2.4 Misc Events

* [`change`](https://developer.mozilla.org/en-US/docs/Web/Events/change) - Fired for value input events like textboxes whenever the input value changes.
* [`load`](https://developer.mozilla.org/en-US/docs/Web/Reference/Events/load_(ProgressEvent)) - The element has finished loading.


## 8. Communicating with a Backend

Previously, we learned about DOM events and using them to make our website interactive. Now let's make our website into a web application by allowing it to communicate with a server (called the _backend_). There are two ways to do this: the old way using HTML forms and the new way using AJAX (Asynchronous JavaScript).

### 8.1 Review of HTML Forms

For historical context we briefly review forms.

**A bit of history**. Forms used to be the *only* way for a user of a website to communicate with the server. Essentially, they are an HTML-only way to send data to the server. Let's look at an example of a web page that uses forms. Can you guess what the below code does when the user clicks the "submit my info" button?

```html
<form action="example.com/hello" method="POST">
    <input type="text" name="my_name" />
    <button type="submit">submit my info</button>
</form>
```

If you guessed that the web browser would send the contents of the form input elements to the server, you guessed right! In particular, the data that gets sent to the server looks like a dictionary with a single key and value:
```javascript
{ my_name: "<whatever the user inputted into the single text input element>" }
```

Notice that the single key - `my_name` - corresponds exactly to the `name` attribute of the html text input element.

Now, some things stand out to us about the behavior of the web page after the user clicks submit:
* When the user receives the server's response, _the entire web page will reload and interpret the server's response as a new HTML page_! For this reason, when we use `form` elements to send data to the server, the server should always be returning a completely new HTML page, rather than chunks of data, because the web browser has this default behavior of interpreting the response as a new page.
* There is very little we can do to change how the web page sends data to the server. That is, it will by default send data in this prescribed way of sending a dictionary with keys corresponding to the input element's `name` attributes, and values corresponding to the respective input element's values.
* The good thing is that we generally don't need to change this behavior, and in the olden days before web applications (when web sites were literally just HTML) this was all people needed. We still teach the `form` way of doing things because of how simple it is.

### 8.2 Asynchronous JavaScript

Sometime in the mid 2000s, web applications became much more complex, and interactions with the server such as posting comments and receiving notifications in real time became much more common; since hundreds of these interactions could occur in the lifetime of a page, reloading the page for every interaction became unnecessary and infeasible. Instead, web pages used raw HTTP requests to request small chunks of data from web APIs and iteratively modify the page instead of reloading the page for every server interaction. This mode of interaction is historically called **AJAX** ("Asynchronous JavaScript").

#### 8.2.1 Making Asynchronous HTTP Requests

The [**Fetch API**](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch) is present in every modern browser and provides a simple interface to make asynchronous HTTP requests using JavaScript.

##### 8.2.1.1 GET Fetch Requests

Making GET requests is very easy using the Fetch API; here is an example script that gets the weather from the Weather Underground API:

```javascript
fetch("https://api.wunderground.com/api/MY_API_KEY/conditions/q/CA/San_Francisco.json")
  .then(function(response) {
    return response.json();
  })
  .then(function(json) {
    console.log(json.current_observation.weather);
  });
```

Notice the use of `.then(function)` - this is because the fetch API makes use of [promises](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise), which are essentially a cleaner way of adding event listener functions for asynchronous events. We do this because receiving a response to our HTTP request is an asynchronous event; we don't know when or if it will even happen, so the best we can do is listen for the event in the background while the rest of our code continues to execute.

Furthermore, fetch requests do not send authentication data such as cookies by default; in order to include cookies with our request, we must set the request property "credentials" in our second argument:

```javascript
fetch("https://api.wunderground.com/api/MY_API_KEY/conditions/q/CA/San_Francisco.json", {
  credentials: "include"
});
```

##### 8.2.1.2 POST Fetch Requests

Making POST requests requires setting more request properties in our second argument. Here is an example POST request:

```javascript
var postData = {
  username: "dirks"
};
fetch("example.com/hello", {
  method: "POST",
  body: postData,
  headers: { "content-type": "application/json" },
}).then(function(response) {
  return response.json();
}).then(function(json) {
  // ...
  // do whatever we want with the response data
  // ...
})
```

In the interest of replacing clunky forms with fetch requests, here is the same toy example above we made using HTML forms, but using fetch requests instead of forms:

```html
<input type="text" id="name_input" />
<button id="submit_btn">submit my info</button>

<script>
document.getElementById("submit_btn").addEventListener("click", function(e) {
  var textInput = document.getElementById("name_input").value;
  fetch("example.com/hello", {
    method: "POST",
    body: { my_name: textInput },
    headers: { "content-type": "application/json" },
  });
});
</script>
```

Now, the HTML form used to decide everything for us, including:
* What data to send to the server, since forms automatically grab the values of all input elements in between the form tags.
* How to send that data, as forms always send data as an object with keys corresponding to input element name attributes.

We're no longer using forms, so we have to decide these things ourselves. In particular, we have to explicitly grab the value of the input element ourselves, name the HTTP method being used, and set the request body to an object with the key `"my_name"`. This is a bit of extra work we have to do, but in return, we get far more flexibility.

##### 8.2.1.3 Catching Fetch Errors

Occasionally our fetch requests will fail to be fulfilled with a response or will receive an HTTP error, and our response listener will never be called. We can catch these errors easily by simply adding an _error listener_ to the promise:

```javascript
fetch("https://api.wunderground.com/api/MY_API_KEY/conditions/q/CA/San_Francisco.json")
  .then(function(response) {
    return response.json();
  })
  .then(function(json) {
    console.log(json.current_observation.weather);
  })
  .catch(function(error) {
    console.error("Error:", error);
  });
```

Thus using fetch, we can asynchronously do everything that an HTML form can do and more, including send input data and files. [Read the Fetch documentation for more.](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch)
