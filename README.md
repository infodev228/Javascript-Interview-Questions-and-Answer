## 📋 Table of Contents

| No. | Section / Question                                                                                               |
| --- | ---------------------------------------------------------------------------------------------------------------- |
| 1.  | [What is the difference between primitive and non-premitive data types](#premitive-and-non-premitive-data-types) |
| 2.  | [Waht is Heap in javascript](#what-is-heap-in-javascript)                                                        |
| 3.  | [What is call stack in javascript](#What-is-call-stack-in-javascript)                                            |
| 4.  | [What is call back queue in javascript](#what-is-call-back-queue-in-javascript)                                  |
| 5.  | [What is Event Loop](#what-is-event-loop)                                                                        |
| 6.  | [What is lexical scope in javascript](#what-is-lexical-scope)                                                    |
| 7.  | [What is Debounce](#what-is-debounce)                                                                            |
| 8.  | [Write a function sum that can be called like sum(1)(2)(3)...() and returns the total](#infinite-currying)       |
| 9.  | [What Are Closures in JavaScript](#what-are-closures-in-javaScript)                                              |
| 10. | [Contact](#contact)                                                                                              |

## Premitive and non premitive data types

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

1. ## What is call stack in javascript

2. ## What is call back queue in javascript

3. ## What is Event Loop

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

4. ## What is lexical scope

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

5. ## What is debounce

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

6. ## Infinite Currying

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

7.  ## What Are Closures in JavaScript?

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

1. ##
