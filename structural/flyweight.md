# Flyweight Pattern


## What is it?

The Flyweight pattern is a classical structural solution for optimizing code that is repetitive, slow and inefficiently shares data. It aims to minimize the use of memory in an application by sharing as much data as possible with related objects (e.g application configuration, state and so on).

There are two ways in which the Flyweight pattern can be applied. The first is at the data-layer, where we deal with the concept of sharing data between large quantities of similar objects stored in memory.

The second is at the DOM-layer where the Flyweight can be used as a central event-manager to avoid attaching event handlers to every child element in a parent container we wish to have some similar behavior.


## Diagram
![Flyweight Pattern](http://www.dofactory.com/images/diagrams/javascript/javascript-flyweight.jpg)

## Benefits
-  minimize the use of memory in an application by sharing as much data as possible with related objects (e.g application configuration, state and so on).
- Sharing to support large numbers of fine-grained objects efficiently.

## Drawbacks

- Additional Complexity

## Implementations

### Basic

```javascript
function Flyweight (make, model, processor) {
    this.make = make;
    this.model = model;
    this.processor = processor;
};
 
var FlyWeightFactory = (function () {
    var flyweights = {};
 
    return {
 
        get: function (make, model, processor) {
            if (!flyweights[make + model]) {
                flyweights[make + model] = 
                    new Flyweight(make, model, processor);
            }
            return flyweights[make + model];
        },
 
        getCount: function () {
            var count = 0;
            for (var f in flyweights) count++;
            return count;
        }
    }
})();
 
function ComputerCollection () {
    var computers = {};
    var count = 0;
 
    return {
        add: function (make, model, processor, memory, tag) {
            computers[tag] = 
                new Computer(make, model, processor, memory, tag);
            count++;
        },
 
        get: function (tag) {
            return computers[tag];
        },
 
        getCount: function () {
            return count;
        }
    };
}
 
var Computer = function (make, model, processor, memory, tag) {
    this.flyweight = FlyWeightFactory.get(make, model, processor);
    this.memory = memory;
    this.tag = tag;
    this.getMake = function () {
        return this.flyweight.make;
    }
    // ...
}
 
// log helper
 
var log = (function () {
    var log = "";
 
    return {
        add: function (msg) { log += msg + "\n"; },
        show: function () { alert(log); log = ""; }
    }
})();
 
function run() {
    var computers = new ComputerCollection();
    
    computers.add("Dell", "Studio XPS", "Intel", "5G", "Y755P");
    computers.add("Dell", "Studio XPS", "Intel", "6G", "X997T");
    computers.add("Dell", "Studio XPS", "Intel", "2G", "U8U80");
    computers.add("Dell", "Studio XPS", "Intel", "2G", "NT777");
    computers.add("Dell", "Studio XPS", "Intel", "2G", "0J88A");
    computers.add("HP", "Envy", "Intel", "4G", "CNU883701");
    computers.add("HP", "Envy", "Intel", "2G", "TXU003283");
 
    log.add("Computers: " + computers.getCount());
    log.add("Flyweights: " + FlyWeightFactory.getCount());
    log.show();
}
```

## References
- [Learning Javascript Design Patterns](https://addyosmani.com/resources/essentialjsdesignpatterns/book/#detailflyweight)
- [Dofactory](http://www.dofactory.com/javascript/flyweight-design-pattern)