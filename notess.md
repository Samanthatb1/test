# my summary
Factory functions are one way to create multiple isntances of an object by calling the function and assining it to a variable. the only downside is that they all have a new instance of their props, meaning they all have a unique instance of their member methods, meaning if u change a func in one it wont change in another. To fix this we must inherit (using setPrototypeOf) an obj that will let all children use its prop

Use prototypal inheritence on factory funcs / regular OBJECTS instance, or constructor funcs INSTANCE (classes):
Object.setPrototypeOf(child, parent)

.prototype is done on the class
setPrototypeOf is done on the instance

``` obj.__proto__ === Object.prototype``` 
-> ACTUAL SYNTAX ```Object.getPrototypeOf(me) == constructorFunc.prototype```

frpm what ive read, for constructor functions, the prototype is the constructor and its not really good to overwrite it, so instead use 
``` ConstructorName.protoype.newProp = prop ``` for new stuff


if you set ```Class.prototype = ``` IT BETTER BE AN OBJ OR NULL. DO NOT SET IT TO A CONSTRUCTOR FUNC
also... when you do this, you loose the "constructor" prop on prototype, so instead do 
```Class.prototype = {...newObj, constructor : Class}```
recall constructor props just point to itself

```.prototype``` is only applicable to constructor functions. if you do it on an obj, itll be undefined

## .prototype
- a special property that almost all functions have that is only used when a function is invoked as a constructor function
- when a constructor is used to instantiate or create a new object, .prototype is set as the prototype of the new object (which is itself)

## [[prototype]]
- [[Prototype]] is a hidden private property that all objects have in Javascript, it holds a reference to the object’s prototype.
- An object’s prototype is the object that an object inherits or descends from.

-- 

promises are asyncronous, meaning theres two ways to deal with them: await or then.



## strict mode:
- The purpose of "use strict" is to indicate that the code should be executed in "strict mode"
- With strict mode, you can not, for example, use undeclared variables

## if, else if, else
||, &&
let result = condition ? valueIfTrue : valueIfFalse;

# for
for (let i = 0; i < 3; i++) { // shows 0, then 1, then 2
  alert(i);
}
for (let item of arr)
arr.forEach(function(item, index, array) {
  // ... do something with item
});


switch (a) {
  case 3:
    alert( 'Too small' );
    break;
  case 4:
    alert( 'Exactly!' );
    break;
  case 5:
    alert( 'Too big' );
    break;
  default:
    alert( "I don't know such values" );
}

# FUNCTIONS

function name(parameter1, parameter2, ... parameterN = "default") {
 // body
}

function decleration
function sayHi() {
  alert( "Hello" );
}
function expression
let sayHi = function() {
  alert( "Hello" );
};
- main diff, func decleration you can declare AFTER u call it

## Arrow syntax
let sum = (a, b) => a + b;
This arrow function is a shorter form of:
let sum = function(a, b) {
  return a + b;
};

- one liners do NOT need a return statement or curly braces


# objects
- theyre stored by reference
- an array is an object

# symbols
Symbols are created with Symbol() call with an optional description (name)
Symbols are always different values, even if they have the same name. If we want same-named symbols to be equal, then we should use the global registry: Symbol.for(key) returns (creates if needed) a global symbol with key as the name. Multiple calls of Symbol.for with the same key return exactly the same symbol.
use cases
- “Hidden” object properties.

# arrays
alert( [] == [] ); // false
alert( [0] == [0] ); // false
alert( String(arr) === '1,2,3' ); // true
- compare them item-by-item in a loop or using iteration methods
push(...items) adds items to the end.
pop() removes the element from the end and returns it.
shift() removes the element from the beginning and returns it.
unshift(...items) adds items to the beginning.

# higher order funcs
To add/remove elements:

push(...items) – adds items to the end,

pop() – extracts an item from the end,

shift() – extracts an item from the beginning,

unshift(...items) – adds items to the beginning.

splice(pos, deleteCount, ...items) – at index pos deletes deleteCount elements and inserts items.

slice(start, end) – creates a new array, copies elements from index start till end (not inclusive) into it.

concat(...items) – returns a new array: copies all members of the current one and adds items to it. If any of items is an array, then its elements are taken.

To search among elements:

indexOf/lastIndexOf(item, pos) – look for item starting from position pos, return the index or -1 if not found.
includes(value) – returns true if the array has value, otherwise false.
find/filter(func) – filter elements through the function, return first/all values that make it return true (filter what you want)

The some() method tests whether at least one element in the array passes the test implemented by the provided function. It returns true if,

findIndex is like find, but returns the index instead of a value.
To iterate over elements:

forEach(func) – calls func for every element, does not return anything.
To transform the array:
## map
map(func) – creates a new array from results of calling func for every element (return is assigned to index)

```
const vals = [1,5,4,6,4,2]

function doubler(x, index){
  return {x: x * 2, index}
}

// regular
const vals2 = vals.map(doubler)
console.log(vals2)

// anonymous
const vals3 = vals.map(function(x) {
  return x * 2
})
console.log(vals3)

// arrow
const vals4 = vals.map(x => x*2)
console.log(vals4)
```

## sort 
function compareNumeric(a, b) {
  if (a > b) return 1; -> a goes after b
  if (a == b) return 0; -> keep original order
  if (a < b) return -1; -> a goes before b
}
arr.sort(compareNumeric);

reverse() – reverses the array in-place, then returns it.

split/join – convert a string to array and back.

reduce/reduceRight((accumulator, currVal) => {}), initial – calculate a single value over the array by calling func for each element and passing an intermediate result between the calls. It takes the
return and sets it as the next accumulator value
- ex. find sum of array
- ex. find max of array

```
let howManyElements = vals.reduce((acc, curr) => {
  return acc + 1
}, 0)

let maxVal = vals.reduce((currMax, curr) => (curr > currMax) ? curr : currMax);
```

Additionally:

Array.isArray(value) checks value for being an array, if so returns true, otherwise false.

# Classes

## THIS
this inside just a regular file gives u the Window
this inside a class gives you the entire calss object
this inside a func will give u the Window. This is bad bc imagine u make a function
  IN a member func for your class (solution: arrow func)
this inside arrow func gives you the object thats right above it
THIS BREAKS:
``` 
class Counter {
  constructor(){
    this.count = 0;

    countIt();

    function countIt(){
      this.count++;
    }
  }
}
```

# promises
- with async programming, your code will not wait for an async function to finish. The rest of the code will keep going. What if you literally need it to wait though, because you need the new value... use a promise! then (that area of code) will actually wait :)
1. pending
2. fulfilled
3. rejected

```
// these all return promises (=> implicitely returns it, but for the 2 
// liner you need to write the word return)
fetch(url)
  .then(res => res.json())
  .then(data => {
    console.log(data)
    return fetch(url2)
  })
  .then(res => res.json())
  .then(data => console.log(data))
  .catch(err => console.log("my error is ", err))
```

```
// even though its all async, this program guarentees you eat the pizza after its delivered
let pizza = "none"

function orderPizza(callback){
  setTimeout(() => {
    callback()
  }, 1000);
}

function eatPizza(){
  console.log("eat pizza") // #3
}

console.log(orderPizza(eatPizza)) // #1 undefined console log
console.log("watch tv") // #2

// this can get us into callback hell: fix with promises

function orderPizza2(){
  console.log("ordered the pizza")
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve(3)
    }, 2000);
  })
}

orderPizza2()
  .then((numberOfPizzas) => {
    console.log("pizzas here!" , numberOfPizzas)
  })
```
## async and await
- any function that is async, everything around it will run without waiting
- but everything IN IT will be syncronous if you use await
```
// ES8
getData() // await code RETURNS a promise !!! (bc its async !?)
  .then(data => console.log(data))
  .catch(err => console.log(err))

async function getData(){
  const response = await fetch(url) // fetch returns a promise so we have to await
  const data = await response.json() // response.json returns a promise which is why we have to await
  return data // the stuff on the RHS returns the promose. the LHS is the value (await converts promise to value)
  // return data will run AFTER the two awaits are done. its like syncronous programming (even though its now). This is opposite to .then(), with then() itll run everything else while waiting
}
```

```
const fetchData = async () => {
  try {
    const response = await fetch(url)
    const countries = await response.json()
    console.log(countries)
  } catch (err) {
    console.error(err)
  }
}
console.log('===== async and await')
fetchData()
```

# Classes and Inheritence
inheritance - child class inherits properties or functions of the parent
encapsulation - 
polymorphism - many forms 
```
class Particle{

  constructor(x = 30, y = 20){
    this.x = x;
    this.y = y;
  }

  move(distance){
    this.x += distance
  }

  show(){
    console.log(this.x, this.y, "o")
  }

  bounce(num){
    console.log(`bounce ${num} times`)
  }
}

class Square extends Particle{
  constructor(x, y){
    super(x, y)
    this.square = true
  }

  show(){
    console.log(this.x, this.y, "[]")
  }

  bounce(num){
    super.bounce(num)
    console.log("slam!")
  }
}
```


# Prototypal Inheritance tutorial
- actual definition: When we read a property from object, and it’s missing, JavaScript automatically takes it from the prototype
- imagine a function is ur class. if u add a func in that func with "this." its a property of
  the obj. If u add a function with the prototype key, then its a method. if u use "this."
  and u want to modify it later, you'll need to modify it in *every* instance

- peoperties: should be added with "this."
- methods: should be added with Class.prototype.name = function(){}

- when you console log an object, the first set of props is the props that are applied to the instance itself
  - then when you expand the prototype section, those are props that belong to ALL objects

- you can also create objects with *pure* / *literal* js objects:
```
const person = {
  talk(){
    return "talking" 
  }
}
// this way, all instances share the SAME talk()
const me = Object.create(person) // these are like equivalent
const you = Object.setPrototypeOf(meObj, personObj)
console.log(me.talk())
console.log(you.talk())
```

ex
```
let animal = {
  eats: true
};
let rabbit = {
  jumps: true
};

Object.setPrototypeOf(rabbit, animal)
console.log(rabbit.eats)
```

# FACTORY FUNC VS CONSTRUCTOR FUNC
## factory
```
function fact(){
  return {}
}
```
- youre assigning an OBJ to a var, meaning if u change var.name, itll only change for that one
- this is like how youd expect a normal object to operate
## constructor
```
function Cons(){
  this...
}
const var = new Cons()
```

another example
```
factory vs constructor
function ConstructorFunction() {
   this.someProp1 = "1";
   this.someProp2 = "2";
}
ConstructorFunction.prototype.someMethod = function() { /* whatever */ };

function factoryFunction() {
   var obj = {
      someProp1 : "1",
      someProp2 : "2",
      someMethod: function() { /* whatever */ }
   };
   // other code to manipulate obj in some way here
   return obj;
}
```


- className.prototype.newFunc = function(){return this.name} this will add a new func to ALL objects
- this is like how youd expect a normal class to operate

## using set prototype with factory func vs constructor func (they both work!)
```
const Parent = {
	getNamePeriod : function(){
  	return this.name + "."
  }
}

// factory func
function myFactory(n){
	const name = n
  
  return {
  	name
	}
}

const sam = myFactory("sam")
Object.setPrototypeOf(sam, Parent)
console.log(sam)
console.log(sam.getNamePeriod())

// constructor func
function myConstructor(n){
	this.name = n
}

const mia = new myConstructor("mia")
Object.setPrototypeOf(mia, Parent)
console.log(mia)
console.log(mia.getNamePeriod())
```
- the reason why when you tried to do BOTH setPrototypeOf AND class.prototype.prop = it didnt work is because once you make an obj, it takes the prototype it has when it was made, if u change it later it wont change, it only uses the prototype it was given right before it was made

## __ proto __ vs prototype
object.__ proto __ === class.prototype
- every object literal has a proto called Object (the OG base object)
- proto is a property of evvery variable (obj, array, string) that points to
  the parent object that it inherits from
- prototype is a property on the constructure function that contains everything that will
  be inherited by its instance (a constructor function is like Class())

# this / constructor function
when you put a "new" in front of a function call
``` 
const hi = new Person()

function Person(){}
```
it implicitely does this
``` 
function Person(){
  const this = {}
  return this
}
``` 
``` 
function Person(name){
  this.name = name
  this.talk = () => return "talking"
}
const sam = new Person("sam")
```

Practical inheritance example
```
const Mammal = function(legs){
  this.legs = legs
}

const Cat = function(legs, isDomesticated){
  Mammal.call(this, legs)
  this.isDomesticated = isDomesticated
}

const lion = new Cat(4, false)
console.log(lion)
```

### this within a object
```
const obj = {
  name: "sam",
  talk: function(){console.log(this)}, // returns me
  talk2: () => {console.log(this)}, // returns window
  prop: this // returns window
}
```
- objects do not create a binding with "this". only functions do
- therefore, methods inside objects should not be arrow functions 
[example](https://www.google.com/search?q=javascript+function+in+object&sxsrf=AJOqlzXiFW7biWGH3OMeLcKCRASv3GvD9w:1677977866471&source=lnms&tbm=isch&sa=X&ved=2ahUKEwi226_VysP9AhV5jokEHTDOA3kQ0pQJegQIBRAC#imgrc=H4LlKAimszxAMM)

### use case of arrow func in obj
```
const obj = {
  name: "sam"
  talk: function(){
    setInterval(() => {
      console.log(this.name)
    }, 100)
  }
}
```
- first ask yourself, what would this.name be outside of the arrow func? it would be Sam
- and since we know arrow funcs take the scope of the outside, then this.name in the arrow func would be sam too
- arrow func always uses its outside scope


# Closures
- basically scope
- common use case: functions inside of functions
- inner function has access to everything in the outer scope, even if that outerscope 
has been executed and is gone by the time the inner function is called

```
function outerFunc(outsideVar){
  return function innerFunc(insideVar){
    console.log(`outside ${outsideVar}`)
    console.log(`inside ${insideVar}`)
  }
}

const innerFunctionWithSpecificOuter = outerFunc("out")
innerFunctionWithSpecificOuter("in")
```
-> notice how innerFunc still has access to outsideVar even after outsideFunc is done executing

# Bind
- lets a function know what "this" is 
- returns a copy of a method BINDED to the "this" you give it
- returns a copy of the same function such that everywhere that has a "this" is replaced with the "this" you pass in
function.bind(thisValue, arg, arg, arg)
it returns a func
```
function talk(){
  console.log(`hi my name is ${this.name}`)
}

const me = {
  name: "sam"
}

const func = talk.bind(me)
func()
```

```
function Person(name){
  this.name = name

  setInterval(function(){
    console.log(this)
  }.bind(this), 1000);
}

const me = new Person("sam")
```

## call
- call is the same thing but doesnt return a func
```talk.call(me, args)```

```
const me = {name: "sam", l:"g"}
const you = {name: "mia", l:"c"}

const printFullName = function(){
  console.log(this.name + " " + this.last)
}

printFullName.call(me /*, params, go, after */)
```

## apply
```talk.call(me, [args])```
note that it doesnt acc pass an array, it passes multiple params in that order

## use case of bind
- callback functions do not know what "this" is because its kinda outside the scope
```
function Person(name){
  this.name = name
  this.talk = function(){console.log(this)}
  this.talk = () => {console.log(this)} // both work !

  setInterval(function(){
    console.log(this.name)
  }.bind(this), 1000); // need to bind the callback
}
```
- if it was an arrow function you would NOT need bind

# parameters
url parameters -> in the url, blahblah?param=val

headers

# destructuring
```
let [one, two, three] = [5, 6]
// one = 5
// two = 6
// three = undefined
```

## spread
```
const nums = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
let [num1, num2, num3, ...rest] = nums

console.log(num1, num2, num3)
console.log(rest)
1 2 3
[4, 5, 6, 7, 8, 9, 10]
```
object
```
const rectangle = {
  width: 20,
  height: 10,
  area: 200
}
let { width, height, area, perimeter } = rectangle
```

copy an array with spread
```
const evens = [0, 2, 4, 6, 8, 10]
const evenNumbers = [...evens]
```

copy an object with spread and modify it
```
const user = {
  name:'Asabeneh'
}
const copiedUser = {...user, title:'instructor'}
```

unlimited function arguments
```
const sumAllNums = (...args) => {
  console.log(args)
}

sumAllNums(1, 2, 3, 4, 5)
```

```
function addProps({name, age, skills: {frontEnd, backEnd, dataBase, dataScience}}){
	const newStudent = {
	    name,
	    age,
	    skills : {
	    	frontEnd : [...frontEnd, {skill: 'BootStrap',level: 8}],
        backEnd : [...backEnd, {skill: 'Express',level: 9}],
        dataBase : [...dataBase, { skill: 'SQL',level: 8}],
        dataScience : [...dataScience, "SQL"]
	    }
	  } 
  return newStudent
}

console.log(addProps(student))
```

## rest parameters
- in old javascript, if u dont know how many params there are u can use the auto arguments array
- now, just do function(...args) which will give u an array called args with all the parameters

# currying
- the technique of translating the evaluation of a function that takes multiple arguments into evaluating a sequence of functions, each with a single argument
```
function curry(a){
  return function(b){
    return function(c){
      return a + b + c
    }
  }
}

const curry = a => b => c => a + b + c

let result = curry(1)
result = result(1)
result = result(1)
console.log(result)

result = 0

result = curry(1)(1)(1)
console.log(result)
```

```
// little use case
const multiplyBy = x => n => x * n

const double = multiplyBy(2)
console.log(double(2))
console.log(double(4))

const triple = multiplyBy(3)
console.log(triple(2))
console.log(triple(4))
```

# memoization
- uses closures to keep a history of the return values of inner functions, so you dont have to keep recomputing long computations

```
const memoizeMultiplyBy10 = () => {
  const cache = {}

  return function(num){
    if (num in cache) return cache[num]
    
    const result = num * 10
    cache[num] = result
    return result
  }
}

const multiply10 = memoizeMultiplyBy10()
console.log(multiply10(3))
console.log(multiply10(4))
console.log(multiply10(3))
```

# hoisting
```
blah blah
var x = 5;
```
BECOMES
```
var x;
blah blah
x = 5
```
this is why you can declare / call functions anywhere on the page. But if you make a func with const name = () => then you CANT use it anywhere since **const and let are not hoisted**
