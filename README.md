# javascript-tricky-interview-question
**Question 1**. Predict and Explain the Output of the below JavaScript program. ?.

```javascript
for (var i = 0; i < 5; i++) {
  setTimeout(function() { console.log(i); }, i * 1000 );
}
```
<details><summary><b>Answer</b></summary>

```javascript
5
5
5
5
5
```
It will print 5, five times because callback schedule with setTimeout function, when callback came back til the time other part of code already got executed so loop fails when i = 5 as i is a global variable, because of that it will print 5
</details>

**Question 2**. Predict and Explain the Output of the below JavaScript program. ?.

```javascript
function foo1() {
    return {
       bar: "hello",
    };
 }
   
 function foo2() {
    return
    {
       bar: "hello";
    };
 }
   
 console.log(foo1());
 console.log(foo2());
```
<details><summary><b>Answer</b></summary>

```javascript
{ bar: 'hello' }
undefined
```

</details>


**Question 3**. Predict and Explain the Output of the below JavaScript program. ?.

```javascript
for (let i = 0; i < 5; i++) {
  setTimeout(function() { console.log(i); }, i * 1000 );
}
```
<details><summary><b>Answer</b></summary>

```javascript
0
1
2
3
4
```
</details>


**Question 4**. Predict and Explain the Output of the below JavaScript program. ?.

```javascript
for (cont i = 0; i < 5; i++) {
  setTimeout(function() { console.log(i); }, i * 1000 );
}
```
<details><summary><b>Answer</b></summary>

```javascript
TypeError: Assignment to constant variable.
```
</details>

**Question 5**. Predict and Explain the Output of the below JavaScript program. ?.

```javascript
function delayLog(message, delay) {
  return new Promise((resolve) => {
    setTimeout(() => {
      resolve(message);
    }, delay);
  });
}

async function printNumbersInOrder() {
  console.log(await delayLog(1, 1000));
  console.log(await delayLog(2, 2000));
  console.log(await delayLog(3, 1000));
}

printNumbersInOrder();

```
<details><summary><b>Answer</b></summary>

```javascript
1
2
3
```
# delayLog and printNumbersInOrder Functions

## Overview
The `delayLog` function returns a `Promise` that resolves with the given message after a specified delay using `setTimeout`.

The `printNumbersInOrder` function is `async`, which means it can use the `await` keyword to wait for each `Promise` to resolve before proceeding to the next line.

## Sequence
1. `await delayLog(1, 1000)` - waits 1 second, then prints `1`.
2. `await delayLog(2, 2000)` - waits 2 seconds, then prints `2`.
3. `await delayLog(3, 1000)` - waits 1 second, then prints `3`.

The `await` ensures that each `console.log` happens only after the previous `delayLog` has resolved, so the numbers are printed sequentially in the order `1, 2, 3` despite different delays.

</details>


**Question 6**. Predict and Explain the Output of the below JavaScript program. ?.

```javascript
function delayLog(message, delay) {
  return new Promise((resolve) => {
    setTimeout(() => {
      console.log(message);
      resolve();
    }, delay);
  });
}

function printNumbersInOrder() {
  delayLog(3, 1000)
    .then(() => delayLog(2, 2000))
    .then(() => delayLog(1, 1000));
}
printNumbersInOrder();

```
<details><summary><b>Answer</b></summary>

```javascript
3 (after 1 second)
2 (after 3 seconds)
1 (after 4 seconds)
```
## Explanation of Code

In the code, `delayLog` is a function that returns a `Promise` which resolves after a specified delay, printing a message when done.

`printNumbersInOrder` calls `delayLog` with different delays in sequence. The `.then()` chaining ensures that each log happens after the previous one finishes.

### Example Breakdown:
- 3 is printed after 1 second.
- 2 is printed after a total of 3 seconds (1 second for 3, 2 seconds for 2).
- 1 is printed after a total of 4 seconds.

</details>

**Question 7**. Predict and Explain the Output of the below JavaScript program. ?.

```javascript
function delayLog(message, delay, callback) {
  setTimeout(() => {
    console.log(message);
    callback();
  }, delay);
}

function printNumbersInOrder() {
  delayLog(3, 1000, () => {
    delayLog(2, 2000, () => {
      delayLog(1, 1000, () => {});
    });
  });
}

printNumbersInOrder();

```
<details><summary><b>Answer</b></summary>

```javascript
3 (after 1 second)
2 (after 3 seconds)
1 (after 4 seconds)
```
## Explanation of Code

### `delayLog(message, delay, callback)`
- Takes a `message`, a `delay`, and a `callback` function.
- After the specified `delay`, it logs the `message` and calls the `callback` to continue the sequence.

### `printNumbersInOrder()`
- Calls `delayLog` with the number `3` after a delay of 1 second.
- When `3` is printed, it triggers the callback to call `delayLog` for `2` after 2 seconds.
- When `2` is printed, it triggers the callback to call `delayLog` for `1` after a delay of 1 second.

This ensures the numbers are printed in the desired order with the corresponding delays between each print.

</details>

**Question 8**. Predict and Explain the Output of the below JavaScript program. ?.

```javascript
for (let i = 0; i < 5; i++) {
  setTimeout(function() { console.log(i); }, i * 1000);
}

```
<details><summary><b>Answer</b></summary>

```javascript
0 1 2 3 4

```
## Explanation of Code

In this case, the variable `i` is declared using `let`, which has **block scope**. This means that a new `i` is created for each iteration of the loop, preserving its value inside the `setTimeout` closure.

### How it works:
- During each iteration, the `setTimeout` is scheduled to log the current value of `i` after the respective delay (`i * 1000`).
- Since `let` creates a new scoped variable for each iteration, each `setTimeout` function captures the current value of `i` at that point in time.
- This ensures that each `setTimeout` prints the correct value of `i` based on its iteration.

As a result, the numbers from 0 to 4 will be logged, each with a respective delay.

</details>

**Question 9**. Predict and Explain the Output of the below JavaScript program. ?.

```javascript

for (var i = 0; i < 3; i++) {
  setTimeout(function () {
    console.log(i);
  }, i * 1000);
}

setTimeout(function () {
  console.log("Last:", i);
}, 2000);


```
<details><summary><b>Answer</b></summary>

```javascript
3
3
3
Last: 3

```
## Explanation of Code

In the first `setTimeout` loop, the `var i` is used, so the `i` is shared across all the iterations. After the loop finishes, `i` is 3, and all the `setTimeout` functions will refer to the final value of `i`, which is 3.

### How it works:
- The first three `setTimeout` calls will all print `3`, because they all capture the same reference to `i`, which equals `3` after the loop ends.
- The second `setTimeout` prints the final value of `i`, which is also `3` since `i` was incremented to `3` by the loop.
- This happens because `var` has function scope, so the `i` variable is not scoped to each iteration of the loop, and thus all `setTimeout` functions share the same reference to `i`.

As a result, the loop prints `3` multiple times instead of printing `0`, `1`, `2`, and `3` as intended.


</details>

**Question 10**. Predict and Explain the Output of the below JavaScript program. ?.

```javascript

const promise = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve("Success");
  }, 1000);
});

promise
  .then((result) => console.log(result))
  .then((result) => console.log(result))
  .catch((error) => console.error(error));


```
<details><summary><b>Answer</b></summary>

```javascript
Success
undefined

```
## Explanation of .then() Behavior

In this example, we have two `.then()` methods chained to a promise. Here's the breakdown of how each `.then()` behaves:

1. **First `.then()`**: 
    - Logs `"Success"` because the promise is resolved with that value.
    
2. **Second `.then()`**: 
    - Logs `undefined` because the first `.then()` doesn't explicitly return a value. By default, `undefined` is passed to the second `.then()`.

</details>

**Question 15**. Predict and Explain the Output of the below JavaScript program. ?.

```javascript

const promise = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve("Success");
  }, 1000);
});

promise
  .then((result) => {
    return result;
  })
  .then((result) => {
    console.log(result);
  })
  .then((result) => {
    console.log("Success");
    return result;
  })
  .catch((error) => console.error(error));



```
<details><summary><b>Answer</b></summary>

```javascript

Success
Success


```
In this example, we demonstrate the behavior of promise chaining with `.then()` and `.catch()`. Here's the breakdown of each step:

1. **Promise resolves with "Success"**: 
    - The promise is resolved with the value `"Success"`.

2. **First `.then()`**: 
    - Returns `"Success"`, passing the value to the next `.then()`.

3. **Second `.then()`**: 
    - Logs `"Success"` as the value passed from the first `.then()`.

4. **Third `.then()`**: 
    - Logs `"Success"` again and returns the same value.

Since there are no errors in this chain, the `.catch()` block is not triggered.
</details>




**Question 19**. Predict and Explain the Output of the below JavaScript program. ?.

```javascript

for (var i = 0; i < 4; i++) {
  setTimeout(function () {
    console.log(i);
  }, i * 1000);
}

setTimeout(function () {
  console.log("Last:", i);
}, 2000);


```
<details><summary><b>Answer</b></summary>

```javascript

4
4
4
Last: 4

```
## Explanation of Code

The `for` loop runs from `i = 0` to `i = 3`, and it schedules four `setTimeout` functions with different delays:

- `i = 0`: Schedules `setTimeout(function () { console.log(i); }, 0 * 1000)` → Executes after 0ms.
- `i = 1`: Schedules `setTimeout(function () { console.log(i); }, 1 * 1000)` → Executes after 1000ms (1 second).
- `i = 2`: Schedules `setTimeout(function () { console.log(i); }, 2 * 1000)` → Executes after 2000ms (2 seconds).
- `i = 3`: Schedules `setTimeout(function () { console.log(i); }, 3 * 1000)` → Executes after 3000ms (3 seconds).

### Important Point:
- The loop runs immediately and quickly, scheduling the `setTimeout` functions without waiting for them to execute.
- By the time any of the `setTimeout` functions execute, the loop has already completed, so the value of `i` will be `4` when the callbacks run.
- The `setTimeout` functions are scheduled to run after the specified delays, but due to how JavaScript's event loop works, all the `setTimeout` callbacks will be executed after the event loop finishes processing the synchronous code (like the loop).
- By the time these callbacks run, the value of `i` has already been incremented to `4` (because `i` was incremented four times during the loop).

As a result, when the `setTimeout` callbacks execute, the value of `i` is logged as `4` for each of the scheduled functions.

### Final Log:
- All `setTimeout` callbacks will log `4` because the loop finishes executing before any of the `setTimeout` functions run, and the value of `i` is `4` at that point.

</details>

**Question 20**. Predict and Explain the Output of the below JavaScript program. ?.

```javascript

const promise = new Promise((resolve, reject) => {
  setTimeout(() => {
    reject("Error");
  }, 1000);
});

promise
  .then((result) => {
    return result;
  })
  .then((result) => {
    console.log(result);
  })
  .then((result) => {
    return result;
  })
  .catch((error) => console.log(error))
  .catch((error) => console.log(error));


```
<details><summary><b>Answer</b></summary>

```javascript

Error

```
## Explanation of Promise Rejection and `.catch()` Behavior

In the provided code, only one `"Error"` is printed because only the first `.catch()` is executed. Here's the breakdown:

1. **Promise rejection**: 
    - The promise is rejected with the message `"Error"` after 1 second.

2. **First `.then()`**: 
    - This does not execute because the promise is rejected, so it skips to the `.catch()` block.

3. **First `.catch()`**: 
    - This catches the rejection and logs `"Error"`.

4. **Second `.catch()`**: 
    - The second `.catch()` is **not triggered** because once an error is handled by a `.catch()`, the error is considered "consumed," and the subsequent `.catch()` won't handle the same error again.

</details>