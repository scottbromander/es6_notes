# ES6 / ES 2015

## LET Declarations
Let is a new way to declare variables and have them scoped to the nearest code block (and not to the nearest function, as with the standard `var` declaration). 

Consider this:
```javascript
function regularFunction(){
  if(true){
    var trueBlockVariable = 'Hello';
  } else {
    var falseBlockVariable = 'Goodbye!';
  }
  
  console.log(falseBlockVariable);
}
```

In the above code, the console log will produce `undefined` rather than the normal 'not defined' error. To test this, you can try console logging any other made up variable, such as 'cats' on the very next line after the 'falseBlockVariable' console log. 

The reason for this is because of the 'var' declaration and hoisting. Hoisting will lift the variable declarations to the top of the function and set them to undefined. 

The answer of course, is a `let` declaration.

Consider this:
```javascript
function regularFunction(){
  if(true){
    let trueBlockVariable = 'Hello';
  } else {
    let falseBlockVariable = 'Goodbye!';
  }
  
  console.log(falseBlockVariable);
}
```

This will produce an error of 'not defined'. This matches our expectation of what we would see in other programming languages. 

### Instructor Notes
* Make sure that students really understand scope,
* Make sure that the students understand the difference between 'undefined' and 'not defined',
* One of the considerations that need to be made is whether or not an error is actually better than undefined for the need of the application.

## CONST Declarations

Const declarations allow us to create variables that cannot change. Which on the surface seems like a bad idea, but it allows us to constrain and address 'magic numbers'. 

Consider this example that checks the number of toppings on a pizza order. If its over three toppings, then it does not qualify for a special:
```javascript
var numOfToppings = 4;

if(numOfToppings > 3){
  // Does not qualify for deal.
} else {
  // Qualifies for deal.
}
```

The problem in the above, is that the number '3' would be a complete mystery without the explanation above it. This is what we call a `magic number`. Magic numbers are numbers that have meaning, but they are not described in the code at all. Typically they get used because they are meant to be unchanging values. This is where the `const` declaration can help. We use the const declaration to help us control the value, but also be descriptive about what that value represents. We can pair that with the `let` declaration on the `numOfToppings` for extra ES6'iness.

Finally, naming convention for `const` variables uses capital letters with underscores in between. So for our pizza deal declaration, we would use something like this: `const TOPPINGS_FOR_DEAL`

```javascript
let numOfToppings = 4;
const TOPPINGS_FOR_DEAL = 3; 

if(numOfToppings > TOPPINGS_FOR_DEAL){
  // Does not qualify for deal.
} else {
  // Qualifies for deal.
}
```

The code is now more readable in terms of being able to look at the code and quickly infer what the code is doing. Additionally, we know with the naming convention that the `TOPPINGS_FOR_DEAL` is a constant and that the value cannot be changed. 

### Instructor Notes
* Ensure that students understand what a Magic Number is. And even though it has a good name, it's actually a bad thing,
* Sell the idea of code readability here, restate the if statement out loud, pointing to the variables. Example "If the number of toppings is greater than the toppings for the deal, then...",
* Demonstrate that you cannot change the value of a const. Like the example below:
```javascript
const SOME_CONST = 6;
SOME_CONST = 5;
```

## Function Arguments
Javascript is very flexible when it comes to working with arguments within functions. We can pass in extra arguments or even omit arguments all together on functions that would normally accept arguments. In these cases, Javascript will not produce errors. 

Consider this:
```javascript
function processArray(array){
  console.log(array.length);
  //do things to the array
}

processArray( [1,2,3] ); // logs '3'
processArray( ); //cannot read property '.length' of undefined.
processArray( undefined ); //cannot read property '.length' of undefined.
```

The error of `cannot read property '.length' of undefined` comes from the fact that we are trying to read .length within the console log, not that we passed in nothing or undefined itself. Actually passing the arguments or not is something that Javascript allows us to do. 

## Default Parameter Values
We can now create and assign default parameters to our function arguments! If the value is supplied, it supplied value will override the default set. We simply assign the default value in the `function signature`. For example `function processArray(array = []){...}`. Note that supplying an undefined value *WILL NOT* override the default parameter value. Meaning that an undefined supplied value will become the default parameter value.

Looking at the previous example, we can see how the logs will now be different:
```javascript
function processArray(array = []){
  console.log(array.length);
  //do things to the array
}

processArray( [1,2,3] ); // logs '3'
processArray( ); //logs '0'
processArray( undefined ); //logs '0'
```

### Instructor Notes
* Take a moment to clean up the phrase 'function signature' with students,
* Point out that default parameters are available in other languages,
* Type is implied with the default parameters, but another type could be entered at the time of the function call (so it does not fix everything)

## Configuration Objects and Named Parameters
A common pattern in Javascript is to accept a configuration object as an argument to a function. 

For example:
```javascript
function setupUser(configObject){
  var name = configObject.name;
  var admin = configObject.admin;
  //do things
}

setupUser({name: 'Scott', admin: true});
```

From what we learned about default parameters, we may be tempted to additionally use a default value for the `configObject` to at least check whether or not the supplied argument is an object. Problem is, we are still writting assignment code, Which might look something like this:
```javascript
function setupUser(configObject = {}){
  var name = configObject.name;
  var admin = configObject.admin;
  //do things
}

setupUser({name: 'Scott', admin: true});
```

But we can take this up another step. We can instead use the declaration names within an object as an argument to the function itself. Check it out: 

```javascript
function setupUser( {name,admin} ){
  //do things
}

setupUser({name: 'Scott', admin: true});
```

Inside the function, we have access to the `name` and `admin` values, already declared as we did in the examples above. As a bonus, the function signature is more descript about that the function accepts! Note that as a final step, we can still assign a default parameter. 

```javascript
function setupUser( {name,admin} = {} ){
  //do things
}

setupUser({name: 'Scott', admin: true});
```

## [Rest Parameters](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/rest_parameters)
A Rest parameter allows us to accept an indefinite amount of arguments and puts them into an array. We access the rest parameter with the `...` leading syntax followed by what we would like to call the param. 

For example:
```javascript
function restFunction(...list){
    for(let i = 0; i < list.length; i++){
        console.log(list[i]);
    }
}

restFunction('Scott', 'Fred', 'Mark', 'Taylor', 'Chris');
```

Additionally, we can put arguments in front of the rest parameter to accepted needed arguments that should not be considered in the rest array.

For example:
```javascript
function restFunction(instructor = 'Unassigned', ...list){
  for(let i = 0; i < list.length; i++){
    console.log(list[i]); // Logs list without 'Scott'
  }

  console.log(instructor); // Logs 'Scott'
}

restFunction('Scott', 'Fred', 'Mark', 'Taylor', 'Chris');
```

## [Spread Operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_operator)
Spread operators have a similar syntax as rest parameters, however instead of using the `...` syntax in a function argument, we use it in the function call. The functional difference is that it take an array of values and sends them to the function as individual arguments into the function.

Consider this:
```javascript
let atticus = ['Atticus', 392811, 94000];

function createEmployeeObject(array){
  var name = array[0];
  var employeeNumber = array[1];
  var salary = array[2];
  //Do things
}

createEmployeeObject(atticus);
```

In the above example, we see the array of information passed into the function call, then inside the function the array is accepted. That array is then used to assign value to variables created in the function. As we have seen in ES6 before, we know that this pattern of boilerplate variable assignment is not ideal. So instead, we can pair up the spread operator with stated arguments. For example:
```javascript 
let atticus = ['Atticus', 392811, 94000];

function createEmployeeObject(name = 'Un-named', employeeNumber = '00000', salary = '10000'){
  //Do things
}

createEmployeeObject(...atticus);
```

In the example above, we can see that the variable creation is handled in the function signature. The spread operator can them separate them into different arguments. Additionally, we can pair both the rest and spread operator together for some great flexibility. Run the following code and notice how the console logs are different:
```javascript
let atticus = ['Atticus', 392811, 94000];

function createEmployeeObject(name = 'Un-named', employeeNumber = '00000', salary = '10000', ...extras){
    console.log(name, employeeNumber, salary); // logs Atticus, 392811, 94000
    console.log(extras);                       // logs [4, 5, 6]
    console.log(...extras);                    // logs 4, 5, 6
}

createEmployeeObject(...atticus, 4, 5, 6);
```

## [Arrow Functions and Lexical Binding](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions)
Arrow functions is one of the most exciting new features of ES6. At first glance, it seems like a fancy new way to create functions. But below the surface, is a very important consideration around the binding of 'this' as it relates to method calls. But more on that in a second.

Lets take a look at the same function, defined in both ES5 and ES6:
```javascript
// ES5
var normalFunction = function(){
  console.log('Normal function');
}

//ES6
var arrowFunction = () => {
  console.log('Arrow function');
}
```

First thing we notice is how the function is actually defined. Instead of using the keyword `function`, we use a set of `( )` followed by a `=>` then the regular code block. At a closer look, the other thing that we see, is that we need to use function expressions and anonymous functions to properly set up an arrow function in this regard.

Let's look at the same example, but with an argument in the function as well:
```javascript
// ES5
var normalFunction = function(message){
  console.log('Normal function: ', message);
}

//ES6
var arrowFunction = (message) => {
  console.log('Arrow function: ', message);
}
```
Now the short creation of functions is cool, but not the only point of arrow functions. One of the most common problems in Javascript, is the creation of Objects that have methods. More specifically, how that method is able to access the objects properties to which the method belongs. Let's look at an example of the problem below in ES5:
```javascript
function PersonES5() {
  var that = this; // We need to bind 'this' to a new variable to preserve the context of 'this' for use inside the method.
  that.age = 0;

  setInterval(function growUp() {
    // The callback refers to the `that` variable of which
    // the value is the expected object.
    that.age++; // This iterates the value of 'age' properly on the object.
    console.log(that.age); // We can see that this increments correctly.
    this.age++; // This produces NaN
    console.log(this.age, this); // We discover that 'this' inside the method has a new context. That to the window.
  }, 1000);
}

var scott = new PersonES5();
```

### Lexical Binding
In the previous example, we observed that once we were inside the method of the object, the context of `this` shifted from the object, to the window, as that is where the function is technically called. Something that we would not expect. Luckily, with Arrow Functions, it preserves the context of `this` to what we would expect. So lets look at how we can hook into Arrow Functions to help with the example from above, rewritten with ES6 and Arrow Functions:
```javascript
function PersonES6(){
  this.age = 0;

  setInterval(() => {
    this.age++; // |this| properly refers to the person object.
    console.log(this); // Iterates the age of the Person object as we would hope.
  }, 1000);
}

var scott = new PersonES6();
```
Arrow functions bind to the scope of where they are defined, not where we are used. This is known as `Lexical Binding`.  

## [Object Initialization Shorthand](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Object_initializer)

We now have a shorthand method for creating objects that have key value pairs that match the same name. First, let's look at some ES5 syntax to understand where the upgrade comes from:
```javascript
let name = 'Hamburger';
let price = 7.99;
let sides = ['Fries', 'Coleslaw'];

let order = {name: name, price: price, sides: sides};
console.log(order.name, order.price, order.sides); //logs 'Hamburger', 3.99, ['Fries', 'Coleslaw']
```

As you can see, there is a little bit of repetition in the creation of the order variable. In the object we create, we find ourself repeating the key value pairs. If we want them key and the value to be the same (value pointing to another variable of course), we can use a shorthand:
```javascript
let name = 'Hamburger';
let price = 7.99;
let sides = ['Fries', 'Coleslaw'];

let order = {name, price, sides};
console.log(order.name, order.price, order.sides); //logs 'Hamburger', 3.99, ['Fries', 'Coleslaw']
```

## [Object Destructing](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)

### Array
Object destructing allows us to assign multiple values based on returns of multiple values. Below are some examples of how this works:
```javascript
let someArray = ['Hamburger', 3.99, ['Fries', 'Coleslaw']];

let [name, price, sides] = someArray;
console.log(name, price, sides); //logs 'Hamburger', 3.99, ['Fries', 'Coleslaw']
```

Above, you can see that we defined an array with three values, a String, a Number, and an Array. Then we use a variable declaration to create three new variables with bracket syntax and then set it equal to an array. The three new values then become equal to the three values from the array.

We can also skip variables by omitting a variable name:
```javascript
let someArray = ['Hamburger', 3.99, ['Fries', 'Coleslaw']];

let [name, , sides] = someArray;
console.log(name, sides); //logs 'Hamburger', ['Fries', 'Coleslaw']
```

## Method Initializer Shorthand

```javascript 
//Old
function Dog(name){
  return {
    name,
    bark : function(){
      alert('Bark!');
    }
  }
}

//New
//Old
function Dog(name){
  return {
    name,
    bark(){
      alert('Bark!');
    }
  }
}
```


## Template Strings

```javascript
//Old
function Person(first, last){
  let fullname = first + ' ' + last;
}

//New
function Person(first, last){
  let fullname = `${first} ${last}`;
}

```

Also, multiline strings are supported with the back ticks:
```javascript
let scottsJoke = `Two muffins are sitting in an oven.

The first muffin says to the second 'Its really hot in here'.

The second muffin says 'AH! A TALKING MUFFIN!'`

console.log(scottsJoke);
```

## Array with Destructing Variables
We can use destructing to assign multiple values from an array to local variables. Common case for variable assignment from Arrays:
```javascript
let people = ['Scott', 'Chris', 'Kris'];
let a = people[0];
let b = people[1];
let c = people[2];
console.log(a,b,c);
```

But we can use Destructing Variables to shorten the assignment:
```javascript
let people = ['Scott', 'Chris', 'Kris'];
let [a,b,c] = people;
console.log(a,b,c);
```

### Array with Function Returns and Destructing Variables
Similar to the examples above, this also works with functions that return arrays as well:
```javascript
function basePizzaToppings(){
  let toppings = ['Sausage', 'Cheese', 'Pepperoni'];
  return toppings;
}

let [a,b,c] = basePizzaToppings();
console.log(a,b,c);
```

## 'For Of' Loops
A very common task is to iterate over arrays to complete some task. Using a 'For In' loop allows us to go through each item in an array and do something with it, however it has an extra step:
```javascript
let people = ['Scott', 'Chris', 'Kris'];

for(let index in people){
  console.log(people[index]);
}
```

In the above step, we track the `index` and use it to get the specific person out of the people array. It would be much handier if we were able to drop a step since this is such a common set. Enter 'For Of' loops:
```javascript
let people = ['Scott', 'Chris', 'Kris'];

for(let person of people){
  console.log(person);
}
```

## Classes
A common approach to encapsulation within Javascript is to use a combination of constructor functions and assigning methods to the prototype:

```javascript
function AudioPlayer(currentSong){
  this.currentSong = currentSong;
  this.currentTime = 0;
}

AudioPlayer.prototype.play = function(){ ... } ;
AudioPlayer.prototype.stop = function(){ ... } ;

let newAudioPlayer = new AudioPlayer('Sleep Apnea');
newAudioPlayer.play();
```

But in ES6 syntax, we have a much more elegant way to define our classes. To those coming from other OOP languages, the syntax is much more familiar. It even comes with a `constructor` method that is invoked whenever an instance of the class created!

Here is the same class defined above in the new syntax:
```javascript
class AudioPlayer {

  constructor(currentSong){
    this.currentSong = currentSong;
    this.currentTime = 0;
  }
  
  play(){
    //  ...
    console.log("Playing " + this.currentSong + "!");
  }
  
  stop(){
    //  ...
    console.log("Stopping " + this.currentSong + "!");
  }
  
}

let newAudioPlayer = new AudioPlayer('Sleep Apnea');
newAudioPlayer.play();
```

Notice that we create the object just as we did before. Another thing to notice is that the `this` keyword is properly bound to the class scope. Meaning that we can access properties within the class with the `this` keyword. 

Note that Javascript does not have any access modifers, so we are unable to control `public` and `private` methods and variables through ES6 syntax. In fact, there is no addition "power" in the Class syntax above. Either the stated ES5 or ES6 methods are acceptable, but the ES6 syntax is closer to what you would see in other languages. 

## Inheritance
We can extend the functionality from one class to the next by using the `extend` keyword. This will cause the `subclass` (or`childclass`) to inherit its functionality from the `superclass` (or `parentclass`). Let's take a look at an example below:

```javascript 
class MarketItem {

  constructor(name, price, imgUrl){
    this.name = name;
    this.price = price;
    this.imgUrl = imgUrl;
  }

  changePrice(){
    this.price++;
    console.log('Price Changed! ', this.price);
  }
}

class Fruit extends MarketItem { 

  constructor(name, price, imgUrl, freshness){
    super(name, price, imgUrl);
    this.freshness = freshness;
  }

  changePrice(){
    super.changePrice();
    this.freshness--;
    if(this.freshness <=0){
      this.price = 0;
      console.log('Food spoiled: ', this.price);
    } else {
      console.log('Freshness: ', this.freshness);
    }
  }
}

var apple = new Fruit('Apple', 1, 'something.jpg', 2);
console.log(apple);
apple.changePrice();

```
