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
# delayLog and printNumbersInOrder Functions

# Explanation of Code

In the code, `delayLog` is a function that returns a `Promise` which resolves after a specified delay, printing a message when done.

`printNumbersInOrder` calls `delayLog` with different delays in sequence. The `.then()` chaining ensures that each log happens after the previous one finishes.

### Example Breakdown:
- 3 is printed after 1 second.
- 2 is printed after a total of 3 seconds (1 second for 3, 2 seconds for 2).
- 1 is printed after a total of 4 seconds.

</details>

