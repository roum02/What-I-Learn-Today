### Assignment

```javascript
var score;
score = 80;

var score = 80;
```

The JavaScript engine executes a two-step progress: the first step is Declaration, and the second is Assignment
even though it appears as only one sentence.

the timing of variable declaration and Assignment differs. 
variable declarations are progressed before runtime, whereas value assignments occur during runtime.

> also you can view the details [here](variable-declaration.md)

Please see the Image below.

![img.png](img.png)

when the variable is reassigned, from 'undefined' to the number 80, 
the old value, 'undefined' is not immediately deleted but remains in memory for a time.

Meanwhile, the new value, the number 80 is allocated to a new location in memory.