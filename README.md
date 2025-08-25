This repository aims to add more JavaScript interview questions and answers.

## 📋 Table of Contents

| No. | Section / Question                                                                                                                                   |
| --- | ---------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1.  | [What is the difference between primitive and non-premitive data types](#premitive-and-non-premitive-data-types)                                     |
| 2.  | [What is Heap in javascript](#what-is-heap-in-javascript)                                                                                            |
| 3.  | [What is call stack in javascript](#What-is-call-stack-in-javascript)                                                                                |
| 4.  | [What is call back queue in javascript](#what-is-call-back-queue-in-javascript)                                                                      |
| 5.  | [What is Event Loop](#what-is-event-loop)                                                                                                            |
| 6.  | [What is lexical scope in javascript](#what-is-lexical-scope)                                                                                        |
| 7.  | [What is Debounce](#what-is-debounce)                                                                                                                |
| 8.  | [Write a function sum that can be called like sum(1)(2)(3)...() and returns the total](#infinite-currying)                                           |
| 9.  | [What Are Closures in JavaScript](#what-are-closures-in-javaScript)                                                                                  |
| 10. | [Explain why setTimeout printing 3 times inside a loop](#explain-why-setTimeout-printing-3-times-inside-a-loop)                                      |
| 11. | [ Types of Type Coercion](#types-of-coercion)                                                                                                        |
| 12. | [Write a function to flatten multidimensional/nested array into single array](#Write-a-function-to-flatten-multidimensional-array-into-single-array) |
| 13. | [Write a function group by on an array of objects](#write-a-function-group-by-on-an-array-of-objects)                                                |
| 14. | [Write a polyfill of map function](#write-a-polyfill-of-map-function)                                                                                |
| 15. | [Write a polyfill of filter function](#write-a-polyfill-of-filter-function)                                                                          |
| 16. | [What is Recursion in JavaScript?](#wWhat-is-recursion-in-javaScript)                                                                                |
| 17. | [Reverse a String Recursively](#reverse-a-string-recursively)                                                                                        |
| 18. | [Write a function to count each charter](#write-a-function-to-count-each-charter)                                                                    |
| 19. | [Write a palindrome function without using built in function](#write-a-function-to-check-given-string-is-a-palindrome-without-inbuilt-in-function)   |
| 20. | [](#)                                                                                                                                                |

1. ## Premitive and non premitive data types

### Primitive Data Types

These are basic and immutable data types. They store single values, not collections or complex objects.

**Characteristics**

1. Stored by value
2. Immutable (can’t be changed directly)
3. Compared by value

```javascript
// Primitive Example
let x = 5;
let y = x;
y = 10;

console.log(x); // 5 (original x is unchanged)
```

---

## Non-Primitive (Reference) Data Types

These are complex data types used to store collections or objects.

**Characteristics:**

1. Stored by reference
2. Mutable (can be changed)
3. Compared by reference (not by content)

```javascript
// Non-Primitive Example
let obj1 = { name: "Alice" };
let obj2 = obj1;
obj2.name = "Bob";

console.log(obj1.name); // "Bob" (obj1 changed because obj2 references the same object)
```

2. ## What is Heap in javascript
   Heap is an unstrutured memory that is used for memory allocation of the variables and the objects.
3. ## What is call stack in javascript

   The call stack is a data structure that keeps track of the function execution order. Functions are pushed onto the stack when called and popped when completed.

   ```javascript
   function greet() {
     console.log("Hello");
   }
   function main() {
     greet();
     console.log("World");
   }
   main();
   ```

4. ## What is call back queue in javascript
   The callback queue is a data struture.the callback queue stores all the callback functions in the order in which they are added.

```javascript
console.log("Start");

setTimeout(() => {
  console.log("Timeout callback");
}, 0);

console.log("End");
// Start
// End
// Timeout callback
```

Even though the timeout is 0ms, the callback waits until the call stack is empty before being executed.

5. ## What is Event Loop

The event loop monitors the call stack and callback queue. If the stack is empty, it pushes the first callback from the queue into the stack.

**Example:**

```javascript
console.log("Script start");

setTimeout(() => {
  console.log("Inside setTimeout");
}, 0);

Promise.resolve().then(() => {
  console.log("Inside Promise");
});

console.log("Script end");
```

**output:**

```bash
Script start
Script end
Inside Promise
Inside setTimeout
```

**Notes:**
Microtasks `(Promises)` are handled before macrotasks `(setTimeout)`.

**[⬆ Back to Top](#-table-of-contents)**

6. ## What is lexical scope

Lexical scope means a function’s scope is defined by where the function is written in the code. It determines what variables are accessible to the function based on its position in the source code.

```javascript
function outer() {
  let outerVar = "I'm from outer";

  function inner() {
    console.log(outerVar); // inner can access outerVar
  }

  inner();
}

outer();
```

`inner() has lexical access to outerVar because it is defined inside the outer() function.
The scope is based on the nesting structure of functions when the code is written.`

**[⬆ Back to Top](#-table-of-contents)**

7. ## What is debounce

Debouncing forces a function to wait a certain amount of time before run again.

```javascript
function debounce(func, delay) {
  let timeoutId;
  return function (...args) {
    clearTimeout(timeoutId);
    timeoutId = setTimeout(() => func.apply(this, args), delay);
  };
}
```

**[⬆ Back to Top](#-table-of-contents)**

8. ## Infinite Currying

```javascript
function add(a) {
  return function (b) {
    if (b !== undefined) {
      return add(a + b); // Keep accumulating
    } else {
      return a; // Final result
    }
  };
}

console.log(add(1)(2)(3)(4)()); // 10
```

`You keep calling add(n), and it keeps returning a new function. The addition happens when you finally call it with no argument (()).`

**[⬆ Back to Top](#-table-of-contents)**

9.  ## What Are Closures in JavaScript?

    A closure is a function that remembers the variables from its lexical scope even when that function is executed outside of that scope.

```javascript
function outer() {
  let counter = 0; // `counter` is in the outer scope

  function inner() {
    counter++;
    console.log(counter);
  }

  return inner;
}

const myClosure = outer(); // `outer` returns `inner`, but `counter` still exists
myClosure(); // 1
myClosure(); // 2
myClosure(); // 3
```

1. outer() runs and returns inner().
2. inner() remembers the counter variable even though outer() has finished.
3. This is a closure.

**Why Use Closures?**

1. Data privacy (e.g., private variables).
2. Stateful functions (like counters).
3. actory functions that create customized behaviors.

**What is a closure in JavaScript and where would you use it?**
A closure is a function that has access to its outer function’s variables even after the outer function has returned. Closures are useful for creating private variables and encapsulating state.

**[⬆ Back to Top](#-table-of-contents)**

10. ## Explain why setTimeout printing 3 times inside a loop

```javascript
for (var i = 0; i < 3; i++) {
  setTimeout(() => {
    console.log(i);
  }, 0);
}
```

**what is happening:**
You are using a for loop with var, and inside each iteration, you're setting a setTimeout with a delay of `0` milliseconds to print `i`.
**Key concept:**

1. var is function-scoped – meaning the variable i is shared across all iterations of the loop, not block-scoped like let.
2. setTimeout is asynchronous – it queues the callback to run after the current execution stack (the loop) finishes.
3. The loop completes before the setTimeout callbacks execute – by the time setTimeout runs, i has already reached 3.
   **Execution Flow:**
   `Step 1:` Loop starts, i = 0, schedules setTimeout to print i.
   `Step 2:` i = 1, schedules another setTimeout.
   `Step 3:` i = 2, schedules another setTimeout.
   `Step 4:` Loop ends, i = 3.
   `Step 5:` Now the JavaScript event loop processes the 3 scheduled setTimeout callbacks.
   `Step 6:` Each callback accesses the same i, which is now 3.

   **How to Fix It:**
   Use let instead of var, so each iteration gets a new block-scoped i.
   or Using IIFE(Immediately Invoked Function Expression)

   ```javascript
   for (let i = 0; i < 3; i++) {
     setTimeout(() => {
       console.log(i);
     }, 0);
   }
   // using IFFE
   for (var i = 0; i < 3; i++) {
     (function (j) {
       setTimeout(() => {
         console.log(j);
       }, 0);
     })(i);
   }
   ```

   **[⬆ Back to Top](#-table-of-contents)**

## Types of Type Coercion

There are two types of coercion in JavaScript:

**Implicit Coercion**
JavaScript automatically converts data types when needed.

**Explicit Coercion**
You manually convert data types using functions or operators.

**Implicit Coercion (Automatic)**
JavaScript automatically converts types when using operators like +, ==, etc.

```javascript
"5" + 1; // '51'   -> number 1 is coerced to string
"5" - 1; // 4      -> string '5' is coerced to number
true + 1; // 2      -> true becomes 1
false == 0; // true   -> false is coerced to 0
null == undefined; // true -> loose equality comparison
```

**Explicit Coercion (Manual)**
You convert values on purpose using functions like Number(), String(), Boolean().

```javascript
Number("123"); // 123
String(123); // '123'
Boolean(0); // false
Boolean("hello"); // true
parseInt("42px"); // 42
```

**[⬆ Back to Top](#-table-of-contents)**

12. ## Write a function to flatten multidimensional array into single array

```javascript
function flattenArray(arr) {
  const result = [];

  for (let item of arr) {
    if (Array.isArray(item)) {
      result.push(...flattenArray(item)); // Recursively flatten
    } else {
      result.push(item);
    }
  }

  return result;
}

// Example usage:
const nested = [1, [2, [3, 4], 5], 6];
console.log(flattenArray(nested)); // Output: [1, 2, 3, 4, 5, 6]
```

**[⬆ Back to Top](#-table-of-contents)**

13. ## Write a function group by on an array of objects

```javascript
const users = [
  {
    name: "Jim",
    color: "blue",
  },
  {
    name: "Sam",
    color: "blue",
  },
  {
    name: "Eddie",
    color: "green",
  },
  {
    name: "Robert",
    color: "green",
  },
];
const groupBy = (arr, key) => {
  const initialValue = {};
  return arr.reduce((acc, cval) => {
    const myAttribute = cval[key];
    acc[myAttribute] = [...(acc[myAttribute] || []), cval];
    return acc;
  }, initialValue);
};

const res = groupBy(users, "color");
console.log("group by:", res);
```

**[⬆ Back to Top](#-table-of-contents)**

14. ## Write a polyfill of map function

```javascript
Array.prototype.myMap = function (callbackFun) {
  let newArray = [];
  for (let i = 0; i < this.length; i++) {
    newArray.push(callbackFun(this[i], i, this));
  }
  return newArray;
};
let arr = [10, 20, 30];
let newArr = arr.myMap((x) => {
  return x * 2;
});
console.log(newArr);
// output : [ 20, 40, 60 ]
```

**[⬆ Back to Top](#-table-of-contents)**

15. ## Write a polyfill of filter function

```javascript
Array.prototype.myFilter = function (callbackFun) {
  let newArray = [];
  for (let i = 0; i < this.length; i++) {
    if (callbackFun(this[i], i, this)) {
      newArray.push(this[i]);
    }
  }
  return newArray;
};
let arr = [10, 15, 30];

let newArr = arr.myFilter((x) => {
  return x % 10 == 0;
});
console.log(newArr);
// Output:  [10 , 30]
```

**[⬆ Back to Top](#-table-of-contents)**

16. ## What is Recursion in JavaScript?
    **Recursion** is a programming concept where a function calls itself directly or indirectly in order to solve a problem. Each recursive call should bring the problem closer to a base case, which is the condition that stops the recursion.

```javascript
function factorial(n) {
  if (n === 0 || n === 1) return 1; // base case
  return n * factorial(n - 1); // recursive call
}

console.log(factorial(5)); // Output: 120
```

**[⬆ Back to Top](#-table-of-contents)**

17. ## Reverse a String Recursively

```javascript
function reverseString(str) {
  if (str === "") return "";
  return reverseString(str.slice(1)) + str[0];
}

console.log(reverseString("hello")); // Output: "olleh"
```

**[⬆ Back to Top](#-table-of-contents)**

18. ## Write a function to count each charter

```javascript
function countChar(str) {
  const obj = {};
  for (let x of str) {
    if (obj[x]) {
      obj[x] += 1;
    } else {
      obj[x] = 1;
    }
  }
  return obj;
}
```

19. ## Convert array into object

```javascript
obj = arr.reduce((ac, iterate, i) => ({ ...ac, [i]: iterate }), {});
```

19. ## // validate value is a valid positive integer, otherwise through correct error

```javascript
function validateInput(value) {
  if (typeof value === "number" && Number.isInteger(value) && value > 0) {
    return "Postive number";
  } else {
    throw new Error("not valid number");
  }
}
try {
  validateInput(10);
} catch (error) {
  console.error("Validation error:", error.message);
}
```

20. ## write a function to check given string is a palindrome without inbuilt in function

```javascript
function isPalindrome(str) {
  let len = str.length;

  for (let i = 0; i < len / 2; i++) {
    if (str[i] !== str[len - 1 - i]) {
      console.log("String is not palindrome");
      return false;
    }
  }
  console.log("String is palindrome");
  return true;
}
```
