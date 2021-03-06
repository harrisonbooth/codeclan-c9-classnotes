#JS Prototypes

##Learning objectives
- Describe inheritance in JavaScript
- Set the prototype of a constructor function
- Explain the benefits of using a prototype on a constructor
- Find the prototype of an object

### What is a Prototype

##Why learn about prototypes
Let's look at the Array documentation for the push method.
https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Array/push

Array.prototype.push().  What is this prototype business?  While we might not use these ourselves in the course.  It is worth knowing what they are so we can look at documentation and other libraries.


#What is a prototype
Every object in JS has a prototype.  We can think of the prototype as kind of fall back that the object goes to whenever it doesn't have the attribute on it itself. In JS objects inherit from an other object, called it's prototype.

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Inheritance_and_the_prototype_chain

We can set a prototype of the object when we create it using the object constructor.  This is not something we will be doing throughout this course,  but it showcases how prototypes work.

```
#terminal 

mkdir proto_play
cd proto_play

touch proto_play.js
subl .
```

```js
//proto_play.js

var myPerson = Object.create(null);
myPerson.walk = function() {console.log('left right left right')};
```

```js
//proto_play.js

var wisePerson = {
  wisdom: function() {
    console.log('commit often');
  }
};

var myPerson = Object.create(wisePerson);
myPerson.walk = function() {
  console.log('left right left right');
};

myPerson.wisdom();
```


### Constructor prototypes

Now let's see why the push method was declared on the Array prototype.

We've seen how constructor functions can be used to create multiple objects of the same 'type'.

```js
//proto_play.js

var Fish = function(name, colour){
  this.name = name;
  this.colour = colour;
  this.swim = function() {
    console.log('splash');
  };
};

var myFish = new Fish('nemo', 'orange');
myFish.swim();
```

Every fish we create will be assigned a new name and color and swim functions.  This is waste of memory as the swim function is identical for each fish.  We can give the constructor function a prototype, all objects created by this will have the attributes available on the prototype.  This is a very common pattern.

```js
//proto_play.js

var Fish = function(name, color) {
  this.name = name;
  this.color = color;
};

Fish.prototype = {
  swim: function() {
    console.log('splash');
  }
};

var myFish = new Fish('nemo', 'orange');
myFish.swim();
```

[i]: Explain how it won't find the method on the fish but will look up the prototype chain and find it on the prototype.

[i]: If we use this in the constructor it will find it in the prototype.

[Task] What would happen if we moved 'name' from the constructor function to the prototype?

We can ask an object about it's prototype

###Finding out the prototype of an object
```js
//proto_play.js

Object.getPrototypeOf(myFish) // new ES6 syntax
myFish.__proto__  // old syntax
```
