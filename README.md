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
It will print 5, five times because callback schedule with setTimeout function, when callback came back til the time other part of code already got executed so loop fails when i = 5, because of that it will print 5
</details>