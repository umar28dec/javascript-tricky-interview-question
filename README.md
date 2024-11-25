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
# Explanation of Code

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
# Explanation of Code

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
# Explanation of Code

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
# Explanation of Code

In the first `setTimeout` loop, the `var i` is used, so the `i` is shared across all the iterations. After the loop finishes, `i` is 3, and all the `setTimeout` functions will refer to the final value of `i`, which is 3.

### How it works:
- The first three `setTimeout` calls will all print `3`, because they all capture the same reference to `i`, which equals `3` after the loop ends.
- The second `setTimeout` prints the final value of `i`, which is also `3` since `i` was incremented to `3` by the loop.
- This happens because `var` has function scope, so the `i` variable is not scoped to each iteration of the loop, and thus all `setTimeout` functions share the same reference to `i`.

As a result, the loop prints `3` multiple times instead of printing `0`, `1`, `2`, and `3` as intended.


</details>