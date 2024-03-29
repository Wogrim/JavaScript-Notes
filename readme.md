# Important

- dynamically typed variables
- some things will return things like NaN, undefined, or null instead of causing an error that stops the code
- == and != will do a type conversion if you are comparing different types, which can cause tricky bugs with the above feature
- as the expression in a condition, the following values are false: **false**, **0**, **""** (empty string), **null**, **undefined**, **NaN** (not a number)
- === and !== to do proper comparisons to avoid this problem
- statments are ended with a semicolon, but they are sort of not required (safer to put them for clarity)
  - if you don't have a semicolon at the end of a line, the interpreter will try to put one there if it makes valid syntax
- ECMAScript (ES) is the standard of JS, each new version (ES5, ES6) adds more features
- you can assign functions to variables, pass functions as arguments, return functions from functions, etc
- arrow functions are a popular syntax for defining functions, technically a little different from other ways to make a function
- JS is single-threaded non-blocking; some things are asynchronous

# Data Types and Variables

variables can be declared as
- **var** (gets *hoisted* so it can actually be used before where it is declared
  - if initialized with the declaration the assignment portion stays in place
  - var is function scoped; if you declare it in a loop it is accessible outside the loop also
  - generally, never use var
- **let** is "new" (ES6) block scoped, not hoisted
- **const** is also "new" (ES6) block scoped, not hoisted, can't be changed
  - but while a const array or object can't be reassigned, you can change the contents
    - use `Object.freeze(arr);` to make it properly immutable

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

length of array / iterate through array (there are other methods)
```
for(var i=0; i<array_with_stuff.length; i++)
    console.log(array_with_stuff[i]);
```

copy a portion of array to new array with `arr.slice(start=0, end=arr.length)`  
(end is not inclusive, start and end can be negative)
```
var arr = [0,1,2,3,4,5,6,7];
console.log(arr.slice(2,-2)); // [2,3,4,5]
```

`.map()` a function to each element of an array; creates a new array with modified copies of the original
```
// a copy of the array with all the elements increased by 1
var arr2 = arr.map(element => element + 1);
// a copy of the array with all the elements increased by their index
var arr3 = arr.map((element, index) => element + index);
```

`.filter()` makes a copy of the array but only keeps elements that pass the filter test (return *true* = keep)
```
// a copy of the array that removes negative values
var arr4 = arr.filter(element => return element >= 0);
// a copy of the array that keeps values that are greater than their index
var arr5 = arr.filter((element, index) => return element > index);
```

`.concat()` mashes two arrays together (in a new array)
```
var arr6 = arr4.concat(arr5);
```

`.sort()` sorts array values as strings by default, or give it a function
- function should be positive if a > b, zero if a === b, negative if a < b
```
//sort an array of strings by their second letter
console.log(arr.sort((a,b) => a[1].localeCompare(b[1])));
```

(ES6) destructure an array to get values out in named variables (commas to skip values)
```
var secondElement = arr[1];
var fifthElement = arr[4];
// becomes
const [ , secondElement, , , fifthElement] = arr;
```
(object destructuring more common)

(ES6) rest operator (...) when destructuring to get the remainder of the array copied into a new array (like a slice)
```
const [firstElement, ...remainingElements] = arr;
```

make a copy of the array with additional stuff
```
const arrPlus = [...arr, 27, 28];
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

objects largely work as a hashmap (Python dictionary / C++ unordered_map)

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
if(!('Thomas' in scores))
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

destructure an object (ES6): get values and put them in new variables
```
var email = person.email;
// becomes
const { email } = person;
```

can get multiple at once
```
var name = person.name;
var email = person.email;
// becomes
const {name, email} = person;
```

destructure into a different variable name
```
var personsEmail = person.email;
// becomes
const {email: personsEmail} = person;
```

nested destructuring lets you get values inside a nested object/array  
(let's say a response is an object which contains an object called *error* from which we want *status* as *errorStatus*)
```
const {error : {status: errorStatus}} = response;
```
(can become too difficult to read)

object spread copies (shallow) the rest of the object's key-value pairs to a new object
```
const {name, email, ...extra} = person;
```

2 ways to copy (shallow) the whole original
```
const {...personCopy} = person;
const personCopy2 = {...person};
```
 
copy and add/overwrite keys/values
```
const personCopy3 = {...person, age: 50};
```

## classes... sort of (ES6)

- capitalize class name
- class definitions are not hoisted
- **constructor** is a special method name (required)
- methods written as arrow functions show up as part of the object if you console.log() it
```
class Node {
    constructor(val) {
        this.value = val;
        this.next = null;
    }
    dosomething() {
        console.log(`doing something with ${this.value}`);
    }
    dosomethingelse = () => {
        console.log(`doing something else with ${this.value}`);
    }
}
```

create an instance of the class using the constructor
```
var bob = new Node(5);
```

inheritance, override method, calling overridden method
```
class DLLNode extends Node{
    constructor(val){
        super(val); //parent class constructor
        this.prev = null;
    }
    dosomething(){
        console.log("DLLNode's dosomething() doesn't do much");
        super.dosomething();
    }
}
```

to make check that a parameter is an instance of a class (parent class will return true)
```
function nullify(node) {
    if(! node instanceof Node)
        return;
}
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

ternary operator to have an if statement in an expression
```
console.log(`I have 10 ${count!==1? 'mice' : 'mouse'}.`);
```

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

*for of* method of traversing through an iterable
```
for(const element of arr) {
    console.log(element);
}
```

## functions

functions can be declared in a simple way, with or without parameters, return optional, will be hoisted
```
function do_something(x,y,z)
{
    console.log(`"${x} ${y} ${z}");
    return x * y * z;
}
```

you can call functions without all arguments and the parameters will be undefined
- or you can set default values for parameters
- JavaScript does not have named arguments
```
function do_something(x=1,y=1,z=1)
{
    console.log(`"${x} ${y} ${z}");
    return x * y * z;
}
```

another way which won't get hoisted
```
const do_something = function(x,y,z) {
    console.log(`"${x} ${y} ${z}");
    return x * y * z;
}
```

you can do the same thing with an arrow function
- an arrow function has the advantage of being able to look in the parent scope for **this**
```
const do_something = (x,y,z) => {
    console.log(`"${x} ${y} ${z}");
    return x * y * z;
}
```

anonymous function as parameter to arr.forEach() (which maps a function to each element)
- creates its own context so unable to use **this**
```
arr.forEach(function(element){
    console.log(element);
});
```

an arrow function with only a return statement can be written as
```
const do_something_else = (x,y,z) => x * y * z;
```

to return a new object, must put parentheses around it or else sytnax will think it is a block
```
const objectify = (name,age) => ({name: name, age: age});
```

the common use for an arrow function is when a function is an argument, and you want to make a short one  
example: arr.map(func) returns an array of that function applied to each element in the array  
note no parentheses needed for single parameter arrow functions
```
console.log(names.map(name => "Ninja " + name));
```

## exceptions

typical **try** / **catch** syntax
- **finally** block (optional) is run before exiting the whole try/catch structure, no matter how it is exited
```
try{
    //do something that might throw an exception
    if(!(target instanceof Unit)){
        throw new Error("Unit.attack(target): target is not a Unit");
    }
}
catch (error) {
    //do something about the exception
    console.log("ERROR:",error.message);
}
finally {
    //TODO: some kind of clean-up
}
```

## Promises and fetch from API

a Promise is an object that keeps track of the status of a (typically) asynchronous action
- **pending** is when the action is in progress
- **resolved** is when the action is successful
- **rejected** is when the action fails

you can manually make a Promise, and resolve/reject it as appropriate
```
const tenSeconds = new Promise((resolve, reject) => {
    setTimeout(()=>{
        resolve("ten seconds are up!")
    }, 10000
    );
});

//.then or .catch will happen with the promise is resolved or rejected 
//(in this case resolved after 10 seconds)
tenSeconds
    .then(res => console.log(res))
    .catch(err => console.log(err));

//this will happen right away, before the promise is resolved; the promise is pending
console.log(tenSeconds);
```

but the typical situation is you are trying to fetch data from an API
- **fetch** returns a promise; if we get data the first **.then()** function is run
  - response.json() is also a promise, which converts the server response to JSON
    - after that happens we do what we want with the data
  - if either promise fails (fetch or .json), **.catch** happens
```
//get the first 101 pokemon from the API
fetch("https://pokeapi.co/api/v2/pokemon?limit=101")
    .then(response => response.json())
    .then(response => {
        //for this API, response is an object
        //response.results is an array of pokemon objects
        //for another API, check its documentation or console.log the response
        //we will just put the names of the pokemon in our own array
        allPokemon = (response.results.map(p => p.name));
    })
    .catch(err => {
        console.log(err);
        allPokemon = [];
    });
```
