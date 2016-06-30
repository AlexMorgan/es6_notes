# Introduction to ES6 Classes

ES6 Classes are essentially just syntactical sugar for objects and prototypes. However, they offer a much cleaner syntax for dealing with javascript objects and they simplify prototypical inheritance.

#Syntax

ES6 Class syntax is fairly straightforward. The simplest way to define a class is by declaring it with the class keyword, followed by the name of the class. Inside the body of the class is a constructor method which is ran when a new class instance is declared. Within the constructor we can define any properties that a class should have by default. Within the body of the class itself we define methods.

Side Note: Methods are essentially functions associated with an object, but with two key differences.

    1. A method is implicitly passed the object on which it was called.
    2. A method is able to operate on data that is contained within the class.


Ex: Class Expression:

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

let fruit = new Product("apple", 3);
```

