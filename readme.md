# Important

- dynamically typed variables
- some things will return things like NaN, undefined, or null instead of causing an error that stops the code
- == and != will do a type conversion if you are comparing different types, which can cause tricky bugs with the above feature
- as the expression in a condition, the following values are false: **false**, **0**, **""** (empty string), **null**, **undefined**, **NaN** (not a number)
- === and !== to do proper comparisons to avoid this problem
- statments are ended with a semicolon, but they are sort of not required (safer to put them for clarity)
  - if you don't have a semicolon at the end of a line, the interpreter will try to put one there if it makes valid syntax

# Data Types and Variables

variables can be declared as
- **var** (gets *hoisted* so it can actually be used before where it is declared)
- **let**
- **const** (can't be changed)

## numbers

- there is no separate data type for ints/floats
  - all division is float division, so use `Math.floor(a/b)` to get the whole number of times **b** divides into **a**
  - modular division works with floats, so `6.5%2.5 == 1.5`

## arrays

arrays are heterogenous (allow mixed data types)
- but you'll generally want to use them in ways where you can assume they are all the same data type

declaring arrays
```
var empty_arr = [];
var array_with_stuff = [25,20,0,"bacon"];
```

length of array / iterate through array
```
for(var i=0; i<array_with_stuff.length; i++)
    console.log(array_with_stuff[i]);
```

## strings

strings are immutable (can't be changed)
- so when you do various string operations, it creates a new string each time

string concatenation with **+** operator
- other types will be coerced to strings if added to the string
```
var name = "Bobby";
var num = 5;
console.log("Hi, my name is " + name + " and the number is: " + num + ".");
```

insert variables into strings with back-ticks (not single quote)
```
console.log(`Hi, my name is ${name} and the number is: ${num}.`);
```

length of string / iterate through string just like an array, but can't assign values to individual characters
```
for(var i=0; i<name.length; i++)
    console.log(name[i]);
```

## objects

objects largely work like a dictionary

declaring an object with some initial *attributes*
```
var scores = {
    'John' : 10,
    'Paul' : 12,
    'Tim' : 13
};
```

to check if key in object (say we are looking for Thomas's score):
```
if(scores['Thomas'] === undefined)
    console.log("We don't have Thomas's score yet");
```
OR
```
if(!'Thomas' in scores)
    console.log("We don't have Thomas's score yet");
```

to iterate through keys / values in an object:
```
for(name in scores)
    console.log(`${name} scored ${scores[name]} points.`);
```

if you want to use the object like a set, only the keys are important:
```
function withoutDuplicates(arr)
{
    var dict = {};
    for(var i = 0; i < arr.length; i++)
        dict[arr[i]]=1;
    return Object.keys(dict); //array of the keys
}
```

put methods in your object (and reference the object's other stuff through **this**)
```
butler = {
    name: "Mike",
    introduce: function() {
        console.log(`My name is ${this.name}, Sir.`)
    },
    greet() {
        console.log("Hello, Sir.");
    }
}
```

## classes... sort of

capitalize class name, **constructor** is a special method name
```
class Node {
    constructor(val) {
        this.value = val;
        this.next = null;
    }
}
```

create an instance of the class using the constructor
```
var bob = new Node(5);
```

# logic control and such

## conditions and if statements

C-style syntax; use { } for multiple statements
```
if (score > 20)
    do_something();
else if (score > 10)
    do_something_else();
else
    do_nothing();
```

keep in mind that conditions can give confusing bugs if they evaluate to things like *undefined* (which is false)

## loops

C-style syntax **for** and **while** loops, *break* and *continue* available
```
//print numbers from 1 to 100 except multiples of 5
for(var i = 1; i <= 100; i++)
{
    if(i%5==0)
        continue;
    console.log(i);
}
```
```
//find the biggest power of 2 less than 9342875
var x = 1;
while(x * 2 < 9342875)
{
    x *= 2;
}
console.log(x);
```

## functions

functions can be declared in a simple way, with or without parameters, return optional
```
function do_something(x,y,z)
{
    console.log(`"${x} ${y} ${z}");
    return x * y * z;
}
```

you can do the same thing with an arrow function
```
const do_something = (x,y,z) => {
    console.log(`"${x} ${y} ${z}");
    return x * y * z;
}
```

an arrow function with only a return statement can be written as
```
const do_something_else = (x,y,z) => x * y * z;
```

the common use for an arrow function is when a function is an argument, and you want to make a short one  
example: arr.map(func) returns an array of that function applied to each element in the array  
note no parentheses needed for single parameter arrow functions
```
console.log(names.map(name => "Ninja " + name));
```
