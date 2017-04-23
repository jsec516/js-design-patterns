# Facade Pattern


## What it is?
This pattern provides a convenient higher-level interface to a larger body of code, hiding its true underlying complexity. Think of it as simplifying the API being presented to other developers, something which almost always improves usability.


## Diagram
![facade diagram](https://github.com/addyosmani/essential-js-design-patterns/blob/master/diagrams/facade.png)


## Benefits
- Provide abstraction


## Drawbacks
- When using the pattern, try to be aware of any performance costs involved and make a call on whether they are worth the level of abstraction offered.


## Implementation

```javascript
var module = (function() {
 
    var _private = {
        i: 5,
        get: function() {
            console.log( "current value:" + this.i);
        },
        set: function( val ) {
            this.i = val;
        },
        run: function() {
            console.log( "running" );
        },
        jump: function(){
            console.log( "jumping" );
        }
    };
 
    return {
 
        facade: function( args ) {
            _private.set(args.val);
            _private.get();
            if ( args.run ) {
                _private.run();
            }
        }
    };
}());

// Outputs: "current value: 10" and "running"
module.facade( {run: true, val: 10} );
```

 
# References
- [Learning Javascript Design Patterns](https://addyosmani.com/resources/essentialjsdesignpatterns/book/#facadepatternjavascript)