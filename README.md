# ES6 / ES 2015

## LET Declarations
Let is a new way to declare variables and have them scoped to the nearest code block (and not to the nearest function, as with the standard `var` declaration). 

Consider this:
```
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
```
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
```
var numOfToppings = 4;

if(numOfToppings > 3){
  // Does not qualify for deal.
} else {
  // Qualifies for deal.
}
```

The problem in the above, is that the number '3' would be a complete mystery without the explanation above it. This is what we call a `magic number`. Magic numbers are numbers that have meaning, but they are not described in the code at all. Typically they get used because they are meant to be unchanging values. This is where the `const` declaration can help. We use the const declaration to help us control the value, but also be descriptive about what that value represents. We can pair that with the `let` declaration on the `numOfToppings` for extra ES6'iness.

Finally, naming convention for `const` variables uses capital letters with underscores in between. So for our pizza deal declaration, we would use something like this: `const TOPPINGS_FOR_DEAL`


```
let numOfToppings = 4;
const TOPPINGS_FOR_DEAL = 3; 

if(numOfToppings > TOPPINGS_FOR_DEAL){
  // Does not qualify for deal.
} else {
  // Qualifies for deal.
}
```

The code is now more readable in terms of being able to look at the code and quickly infer what the code is doing. Additionally, we know with the naming convention that the `TOPPINGS_FOR_DEAL` is a constant and that the value cannot be changed. 
