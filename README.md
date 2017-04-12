# ES6 / ES 2015

## LET Declarations
Let is a new way to declare variables and have them scoped to the nearest code block (and not to the nearest function, as with the standard `var` declaration). 

Consider this:
```javascript
function regularFunction(){
  if(true){
    var trueBlockVariable = "Hello";
  } else {
    var falseBlockVariable = "Goodbye!";
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
    let trueBlockVariable = "Hello";
  } else {
    let falseBlockVariable = "Goodbye!";
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

setupUser({name: "Scott", admin: true});
```

From what we learned about default parameters, we may be tempted to additionally use a default value for the `configObject` to at least check whether or not the supplied argument is an object. Problem is, we are still writting assignment code, Which might look something like this:
```javascript
function setupUser(configObject = {}){
  var name = configObject.name;
  var admin = configObject.admin;
  //do things
}

setupUser({name: "Scott", admin: true});
```

But we can take this up another step. We can instead use the declaration names within an object as an argument to the function itself. Check it out: 

```javascript
function setupUser( {name,admin} ){
  //do things
}

setupUser({name: "Scott", admin: true});
```

Inside the function, we have access to the `name` and `admin` values, already declared as we did in the examples above. As a bonus, the function signature is more descript about that the function accepts! Note that as a final step, we can still assign a default parameter. 

```javascript
function setupUser( {name,admin} = {} ){
  //do things
}

setupUser({name: "Scott", admin: true});
```

## Rest Parameters
A Rest parameter allows us to accept an indefinite amount of arguments and puts them into an array. We access the rest parameter with the `...` leading syntax followed by what we would like to call the param. 

For example:
```javascript
function restFunction(...list){
    for(let i = 0; i < list.length; i++){
        console.log(list[i]);
    }
}

restFunction("Scott", "Fred", "Mark", "Taylor", "Chris");
```

Additionally, we can put arguments in front of the rest parameter to accepted needed arguments that should not be considered in the rest array.

For example:
```javascript
function restFunction(instructor = "Unassigned", ...list){
  for(let i = 0; i < list.length; i++){
    console.log(list[i]); // Logs list without 'Scott'
  }

  console.log(instructor); // Logs 'Scott'
}

restFunction("Scott", "Fred", "Mark", "Taylor", "Chris");
```

## Spread Operators
Spread operators have a similar syntax as rest parameters, however instead of using the `...` syntax in a function argument, we use it in the function call. The functional difference is that it take an array of values and sends them to the function as individual arguments into the function.

Consider this:
```javascript
let atticus = ["Atticus", 392811, 94000];

function createEmployeeObject(array){
  var name = array[0];
  var employeeNumber = array[1];
  var salary = array[2];
}

createEmployeeObject(atticus);
```

In the above example, we see the array of information passed into the function call, then inside the function the array is accepted. That array is then used to assign value to variables created in the function. As we have seen in ES6 before, we know that this pattern of boilerplate variable assignment is not ideal. So instead, we can pair up the spread operator with stated arguments. For example:
```javascript 
let atticus = ["Atticus", 392811, 94000];

function createEmployeeObject(name = 'Un-named', employeeNumber = '00000', salary = '10000'){
  //Do things
}

createEmployeeObject(...atticus);
```
