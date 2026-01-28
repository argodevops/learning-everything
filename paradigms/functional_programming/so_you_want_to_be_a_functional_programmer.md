# How do I become a Functional Programmer?
In Short forget everything you've learned in Imperative programming (like procedural (Assembly, C) and OOP (Java, C#)) and embrace the wackiness of Declarative programming. Functional programming is the highest form of programming in terms of purity for the average Joe.
![Programmer Evolution Image](https://miro.medium.com/v2/resize:fit:1400/1*AM83LP9sGGjIul3c5hIsWg.png)

## Concepts

### Purity
Pure functions are very simple functions. They only operate on their input parameters. Take this for example:
```javascript
var z = 10;
function add(x, y) {
    return x + y;
}
```
Notice that the add function does NOT touch the z variable. It doesn't read from z and it doesn't write to z. It only reads x and y, its inputs, and returns the result of adding them together.

That’s a pure function. If the add function did access z, it would no longer be pure.

Here’s another function to consider:
```javascript
function justTen() {
    return 10;
}
```
If the function, justTen, is pure, then it can only return a constant. Why?

Because we haven’t given it any inputs. And since, to be pure, it cannot access anything other than its own inputs, the only thing it can return is a constant.

Since pure functions that take no parameters do no work, they aren't very useful. It would be better if justTen was defined as a constant.

> Most useful Pure Functions must take at least one parameter.

Consider this function:
```javascript
function addNoReturn(x, y) {
    var z = x + y
}
```
Notice how this function doesn't return anything. It adds x and y and puts it into a variable z but doesn't return it.

> All useful Pure Functions must return something.

```javascript
function add(x, y) {
    return x + y;
}
console.log(add(1, 2)); // prints 3
console.log(add(1, 2)); // still prints 3
console.log(add(1, 2)); // WILL ALWAYS print 3
```
> Pure Functions will always produce the same output given the same inputs.

Since Pure Functions cannot change any external variables, all other functions are said to be *impure*. 
All of these functions will have **Side Effects** when called. Therefore you can never predict what these functions will return. Since we are modifying the state of the machine and will then cause non deterministic outcomes dependent on execution sequence of the code.

> Pure Functions have no side effects.

So **"HOW THE HELL DO I DO ANYTHING WITH ONLY PURE FUNCTIONS?!"**

At some point we must interact with the real world, therefore some parts of every program must be impure. The goal is to minimize the amount of impure code and segregate it from the rest of our program.

### Immutability
Consider this code
```javascript
var x = 1;
x = x + 1;
```

In functional programming, x = x + 1 is illegal, there are only constants, a value that is set cannot be changed.

> There are no variables in Functional Programming

```javascript
const addOneToSum = (y,z) => {
  const x = 1;
  return x + y + z;
}
```
the constant x only persists in the scope of the function. i.e. when the function gets run again it is reset.

So **"HOW THE HELL AM I SUPPOSED TO DO ANYTHING WITHOUT VARIABLES?!"**

Let's think about when we want to modify variables. There are 2 general cases that come to mind: multi-valued changes (e.g. changing a single value of an object or record) and single-valued changes (e.g. loop counters).

Functional Programming deals with changes to values in a record by making a copy of the record with the values changed. It does this efficiently without having to copy all parts of the record by using data structures that makes this possible.

Functional programming solves the single-valued change in exactly the same way, by making a copy of it.

and of course by **not** having loops.

So **"WHAT NO VARIABLES AND NOW NO LOOPS?!!"**

> Functional Programming uses recursion instead of loops.

Consider this code
```javascript
// simple loop construct
var acc = 0;
for (var i = 1; i <= 10; ++i)
    acc += i;
console.log(acc); // prints 55
// without loop construct or variables (recursion)
function sumRange(start, end, acc) {
    if (start > end)
        return acc;
    return sumRange(start + 1, end, acc + start)
}
console.log(sumRange(1, 10, 0)); // prints 55
```

Notice how recursion, the functional approach, accomplishes the same as the for loop by calling itself with a new start (start + 1) and a new accumulator (acc + start). It doesn’t modify the old values. Instead it uses new values calculated from the old.

Unfortunately, this is hard to see in JavaScript even if you spend a little time studying it, you’re probably not used to thinking recursively.

One of the downsides to recursion is that it gets added to the stack. And assuming you don't have infinite memory you will end up filling the stack and halting the program. This is the cause for Functional Programming being inefficient at enumerating things.

Here are the recursion limits for each browser from 2019:

- Internet Explorer 11: 12,065
- Firefox 65: 20,614
- Chrome 72: 9,643
- Opera 57: 9,638
- Safari 12: 32,035

### Higher-Order Functions

> In Functional Programming, a function is a first-class citizen of the language. In other words, a function is just another value.

Since functions are just values, we can pass them as parameters. Consider this following code with *parseFunc* as a passed in function:
```javascript
function validateValueWithFunc(value, parseFunc, type) {
    if (parseFunc(value))
        console.log('Invalid ' + type);
    else
        console.log('Valid ' + type);
}
```
Therefore our function is called a Higher-order Function. 

> Higher-order Functions either take functions as parameters, return functions or both.

### Closures
When a function is created, all of the variables in its scope at the time of creation are accessible to it for the lifetime of the function. A function exists as long as there still a reference to it. For example, child’s scope exists as long as childFunc still references it.

> A closure is a function's scope that's kept alive by a reference to that function.

![Functional Programming Image](https://static.packt-cdn.com/products/9781788996648/graphics/assets/758bfc09-08e9-4d4c-b9aa-bfecf25dd5e8.png)
