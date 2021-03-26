## The 4 Creational Design Patterns In Node.js You Should Know

First of all, let's start with an explanation of what design patterns are. In the simplest terms, they allow us to re-use code for re-occurring problems. Instead of solving the same problems again and again, we can re-use efficient code that already works. Why would you use design patterns? The reasons are that they are:
* Well documented and tested
* Reusable in many different situations
* Efficient
* Saving you time

It's important to note that these patterns are universal, which means they apply to other programming languages/frameworks/libraries. However, in this article, we use Node.js to implement and understand them.

There are three types of design patterns:
1. Creational - the creation of the object instances
2. Structural - the way the objects are designed
3. Behavioural - how objects interact with each other

# Creational Design Patterns
In this article, you learn about the Creational Design Patterns. They are concerned with the creation of object instances. In the following articles, you will learn about Structural and Behavioural Patterns too.

The Creational Design Patterns covered in the article are:
1. Singleton
2. Factory
3. Builder
4. Prototype

Without further ado, let's start with the Singleton design pattern.

# Singleton
We can get a glimpse of the purpose of this design pattern from its name - **SINGLE**ton. We use this design pattern when we only want a single instance of a class. That means we cannot create multiple instances - just one. If there is no instance, a new one is created. If there is an existing instance, it will use that one.

Let's see an example with the Singleton pattern implemented:
```js
class DatabaseConnection {
  constructor() {
    this.databaseConnection = 'dummytext';
  }

  getNewDBConnection() {
    return this.databaseConnection;
  }
}

class Singleton {
  constructor() {
    throw new Error('Use the getInstance() method on the Singleton object!');
  }

  getInstance() {
    if (!Singleton.instance) {
      Singleton.instance = new DatabaseConnection();
    }

    return Singleton.instance;
  }
}

module.exports = Singleton;
```

As you can see, there is a lot of boilerplate to implement the Singleton. Thus, let's see a shorter way of implementing this design pattern. The solution is to remove the class Singleton altogether and export a new instance of the class DatabaseConnection. 

```js
class DatabaseConnection {
  constructor() {
    this.databaseConnection = 'dummytext';
  }

  getNewDBConnection() {
    return this.databaseConnection;
  }
}

module.exports = new DatabaseConnection();
```

Why does this work? In Node.js, it works because of the module caching system. The module caching system says that "modules are cached after the first time they are loaded" (source - [Node.js docs](https://nodejs.org/api/modules.html#modules_caching)). That means in the second example above, the new instance exported is cached and re-used each time it's required.

Therefore, these are the two ways of implementing the Singleton pattern in NodeJS. To recap:
* Singleton is useful when you want only one instance of a class.
* In NodeJS, we can make use of the module caching system to export an instance directly.

# Factory
We can get an idea of what this design pattern does by looking at its name. The Factory Design Pattern allows us to define an interface or abstract class used to create an object. We then use the interface/abstract class to instantiate different objects.

Consider an application where we have to create and use all types of vehicles. There are motor vehicles (cars, buses, trucks, motorcycles), railed vehicles (trains, trams), aircraft (airplanes, helicopters), and watercraft (ships, boats). Thus, instead of creating instances by calling the constructor of each class individually, we can implement the Factory pattern as follows:

```js
import Motorvehicle from './Motorvehicle';
import Aircraft from './Aircraf';
import Railvehicle from './Railvehicle';

const VehicleFactory = (type, make, model, year) => {
  if (type === car) {
    return new Motorvehicle('car', make, model, year);
  } else if (type === airplane) {
    return new Aircraft('airplane', make, model, year);
  } else if (type === helicopter) {
    return new Aircraft('helicopter', make, model, year);
  } else {
    return new Railvehicle('train', make, model, year);
  }
}

module.exports = VehicleFactory;
```

Instead of creating an instance of each class individually, you can use the VehicleFactory and specify the type. You would create a new Car instance as follows:

```js
const audiAllRoad = VehicleFactory('car', 'Audi', 'A6 Allroad', '2020');
```

The benefit of using the Factory design pattern is that it decouples the objects' constructions from the objects themselves. You can also introduce new objects into your application without breaking existing code. Lastly, it helps you organize your code better because all the code related to creating instances is in one place. To recap:
* Factory pattern provides an interface/abstract class for creating objects.
* You can create different objects by using the same interface/abstract class.
* It improves the structure of the code and makes it easier to maintain it.

# Builder
The Builder design pattern allows us to separate the construction of objects from their representation. Thus, it simplifies the code that creates complex objects. It might be overkill with simple objects, but with complex objects, it simplifies creating them.

To help you with understanding this design pattern, let's think of an example. Let's say we want to build cars. In this example, we would have the `Car` and `CarBuilder` classes.

```js
class Car {
    constructor(make, model, year, isForSale = true, isInStock = false) {
        this.make = make;
        this.model = model;
        this.year = year;
        this.isForSale = isForSale;
        this.isInStock = isInStock;
    }

    toString() {
        return console.log(JSON.stringify(this));
    }
}

class CarBuilder {
    constructor(make, model, year) {
        this.make = make;
        this.model = model;
        this.year = year;
    }

    notForSale() {
        this.isForSale = false;
        
        return this;
    }

    addInStock() {
        this.isInStock = true;

        return this;
    }

    build() {
        return new Car(this.make, this.model, this.year, this.isForSale, this.isInStock);
    }
}

module.exports = CarBuilder;
```

Now we create cars using the `CarBuilder` class instead of the `Car` class. We do it as follows:

```js
const CarBuilder = require('./CarBuilder');

const bmw = new CarBuilder('bmw', 'x6', 2020).addInStock().build();
const audi = new CarBuilder('audi', 'a8', 2021).notForSale().build();
const mercedes = new CarBuilder('mercedes-benz', 'c-class', 2019).build();
```

Using the Builder design pattern makes the creation of complex objects less prone to errors because you can easily understand what each parameter does. For contrast, here is how we would create cars without the `CarBuilder` class:

```js
const bmw = new CarBuilder('bmw', 'x6', 2020, true, true);
```

You can see it can become confusing. What do those two boolean values ("true") mean? Now imagine the object is more complex; creating the object would be confusing, and the chances of introducing errors would be higher.

Thus, the Builder design pattern is useful to separate the creation and representation of complex objects.

# Prototype
JavaScript is a Prototype-based language, which means it uses Prototypal inheritance. That means each object inherits from other objects.

Thus, we create new objects by cloning the prototype's values, which can also be called a sample object. That means the prototype acts as a blueprint for the new objects. One significant benefit of using this design pattern is that functions defined in objects are created by reference. That means all objects point to the same function instead of having their copies of that function. In simpler terms, the prototype's functions are available to all the objects inherited from the prototype. 

Ok, enough talk. Let's see an example so you can understand better what this design pattern is about. We continue with the car scenario.

```js
const atv = {
    make: 'Honda',
    model: 'Rincon 650',
    year: 2018,
    mud: () => {
        console.log('Mudding');
    }
};

const secondATV = Object.create(atv);
```

To create a new object from a prototype, we can use the `Object.create()` method. The second object - `secondATV` - has the same values as the first object - `atv`. To make sure it works correctly, try calling the "mud" function or printing any object property. 

Another way of using the Prototype Design pattern is by specifying the prototype in the "class". You can see an example below:

```js
const atvPrototype = {
    mud: () => {
        console.log('Mudding');
    }
};

function Atv(make, model, year) {
    function constructor(make, model, year) {
        this.make = make;
        this.model = model;
        this.year = year;
    }

    constructor.prototype = atvPrototype;

    let instance = new constructor(make, model, year);
    return instance;
};

const atv1 = Atv();
const atv2 = Atv('Honda', 'Rincon 650', '2018');
```

On the same note, both instances have access to whatever is defined in the `atvPrototype` object. Moreover, they point to the same function, instead of having their "mud" function.

In conclusion, the Prototype design pattern is useful, especially when you want your objects to share the same functions or properties. It also acts as a blueprint for all your new objects.

To recap:
* JavaScript is a Prototype-baed language.
* It uses prototypal inheritance.
* Each object inherits from other objects.
* New objects are created by following a blueprint, called Prototype.
* A function defined on the prototype is inherited by all new classes.
* The new classes point to the same function, rather than having individual copies.


# Conclusion
The article is part of my #learninpublic process. Thus, it's important to note that the article is a starter, and you can dig deeper. I recommend the book [Design Patterns: Elements of Reusable Object-Oriented Software](https://www.amazon.com/Design-Patterns-Object-Oriented-Addison-Wesley-Professional-ebook/dp/B000SEIBB8) if you want to go deeper.

In this article, you learned how to create objects in various ways. You can create new objects using the following design patterns:
* Singleton
* Factory
* Builder
* Prototype

<hr/>
_[daily.dev](https://api.daily.dev/get?r=catalinpit) delivers the best programming news every new tab. We will rank hundreds of qualified sources for you so that you can hack the future._
[![Daily Poster](https://dev-to-uploads.s3.amazonaws.com/i/b996k4sm4efhietrzups.png)](https://api.daily.dev/get?r=catalinpit)