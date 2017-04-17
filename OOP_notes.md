# Object Orientated Programming

## A Case for Object Orientated Programming
In old languages, like Cobol and Assembly, programs were written in a monolithic manner. It had familiar components like Variables written at the top with functions and subroutines in the middle and so on, but when writing large applications, this proved to be problematic. In the 1980s, OOP languages started to gain popularity. 

OOP allowed programs to be written as ‘mini-programs’, each handling a specific part of functionality of the main application. Each object contained its own data and its own logic. The objects are then used to communicate with each other. Each of these objects represents groups of functionality within your application, such as videos, images, and employees, game pieces, and so on. 

Object Orientation is what is referred to as a ‘Programming Paradigm’. Not a language in itself, but rather a set of ideas all languages can use. 

## An Object
When describing Objects, it’s difficult to fall on a crutch like “What is an Object? Well, it’s a thing”, for example. In the real world, we understand very well what an object is. We can look at two Whiteboard Markers and know that they are the same “thing”, but are also very different. Each of the Markers can have a different color, different amount of ‘ink’, a different age since manufacturing, and so on. But we describe them both as Dry Erase Markers. 

The same could be said about the students in this room. We all fall under the categorization of ‘People’, but certainly have a different set of properties that all make us unique. While “Prime Academy Student” is one property that you all share, we all certainly have a different make up of properties that make us unique. Ones that in many ways make us completely different, but there are other properties that make us all the same. Tired might be one of those properties. 

When we look at other objects in the world, we also understand that what one object can do, other objects might not be able to do. For example, the Bird animal can ‘Fly’, where the Turtle animal cannot. But additionally, the same objects may have different values of the same property. One human can be more caffeinated than another. 

Objects generally have three important things that describe an object in programming. Identity, attributes, and behavior. 

Identity describes an object.
Attributes define the state of an object. 
Behavior defines how the objects acts, or ‘things they can do’.

In the real world, we quickly grasp to physical things that we can touch and see when describing objects. But in applications, we can take it further. A Bank Account is a thing that we cannot touch, but it certainly is an object. It has an Identity, “Scotts Bank Account”, it has properties, “$370 dollars”, and it has behaviors it can execute, “Collect Interested”, “Overdraft”, and so on. Each of those behaviors can change the state of itself, or other objects within the application.

Perhaps a good way to think about what an object can be, is to latch onto the word “Noun”. Is the thing you are trying to describe a noun? Or, could you put the word “The” in front of it? 

## Class
Class and Objects go hand in hand. But Classes take it a level up. Classes describe what an object can be, but it is not the object itself. You can think of a class as a Blueprint for an Object. When I say the word ‘Apple’, you begin thinking about the look and characteristics of an Apple, but you are not thinking about a specific apple. Unless of course, it was a particularly good apple. 

For programmers, we build the Class (the blueprint) and we use that Class to build the object. Or in our Apple description, we might have the class for an apple, then create millions of apples from that class. 

### Creating a Class
When we approach the creation of the class, we think about those three things mentioned above: Identity, Attributes, and Behavior. 

* Identity - What is its name? Apple, Bank Account, Person, etc. 
* Attributes - Size, Color, Amount, Weight, Height, etc. 
* Behaviors - Grow, Deposit, Withdraw, Sleep, Eat, etc. 

But you may see different words associated to these three ‘things’. You may not see ‘Name’, but `Type` for example. Attributes may be described as `Properties`. And Behaviors may be referred to as `Methods` or `Operations`. 

If we were to ground this in the Javascript concepts we know, we could look at an example of a class with our current syntax like so:

```javascript
function AudioPlayer(currentSong, currentTime = 0){
  return {
    currentSong,
    currentTime,
    play(){},
    stop(){}
  }
}
```

We can actually diagram these as well. We can think of it almost as a card with three sections, broken apart by how we have been describing these three things. Identity on top, Attributes in the middle, and Behaviors at the bottom:

| AudioPlayer        | 
| ------------- |
| currentSong   
  currentTime| 
| ------------- |
| play()   | 
| stop()      | 
