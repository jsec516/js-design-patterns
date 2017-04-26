# Decorator Pattern


## What is it?

Classically, Decorators offered the ability to add behaviour to existing classes in a system dynamically. The idea was that the decoration itself wasn't essential to the base functionality of the class, otherwise it would be baked into the superclass itself.


## Diagram

## Benefits
- provides code re-use
- alternatives of subclassing
- add additional features on an object withtout modifying consumers code

## Drawbacks

If poorly managed, it can significantly complicate your application's architecture as it introduces many small, but similar objects into your namespace

## Implementations

### Basic decoration of existing object constructors with new functionality

```javascript
function vehicle( vehicleType ){
    /*properties and defaults*/
    this.vehicleType = vehicleType || 'car',
    this.model = 'default',
    this.license = '00000-000'
}
/*Test instance for a basic vehicle*/
var testInstance = new vehicle('car');
console.log(testInstance);
/*vehicle: car, model:default, license: 00000-000*/
/*Lets create a new instance of vehicle, to be decorated*/
var truck = new vehicle('truck');
/*New functionality we're decorating vehicle with*/
truck.setModel = function( modelName ){
    this.model = modelName;
}
truck.setColor = function( color ){
    this.color = color;
}

/*Test the value setters and value assignment works correctly*/
truck.setModel('CAT');
truck.setColor('blue');
console.log(truck);
/*vehicle:truck, model:CAT, color: blue*/
/*Demonstrate 'vehicle' is still unaltered*/
var secondInstance = new vehicle('car');
console.log(secondInstance);
/*as before, vehicle: car, model:default, license: 00000-000*/
```

### Simply decorate objects with multiple decorators

```javascript
//What we're going to decorate
function MacBook() {
    this.cost = function () { return 997; };
    this.screenSize = function () { return 13.3; };
}
/*Decorator 1*/
function Memory(macbook) {
    var v = macbook.cost();
    macbook.cost = function() {
        return v + 75;
    }
}
 /*Decorator 2*/
function Engraving( macbook ){
   var v = macbook.cost();
   macbook.cost = function(){
     return  v + 200;
  };
}

/*Decorator 3*/
function Insurance( macbook ){
   var v = macbook.cost();
   macbook.cost = function(){
     return  v + 250;
  };
}
var mb = new MacBook();
Memory(mb);
Engraving(mb);
Insurance(mb);
console.log(mb.cost()); //1522
console.log(mb.screenSize()); //13.3
```

## References
- [Addy Osmani Blog](https://addyosmani.com/blog/decorator-pattern/)