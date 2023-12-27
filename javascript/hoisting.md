### Hoisting

> javascript is then **interpreter language** which is not needed other compile works.
> 
> Runtime is the point at which the source code is executed line by line sequentially.

```javascript
console.log(score) // undefined

var score;
```

this code seems to trigger a ReferenceError because JavaScript is an interpreted language.

However, That's not the actual issue. Initially, the variable 'score' is undefined. 

This occurs because variable declarations in JavaScript are hoisted and processed just before **runtime**.

The JavaScript engine undergoes an evaluation process, preparing and organizing code execution right before runtime.

The evaluation process initially executes all declarations in the code. 
This results in variable hoisting in JavaScript. 
