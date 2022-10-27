# javascript-tricky-interview-question
## Question 1. Predict and Explain the Output of the below JavaScript program. ?.

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

## Question 2. Predict and Explain the Output of the below JavaScript program. ?.

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


## Question 10. Predict and Explain the Output of the below JavaScript program. ?.

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



## Question 19. Predict and Explain the Output of the below JavaScript program. ?.

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