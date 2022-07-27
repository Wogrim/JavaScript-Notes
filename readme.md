# Funky Features

- dynamically typed variables
- some things will return things like NaN, undefined, or null instead of causing an error that stops the code
- == and != will do a type conversion if you are comparing different types, which can cause tricky bugs with the above feature
- as the expression in a condition, the following values are false: **false**, **0**, **""** (empty string), **null**, **undefined**, **NaN** (not a number)
- === and !== to do proper comparisons to avoid this problem
- statments are ended with a semicolon, but they are sort of not required (safer to put them for clarity)
  - if you don't have a semicolon at the end of a line, the interpreter will try to put one there if it makes valid syntax

# Data Types and Variables

variables can be declared as
- **var**
- **let**
- **const**

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
    return Object.keys(dict);
}
