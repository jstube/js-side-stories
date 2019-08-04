# Javascript Side Stories Chapter 1 - Values vs References

Learning to assign and refer to a variable is perhaps the very first thing every javascript book teaches you. You write `var` at the beginning of a line of code and an adequate name that matches your purpose, then assign a **value** to it.

```javascript
var cake = 'cake';
```

Just a piece of cake, right?

Next, you learn what are objects and arrays, and how to set values and to iterate over them, which is not that hard either. All you need to do is doing what your books tells you to do. There's not much a hassle.

## Your first frustration

You want to experiment with what you've just learnt by writing a simple program (Very good! that's the spirit!).

You want to write a program that does these.

- create common sandwich
- use common sandwich to make both tuna and ham sandwich
- print result

```javascript
var sandwich = { name: 'sandwich', price: 8, unit: 'dollars' };
var tunaSandwich = sandwich;
var hamSandwich = sandwich;

tunaSandwich.name = 'tuna';
tunaSandwich.price = 7;

hamSandwich.name = 'ham';
```

- Your expectation

```javascript
console.log(sandwich); // {name: 'sandwich', price: 8 unit: 'dollars'};
console.log(tunaSandwich); // {name: 'tuna', price: 7, unit: 'dollars'};
console.log(hamSandwich); // {name: 'ham', price: 8, unit: 'dollars'};
```

- Reality

```javascript
console.log(sandwich); // {name: 'ham', price: 7, unit: 'dollars'};
console.log(tunaSandwich); // {name: 'ham', price: 7, unit: 'dollars'};
console.log(hamSandwich); // {name: 'ham', price: 7, unit: 'dollars'};
```

## What's happening in your code

You assigned `sandwich` to both `tunaSandwich` and `hamSandwich` to make two sandwiches out of the common one. You did that because you've done this kind of stuff and it worked.

```javascript
var sandwich = 'sandwich';
var tunaSandwich = 'tuna ' + sandwich; // 'tuna sandwich'
var hamSandwich = 'ham' + sandwich; // 'ham sandwich'

console.log(sandwich); // 'sandwich'
console.log(tunaSandwich); // 'tuna sandwich'
console.log(hamSandwich); // 'ham sandwich'
```

## What you should have been taught

Here comes the time you should know the difference between values and references

### Values

### References

## The right ways

We are not going in depth on each subject matters right now. it's up to you to go deeper.

1. object factory
2. constructor
3. copy

### 1. Object factory

If you need to create a lot of object with same fields but different values, it is good idea to use a factory function.

A factory function accepts several values as argument, then returns an object that suits your needs.

```javascript
function sandwichFactory(name, price) {
  return {
    name: name,
    price: price,
    unit: 'dollars'
  };
}

var tunaSandwich = sandwichFactory('tuna', 5); // returns { name: 'tuna', price: 5, unit: 'dollars' }
var hamSandwich = sandwichFactory('ham', 7.5); // returns { name: 'ham', price: 7.5, unit: 'dollars' }
```

### 2. Constructor

If you need to create a lot of object with same behaviors, you can consider using constructor (or class) function

```javascript
function Sandwich(name, price) {
  this.name = name;
  this.price = price;
  this.unit = 'dollars';
}

Sandwich.prototype.setPrice = function(newPrice) {
  this.price = newPrice;
};

var tunaSandwich = new Sandwich('tuna', 7);
var veganSandwich = new Sandwich('vegan', 100000);

// customers complain vegan sandwich is insanely expensive
veganSandwich.setPrice(10);

console.log(veganSandwich.price); // prints 10
```

### 3. Copy

If what you need is an identical pair of an object, copying is the best option in my opinion.

Most modern browsers provide native `Object.assign` API out of the box, with which you can assign values to the target object, or create a new piece of object.

```javascript
var tunaSandwich = { name: 'tuna', price: 7, unit: 'dollars' };
var anotherTunaSandwich = Object.assign({}, tunaSandwich);

anotherTunaSandwich.price = 8;

console.log(tunaSandwich.price); // prints 7
```

#### should I go shallow or deeper

## Questions

### Why primitive values (numbers and strings) are immune to the problem above ?

immutablitiy vs mutablity
