# Adapter Pattern


## What is it?

Convert the interface of a class into another interface clients expect. Adapter lets classes work together that couldn't otherwise because of incompatible interfaces.

The travel adapter is the most common comparison for this pattern. If you have a three-pronged electrical plug, it won’t fit in a two-prong wall outlet. Instead, you need to use a travel adapter to convert energy from the wall outlet to the plug you have.

## Diagram
![Adapter Diagram](http://buraktas.com/public/images/2015/01/adapter-design-pattern.png)

## Benefits
- Helps achieve reusability and flexibility.
- Client class is not complicated by having to use a different interface and can use polymorphism to swap between different implementations of adapters.

## Drawbacks

- All requests are forwarded, so there is a slight increase in the overhead.
- Sometimes many adaptations are required along an adapter chain to reach the type which is required.

## Implementations

### Basic

```javascript
// old interface
 
function Shipping() {
    this.request = function(zipStart, zipEnd, weight) {
        // ...
        return "$49.75";
    }
}
 
// new interface
 
function AdvancedShipping() {
    this.login = function(credentials) { /* ... */ };
    this.setStart = function(start) { /* ... */ };
    this.setDestination = function(destination) { /* ... */ };
    this.calculate = function(weight) { return "$39.50"; };
}
 
// adapter interface
 
function ShippingAdapter(credentials) {
    var shipping = new AdvancedShipping();
 
    shipping.login(credentials);
 
    return {
        request: function(zipStart, zipEnd, weight) {
            shipping.setStart(zipStart);
            shipping.setDestination(zipEnd);
            return shipping.calculate(weight);
        }
    };
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
    var shipping = new Shipping();
    var credentials = {token: "30a8-6ee1"};
    var adapter = new ShippingAdapter(credentials);
 
    // original shipping object and interface
 
    var cost = shipping.request("78701", "10010", "2 lbs");
    log.add("Old cost: " + cost);
 
    // new shipping object with adapted interface
 
    cost = adapter.request("78701", "10010", "2 lbs");
 
    log.add("New cost: " + cost);
    log.show();
}
```

## References
- [geeksforgeeks](http://www.geeksforgeeks.org/adapter-pattern/)
- [thejsguy](http://thejsguy.com/2015/10/16/the-adapter-pattern-in-javascript.html)
- [dofactory](http://www.dofactory.com/javascript/adapter-design-pattern)
