## 📋 Table of Contents

| No. | Section / Question                                                              |
| --- | ------------------------------------------------------------------------------- |
| 1.  | [Waht is Heap in javascript](#what-is-heap-in-javascript)                       |
| 2.  | [What is call stack in javascript](#What-is-call-stack-in-javascript)           |
| 3.  | [What is call back queue in javascript](#what-is-call-back-queue-in-javascript) |
| 4.  | [What is Event Loop](#what-is-event-loop)                                       |
| 5.  | [Screenshots](#screenshots)                                                     |
| 6.  | [API Reference](#api-reference)                                                 |
| 7.  | [FAQ](#faq)                                                                     |
| 8.  | [Contributing](#contributing)                                                   |
| 9.  | [License](#license)                                                             |
| 10. | [Contact](#contact)                                                             |

## What is Heap in javascript

## What is call stack in javascript

## What is call back queue in javascript

## What is Event Loop

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

**Notes:**
Microtasks `(Promises)` are handled before macrotasks `(setTimeout)`.
```
