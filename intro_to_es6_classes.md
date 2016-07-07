# Introduction to ES6 Classes

ES6 Classes are essentially syntactical sugar for objects and prototypes. However, they offer a much cleaner syntax for dealing with javascript objects and they simplify prototypical inheritance. The purpose of classes is to keep data private by encapsulating functions as methods and variables as properties of a class instance.

#Syntax

ES6 Class syntax is fairly straightforward. The simplest way to define a class is by declaring it with the class keyword, followed by the name of the class. Inside the body of the class is a constructor method which is ran when a new class instance is declared. Within the constructor we can define any properties that a class should have by default. Within the body of the class itself we define methods.

Side Note: Methods are essentially functions associated with an object, but with two key differences.

    1. A method is implicitly passed the object on which it was called.
    2. A method is able to operate on data that is contained within the class.

Example - Class Declaration:

```javascript
class Product {
    constructor (name, price) {
        this._name = name;
        this._price = price;
    }

    productDetails() {
        console.log(`Name: ${this._name} | Price: ${this._price}`); // Here we are making use of Template String notation (introduced in ES6 - allows us to use string substitution)
    }
}

class Toy {
    constructor(name, price, instock) {
        this._name = name;
        this._price = price;
        this._instock = instock
    }

    productDetails() {
        console.log(`Name: ${this._name} | Price: ${this._price}`); // Here we are making use of Template String notation (introduced in ES6 - allows us to use string substitution)
    }

    isinstock() {
        console.log(this._instock);
    }
}

let transformer = new Toy("Optimus Prime", 30, true);

transformer.productDetails(); // "Name: Optimus Prime | Price: $30"
```

## ES6 Classes & Prototypes

`let transformer = new Toy("Optimus Prime", 30);` creates a Javascript object that automatically gets a prototype assigned to it.

We can explore the available attributes assigned in the `constructor`:

```javascript
transformer.hasOwnProperty('_name') // true
transformer.hasOwnProperty('_price') //true
```

`name` and `price` are properties that are directly assigned on the new `transformer` object. If we wanted to access any of these properties we would call them like any regular JS object:

```javascript
transformer._name // Optimus Prime
```
But what happens when we check for the prodcutDetails method:

```javascript
transformer.hasOwnProperty('produtDetails') // false
```

It's not in the object, however we can call it with the following line:

`transformer.productDetails(); // Name: Optimus Prime | Price: 30`

The productDetails is actually being shared by all instances of a Toy and is therefore within the prototype chain of transformer.

`transformer.__proto__.hasOwnProperty('productDetails') // true`

The method isn't actually copied everytime we create a new Toy object, it is in the prototype. The object is created automatically by JS when declaring a class and its assigned to all instances of the class.

We can create another instance of a Toy and compare the prototypes of each and we find that they are the same object.

```javascript
let transformer = new Toy("Optimus Prime", 30, true);
let mixtape = new Toy("Supa Hot Fire", 2000, false);

transformer.__proto__ == mixtape.__proto__ // true

```
Thus the methods productDetails and isInStock are being shared by all instances of Toy. Adding methods on the prototypes of objects as opposed to copying the methods on each object allows us to conserve memory.

#Inheritance & Subclasses

Often times you can break classes down into subclasses which are essentially detailed abstractions of a superclass/base class. If we think about our product and toy classes above we can assume that a toy is an abstraction of a product. They both share the same properties and a toy IS-A and WORKS LIKE A specific kind of product.

Example - Inheritance:

```javascript
class Product {
    constructor (name, price) {
        this._name = name;
        this._price = price;
    }

    productDetails() {
        console.log(`Name: ${this._name} | Price: ${this._price}`);
    }
}

class Toy extends Product {
    constructor(name, price, instock) {
        super(name, price);
        this._instock = instock;
    }

    isInStock() {
        if (this._instock) {
            console.log(`${this._name} is in stock`);
        } else {
            console.log(`${this._name} is NOT in stock`);
        }
    }
}

let transformer = new Toy ("Optimus Prime", 30, true);

transformer.isInStock(); // Optimus Prime is in stock
transformer.productDetails(); // Name: Optimus Prime | Price: $30
```

Since the name and price properties and product details method are shared between a toy and a Product, we can simply extend our Toy class from the Product base class by using the 'extends' keyword. Also, note the use of the 'super' keyword. 'super' is used to call methods on an object's parents and it passes similar properties as arguments. When used in a constructor, the 'super' keyword must be defined before the 'this' keyword defines any subclass specific properties.

#Beware

Overuse:
There are however disadvantages of extending your classes/inheritance. We ensure valid state by manipulating data through a small and fixed set of functions.
However, when we inherit we're also increasing the list of functions that can manipulate our data. Too much inheritance is almost equivalent to global
variabes... having too many functions that can directly manipulate our data.


Hoisting:
An important difference between function declarations and class declarations is that function declarations are hoisted and class declarations are not. You first need to declare your class and then access it, otherwise code like the following will throw a ReferenceError:

```javascript
var p = new Polygon(); // ReferenceError

class Polygon {}
```
