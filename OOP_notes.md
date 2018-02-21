##### Note that these notes are intended for Javascript Learners looking at OOP for the first time.

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

| AudioPlayer   | 
| ------------- |
| currentSong   
  currentTime| 
| ------------- |
| play()   | 
| stop()   | 

In this example, we see that we have an Audio Player Class described above. If we were to deploy our application and allow users to paly their own songs on their own `instance` of an audio player, we would have different properties and names. 

| ScottsAudioPlayer   | 
| ------------- |
| Sleep Apnea   
  0:37| 
| ------------- |
| play()   | 
| stop()   | 

| RachaelsAudioPlayer   | 
| ------------- |
| Everybody   
  1:24| 
| ------------- |
| play()   | 
| stop()   | 

### Instances
An instance is an individual creation from a Class. While Whiteboard Marker might be the class, each of these markers are individual `instances` of the class. The process of creation of an instance from a class, is an `instantiation`. 

### Types and Classes
In most languages, the language itself comes with its own collection of Classes that are already available to us. In Javascript, we may be familiar with the term `type` or `object`. We work with these objects all the time and because of the ease of Javascript, we skip right past the parts that make us think of how they began as classes. For example, we instantiate Numbers, Strings, and Arrays all the time. But because of Javascript shorthand, we miss the critical clues that tell use we are using a Blueprint of sorts. 

## Abstraction
Abstraction has to do with the 'idea' of something. If I said to you the word 'House'. You would know what I am talking about. There are a ton of details that would need to be sussed out, but you ‘have the general idea’ of what I am talking about. 

Abstraction just focuses on the essentials, and discards the unimportant pieces of information. We are not focusing on the type of house, just rather what the word represents. We do this all the time in the real world. Chances are great, that as you came together this morning and asked the question “How was your weekend? What did you do?”, as the person described their weekend, you did not need to stop them every second to hop into the minutiae of every detail, but rather listened to the story and were able to track fine.

The phrase “I went to my brothers house for Sunday brunch” prompts a general image in your mind that does not need the specific details of the brother, his house, and what was for brunch. 

Faction NEEDS this idea of abstraction to function at all. Often times we find ourselves drawn into faction because the writer does a great job describing the needed details to frame the story, but also allows the reader's imagination to fill in the blanks.

If we were writing code, we do not write a class for each and every Bank Account let's say, but rather we establish a base in which all bank accounts derive from.

Abstraction is at the core of the other fundamentals of Object Orientated Programming, and we will see how it plays a critical role.

## Encapsulation

Surrounding something. Protecting contents. Taking attributes and behaviors, then bundling them up in a class. But it’s more than just the idea of class. It is about the protection of of those attributes and behaviors. This is referred to as ‘data hiding’. 

The main concept of data hiding, is that you are ONLY revealing attributes and behaviors that are ABSOLUTELY necessary in order for your application to work.  

A simple example of this is a Bank Account application. You should not be able to access the property of balance directly from any other part of the application. You should have to go through the deposit or withdraw methods in order to change the balance. This is because there are other considerations that need to be made. If you were able to subtract from the balance from anywhere in the application, then you would probably need to check for an overdraft in each place you made negative adjustments. It would be so much easier if you just went through one method to do it. 

This means that the balance cannot be changed directly, but rather just through the withdraw and deposit methods which can reach inside its own class to manipulate the balance, with the other considerations that go along with it.

Another example is a toaster. A toaster is fairly simple. Adjust time, then push the handle down to toast. The time mechanism is something that you have direct access to, a property you can manipulate directly. But the inner workings of a toaster are not available to you. You actually have no idea how the time dial changes the inner workings of the toaster, or rather, how that dial fits into the mechanics of the toaster. Same for the handle. You push it down, but inside of the toaster, you could probably not speak to exactly what the toaster does to start the warming process of the bread. Changing the inner mechanisms of the toaster probably do not change the inputs of the toaster itself. Unless of course, you got a better toaster.

## Inheritance
When it comes to working with Classes, we may run into situations where two objects could be similar, and even categorized under one one class, but they are different enough to each need special properties, methods, or both. Thinking about a Bike and a Motorcycle, we can conclude that they are very different, but have some common attributes and behaviors. Both have wheels, are used as modes of transportation, but there are also differences. Such as mode of power, the need for fuel, and so on. 

So in this case, we could create a ‘Vehicle’ class. We could then find the commonalities and draw out the properties and methods that the two share:

| Vehicle   | 
| ------------- |
| numWheels | 
| ------------- |
| moveForward() 
  stop()| 
  
But in this example, we would want to create two different objects from this Vehicle class, but lets consider the need to create 100's of Bike and 100's of Motorcycles. We should have a class for each of those two. But luckily, we don't need to start from scratch when we do this. We do not need to create two different classes that share some things but not others. We can `extend` the Vehicle class we created, and allow the two new classes to automatically have the properties and methods of the Vehicle class. 

| Motorcycle : Vehicle   | 
| ------------- |
| engine   
  fuelLevel| 
| ------------- |
| startEngine() 
  stopEngine()| 
  
  
| Bike : Vehicle   | 
| ------------- |
| hasKickstand| 
| ------------- |
